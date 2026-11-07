---
title: "Integrating the Web Editing SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/integrating-the-web-editing-sdk"
---

This guide is for frontend developers who want to add video editing capabilities to a web application. The AI MediaKit Web Editing SDK lets you embed a complete editing workspace—including material management, track editing, effect rendering, and video export—directly into your application without building the underlying editor components yourself.

## SDK overview

The AI MediaKit Web Editing SDK, `@byteplus/amk-editor`, combines the editor UI, material management, track editing, effect rendering, and video export in a single package. Provide an editing project ID and a proxy endpoint to embed the complete editing experience in your application.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1aff130462a4498daaee61f1eff71cc3)

|Capability |Description |
|---|---|
|Theme and layout |The SDK includes a polished, ready\-to\-use editing UI. You can switch between light and dark themes to match your application. Built\-in layout controls, such as collapsing and expanding the material panel, work without additional development. |
|Editing project management |An editing project is a self\-contained editing task or draft. It stores the video, audio, and image materials used in the current edit, their arrangement on the timeline, applied effects and subtitles, and all other editing data. The SDK uses a unique project ID (`projectId`) to load and save this work automatically. |
|Material library management |The SDK provides a complete material management panel. Users can upload local files, add online resources by URL, or import materials from your asset library after you implement the required callbacks. The SDK automatically starts a frame\-extraction task for each material to generate preview thumbnails. Every material belongs to the current editing project and appears in the panel, ready to be dragged onto a track. |
|Preset resources |The SDK comes with a rich library of preset resources, including fonts, styled text, text animations, transitions, filters, and visual effects. Configuration options let you choose which resource panels to enable, giving your users a diverse set of creative tools. |
|Video export |The SDK includes a built\-in export dialog for settings such as resolution, frame rate, and format. After the user configures these settings, the SDK submits the entire editing project for asynchronous server\-side rendering and compositing. Users can view and download the finished video from the task list in the upper\-right corner. |
|ASR subtitles |Users can start a speech\-to\-subtitle (ASR) task for a video or audio material directly in the editor. When the task finishes, the SDK automatically adds the generated text and timestamps to the subtitle track. |

## Architecture and core concepts

The AI MediaKit Web Editing SDK follows one core design principle: to protect your API key, the browser must not call AI MediaKit directly. Instead, it sends requests through a proxy that you implement on your server. This proxy performs two functions:

* **Attach the API key securely**: Add the AI MediaKit API key stored on your server to each request.

* **Forward requests**: Securely forward SDK requests to the AI MediaKit server.

This architecture requires two key values in your SDK configuration:

|Concept |Description |
|---|---|
|projectId |**The unique identifier of an editing project.**  The SDK uses this ID to associate the project's material library with its editing data. Create an editing project through the server\-side API and obtain this ID before initializing the SDK. |
|endpoint (business proxy) |**The base URL of your proxy**, which injects the AI MediaKit API key, verifies user permissions, and securely forwards requests to AI MediaKit. For example, if you specify `xxx.xxx.com/api/amk-proxy`, the SDK sends requests to `xxx.xxx.com/api/amk-proxy/{targetPath}/...`. |

In short, you **create the project, implement the proxy, and configure the callbacks**. The SDK handles everything else, from UI rendering and data persistence to material management and video export. The following diagram illustrates this architecture:

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/11771271af9345a9a0f8207f0e148a99)

## Prerequisites

Before writing any integration code, complete the following one\-time setup to obtain the permissions and credentials required to create projects and implement the proxy.

* **Activate AI MediaKit**: Make sure AI MediaKit is activated for your [BytePlus account](https://console.byteplus.com/imp/ai-mediakit).

* **Obtain and protect your API key**: The API key is the only credential used to authenticate server\-side AI MediaKit API calls. Because it is tied to your account and grants extensive permissions, you must keep it secure. Create a dedicated key on the [API key management page](https://console.byteplus.com/imp/ai-mediakit/settings) in the AI MediaKit console, then store it as an environment variable on the server that hosts your proxy.

* **Enable MaaS subtitle recognition**: The SDK uses the `maas` provider for subtitle recognition. Complete the following setup before users submit an ASR request:

   1. Open [API Key](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default) in the Seed Speech console and create a dedicated API key.

   2. Open [Service Activation](https://console.byteplus.com/voice/new/setting/activate?projectName=default), find **Speech\-to\-Text (ASR) \- Audio File 2.0**, and click **Activate** in the upper\-right corner.

   3. On the [Settings](https://console.byteplus.com/imp/ai-mediakit/settings) page of the AI MediaKit console, grant AI MediaKit cross\-service access to Seed Speech.

   4. Wait about one minute for the configuration to take effect before submitting an ASR request. Requests sent during this period may fail with an insufficient\-permission error.

The API key is a privileged credential and must remain on the server. **Never** hardcode it in frontend code or expose it to the browser. Browser requests must go only to your proxy endpoint.

## Quick start

This section guides you through an end\-to\-end integration flow.

### Step 1: Install the frontend SDK

Run the following command in the root directory of your frontend project to add the SDK package to your project.

```Bash
# Using npm
npm install @byteplus/amk-editor

# Or using pnpm
pnpm add @byteplus/amk-editor
```

### Step 2: Create an editing project on the server

Call the AI MediaKit API from your server to create a cloud draft for each editing session. Then pass the returned `project_id` to the frontend as `projectId`. This ID identifies the project in all subsequent operations.

```Bash
# Run this request on your server
curl -X POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/editing/projects \
  -H "Authorization: Bearer $AMK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "name": "my-first-project" }'
```

`$AMK_API_KEY`: Replace this with the AI MediaKit API key you obtained from the AI MediaKit console and store securely on your server.

Response example:

```JSON
{
  "data": {
    "project_id": "proj_abc123",
    "name": "my-first-project",
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

Save `data.project_id` and pass it to the frontend as `projectId`.

### Step 3: Set up the server\-side proxy

Set up a proxy so the frontend SDK can call AI MediaKit through your backend without exposing the API key in the browser. The following minimal Node.js and Express implementation provides a starting point. For production use, add user authentication, rate limiting, and audit logging.

```JavaScript
// You can refer to the following logic and implement it with your own tech stack (such as Java, Go, or Python)
import express from 'express';
import fetch from 'node-fetch';

const app = express();
app.use(express.json({ limit: '10mb' }));

// --- The part you need to configure ---
const UPSTREAM_HOST = 'https://mediakit.ap-southeast-1.bytepluses.com'; // AI MediaKit server domain
const API_KEY = process.env.AMK_API_KEY; // Read your API key from an environment variable

if (!API_KEY) {
  throw new Error('AMK_API_KEY is not set in environment variables.');
}
// --- End of configuration ---

// --- The following code can usually be reused as is ---
// Define an allowlist of core SDK API paths to ensure security
const ALLOWED_PATHS = [
  /^\/api\/v1\/editing\//,
  /^\/api\/v1\/tools\/(multi-track-edit|extract-frames|extract-audio|transcode-audio|call-maas-proxy)$/,
  /^\/api\/v1\/tools-sync\/probe-image-metadata$/,
  /^\/api\/v1\/tools\/probe-(video|audio)-metadata$/,
  /^\/api\/v1\/tasks\/[^/]+$/,
];

app.all('/api/amk-proxy/api/v1/*', async (req, res) => {
  const path = req.originalUrl.replace('/api/amk-proxy', '');

  // 1. Path allowlist check (reusable as is)
  if (!ALLOWED_PATHS.some(rule => rule.test(path.split('?')[0]))) {
    return res.status(403).json({ error: 'AMK API path is not allowed' });
  }

  // 2. [You need to implement this] Business permission check
  // Verify here whether the currently signed-in user is authorized to access the requested projectId.
  // This is critical to preventing unauthorized data access.
  // const { projectId } = req.params;
  // const userId = req.session.userId;
  // if (!canUserAccessProject(userId, projectId)) {
  //   return res.status(403).json({ error: 'Forbidden' });
  // }

  // 3. Construct and forward the request (reusable as is)
  try {
    const upstreamResponse = await fetch(`${UPSTREAM_HOST}${path}`, {
      method: req.method,
      headers: {
        'Authorization': `Bearer ${API_KEY}`, // Inject the API key
        'Content-Type': req.method !== 'GET' ? 'application/json' : undefined,
      },
      body: req.method === 'GET' ? undefined : JSON.stringify(req.body ?? {}),
    });

    // 4. Pass the response through as is (reusable as is)
    const body = await upstreamResponse.text();
    res.status(upstreamResponse.status);
    res.setHeader('Content-Type', upstreamResponse.headers.get('content-type') ?? 'application/json');
    res.send(body);
  } catch (error) {
    console.error('Proxy request failed:', error);
    res.status(502).json({ error: 'Bad Gateway' });
  }
});
```

### Step 4: Initialize the SDK in the frontend

In your frontend, import and initialize the SDK to render the editor in a specified DOM container and load the project identified by `projectId`. Also configure the upload and asset\-management callbacks required by your application.

```TypeScript
import { AmkEditor } from '@byteplus/amk-editor';
import type { MaterialItem } from '@byteplus/amk-editor';

let editor: AmkEditor | null = null;

export async function mountAmkEditor(
  container: HTMLElement, // The DOM element in your page that hosts the editor
  projectId: string       // The project ID obtained in step 2
) {
  // Destroy the old instance to prevent duplicate mounting
  if (editor) {
    editor.destroy();
  }

  editor = new AmkEditor({
    // --- Required configuration ---
    container,
    projectId,
    endpoint: '/api/amk-proxy', // Points to the proxy address you created in step 3
    source: 'your-business', // Optional: an analytics source identifier used to distinguish which business integrates the SDK.
    accountId: 'your-account-id', // Optional: a business account or tenant ID, written into the AccountID analytics parameter.
    // --- Optional configuration (adjust according to your business needs) ---
    getHeaders: () => {
      // If your business proxy requires authentication, return an object containing the token here
      return {
        'X-Business-Token': getBusinessProxyToken(),
      };
    },
    theme: 'dark', // 'light' or 'dark'
    header: {
      show: true,
      onBack: () => history.back(), // Optional, defines the behavior when the back button is clicked
      onClose: () => history.back(), // Optional, defines the behavior when the close button is clicked
    },
    material: {
      uploadAccept: 'video/*,audio/*,image/*', // Optional: the file types supported by the local file picker

      // Triggered after the user confirms a local upload. This function is called once per file.
      // If configured, this custom callback takes priority over the built-in VOD upload.
      onUploadFile: async (file: File): Promise<MaterialItem> => {
        const item = await uploadFileToYourStorage(file);

        return {
          source_material_id: item.id, // Required: the unique ID of the business material
          name: item.name,
          type: item.type,             // 'video', 'audio', or 'image'
          url: item.playUrl,
          source: item.source,       // The original resource identifier used by the server for compositing
          duration: item.duration,   // Required for audio and video
          width: item.width,
          height: item.height,
        };
      },

      onUploadUrlMaterial: async (urls: string[]): Promise<MaterialItem[]> => {
        return importUrlsToYourStorage(urls); // Optional: import materials by URL; the return structure is the same as above
      },

      onRefreshPlayInfo: async (materials: MaterialItem[]): Promise<Partial<MaterialItem>[]> => {
        const result = await refreshMaterialPlayInfo(
          materials.map(item => ({
            sourceMaterialId: item.source_material_id,
            posterStorageKey: item.poster_storage_key,  // The backend can re-sign using a custom poster identifier
            spriteStorageKeys: item.sprite_storage_keys,  // The backend can re-sign using a custom sprite-sheet identifier
          })),
        );

        return result.map(item => ({
          material_id: item.materialId, // The unique field; the SDK matches the original material internally by material_id
          url: item.playUrl,
          source: item.playUrl,
          poster: item.poster,
          sprite: item.sprite,
        }));
      },

      onPersistExtractUrls: async ({ kind, urls, material }) => { // Persist the temporary URLs produced by the SDK's frame extraction into long-lived addresses
        const result = await persistExtractResults({
          kind,
          urls,
          sourceMaterialId: material.source_material_id,
        });

        return {
          urls: result.urls,
          materialPatch:
            kind === 'poster'
              ? { poster_storage_key: result.storageKeys[0], }
              : { sprite_storage_keys: result.storageKeys, },
        };
      },
    },

    decode: {
      enableAudioFrontendDecode: true, // Optional, audio waveform decoding
      enableVideoFrontendDecode: true, // Optional, video thumbnail decoding
    },
  });

  // Wait for the project to load and the editor to finish mounting
  await editor.whenReady();

  return editor;
}

export function unmountAmkEditor() {
  editor?.destroy();
  editor = null;
}
```

The material objects returned by the callbacks must conform to the SDK's standard format. For details, see [The material object format](https://docs.byteplus.com/en/docs/25/123449#the-material-object-format).

### Step 5: Create materials in bulk on the server

To add materials to a project before the user opens the editor, such as materials selected from an existing asset library, create them in bulk through the server\-side API.

```Bash
# Run this request on your server
curl -X POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/editing/projects/{projectId}/materials \
  -H "Authorization: Bearer $AMK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "materials": [
      {
        "source_material_id": "your_video_id_001",
        "name": "intro.mp4",
        "type": "video",
        "url": "https://example.com/intro.mp4",
        "duration": 15.2,
        "width": 1920,
        "height": 1080
      }
    ]
  }'
```

This API supports creating up to 100 materials per batch. The operation is atomic: if any material fails validation, the entire batch fails and no data is written.

### Step 6: Verify the integration

After completing the preceding steps, start your web application, open the editor page, and verify the following:

* **UI rendering**: Confirm that the editor loads correctly and displays the project name.

* **Material loading**: If you added materials through the API, confirm that they appear in the material library.

* **Local import**: Use the "Import" button to upload a local video or image, then confirm that it appears in the material library.

* **Track editing**: Drag a material from the library onto the timeline and preview it.

* **Auto\-save**: Trim or move an item on the timeline, refresh the page, and confirm that the editor restores the saved state.

If all checks pass, the basic SDK integration is complete.

## Advanced usage

This section describes advanced options for tailoring the SDK's behavior and appearance to your application.

### Material import and storage

This section helps you choose a material integration method, configure the import entries, and connect the SDK to custom storage or BytePlus VOD.

#### Choose an integration method

When users import local materials, choose either of the following methods:

* **Custom upload**: Configure `material.onUploadFile` to upload each file to your storage service. Use this method if you already have a material upload service or need full control over the upload flow.

* **Built\-in VOD upload**: Configure `storage` with a BytePlus VOD space and a credential callback. The SDK handles file upload, publishing, and playback\-address resolution. For details, see [Configure built-in BytePlus VOD storage for the SDK](https://docs.byteplus.com/en/docs/25/123449#configure-built-in-byteplus-vod-storage-for-the-sdk).

If both methods are configured, `material.onUploadFile` takes priority. If neither method is configured, the SDK does not show the local upload entry.

#### Import menu behavior

Depending on the `material` callbacks you implement, the behavior of the "Import" button in the material panel adjusts accordingly:

|Enabled import capabilities |Import entry behavior |
|---|---|
|No local upload, URL import, or asset\-library import capability |The "Import" button is not shown. |
|One capability, including built\-in VOD upload |The corresponding entry, such as "Local import", is shown directly. |
|Two or more capabilities |The enabled entries are grouped in an "Import" dropdown menu. |

#### Configure upload concurrency

Set `material.uploadConcurrency` to a positive integer, such as `3`, to limit concurrent custom single\-file uploads, built\-in VOD uploads, and temporary\-file persistence. A failed file does not affect files that upload successfully. URL import still calls `onUploadUrlMaterial(urls)` once for the entire batch. Temporary URLs are persisted individually, with a default maximum concurrency of 5. Your application controls concurrency for asset\-library imports.

### Configure custom material integration

Use material callbacks to connect your storage service or asset library and refresh playback addresses, posters, and sprite sheets when needed.

#### Key callback functions

The following are the purposes and implementation points of several core callbacks:

|Callback |Trigger timing |What you need to do |
|---|---|---|
|`onUploadFile` |After the user selects a local file in the UI. |Upload the single `File` to your storage service, then return a `MaterialItem` with a unique and immutable `source_material_id`. This callback takes priority over built\-in VOD upload. |
|`onUploadUrlMaterial` |After the user enters material URLs. |Import or transfer the URLs and return `MaterialItem[]`. |
|`onUploadFromSystem` |After the user chooses to import from the asset library. |Open your asset picker and return the selected `MaterialItem[]`; return `null` if the user cancels. |
|`onRefreshPlayInfo` |When custom storage is used and the SDK initializes or a playback URL expires. |Return the material fields whose playback URLs need to be updated. This callback is not required for built\-in VOD storage. |
|`onPersistExtractUrls` |After the SDK extracts a poster or sprite sheet. |Persist the generated temporary files and return new access addresses and storage identifiers. After writing a long\-lived address to `poster` or `sprite`, clear the corresponding `poster_task_id` or `sprite_task_id` when appropriate. |

#### Refresh playback addresses

The following example refreshes time\-limited material addresses when you use custom storage:

```TypeScript
material: {
  onRefreshPlayInfo: async (materials: MaterialItem[]) => {
    const idsToRefresh = materials.map(m => m.source_material_id);
    const refreshedResult = await fetchFreshPlayInfoFromYourBackend(idsToRefresh);

    return refreshedResult.map(item => ({
      material_id: item.material_id,
      url: item.fresh_url,
      poster: item.fresh_poster,
      source: item.fresh_url,
      sprite: item.fresh_sprite,
    }));
  },
}
```

#### Persist frame\-extraction results

The poster and sprite\-sheet URLs generated by the SDK may be temporary. Implement `onPersistExtractUrls` to save these files to your own storage and write the new storage identifiers, such as object keys, back to the material object for future refreshes.

```TypeScript
material: {
  onPersistExtractUrls: async ({ kind, urls, material }) => {
    const result = await yourBusinessPersistLogic({ kind, urls, material });

    return {
      urls: result.persistentUrls,
      materialPatch: kind === 'poster'
        ? { poster_storage_key: result.storageKeys[0] }
        : { sprite_storage_keys: result.storageKeys },
    };
  },
}
```

#### Trigger material import from application code

Call `requestMaterialImport(type, { onMaterialsImported })` to open the `local`, `url`, or `system` import entry. The `onMaterialsImported` callback in `options` applies only to that call. Use `material.onMaterialsImported` to listen for all material import results.

### Common configuration for the SDK's built\-in storage

To enable built\-in upload, configure both of the following fields in the top\-level `storage` object. SDK initialization fails if either field is missing.

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`storage.media_output_destination` |`string` |Conditionally required |\- |The material upload destination, in the format `vod://<space>`. `outputDestination` is not a valid option. |
|`storage.getUploadSTS` |`() => Credentials \| Promise<Credentials>` |Conditionally required |\- |Obtains short\-lived credentials from your business server. Return the credential object directly, or extract it from a response wrapper before returning it. |

Each `storage` object can specify only one upload destination.

### Configure built\-in BytePlus VOD storage for the SDK

You can use a [BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod) space as the upload destination for local materials. Configure the target space and a temporary\-credential callback when initializing the SDK. The SDK then handles file upload, media publishing, and playback\-address retrieval and refresh.

#### Core concepts

|Concept |Description |
|---|---|
|VOD space |The top\-level container for media assets in BytePlus VOD, uniquely identified by its space name. The SDK uploads and publishes local materials in this space. |
|`vod://` address |The fixed format used to specify the upload destination: `vod://<space>`. Enter only the space name. Do not include a Vid, subdirectory, query parameters, URL fragment, or playback domain. This value identifies an upload destination and is not an HTTP address that a browser can play directly. |
|Temporary STS credentials |Time\-limited VOD credentials issued by your server for the current user. The SDK uses them to upload and publish materials and query playback information without exposing a long\-term AK/SK in the browser. |

#### Workflow

The browser, your business server, and BytePlus VOD interact as follows:

1. The user selects a local file in the browser.

2. The SDK calls your `getUploadSTS` callback and requests temporary credentials from your business server.

3. Your server verifies that the signed\-in user can access the editing project, uses its securely stored long\-term AK/SK to issue temporary credentials for the target VOD space, and returns the credentials to the frontend.

4. The SDK uses the temporary credentials to upload and publish the file and retrieve its playback information.

5. When the project is loaded again or a temporary playback address is about to expire, the SDK calls `getUploadSTS` again and refreshes the playback address.

#### Step 1: Create a VOD space

Create a space in the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and record its space name. Set `storage.media_output_destination` to `vod://<space-name>`. Do not enter a playback domain, Vid, or HTTP(S) address.

#### Step 2: Implement an endpoint that issues temporary VOD credentials

Create an endpoint on your business server that issues temporary credentials for the signed\-in user. Before issuing credentials, verify that the user can access the requested editing project. Keep the long\-term AK/SK on the server and never return it to the browser.

The temporary credentials must include only the permissions required by the built\-in VOD workflow:

* `Vod:ApplyUploadInfo`

* `Vod:CommitUploadInfo`

* `Vod:UpdateMediaPublishStatus`

* `Vod:GetPlayInfo`

Your endpoint must return the following five fields. Field names are case\-sensitive.

|`getUploadSTS` return field |Type |Required |Default |Description |
|---|---|---|---|---|
|`AccessKeyId` |`string` |Yes |\- |Temporary Access Key ID. |
|`SecretAccessKey` |`string` |Yes |\- |Temporary Secret Access Key. |
|`SessionToken` |`string` |Yes |\- |STS session token. |
|`ExpiredTime` |`string` |Yes |\- |Credential expiration time. Use an ISO 8601 value that `Date.parse` can parse. A playback address cannot remain valid beyond the shorter of the credential's remaining lifetime and the 24\-hour limit, and its actual lifetime may also depend on the VOD domain authentication settings. Do not cache it indefinitely. |
|`CurrentTime` |`string` |Yes |\- |Current time returned by the service that issues the credentials. |

Install the BytePlus VOD Node.js SDK on your server:

```Bash
npm install @byteplus/vcloud-sdk-nodejs
```

The following example issues credentials with a 30\-minute lifetime:

```JavaScript
import { vodOpenapi } from '@byteplus/vcloud-sdk-nodejs';

if (!process.env.BYTEPLUS_ACCESSKEY || !process.env.BYTEPLUS_SECRETKEY) {
  throw new Error('BytePlus VOD AK/SK is not configured.');
}

const vodService = new vodOpenapi.VodService({
  accessKeyId: process.env.BYTEPLUS_ACCESSKEY,
  secretKey: process.env.BYTEPLUS_SECRETKEY,
  region: 'ap-southeast-1',
  host: 'vod.byteplusapi.com',
});

function createVodUploadSTS() {
  return vodService.signSts2(
    {
      Statement: [
        {
          Effect: 'Allow',
          Action: [
            'Vod:ApplyUploadInfo',
            'Vod:CommitUploadInfo',
            'Vod:UpdateMediaPublishStatus',
            'Vod:GetPlayInfo',
          ],
          Resource: [],
        },
      ],
    },
    30 * 60 * 1000,
  );
}

app.get('/api/vod-upload-sts', requireSignedInUser, async (req, res) => {
  await assertProjectAccess(req.user.id, req.query.projectId);
  res.json(createVodUploadSTS());
});
```

In this example, `Resource: []` does not restrict the credentials to a specific VOD resource. In production, follow the BytePlus VOD authorization rules and grant access only to the resources required by your application. For details, see the [BytePlus VOD Node.js SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk).

#### Step 3: Configure VOD storage when initializing the SDK

```TypeScript
import { AmkEditor } from '@byteplus/amk-editor';

async function fetchVodUploadSTS() {
  const response = await fetch(
    `/api/vod-upload-sts?projectId=${encodeURIComponent(projectId)}`,
    {
      credentials: 'include',
      headers: await getAmkHeaders(),
    },
  );
  if (!response.ok) {
    throw new Error(`Failed to get VOD STS: HTTP ${response.status}`);
  }
  const token = await response.json();
  return {
    AccessKeyId: token.AccessKeyId,
    SecretAccessKey: token.SecretAccessKey,
    SessionToken: token.SessionToken,
    ExpiredTime: token.ExpiredTime,
    CurrentTime: token.CurrentTime,
  };
}

const editor = new AmkEditor({
  container,
  projectId,
  endpoint: '/api/amk-proxy',
  source: 'your-app-name',
  storage: {
    media_output_destination: 'vod://your-space-name',
    getUploadSTS: fetchVodUploadSTS,
  },
});
```

You implement `/api/vod-upload-sts`; it is not a fixed SDK endpoint. Configure `storage.media_output_destination` and `storage.getUploadSTS` together. If you also configure `material.onUploadFile`, the custom callback takes priority.

### Business proxy security hardening

In production, your proxy must provide security and reliability in addition to basic request forwarding.

#### API allowlist

Define a strict API path allowlist to prevent proxy abuse and accept only legitimate SDK requests:

|Method |Path |Purpose |
|---|---|---|
|GET |`/api/v1/editing/projects/{projectId}` |Read project information |
|PATCH |`/api/v1/editing/projects/{projectId}` |Modify the project name |
|GET |`/api/v1/editing/projects/{projectId}/materials` |Read the material library with pagination |
|POST |`/api/v1/editing/projects/{projectId}/materials` |Add or bulk\-add materials |
|PUT |`/api/v1/editing/projects/{projectId}/materials` |Update material information |
|DELETE |`/api/v1/editing/projects/{projectId}/materials` |Delete materials |
|GET |`/api/v1/editing/projects/{projectId}/editor` |Read editing data |
|PUT |`/api/v1/editing/projects/{projectId}/editor` |Save editing data |
|GET |`/api/v1/editing/preset-library` |Get preset resources |
|POST |`/api/v1/tools/multi-track-edit` |Submit a video export task |
|POST |`/api/v1/tools/extract-frames` |Submit a frame\-extraction task |
|POST |`/api/v1/tools/extract-audio` |Extract audio for MaaS subtitle recognition |
|POST |`/api/v1/tools/transcode-audio` |Transcode audio for MaaS subtitle recognition |
|POST |`/api/v1/tools/call-maas-proxy` |Submit a MaaS subtitle recognition request |
|POST |`/api/v1/tools-sync/probe-image-metadata` |Get image metadata |
|POST |`/api/v1/tools/probe-video-metadata` |Submit a video metadata task |
|POST |`/api/v1/tools/probe-audio-metadata` |Submit an audio metadata task |
|GET |`/api/v1/tasks/{taskId}` |Query an asynchronous task |

#### Security essentials

* **API key isolation**: Inject the API key only within your proxy. It must never appear in browser requests.

* **Strong permission checks**: Verify that the current user can access the requested `projectId`.

* **Response pass\-through**: Pass through the status codes and response bodies returned by AI MediaKit so the SDK can handle task states and errors correctly.

* **Logging and monitoring**: Record the request ID, project ID, user ID, and request duration for troubleshooting, but never record the API key.

#### CORS and dynamic request headers

SDK requests to AI MediaKit include the `X-Amk-Task-Source: vibe-editing` header. Allow this header in your proxy's CORS configuration. `getHeaders` can return an object or a Promise and is called before each request, making it suitable for short\-lived business tokens. Configure CORS separately for direct storage uploads, output CDNs, and the business proxy.

### UI configuration and resource panels

You can configure the editor's appearance and available features to match your application.

#### Theme and title bar

You can customize the editor's theme and define the behavior of the back and close buttons in the title bar. Use `header.mount` to mount an external header and `header.onTitleUpdateSuccess` to run a callback after the title is saved.

```TypeScript
const editor = new AmkEditor({
  // ... other configuration
  theme: 'dark',  // 'light' or 'dark', defaults to 'light'
  header: {
    show: true,   // Whether to show the title bar, defaults to true
    onBack: () => { // Define the behavior when the back button is clicked, such as returning to the previous page
      history.back();
    },
    onClose: () => { // Define the behavior when the close button is clicked
      console.log('Close button clicked');
    },
  },
});
```

#### Resource panel switches

The SDK includes preset resource panels for fonts, styled text, transitions, and more. You can disable individual panels to simplify the UI or tailor the available features.

|Option |Description |Default |
|---|---|---|
|`font` |Font panel |`true` |
|`wordArt` |Styled text panel |`true` |
|`textAnimation` |Text animation (entrance/exit/loop) panel |`true` |
|`transition` |Transition panel |`true` |
|`filter` |Filter panel |`true` |
|`effect` |Visual effect panel |`true` |

Setting an option to `false` hides that panel and prevents the SDK from requesting its resources, which can improve loading performance. For example, the following configuration disables styled text and transitions:

```TypeScript
const editor = new AmkEditor({
  // ... basic configuration
  wordArt: false,    // Disable the styled text panel
  transition: false, // Disable the transition panel
  // Other panels keep their default enabled state
});
```

#### Left panel layout

The SDK includes built\-in collapse and expand functionality for the left material panel, with no extra configuration required. After the user clicks the collapse button, the preview area automatically expands to full width and shows a "Materials" entry on the left edge to reopen the panel.

### Configure subtitle recognition (ASR)

The subtitle recognition entry uses the `maas` provider. You can omit `toolbar.asr.provider` or set it to `maas` explicitly:

```TypeScript
const editor = new AmkEditor({
  container,
  projectId,
  endpoint: '/api/amk-proxy',
  toolbar: {
    asr: { provider: 'maas' },
    builtInVisibility: { asrSubtitle: true },
  },
});
```

Before using this feature, complete the Seed Speech setup described in [Prerequisites](https://docs.byteplus.com/en/docs/25/123449#prerequisites). The business proxy must allow `extract-audio`, `transcode-audio`, `call-maas-proxy`, and task\-query paths. The source media URL must remain accessible to the server while the task runs. Temporary audio generated during processing is not added to the material library.

Canceling or closing the progress dialog, or calling `destroy()`, stops local waiting and prevents the subtitles from being written to the project, but does not cancel a task that has already been submitted.

### Export and asynchronous tasks

When the user clicks the "Export video" button in the title bar, the SDK opens a built\-in form for configuring the video name, resolution, frame rate, format, encoding method, and quality\-enhancement option. Export runs asynchronously, so users can continue editing while the background task runs.

Set `header.exportTaskList` to `false` to hide the export\-history entry and stop its queries. Set `export.qualityEnhancement` to `true` to show the quality\-enhancement option. The export history belongs to the current page session and is not restored after a refresh.

Submitting an export task does not change the current project state or preview. If the selected export resolution differs from the canvas resolution, the SDK adapts the exported content automatically.

|Task type |Tool API |Description |
|---|---|---|
|Video export |`multi-track-edit` |Renders and composites the editing data into a video file. |
|MaaS subtitles |`extract-audio`, `transcode-audio`, and `call-maas-proxy` |Extracts and transcodes audio as needed, then recognizes speech and writes subtitle text to the current project. |
|Frame extraction |`extract-frames` |Generates a poster or sprite sheet for a video material. |

All asynchronous tasks are polled through `GET /api/v1/tasks/{taskId}`. Subtitle recognition presents a blocking progress dialog in the SDK and writes the result to the subtitle track after the task succeeds. Closing the page or calling `editor.destroy()` stops browser\-side polling only; it does not cancel a task already submitted to the server.

## Reference

This chapter provides the detailed reference information needed when integrating the Web Editing SDK, including server\-side APIs, SDK initialization configuration, instance methods, and events.

### Server\-side API reference

The following APIs are the interfaces you may need to call on your server when interacting with the AI MediaKit backend service.

#### Basic information

|Item |Description |
|---|---|
|Host |`https://mediakit.ap-southeast-1.bytepluses.com` |
|Base Path |`/api/v1/editing` |
|Authentication |`Authorization: Bearer <YOUR_AMK_API_KEY>` |

#### Response conventions

All APIs return `200 OK` at the HTTP level. Check the response body to determine whether the request succeeded or failed.

|The response body contains |Meaning |
|---|---|
|The `data` field |The request succeeded. |
|The `error` field |The request failed. The `error.code` field identifies the error type. |

Common error codes:

|`error.code` |Meaning |
|---|---|
|`invalid_request` |Request parameter validation failed. |
|`unauthorized` |Authentication failed or no permission to access the resource. |
|`not_found` |The requested resource does not exist. |
|`conflict` |Resource conflict (for example, trying to create a project with a duplicate name). |
|`internal_error` |An internal server error. |

#### The material object format

All material\-related APIs and callbacks follow this standard format.

|Field |Type |Required |Default |Description |
|---|---|---|---|---|
|`material_id` |`string` |No |\- |The unique material ID within the project, generated by AI MediaKit after creation. |
|`source_material_id` |`string` |Yes |\- |The unique primary key in your system, such as a VOD Vid or storage object key. The maximum length is 255 characters. |
|`name` |`string` |Yes |\- |The display name, up to 255 characters. |
|`type` |`string` |Yes |\- |The material type: `video`, `audio`, or `image`. |
|`source` |`string` |Yes |\- |The original resource identifier used for server\-side compositing. Use `vid://<Vid>` for authorized BytePlus VOD resources. Other resources must use an HTTP(S) address accessible from the public internet. |
|`url` |`string` |Yes |\- |The public HTTPS address used by the browser for preview. For smoother preview and higher export quality, use a low\-bitrate file for `url` and retain the original file in `source`. |
|`duration` |`number` |Conditionally required |\- |Required for `video` and `audio`, in seconds. |
|`width` |`number` |Conditionally required |\- |Required for `video` and `image`, in pixels. |
|`height` |`number` |Conditionally required |\- |Required for `video` and `image`, in pixels. |
|`poster` |`string` |No |\- |The video poster address. If omitted, the SDK may submit a frame\-extraction task when needed. |
|`sprite` |`object` |No |\- |Sprite\-sheet data for timeline preview, typically including `storeurls` and `capturenum`. |
|`waveform` |`object` |No |\- |Audio waveform data displayed on the timeline. |
|Custom fields |Any |No |\- |You can add business fields such as `my_custom_field`; the server stores and returns them unchanged. |

#### Create a project

`POST /api/v1/editing/projects`

Create a new editing project and return its unique identifier `project_id`.

**Request parameters**

|Parameter |Type |Required |Description |
|---|---|---|---|
|`name` |`string` |Yes |The project name, up to 255 characters. |
|`description` |`string` |No |A detailed description of the project. |

**Request example**

```JSON
{
  "name": "my-awesome-project",
  "description": "An optional description for the project."
}
```

**Response example**

```JSON
{
  "data": {
    "project_id": "proj_abc123xyz",
    "name": "my-awesome-project",
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

#### Create materials in bulk

`POST /api/v1/editing/projects/{projectId}/materials`

Add materials to the specified project in bulk. This operation is atomic: if any material fails validation, the entire batch fails.

**Request parameters**

|Parameter |Type |Required |Description |
|---|---|---|---|
|`materials` |`MaterialItem[]` |Yes |An array of material objects, each conforming to [the material object format](https://docs.byteplus.com/en/docs/25/123449#the-material-object-format). A single request supports up to 100 materials. |

**Request example**

```JSON
{
  "materials": [
    {
      "source_material_id": "vid_001",
      "name": "intro.mp4",
      "type": "video",
      "url": "https://example.com/intro.mp4",
      "duration": 15.2,
      "width": 1920,
      "height": 1080
    }
  ]
}
```

**Response example**

```JSON
{
  "data": {
    "materials": [
      {
        "material_id": "mat_pqr789",
        "source_material_id": "vid_001",
        "name": "intro.mp4",
        "type": "video",
        "url": "https://example.com/intro.mp4",
        "duration": 15.2,
        "width": 1920,
        "height": 1080
      }
    ]
  }
}
```

#### Update materials in bulk

`PUT /api/v1/editing/projects/{projectId}/materials`

Update or insert materials in the specified project in bulk. This operation is atomic: if any material in the request fails to process, the entire batch is rolled back and no partial data is written. This API automatically decides whether to update or insert based on `source_material_id`:

* Update an existing material: If the `source_material_id` of a material in the request **already exists** in the project, that material is updated. In this case, you only need to provide the fields to be modified. For example, passing in only `name` renames the material, and the other fields remain unchanged.

* Insert a new material: If the `source_material_id` **does not exist** in the project, a new material record is created. In this case, you must provide all the required fields for creating a material (such as `type`, `url`, and `source`).

**Request parameters**

|Parameter |Type |Required |Description |
|---|---|---|---|
|`materials` |`Partial<MaterialItem>[]` |Yes |An array of material objects, each conforming to [the material object format](https://docs.byteplus.com/en/docs/25/123449#the-material-object-format). A single request supports up to 100 materials. |

**Request example**

```JSON
{
  "materials": [
    {
      "source_material_id": "vid_001",
      "name": "new-intro.mp4",
      "url": "https://example.com/new-intro.mp4"
    }
  ]
}
```

**Response example**

```JSON
{
  "data": {
    "materials": [
      {
        "material_id": "mat_pqr789",
        "source_material_id": "vid_001",
        "name": "new-intro.mp4",
        "type": "video",
        "url": "https://example.com/new-intro.mp4",
        "duration": 15.2,
        "width": 1920,
        "height": 1080
      }
    ]
  }
}
```

### SDK initialization configuration

The following table lists all configuration options supported by `new AmkEditor()`.

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`container` |`HTMLElement` |Yes |\- |The DOM container where the SDK is mounted. |
|`projectId` |`string` |Yes |\- |The ID of a created editing project. |
|`endpoint` |`string` |Yes |\- |The address of the business proxy. |
|`getHeaders` |`() => Record<string, string> \| Promise<Record<string, string>>` |No |\- |Obtains headers before each proxy request and can pass short\-lived business tokens. |
|`theme` |`'light' \| 'dark'` |No |`'light'` |The editor theme. |
|`header` |`object` |No |\- |Title\-bar configuration, including `show`, `onBack`, `onClose`, `mount`, `onTitleUpdateSuccess`, and `exportTaskList`. |
|`material` |`object` |No |\- |Material import, refresh, persistence, `uploadConcurrency`, and `onMaterialsImported` configuration. |
|`export` |`object` |No |\- |Export dialog and export parameter configuration, including `qualityEnhancement`. |
|`getLicenseUrl` |`string` \| `function` |No |\- |The address or function used to obtain the license for encrypted video playback. |
|`storage` |`object` |No |\- |Built\-in BytePlus VOD upload and playback\-address resolution. `storage.media_output_destination` and `storage.getUploadSTS` must be configured together. |
|`i18n` |`object` |No |\- |Locale and custom copy overrides. The BytePlus default is `en-US`. |
|`font` ... `effect` |`boolean` |No |`true` |Switches for fonts, styled text, text animations, transitions, filters, and effects. |
|`layout`, `track`, `toolbar`, `shortcut` |`object` |No |\- |Editor layout, timeline, toolbar, and shortcut configuration. `toolbar.asr.provider` uses `maas` by default and accepts `maas` as its provider value. |
|`interaction.readonly` |`boolean` |No |`false` |Enables read\-only mode. |
|`frameRate` |`object` |No |\- |Frame mode and frame\-rate configuration. |
|`timeDisplayFormat` |`'hms' \| 'msms' \| 'msf'` |No |\- |Timeline time display format. |
|`debug` |`boolean` |No |`false` |Enables debug logs. |
|`source` |`string` |No |\- |A business source identifier. |
|`accountId` |`string` |No |\- |A business account or tenant identifier. |

### SDK instance methods

The `AmkEditor` instance exposes the following common methods.

|Method |Return value |Description |
|---|---|---|
|`whenReady()` |`Promise<this>` |Returns a Promise that resolves after the project is loaded and the editor is mounted. |
|`getEditor()` |`VeVeditor` instance |Gets the underlying `VeVeditor` editor instance, used to call richer underlying capabilities or listen for events. |
|`getI18n()` |i18n instance |Gets the internationalization instance for switching locales dynamically. |
|`requestExport()` |`Promise<result>` |Opens the export dialog programmatically. |
|`requestMaterialImport(type, options?)` |`boolean` |Opens the `local`, `url`, or `system` material import entry. `options.onMaterialsImported` applies only to this call. |
|`getProject()` |`object` |Returns a synchronous snapshot of the current project, including its name, materials, and editing data. |
|`fetchProjectMaterials()` |`Promise<MaterialItem[]>` |Fetches the latest material list from the server without updating the material panel automatically. |
|`refreshPlayInfo(ids?)` |`Promise<void>` |Manually triggers a playback\-information refresh for the specified list of `material_id` values or for all materials. |
|`invokeTool(options)` |`Promise<T>` |Calls a general AI MediaKit Tool API. |
|`destroy()` |`void` |Destroys the editor instance and releases all resources, event listeners, and timers. |

### SDK event listening

Use `editor.getEditor().on(eventName, handler)` to listen for events from the underlying editor.

|Event name |Description |
|---|---|
|`editParam:changed` |A track or canvas parameter changed. **Note**: The SDK has implemented auto\-save, so you usually do not need to manually submit data in this event. |
|`element:selected` |The user selected an element on a track or the canvas. |
|`track:changed` |An element on the timeline track was added, deleted, or modified. |
|`material:changed` |The list content in the material panel changed. |
|`playback:play` / `playback:pause` |The player state switched between playing and paused. |
|`playback:seek` |The time point of the preview playback changed. |
|`history:stackChanged` |The undo/redo history stack changed. |
|`timeline:scaleChanged` |The user zoomed the timeline. |
|`crashed` |The editor instance crashed. |

Listening and destruction example:

```TypeScript
await editor.whenReady();
const vev = editor.getEditor();

const handleTrackChange = (payload) => {
  console.log('Track has been changed:', payload);
};

// Listen for the event
vev?.on?.('track:changed', handleTrackChange);

// When the component unmounts (such as in a React useEffect cleanup function or Vue onUnmounted),
// be sure to remove the listener and destroy the editor to prevent memory leaks.
function cleanup() {
  vev?.off?.('track:changed', handleTrackChange);
  editor.destroy();
}
```

### Built\-in resource reference

To help you build features quickly, the SDK comes with a rich preset resource library covering styled text, fonts, visual effects, transitions, filters, and text animations. You can enable or disable them as needed through [UI configuration and resource panels](https://docs.byteplus.com/en/docs/25/123449#ui-configuration-and-resource-panels).

The current BytePlus preset resource library includes **5 fonts** (Montserrat, Inter, Source Han Serif, Roboto, OPPO Sans) and **24 transitions**, along with visual effects, filters, styled text, and text animations. For the complete list of resource IDs available to your account, call the preset library API (`/api/v1/editing/preset-library`).

### SDK release history

|Date |Version |Description |
|---|---|---|
|October 21, 2026 |0.0.10 |First release. |

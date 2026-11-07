---
title: "Integrating the Web Vibe Editing SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/integrating-the-web-vibe-editing-sdk"
---

This guide is for frontend and server\-side developers who want to add AI Vibe Editing capabilities to a web application. The AI MediaKit Web Vibe Editing SDK (`@byteplus/amk-editor-assistant`) lets you embed a complete set of AI\-powered video creation tools, from material management and intelligent sequencing to effect rendering and high\-resolution export, without integrating each editing component and AI service separately.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/aa14c00c36d143f6a32a9b530e72d086)

## SDK overview

`@byteplus/amk-editor-assistant` is an all\-in\-one intelligent video editing SDK for the browser. It combines a powerful AI assistant with a professional editor to provide a natural\-language\-driven video creation experience.

|Core capability |Description |
|---|---|
|AI assistant |Users can complete complex editing tasks through natural\-language conversation. For example: "Analyze the video, extract the highlights, and add subtitles" or "Use the provided materials to create a well\-structured vlog." The AI assistant interprets the request and invokes the appropriate tools automatically. |
|Web editor |A fully featured built\-in editor with multi\-track editing, precise trimming, real\-time preview, text and subtitles, visual effects, transitions, filters, and other professional capabilities for fine\-grained adjustments. |
|Cloud\-based AI tools |Built\-in AI MediaKit tools for automatic speech recognition (ASR), video frame extraction, video understanding, highlight recognition, and other media\-processing tasks. The AI assistant selects and invokes these tools based on the user's request. |
|Scenario\-based Vibe Editing workflows |Ready\-to\-use workflows for general and short\-drama highlight editing, rough cuts for AI\-generated short comics, automated multi\-asset editing, and vlog creation. Each workflow automates material selection, sequencing, and effect application to accelerate video production. |

## Architecture and core concepts

The Web Vibe Editing SDK runs in the browser and communicates with AI MediaKit through a proxy that you implement on your server.

![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/92f992143a984d8ba970067059ff82ae)

### Request paths

The browser uses two logical request paths: one for the editor and one for the AI assistant. Both share a top\-level `endpoint` that points to the same proxy entry. The SDK appends the appropriate upstream path for each:

|Path |SDK configuration entry |Main responsibilities |
|---|---|---|
|Editing API |Top\-level `endpoint`, `getHeaders` |Load and save editing projects, manage materials, call basic editing tools (such as transcoding and concatenation), query task status, and access the preset resource library. |
|Assistant Runtime API |Top\-level `endpoint` (the Runtime address is derived automatically), `assistant.runtime.getHeaders` |Run the language model, manage conversation history, and call AI assistant tools, including cloud editing tools and frontend tools. |

### Business proxy

To protect your API key, the browser must not call AI MediaKit directly. All requests must go through a proxy that you implement on your server. This proxy performs three functions:

1. **Attach the API key securely**: Add the AI MediaKit API key stored on your server to the request headers.

2. **Verify user permissions**: Confirm that the signed\-in user can access the requested `projectId` to prevent unauthorized data access.

3. **Forward requests**: Securely forward SDK requests to the appropriate AI MediaKit service.

## Pricing

Using the Web Vibe Editing SDK may incur three types of fees: ModelArk model usage fees, AI MediaKit video tool fees, and AI MediaKit editing tool fees. Billing follows a pay\-as\-you\-go model with daily settlement: charges from the previous day are calculated and settled at 6:00 the following day.

### ModelArk model usage fees

The AI assistant uses the ModelArk models configured in the SDK for natural\-language conversation and multimodal content understanding. ModelArk charges for the input and output tokens consumed by these models. For pricing by model, see [ModelArk Pricing](https://docs.byteplus.com/en/docs/ModelArk/1544106).

### AI MediaKit capability fees

The AI assistant and manual editing operations may invoke AI MediaKit capabilities. These charges fall into two main categories:

* **Video tools**: The AI assistant may call video tools for subtitle recognition, frame extraction, video understanding, and highlight recognition. Each capability is billed according to its own rules. For details, see [Pricing](https://docs.byteplus.com/uchbv7an/hngf1zm0).

* **Editing tools**: Exporting a video incurs an editing fee based on the duration and resolution of the final output. For details, see [Pricing](https://docs.byteplus.com/uchbv7an/hngf1zm0).

## Prerequisites

Before writing any integration code, complete the following setup:

* **Activate the service**: Make sure AI MediaKit is activated for your [BytePlus account](https://console.byteplus.com/imp/ai-mediakit).

* **Obtain an API key**: Create and obtain an API key on the [API key management page](https://console.byteplus.com/imp/ai-mediakit/settings) in the AI MediaKit console. This credential is used by your server\-side proxy.

* **Obtain the model endpoint IDs**: Go to the [ModelArk Console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint) to enable the required model services and obtain their endpoint IDs. The Web Vibe Editing SDK requires a language model and supports optional multimodal understanding models:

   * Language model (required): Interprets the user's natural\-language instructions and plans the workflow. Set the endpoint ID through `assistant.model` when initializing the SDK. Choose one of the following models based on response quality, latency, and cost:

      * `dola-seed-2-1-turbo-260628`

      * `seed-2-0-pro-260328`

   * Multimodal understanding models (optional): Analyze video, audio, and image content. Configure their endpoint IDs through `assistant.preferMultiModalModels` when initializing the SDK.

      * Visual understanding (recommended): We recommend `dola-seed-2-1-turbo-260628` for understanding visual content such as video frames and images.

      * Audio understanding (as needed): When the AI assistant needs to understand audio content, configure an audio\-capable multimodal model endpoint ID, such as `seed-2-0-lite-260428`.

* **Perform cross\-service authorization**: Go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console to grant AI MediaKit permission to access your **ModelArk** resources.

* **Enable MaaS subtitle recognition**: Set `toolbar.asr.provider` to `maas`, and complete the following setup before users submit an ASR request:

   1. Open [API Key](https://console.byteplus.com/voice/new/setting/apikeys?projectName=default) in the Seed Speech console and create a dedicated API key.

   2. Open [Service Activation](https://console.byteplus.com/voice/new/setting/activate?projectName=default), find **Speech\-to\-Text (ASR) \- Audio File 2.0**, and click **Activate** in the upper\-right corner.

   3. On the [Settings](https://console.byteplus.com/imp/ai-mediakit/settings) page of the AI MediaKit console, grant AI MediaKit cross\-service access to Seed Speech.

   4. Wait about one minute for the configuration to take effect before submitting an ASR request. Requests sent during this period may fail with an insufficient\-permission error.

## Quick start

This section walks you through an end\-to\-end integration for a basic Vibe Editing application.

### Step 1: Install the frontend SDK

Run the following command in the root directory of your frontend project:

```Bash
# Using npm
npm install @byteplus/amk-editor-assistant react react-dom

# Or using pnpm
pnpm add @byteplus/amk-editor-assistant react react-dom
```

### Step 2: Create an editing project on the server

From your server, call the AI MediaKit API to create a cloud editing project for each editing session, then pass its unique `project_id` to the frontend.

**Request example:**

```Bash
# Make this request on your server
curl -X POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/editing/projects \
  -H "Authorization: Bearer $AMK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "name": "my-smart-project" }'
```

`$AMK_API_KEY`: Replace this with the API key you obtained from the AI MediaKit console and store securely on your server.

**Response example:**

```JSON
{
  "data": {
    "project_id": "proj_smart_abc123",
    "name": "my-smart-project",
    "created_at": "2024-01-01T00:00:00Z"
  }
}
```

Save `data.project_id` and pass it to the frontend as `projectId`.

### Step 3: Set up the server\-side proxy

The editor and AI assistant share one proxy entry, such as `/api/amk-proxy`. The SDK appends the full upstream path for the Editing API or Assistant Runtime API. The following Node.js and Express example includes path allowlists and forwarding logic for both. For production use, add user authentication, project\-level permission checks, rate limiting, and audit logging.

```JavaScript
// For Node.js 18+
import express from 'express';
import { Readable } from 'node:stream';
import { pipeline } from 'node:stream/promises';

const app = express();
app.use(express.json({ limit: '10mb' }));

// --- The part you need to configure ---
const PROXY_PREFIX = '/api/amk-proxy';
const UPSTREAM_BASE_URL = 'https://mediakit.ap-southeast-1.bytepluses.com';
const API_KEY = process.env.AMK_API_KEY; // Read your API key from an environment variable

if (!API_KEY) {
  throw new Error('AMK_API_KEY is not set in environment variables.');
}

// Editing API path allowlist
const ALLOWED_EDITOR_PATHS = [
  /^\/api\/v1\/editing\//,
  /^\/api\/v1\/tools\//,
  /^\/api\/v1\/tools-sync\//,
  /^\/api\/v1\/tasks\/[^/]+\/?$/,
];

// Assistant Runtime API path allowlist
const ALLOWED_ASSISTANT_PATHS = [
  ['GET', /^\/api\/v1\/studio\/agents\/copilotkit\/?$/],
  ['POST', /^\/api\/v1\/studio\/agents\/copilotkit\/?$/],
  ['GET', /^\/api\/v1\/studio\/agents\/threads(?:\/|$)/],
  ['GET', /^\/api\/v1\/studio\/agents\/agents(?:\/|$)/],
];
// --- End of configuration ---

app.use(PROXY_PREFIX, async (req, res) => {
  // The SDK already includes the full /api/v1/... upstream path in the request;
  // the proxy only strips the local prefix and must not append /api/v1/editing again.
  const upstreamPath = req.originalUrl.slice(PROXY_PREFIX.length);
  const pathname = upstreamPath.split('?')[0];
  const assistantRequest = pathname.startsWith('/api/v1/studio/agents/');

  if (assistantRequest) {
    // 1. [Security] Assistant Runtime API path allowlist check
    const allowed = ALLOWED_ASSISTANT_PATHS.some(
      ([method, pattern]) => req.method === method && pattern.test(pathname)
    );
    if (!allowed) {
      return res.status(403).json({ error: 'Assistant Runtime API path is not allowed' });
    }
  } else {
    // 1. [Security] Editing API path allowlist check
    const allowed = ALLOWED_EDITOR_PATHS.some(pattern => pattern.test(pathname));
    if (!allowed) {
      return res.status(403).json({ error: 'Editing API path is not allowed' });
    }
  }

  // 2. [Security - you need to implement this] Business permission check
  // Verify here whether the currently signed-in user is authorized to access the requested projectId, to prevent unauthorized data access.

  const controller = new AbortController();
  const timeoutMs = assistantRequest ? 30 * 60_000 : 60_000;
  const timeoutId = setTimeout(() => controller.abort(), timeoutMs);
  const onClose = () => {
    if (!res.writableFinished) controller.abort();
  };
  res.on('close', onClose);

  try {
    const headers = {
      'Authorization': `Bearer ${API_KEY}`,
      'Accept': assistantRequest
        ? req.headers.accept ?? 'application/json'
        : 'application/json',
    };

    if (!['GET', 'HEAD'].includes(req.method)) {
      headers['Content-Type'] = 'application/json';
    }
    if (assistantRequest && typeof req.headers['x-endpoint-id'] === 'string') {
      headers['X-Endpoint-Id'] = req.headers['x-endpoint-id'];
    }

    const upstreamResponse = await fetch(`${UPSTREAM_BASE_URL}${upstreamPath}`, {
      method: req.method,
      headers,
      body: ['GET', 'HEAD'].includes(req.method)
        ? undefined
        : JSON.stringify(req.body ?? {}),
      signal: controller.signal,
      redirect: 'manual',
    });

    // 3. Pass through the response headers and status code as is
    res.status(upstreamResponse.status);
    res.setHeader(
      'Content-Type',
      upstreamResponse.headers.get('content-type') ?? 'application/json'
    );
    res.setHeader('Cache-Control', 'no-cache');
    res.setHeader('X-Accel-Buffering', 'no'); // Disable buffering for Nginx

    // 4. Stream the response body through (critical)
    if (upstreamResponse.body) {
      await pipeline(Readable.fromWeb(upstreamResponse.body), res);
    } else {
      res.end();
    }
  } catch (error) {
    if (res.destroyed) return;
    if (!res.headersSent) {
      res.status(502).json({ error: 'AI MediaKit request failed' });
    } else {
      res.destroy(); // If the stream has already started, we can only close abnormally
    }
  } finally {
    clearTimeout(timeoutId);
    res.off('close', onClose);
  }
});
```

### Step 4: Initialize the SDK in the frontend

In your frontend page, import the SDK and its styles, prepare a DOM container, and then call `createAmkEditorAssistant` to create and mount the instance.

**Prepare the mount container:**

```HTML
<div id="amk-container"></div>
```

```CSS
/* Make sure the container has explicit dimensions */
#amk-container {
  width: 100%;
  height: 100vh;
}
```

**Create the instance:**

```TypeScript
import {
  createAmkEditorAssistant,
  type AmkEditorUploadSTSCredentials,
  type MaterialItem,
} from '@byteplus/amk-editor-assistant';
import '@byteplus/amk-editor-assistant/styles.css';

// Example: obtain a short-lived credential for accessing the proxy from the business backend.
async function getShortLivedToken(): Promise<string> {
  return 'your_business_auth_token';
}

const getAmkHeaders = async (): Promise<Record<string, string>> => ({
  Authorization: `Bearer ${await getShortLivedToken()}`,
});

// Obtain minimal-privilege, short-lived VOD temporary credentials from the business server.
// The browser must not store or use the customer's long-term AK/SK.
async function getUploadSTS(): Promise<AmkEditorUploadSTSCredentials> {
  const response = await fetch('/api/amk-upload-sts', {
    method: 'POST',
    headers: await getAmkHeaders(),
  });
  if (!response.ok) {
    throw new Error(`Get upload STS failed: HTTP ${response.status}`);
  }
  return (await response.json()) as AmkEditorUploadSTSCredentials;
}

// An alternative implementation for custom storage upload.
// If enabled, this callback takes priority over the built-in VOD upload.
async function uploadFileToBusinessStorage(
  file: File,
): Promise<MaterialItem> {
  const item = await uploadFileToYourStorage(file);
  return {
    source_material_id: item.id, // Required: the unique ID of the business material
    name: item.name,
    type: item.type, // 'video', 'audio', or 'image'
    url: item.playUrl, // A browser-accessible HTTP(S) address
    source: item.source, // The original HTTP(S) resource address used by the server for compositing
    duration: item.duration, // Required for video and audio
    width: item.width, // Required for video and image
    height: item.height, // Required for video and image
  };
}

const container = document.getElementById('amk-container');
if (!container) {
  throw new Error('Container element not found');
}

const sdk = createAmkEditorAssistant({
  // Required configuration
  container,
  projectId: 'proj_smart_abc123', // The project ID created in step 2
  endpoint: '/api/amk-proxy', // The business proxy entry shared by the editor and the assistant
  getHeaders: getAmkHeaders, // Dynamically obtain the editor request headers

  // AI assistant configuration
  assistant: {
    // The language model endpoint ID, used to process natural-language instructions.
    // Recommended: dola-seed-2-1-turbo-260628, seed-2-0-pro-260328
    model: 'ep-language-model',

    // The multimodal understanding model endpoint IDs.
    // Audio understanding: seed-2-0-lite-260428
    // Visual understanding: dola-seed-2-1-turbo-260628
    preferMultiModalModels: ['ep-understanding-model'],

    runtime: {
      // The Runtime address is automatically generated by the SDK from the top-level endpoint.
      getHeaders: getAmkHeaders,
    },
    onIntegrationError: error => {
      console.error('AMK Editor Assistant integration failed', error);
    },
  },

  // Local upload option 1: use the SDK's built-in VOD upload.
  // media_output_destination specifies the VOD space used for browser-side upload
  // and playback URL resolution.
  storage: {
    media_output_destination: 'vod://your-space',
    getUploadSTS,
  },

  // Material import and playback-address maintenance
  material: {
    uploadAccept: 'video/*,audio/*,image/*',

    // Local upload option 2: your business uploads the file and returns a standard material.
    // Enable the next line to use custom upload instead of built-in VOD upload.
    // onUploadFile: uploadFileToBusinessStorage,
    // When multiple files are selected, the SDK calls onUploadFile concurrently for each and stores them separately.

    // Optional: import URLs in bulk. You can reference them directly or transfer them to business storage first.
    onUploadUrlMaterial: async (
      urls: string[],
    ): Promise<MaterialItem[]> => {
      return importUrlsToYourStorage(urls);
    },

  },

  decode: {
    enableAudioFrontendDecode: true, // Audio waveform frontend decoding
    enableVideoFrontendDecode: true, // Video thumbnail frontend decoding
  },

  toolbar: {
    // Use the MaaS provider for subtitle recognition on BytePlus.
    asr: { provider: 'maas' },
    builtInVisibility: { asrSubtitle: true },
  },
});

// Wait for the instance to finish mounting.
await sdk.whenReady();
console.log('SDK is ready!');

// When the component unmounts or the page closes, be sure to release resources.
// For example, in a React useEffect cleanup function:
// return () => sdk.destroy();
```

### Step 5: Verify the integration

After completing the preceding steps, start your web application, open the editor page, and verify the following:

* **UI rendering**: Confirm that the AI assistant panel, editor, project title, materials, and timeline load correctly.

* **Authentication**: Inspect the browser's network requests. Confirm that every request to `/api/amk-proxy` includes the application token and that the browser code contains no hardcoded long\-term API key.

* **Conversation and interaction**: Send an instruction to the AI assistant, such as "Create a 15\-second highlight video." Confirm that the assistant responds and that the editor becomes read\-only while the task runs.

* **Material import**: Upload a media file and confirm that it appears in the material library and is added to the conversation. If you use custom uploads, also confirm that `onUploadFile` is called.

* **Recovery**: Refresh the page and confirm that the same `projectId` restores both the editing project and its associated conversation history.

* **Cleanup**: When leaving the page, confirm that `sdk.destroy()` is called to prevent memory leaks and remove event listeners.

If all checks pass, the basic SDK integration is complete.

## Advanced usage

This chapter describes the material upload and storage options you can configure after completing the basic integration.

### Material import and storage

This section helps you choose a material upload method and configure the built\-in BytePlus VOD storage integration.

#### Choose an upload method

When users import local materials, choose either of the following methods:

* **Custom upload**: Configure `material.onUploadFile` to upload each file to your storage service.

* **Built\-in VOD upload**: Configure `storage` with a BytePlus VOD space and a credential callback. The SDK handles file upload, publishing, and playback\-address resolution. For details, see [Configure built-in BytePlus VOD storage for the SDK](https://docs.byteplus.com/en/docs/25/123450#configure-built-in-byteplus-vod-storage-for-the-sdk).

If both methods are configured, `material.onUploadFile` takes priority. If neither is configured, the SDK does not show the local upload entry.

### Common configuration for the SDK's built\-in storage

To enable built\-in upload, configure both of the following fields in the top\-level `storage` object. SDK initialization fails if either field is missing.

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`storage.media_output_destination` |`string` |Conditionally required |\- |The material upload destination, in the format `vod://<space>`. `outputDestination` is not a valid option. |
|`storage.getUploadSTS` |`() => Credentials \| Promise<Credentials>` |Conditionally required |\- |Obtains short\-lived credentials from your business server. Return the credential object directly, or extract it from a response wrapper before returning it. |

Each `storage` object can specify only one upload destination.

### Configure built\-in BytePlus VOD storage for the SDK

You can use a [BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod) space as the upload destination for local materials. Configure the target space and a temporary\-credential callback when initializing the SDK. The SDK then handles file upload, media publishing, and playback\-address retrieval and refresh. To upload materials to another storage service, implement `material.onUploadFile`.

#### Core concepts

|Concept |Description |
|---|---|
|VOD space |The top\-level container for media assets in BytePlus VOD, uniquely identified by its space name. The SDK uploads and publishes local materials in this space. |
|`vod://` address |The fixed format used to specify the upload destination: `vod://<space>`. Enter only the space name. Do not include a Vid, subdirectory, query parameters, URL fragment, or playback domain. This value identifies an upload destination and is not an HTTP address that a browser can play directly. |
|Temporary STS credentials |Time\-limited VOD credentials issued by your server for the current user. The SDK uses them to upload and publish materials and query playback information without exposing a long\-term AK/SK in the browser. |

#### Workflow

The browser, your business server, and BytePlus VOD interact as follows:

1. The user selects a local file in the browser.

2. The SDK calls the `getUploadSTS` callback that you provided and requests temporary credentials from your business server.

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

// Call this function only after authenticating the user and confirming that
// the user can access the requested editing project.
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

In this example, `Resource: []` does not restrict the credentials to a specific VOD resource. In production, follow the BytePlus VOD authorization rules and grant access only to the resources required by your application. For details about the package and credential generation, see the [BytePlus VOD Node.js SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk).

#### Step 3: Configure VOD storage when initializing the SDK

Set the VOD destination and temporary\-credential callback in the top\-level `storage` object:

```TypeScript
import { createAmkEditorAssistant } from '@byteplus/amk-editor-assistant';
import '@byteplus/amk-editor-assistant/styles.css';

const sdk = createAmkEditorAssistant({
  container,
  projectId,
  endpoint: '/api/amk-proxy',
  getHeaders: getAmkHeaders,
  assistant: {
    model: 'ep-language-model',
    runtime: { getHeaders: getAmkHeaders },
  },
  storage: {
    // Enter only the VOD space name after vod://.
    media_output_destination: 'vod://your-space-name',
    getUploadSTS: async () => {
      const response = await fetch(
        `/api/vod-upload-sts?projectId=${encodeURIComponent(projectId)}`,
        {
          headers: await getAmkHeaders(),
        },
      );
      if (!response.ok) {
        throw new Error(`Failed to get VOD STS: HTTP ${response.status}`);
      }
      const token = await response.json();
      // This example endpoint returns the credential object directly.
      // If your endpoint wraps it in data, extract data before returning it.
      return {
        AccessKeyId: token.AccessKeyId,
        SecretAccessKey: token.SecretAccessKey,
        SessionToken: token.SessionToken,
        ExpiredTime: token.ExpiredTime,
        CurrentTime: token.CurrentTime,
      };
    },
  },
});
```

You implement `/api/vod-upload-sts`; it is not a fixed SDK endpoint. Configure `storage.media_output_destination` and `storage.getUploadSTS` together. Each `storage` object can specify only one upload destination. After you configure `storage`, local files use the built\-in VOD upload by default. If you also configure `material.onUploadFile`, the custom callback takes priority.

## Reference

This chapter provides the SDK initialization configuration, instance methods, and core data structures needed when integrating the Web Vibe Editing SDK.

### SDK initialization configuration

The following tables list the complete configuration options of `createAmkEditorAssistant(options)`. For complete examples, see [Quick start](https://docs.byteplus.com/en/docs/25/123450#quick-start) and [Configure built-in BytePlus VOD storage for the SDK](https://docs.byteplus.com/en/docs/25/123450#configure-built-in-byteplus-vod-storage-for-the-sdk).

#### Top\-level configuration

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`container` |`HTMLElement` |Yes |\- |An existing mount node with explicit width and height. |
|`projectId` |`string` |Yes |\- |The current editing project ID, also used to bind the AI assistant session and project context. |
|`endpoint` |`string` |Yes |\- |The business proxy base address shared by the editor and assistant. The SDK appends the service path automatically. |
|`getHeaders` |`() => Record<string, string> \| Promise<Record<string, string>>` |No |\- |Obtains headers before each Editing API request and can pass short\-lived business tokens. |
|`assistant` |`AmkEditorAssistantConfig` |Yes |\- |AI assistant model, Assistant Runtime API, conversation display, tool extensions, and callbacks. |
|`layout` |`AmkEditorAssistantLayoutOptions` |No |\- |Two\-column assistant and editor layout configuration. |
|`theme` |`'light' \| 'dark'` |No |\- |The editor theme. |
|`header` |`object` |No |\- |The editor title\-bar configuration. |
|`export` |`object` |No |\- |Export configuration and callbacks. |
|`storage` |`object` |No |\- |Built\-in BytePlus VOD upload and playback\-address resolution. |
|`material` |`object` |No |\- |Material import, refresh, persistence, and upload concurrency configuration. |
|`getLicenseUrl` |`function` |No |\- |The address or asynchronous function used to obtain a license for encrypted video playback. |
|`decode` |`object` |No |\- |Frontend audio/video decoding configuration, such as waveform generation. |
|`i18n` |`object` |No |\- |Locale and copy overrides. |
|`toolbar` |`object` |No |\- |Built\-in editor toolbar configuration. Set `toolbar.asr.provider` to `maas` for subtitle recognition. |

#### Language and copy configuration

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`i18n.locale` |`string` |No |`'en-US'` |The UI locale. The SDK includes `zh-CN` and `en-US` and does not automatically follow the browser locale. |

#### Toolbar configuration

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`toolbar.asr.provider` |`'maas'` |No |`'maas'` |Selects the MaaS subtitle recognition service. This option does not affect the assistant's conversation model. |
|`toolbar.builtInVisibility` |`object` |No |\- |Controls built\-in button visibility. Omitting a field uses its default. Hiding a button does not disable its shortcut or function. |
|`toolbar.builtInVisibility.undo` |`boolean` |No |`true` |Undo button. |
|`toolbar.builtInVisibility.redo` |`boolean` |No |`true` |Redo button. |
|`toolbar.builtInVisibility.cut` |`boolean` |No |`true` |Cut button. |
|`toolbar.builtInVisibility.copy` |`boolean` |No |`true` |Copy button. |
|`toolbar.builtInVisibility.delete` |`boolean` |No |`true` |Delete button. |
|`toolbar.builtInVisibility.asrSubtitle` |`boolean` |No |`true` |Subtitle recognition entry. |

#### Storage configuration

Use this option to enable the SDK's built\-in storage integration, such as direct upload to BytePlus VOD. The `storage` object is optional, but if you configure it, you must provide both `media_output_destination` and `getUploadSTS`.

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`storage.media_output_destination` |`string` |Conditionally required |\- |The browser\-side VOD target in the format `vod://<space>`. |
|`storage.getUploadSTS` |`() => Credentials \| Promise<Credentials>` |Conditionally required |\- |Obtains short\-lived VOD credentials from your business server. Return the credential object directly, or extract it from a response wrapper first. |

#### AI assistant configuration

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`assistant.model` |`string \| model list \| grouped list` |Yes |\- |The language model endpoint ID used for instruction understanding and planning. A single string hides the model selector. Recommended models include `dola-seed-2-1-turbo-260628` and `seed-2-0-pro-260328`. |
|`assistant.preferMultiModalModels` |`readonly string[]` |No |\- |Multimodal endpoint IDs used to understand media. For visual understanding, we recommend `dola-seed-2-1-turbo-260628`. When audio understanding is needed, configure an audio\-capable model such as `seed-2-0-lite-260428`. |
|`assistant.runtime` |`AssistantRuntimeConfig` |No |\- |Assistant Runtime API address and request\-header configuration. |
|`assistant.runtime.headers` |`Record<string, string>` |No |\- |Static Assistant Runtime API request headers. Top\-level `getHeaders` is not automatically applied to assistant requests. |
|`assistant.runtime.getHeaders` |`() => Record<string, string> \| Promise<Record<string, string>>` |No |\- |Obtains dynamic headers before each Assistant Runtime API request. |
|`assistant.runtime.runtimeUrl` |`string` |No |`${endpoint}/api/v1/studio/agents` |Overrides the Runtime address only when the Assistant Runtime API and Editing API use different domains or service paths. |
|`assistant.agentId` |`string` |No |`mediakit-editor-sdk-agent` |The Assistant Agent ID. |
|`assistant.composer.actions` |`array \| transform function` |No |\- |Appends custom React controls to the input area. |
|`assistant.onModelChange` |`(event) => void` |No |\- |Receives model selection changes. Keep model\-list references stable to avoid resetting the selection. |
|`assistant.onIntegrationError` |`(error) => void` |No |\- |Receives project\-session initialization, resource loading, and imperative control errors. |
|`assistant.mcp.tools` |`readonly string[]` |No |\- |Selects AI MediaKit tools available to the assistant. Supported names are `video_understand_router`, `asr_subtitles`, `probe_audio_metadata`, `probe_video_metadata`, `probe_image_metadata`, `erase_video_subtitle_pro`, `separate_voice`, `matte_greenscreen_video`, `erase_image`, `remove_image_background`, `extract_frames`, and `call_maas_proxy`. The server\-side MCP service and assistant configuration must also enable them. |
|`assistant.mcp.editDenyTools` |`readonly string[]` |No |\- |Blocks selected editing MCP tools in the project, material, timeline, resource, scenario, export, and task\-query groups. |
|`assistant.maasModel` |`string \| readonly string[]` |No |\- |The `modelId` used by generation tools, normally supplied by the selected `maasModel` group. Do not invoke a generation model when none is selected. |

For grouped models, configure the `maasModel` group with the actual BytePlus service region. Model IDs and regions must match the BytePlus services you activated.

#### Two\-column layout configuration

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`layout.defaultHiddenPanel` |`'assistant' \| 'editor'` |No |\- |Hides the assistant or editor panel initially. Both columns are shown when omitted. |
|`layout.initialWidthPercent` |`number` |No |`37.5` |Initial assistant panel width as a percentage. |
|`layout.minAssistantWidth` |`number` |No |`320` |Minimum assistant panel width in pixels. |
|`layout.minEditorWidth` |`number` |No |`640` |Minimum editor panel width in pixels. |
|`layout.resizable` |`boolean` |No |`true` |Allows users to resize the panels by dragging the divider. |
|`layout.onPanelVisibilityChange` |`(state: AmkEditorAssistantLayoutState) => void` |No |\- |Called after the user opens or closes either panel. |

#### Material configuration

Source audio, video, and image URLs must allow cross\-origin access. Neither initial requests nor retries can use `no-cors` mode.

|Option |Type |Required |Default |Description |
|---|---|---|---|---|
|`material.uploadAccept` |`string` |No |\- |The `accept` string of the local file picker. |
|`material.uploadConcurrency` |positive integer |No |\- |Shared concurrency limit for custom single\-file upload, built\-in VOD upload, and temporary\-file persistence. Local upload has no default limit; temporary\-file persistence defaults to 5 concurrent items. |
|`material.onUploadFile(file)` |`(file: File) => MaterialItem \| Promise<MaterialItem>` |No |\- |Uploads one local file and returns one material. This callback takes priority over built\-in VOD upload. |
|`material.onUploadUrlMaterial(urls)` |`(urls: string[]) => MaterialItem[] \| Promise<MaterialItem[]>` |No |\- |Imports URLs in bulk and enables the assistant's URL import tool. |
|`material.onUploadFromSystem()` |`() => SystemMaterialItem[] \| Promise<SystemMaterialItem[]>` |No |\- |Opens the business asset library and returns selected materials. |
|`material.onRefreshPlayInfo(materials)` |`(materials: MaterialItem[]) => Partial<MaterialItem>[] \| Promise<Partial<MaterialItem>[]>` |No |\- |Refreshes short\-lived playback addresses for custom business storage. It is not required for built\-in VOD storage. |
|`material.onPersistExtractUrls(params)` |`(params: { kind; urls; material }) => PersistExtractUrlsResult \| string[]` |No |\- |Persists temporary posters and sprite sheets. After writing long\-lived addresses, clear the corresponding `poster_task_id` or `sprite_task_id` when appropriate. |

### SDK instance methods

|Method |Return value |Description |
|---|---|---|
|whenReady() |Promise |Wait for the project to load and the editor to finish mounting. |
|getEditor() |AmkEditor |Get the underlying editor instance; should be called after whenReady(). |
|getAssistantController() |AssistantController |Get the imperative controller of the AI assistant; available after the assistant is rendered. |
|setLayoutChromeVisibility(...) |void |Dynamically show or hide the header and the floating split\-panel buttons at runtime. |
|addTimelineElementToConversation(...) |Promise |Append a timeline element to the conversation draft as a structured entity. |
|addMaterialToConversation(...) |Promise |Append a project material to the conversation draft as a structured entity. |
|destroy() |void |Destroy all instances, listeners, and timers, and release resources. |

## Server\-side API reference

Your proxy forwards frontend SDK requests through a single entry to two API groups on the same AI MediaKit host: the Editing API and the Assistant Runtime API.

### Editing API

These APIs manage editing project data, including projects, materials, timelines, and asynchronous tasks.

**Basic information**

|Item |Description |
|---|---|
|Host |`https://mediakit.ap-southeast-1.bytepluses.com` |
|Base path |`/api/v1/editing` |
|Authentication |`Authorization: Bearer <YOUR_AMK_API_KEY>` |

**Response conventions**

All APIs return 200 OK at the HTTP level. Check the response body to determine whether the request succeeded or failed.

|The response body contains |Meaning |
|---|---|
|The `data` field |The request succeeded. |
|The `error` field |The request failed. The `error.code` field identifies the error type. |

**Common endpoints**

* **Create a project**

`POST /projects`

Create a new editing project and return its unique identifier, `project_id`.

**Request parameters**

|Parameter |Type |Required |Description |
|---|---|---|---|
|`name` |`string` |Yes |The project name, up to 255 characters. |
|`description` |`string` |No |A detailed description of the project. |

* **Create or update materials in bulk**

`POST /projects/{projectId}/materials` (create)

`PUT /projects/{projectId}/materials` (update or insert)

Add or update materials in the specified project in bulk. The `PUT` operation decides whether to update an existing material or insert a new one based on `source_material_id`. This operation is atomic: if any material fails validation, the entire batch is rolled back.

**Request parameters**

|Parameter |Type |Required |Description |
|---|---|---|---|
|`materials` |`MaterialItem[]` |Yes |An array of material objects, each conforming to the material standard format. A single request supports up to 100 materials. |

### Assistant Runtime API

These APIs handle model interactions, including natural\-language understanding, conversation management, and AI assistant tool calls.

**Basic information**

|Item |Description |
|---|---|
|Browser\-side proxy prefix |For example, `/api/amk-proxy/api/v1/studio/agents`. The SDK derives this prefix from the top\-level `endpoint`, so you do not need to configure `runtimeUrl` separately. |
|Runtime upstream address |`https://mediakit.ap-southeast-1.bytepluses.com/api/v1/studio/agents` |
|Upstream authentication |Your business proxy injects `Authorization: Bearer <YOUR_AMK_API_KEY>`. |
|Response type |Regular query endpoints return JSON; AI assistant execution endpoints may return a `text/event-stream` streaming response. |

**Endpoint allowlist**

Your business proxy should allow at least the following paths and methods required by the SDK:

|Method |Browser request path (example) |Purpose |
|---|---|---|
|`GET` |`/api/amk-proxy/api/v1/studio/agents/copilotkit` |Establish or check the Runtime connection. |
|`POST` |`/api/amk-proxy/api/v1/studio/agents/copilotkit` |Submit a conversation request and execute an AI assistant task; may return an SSE event stream. |
|`GET` |`/api/amk-proxy/api/v1/studio/agents/threads/{threadId}/messages` |Read conversation history messages. |
|`GET` |`/api/amk-proxy/api/v1/studio/agents/agents/{agentId}/conversations` |Query the conversation list, used to restore the conversation bound to a project. |

## SDK release history

|Date |Version |Description |
|---|---|---|
|October 20, 2026 |0.0.10 |First release. |

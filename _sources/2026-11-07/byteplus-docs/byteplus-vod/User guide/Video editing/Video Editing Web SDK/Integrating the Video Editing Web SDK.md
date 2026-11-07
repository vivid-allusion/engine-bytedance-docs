---
title: "Integrating the Video Editing Web SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/integrating_video_editing_web_sdk"
---

This guide describes how to integrate the Video Editing Web SDK into a Web application and connect it to BytePlus VOD for cloud\-based project management, material management, preview, and video export.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">The Video Editing Web SDK is currently available only in the Asia Pacific (Johor) region. Set <code>region</code> to <code>ap-southeast-1</code> in the SDK configuration and use the same region when signing backend API requests.</div>


<span id="architecture-and-workflow"></span>
## Architecture and workflow

The solution consists of the following components:


* **Video Editing Web SDK:**  Provides the editor UI, including the timeline, material library, and preview window. The SDK does not call BytePlus VOD APIs directly. It invokes the functions that you implement in `actions`.

* **Your backend:**  Receives requests from the SDK, securely signs and calls BytePlus VOD APIs, and returns the required response data to the frontend.

* **BytePlus VOD:**  Stores media, manages cloud editing projects, and runs export tasks.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817092956-36403298943.png) </span>

A typical workflow is as follows:


1. Your backend calls `CreateProject` and obtains a `ProjectId` and `GroupId`.

2. The backend passes these IDs to the frontend.

3. The frontend initializes the SDK with the IDs.

4. As the user edits the timeline, the SDK invokes `actions.updateProject` to save the project draft through your backend.

5. When the user exports the video, the SDK invokes `actions.submitEditTaskAsync` to submit a cloud editing task through your backend.


<span id="supported-material-formats"></span>
## Supported material formats


|Material type |Supported formats |
|---|---|
|Video |MP4, WebM, MOV |
|Audio |MP3 |
|Image |JPEG, PNG |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Importing subtitle files such as SRT and VTT as editing materials is not supported.</div>


* <div data-tips="true" data-tips-type="tip">Editing materials and exported videos must be stored in BytePlus VOD and managed in Vid mode. Direct URL mode and mounted TOS buckets are not supported.</div>


* <div data-tips="true" data-tips-type="tip">Uploaded audio and video files are stored under <strong>Videos</strong>. Uploaded images are stored under <strong>Materials</strong>.</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Known limitations</div>



* <div data-tips="true" data-tips-type="warning">Selecting a VOD category for an exported video is not supported.</div>


* <div data-tips="true" data-tips-type="warning">Deleting or trimming a material on the timeline can cause an audible pop at the edit point.</div>



<span id="prerequisites"></span>
## Prerequisites

Before integrating the SDK, complete the following:


* [Create a BytePlus account](https://console.byteplus.com/auth/signup/) and enable BytePlus VOD. For details, see [Getting started with BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started).

* Create a VOD space in the Asia Pacific (Johor) region for storing editing materials and exported videos.

* Add and enable a VOD playback domain name. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

   * [Configure an SSL certificate](https://docs.byteplus.com/docs/byteplus-vod/docs-configuring-ssl-certificates) so that the editor can load materials over HTTPS.

   * [Configure HTTP response headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers) to allow your Web application to access the media resources across origins.

   * Ensure that the playback domain's origin storage matches the storage bound to the VOD space.

* Deploy a backend that can sign and call BytePlus VOD APIs. For a runnable reference, see [Trying the Video Editing Web SDK demo](https://docs.byteplus.com/docs/byteplus-vod/video_editing_web_sdk_demo).

* Install Node.js v14 or later and npm in the frontend development environment.


Before loading the editor, call [CreateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-createproject) from your backend:

```text
POST https://vod.byteplusapi.com?Action=CreateProject&Version=2025-01-01
```


Sign the request as a BytePlus VOD request in region `ap-southeast-1`. For the endpoint, common parameters, and request\-signing flow, see [API reference overview](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">CreateProject requirements</div>



* <div data-tips="true" data-tips-type="warning">Set both <code>Space</code> and <code>EditParam.Upload.SpaceName</code>, and use the same VOD space name for both fields.</div>


* <div data-tips="true" data-tips-type="warning">Set the <code>EditParam.Canvas</code> size to either <strong>1920 × 1080 (16:9)</strong> or <strong>1080 × 1920 (9:16)</strong>. These are the canvas sizes currently supported by the SDK.</div>



<span id="integration-steps"></span>
## Integration steps

<span id="import-sdk-resources"></span>
### Step 1: Import the SDK resources

Use the CSS and JavaScript resources for BytePlus Video Editing Web SDK.

Add the CSS file in the `<head>` element:

```html
<head>
  <link rel="stylesheet" href="https://lf-unpkg.volccdn.com/obj/vcloudfe/sdk/@byted/veveditor/1.0.7-rc.15/veveditor.css">
</head>
```


Add a container for the editor and import the JavaScript file before the closing `</body>` tag:

```html
<body>
  <div id="editor-container" style="height: 100vh; width: 100vw;"></div>
  <script src="https://lf-unpkg.volccdn.com/obj/vcloudfe/sdk/@byted/veveditor/1.0.7-rc.15/veveditor.umd.js"></script>
</body>
```


<span id="initialize-the-sdk"></span>
### Step 2: Initialize the SDK

Create an editor instance by calling `new window.VeVEditor(param)`. Pass the `projectId` and `groupId` obtained through your backend, and implement the API proxies and event handlers required by your application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Single\-instance limitation</div>


<div data-tips="true" data-tips-type="warning">Only one editor instance is supported on a page. Before creating another instance, call <code>veveditor.destroy()</code> to destroy the existing instance.</div>


```javascript
const projectId = 'your-project-id';
const groupId = 'your-group-id';

const param = {
  container: document.getElementById('editor-container'),
  config: {
    projectId,
    groupId,
    region: 'ap-southeast-1',
    material: {
      showClassification: true,
      defaultClassificationId: '',
    },
  },
  actions: {
    describeProject: async (params) => { /* Call your backend. */ },
    updateProject: async (params) => { /* Call your backend. */ },
    submitEditTaskAsync: async (params) => { /* Call your backend. */ },
    // Implement the remaining required actions described below.
  },
  handlers: {
    onProjectSubmit: (space) => { /* Handle successful task submission. */ },
    onNavBack: (space) => { /* Handle navigation. */ },
  },
};

const veveditor = new window.VeVEditor(param);
```


<span id="parameters"></span>
## Parameters

<span id="param"></span>
### Param


|Parameter |Type |Required |Description |
|---|---|---|---|
|`container` |`HTMLElement` |Yes |DOM element in which the SDK renders the editor. |
|`config` |`object` |Yes |Basic project and UI configuration. See [Config](https://docs.byteplus.com/en/docs/25/118519#config). |
|`actions` |`object` |Yes |API proxy functions implemented by your application. See [Actions](https://docs.byteplus.com/en/docs/25/118519#actions). |
|`handlers` |`object` |Yes |Callbacks for user actions and editor state changes. See [Handlers](https://docs.byteplus.com/en/docs/25/118519#handlers). |


<span id="config"></span>
### Config


|Parameter |Type |Required |Description |
|---|---|---|---|
|`projectId` |`string` |Yes |Project ID returned by `CreateProject`. |
|`groupId` |`string` |Yes |Group ID returned by `CreateProject`. |
|`region` |`string` |Yes |Service region. Set this value to `ap-southeast-1`. |
|`autoPublish` |`boolean` |No |Whether to automatically invoke `UpdateMediaPublishStatus` after a local audio or video upload. The default is `true`. |
|`header` |`object` |No |Header UI configuration. See [Header](https://docs.byteplus.com/en/docs/25/118519#header). |
|`material` |`object` |No |Material library configuration. See [Material](https://docs.byteplus.com/en/docs/25/118519#material). |
|`text` |`object` |No |Text panel configuration. See [Text](https://docs.byteplus.com/en/docs/25/118519#text). |
|`effect` |`object` |No |Effect panel configuration. See [Effect](https://docs.byteplus.com/en/docs/25/118519#effect). |
|`transition` |`object` |No |Transition panel configuration. See [Transition](https://docs.byteplus.com/en/docs/25/118519#transition). |
|`filter` |`object` |No |Filter panel configuration. See [Filter](https://docs.byteplus.com/en/docs/25/118519#filter). |


<span id="actions"></span>
### Actions (API proxies)

Each function in `actions` represents a BytePlus VOD server\-side API operation required by the SDK. Implement every action marked as required. Each function must send the SDK parameters to your own backend; your backend then signs and calls the BytePlus API. Except for the response\-handling cases described below, return the `Result` object from the BytePlus API response to the SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Do not call server APIs from the browser</div>


<div data-tips="true" data-tips-type="warning">Do not sign or call <code>vod.byteplusapi.com</code> directly in frontend code. Doing so would expose your AK and SK. The application\-specific frontend\-to\-backend routes in your implementation are not BytePlus API endpoints.</div>


For the editing APIs with version `2025-01-01`, construct the BytePlus endpoint as follows:

```text
https://vod.byteplusapi.com?Action=<Action>&Version=2025-01-01
```



|Action function |BytePlus server API |Required |Description |
|---|---|---|---|
|`describeProject` |[DescribeProject](https://docs.byteplus.com/docs/byteplus-vod/reference-describeproject) |Yes |Gets the initial project data when the SDK starts. |
|`updateProject` |[UpdateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-updateproject) |Yes |Saves the project draft during editing operations such as moving, trimming, or deleting materials. |
|`submitEditTaskAsync` |[SubmitEditTaskAsync](https://docs.byteplus.com/docs/byteplus-vod/reference-submitedittaskasync) |Yes |Submits a cloud video editing task when the user exports the project. |
|`searchVideo` |[SearchVideo](https://docs.byteplus.com/docs/byteplus-vod/reference-searchvideo) |Yes |Lists or searches audio and video assets in the VOD space for **Import from system \> Videos**. |
|`mGetMaterial` |[MGetMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-mgetmaterial) |Yes |Gets materials from the VOD material library for **Import from system \> Materials**. |
|`searchEditMaterial` |[SearchEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-searcheditmaterial) |Yes |Gets the materials referenced by the current project. |
|`deleteEditMaterial` |[DeleteEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteeditmaterial) |Yes |Removes a material from the current project. |
|`createEditMaterial` |[CreateEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-createeditmaterial) |Yes |Adds a material to the current project. This action does not refresh the material library automatically. |
|`getEffectList` |[GetEffectList](https://docs.byteplus.com/docs/byteplus-vod/reference-geteffectlist) |Yes |Gets the resources used by the effect, transition, and filter panels. |
|`updateMediaPublishStatus` |[UpdateMediaPublishStatus](https://docs.byteplus.com/docs/byteplus-vod/reference-updatemediapublishstatus) |Yes |Publishes an uploaded audio or video asset when `autoPublish` is `true`. |
|`getVideoInfo` |`(media:{Vid:string;Space:string})=> Promise<MediaInfo>` |Yes |Gets the playback URL, poster, duration, width, and height used to preview a material. The SDK passes `{ Vid, Space }`. Return a [MediaInfo](https://docs.byteplus.com/en/docs/25/118519#media-info) object. |
|`listVideoClassifications` |[ListVideoClassifications](https://docs.byteplus.com/docs/byteplus-vod/reference-listvideoclassifications) |Conditional |Required when `config.material.showClassification` is `true`. Gets the category tree displayed in the material library. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Response handling</div>



* <div data-tips="true" data-tips-type="tip">For editing APIs and <code>ListVideoClassifications</code>, return the API response's <code>Result</code> object.</div>


* <div data-tips="true" data-tips-type="tip"><code>getVideoInfo</code> is an adapter action. Extract the required fields from the <code>GetVideoPlayInfo</code> result and return a <code>MediaInfo</code> object.</div>


* <div data-tips="true" data-tips-type="tip"><code>UpdateMediaPublishStatus</code> has no API\-specific <code>Result</code> object. After the API succeeds, resolve the action Promise with <code><UPDATE_MEDIA_PUBLISH_STATUS_ACTION_RETURN_VALUE></code>. Confirm this SDK adapter value before publication.</div>



<span id="media-info"></span>
#### MediaInfo

The `getVideoInfo` action must return an object with the following fields, assembled from the `GetVideoPlayInfo` response.


|Parameter |Type |Required |Source field |
|---|---|---|---|
|`PlayUrl` |`string` |Yes |`VideoDetail.VideoDetailInfo.PlayInfo.MainPlayUrl` |
|`PosterUrl` |`string` |Yes |`VideoDetail.VideoDetailInfo.PosterUrl` |
|`Duration` |`number` |Yes |`VideoDetail.VideoDetailInfo.Duration` |
|`Width` |`number` |Yes |`VideoDetail.VideoDetailInfo.Width` |
|`Height` |`number` |Yes |`VideoDetail.VideoDetailInfo.Height` |


<span id="handlers"></span>
### Handlers


|Handler |Type |Required |Description |
|---|---|---|---|
|`onUploadMaterial` |`(params: { type: 'video' \\| 'material'; Space: string }) => void` |Conditional |Invoked when the user confirms a local upload. Required when the upload workflow uses this callback. Use it to open your custom upload component or page. |
|`onProjectSubmit` |`(Space: string) => void` |Yes |Invoked after `submitEditTaskAsync` succeeds. Use it to display task status or navigate to a task page. |
|`uploadMaterial` |`function` |Conditional |Performs the local\-file upload. Required when `config.material.enableLocalUpload` is `true`. Integrate the [Web Upload SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-web-upload-sdk) and return the uploaded media information. |
|`onNavBack` |`(Space: string) => void` |No |Invoked when the user clicks **Back**. Use it to navigate or display a confirmation dialog. |
|`onNodePreviewError` |`(type: 'video' \\| 'audio') => void` |No |Invoked when previewing a video or audio material fails. Use it for error reporting or a custom message. |


<span id="header"></span>
### Header


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |No |`true` |Whether to display the entire header. |
|`isNavBackVisible` |`boolean` |No |`true` |Whether to display **Back**. |
|`isProjectSubmitVisible` |`boolean` |No |`true` |Whether to display **Export**. |
|`isProjectNameEditable` |`boolean` |No |`true` |Whether the project name can be edited. |


<span id="material"></span>
### Material

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817093755-1243043369630.png) </span>


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |No |`true` |Whether to display the material library. |
|`showClassification` |`boolean` |No |`false` |Whether to enable category filtering. If set to `true`, implement `actions.listVideoClassifications`. |
|`defaultClassificationId` |`string` |No |`''` |Category selected when the material library opens. An empty value means **Uncategorized**. |
|`enableLocalUpload` |`boolean` |No |`true` |Whether to enable local upload. If set to `true`, implement `handlers.uploadMaterial`. |
|`uploadAccept` |`string` |No |`'image/*,.mp3,.mp4,.webm,.mov'` |File types accepted for local upload. |
|`videoAccept` |`string` |No |`'.mp4,.webm,.mov'` |Video file types accepted when importing from the VOD space. |
|`emptyIcon` |`string` |No |`''` |URL of a custom icon displayed when the material library is empty. |


<span id="text"></span>
### Text


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |Yes |`false` |Whether to display the text panel. You have to set this to `false` because the text panel is currently not supported. |


<span id="effect"></span>
### Effect

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817093755-879722302318.png) </span>


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |No |`true` |Whether to display the effect panel. |


<span id="transition"></span>
### Transition

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817093755-486088517305.png) </span>


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |No |`true` |Whether to display the transition panel. |


<span id="filter"></span>
### Filter

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817093755-1486522350050.png) </span>


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`show` |`boolean` |No |`true` |Whether to display the filter panel. |


<span id="i18n"></span>
### i18n


|Parameter |Type |Required |Default |Description |
|---|---|---|---|---|
|`locale` |`string` |No |`'zh-CN'` |Locale for the editor. Supported values: `en-US` and `zh-CN`. Set it to `en-US` to use English interface. |


<span id="complete-example"></span>
## Complete initialization example

The frontend\-to\-backend route names in this example are illustrative. Define these routes in your own backend, then map each route to the BytePlus API, version, and method listed in [Actions](https://docs.byteplus.com/en/docs/25/118519#actions).

```javascript
async function callBackend(operation, params) {
  const response = await fetch(`/api/video-editing/${operation}`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(params),
  });

  if (!response.ok) {
    throw new Error(`Video editing request failed: ${response.status}`);
  }

  const body = await response.json();
  return body.Result;
}

const veveditor = new window.VeVEditor({
  container: document.getElementById('editor-container'),
  config: {
    projectId: 'your-project-id',
    groupId: 'your-group-id',
    region: 'ap-southeast-1',
    autoPublish: true,
    material: {
      show: true,
      enableLocalUpload: true,
      showClassification: true,
      defaultClassificationId: '',
      uploadAccept: 'image/*,.mp3,.mp4,.webm,.mov',
      videoAccept: '.mp4,.webm,.mov',
    },
  },
  actions: {
    describeProject: (params) => callBackend('describe-project', params),
    updateProject: (params) => callBackend('update-project', params),
    submitEditTaskAsync: (params) => callBackend('submit-edit-task-async', params),
    searchVideo: (params) => callBackend('search-video', params),
    mGetMaterial: (params) => callBackend('get-materials', params),
    searchEditMaterial: (params) => callBackend('search-edit-material', params),
    deleteEditMaterial: (params) => callBackend('delete-edit-material', params),
    createEditMaterial: (params) => callBackend('create-edit-material', params),
    getEffectList: (params) => callBackend('get-effect-list', params),
    updateMediaPublishStatus: (params) => callBackend('update-media-publish-status', params),
    getVideoInfo: (params) => callBackend('get-video-info', params),
    listVideoClassifications: (params) => callBackend('list-video-classifications', params),
  },
  handlers: {
    onProjectSubmit: (space) => {
      // Display task status or navigate to your task page.
    },
    onNavBack: (space) => {
      // Navigate away from the editor.
    },
    uploadMaterial: async (file, options) => {
      // Integrate the BytePlus Web Upload SDK here.
      // If a category is selected, its ID is available as options.classificationId.
    },
    onNodePreviewError: (type) => {
      // Report or display the preview error.
    },
  },
});
```


<span id="sdk-release-history"></span>
## SDK release history


|Date |Version |Description |
|---|---|---|
|2026\-09\-29 |1.0.7\-rc.15 |Fixed known issues. |
|2026\-08\-17 |1.0.7\-rc.4 |Initial release. |


<span id="faq"></span>
## FAQ

<span id="why-does-a-timeline-material-display-a-black-screen-or-fail-to-preview"></span>
### Why does a timeline material display a black screen or fail to preview?

Check the following:


* The playback domain is enabled and its DNS configuration is valid.

* The domain has a valid SSL certificate and the VOD distribution protocol is HTTPS.

* The domain's origin storage matches the storage used by the VOD space.

* The playback domain returns the HTTP response headers required for cross\-origin access.

* The media file is intact, published, and accessible from the user's network.


<span id="how-do-i-use-vod-categories-in-the-material-library"></span>
### How do I use VOD categories in the material library?


* Set `config.material.showClassification` to `true` and implement `actions.listVideoClassifications`.

* When the user filters videos by category, the SDK passes the selected IDs to `actions.searchVideo` in `params.ClassificationIds`. Forward this field to `SearchVideo`.

* When the user selects a category during local upload, the SDK provides the ID in `options.classificationId`. Pass it to the Web Upload SDK as `ClassificationId` in the `AddOptionInfo` process action.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Category scope</div>


<div data-tips="true" data-tips-type="warning">Categories apply to audio and video assets. Image materials do not support VOD category management.</div>

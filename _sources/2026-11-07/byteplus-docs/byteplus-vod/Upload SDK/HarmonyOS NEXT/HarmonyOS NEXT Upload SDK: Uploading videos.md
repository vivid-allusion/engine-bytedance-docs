---
title: "HarmonyOS NEXT Upload SDK: Uploading videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-harmonyos-upload-sdk-features"
---

This page introduces how to upload videos to VOD service using the Upload SDK.

<span id="6cc9d54e"></span>
## **Prerequisites**

You have integrated the Upload SDK. Refer to [HarmonyOS NEXT Upload SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-harmonyos-upload-sdk-quickstart).

<span id="e9a8b633"></span>
## Basic features

<span id="cc1c196f"></span>
### Initialize the SDK

```TypeScript
// Import header file
import { TTUploaderUtil} from '@vcloud/bduploader';

// Initialize the SDK. Only initialize once within the App's lifecycle.
if (this.mSDKInit == 0) {
  // Enable log debugging
  TTUploaderUtil.setEnableNativeLog(1); // 0: disable native log, 1: enable native log
  TTUploaderUtil.init(getContext(this).getApplicationContext());
  this.mSDKInit = 1;
}
```


<span id="187db098"></span>
### Create an instance

```TypeScript
// Import header file
import {
  TTVideoUploader,
  UploadType,
  BDVideoInfo,
  LogInfo,
  VideoInfoListener,
  TTVideoUploadNotifier,
} from '@vcloud/bduploader';

// Create a videoUploader instance
this.videoUploader = new TTVideoUploader();
```


<span id="09fb81c0"></span>
### Set the file to upload

```TypeScript
// Set the path of the file to be uploaded
this.videoUploader.setPathName(this.filePath); 
```


<span id="728515fd"></span>
### Set authentication

You need to issue a temporary upload token to the client by using the BytePlus VOD server\-side SDK on the App server side and then set it for the SDK. For detailed explanations of authentication parameters, please refer to [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads). An example of the implemented code is shown below.

```TypeScript
this.videoUploader.setTopAccessKey(this.accessKey); // Set AK
this.videoUploader.setTopSecretKey(this.secretKey); // Set SK
this.videoUploader.setTopSessionToken(this.sts2Token) // Set STSToken
```


<span id="78519194"></span>
### Set the space

An example of the code to set the space for upload is shown below. For related explanations about space in BytePlus VOD, please refer to [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).

```TypeScript
this.videoUploader.setSpaceName(this.spaceName); // Set the space
```


<span id="869c4ef3"></span>
### Set the storage path

The format of the storage path after file upload completion is as follows:

```Plain
StoreUri = {{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}
```


The following is an example of a complete storage path.

```Plain
ASmapleBucketName/path/to/foo/bar/test.mp4
```


The parameter description is shown in the table below.


|Parameter |Required |Description |
|---|---|---|
|BucketName |N/A |The name of the storage bucket. This is typically handled by the SDK and does not require manual configuration. |
|FilePrefix |No |File prefix, a path string that supports multi\-level paths, such as `path/to/foo/bar/`. The file prefix must end with `/`, otherwise the upload will fail. |
|FileTitle |No |File name. If you do not set it, the SDK will automatically generate a 32\-character string as the file name. |
|FileExtension |Yes |File suffix. The final complete path must include `FileExtension`, otherwise the upload will fail. The file suffix must start with `.` At the beginning, such as `.mp4` and `.mp3`. |


You can refer to the example code below to set the storage path.

```TypeScript
// Set the full fileName
if (this.fileName.length > 0) {
  this.videoUploader.setFileName(this.fileName);
}

// Set the prefix
if (this.filePrefix.length > 0) {
  this.videoUploader.setFilePrefix(this.filePrefix);
}

// Set the suffix
if (this.fileExtension.length > 0) {
  this.videoUploader.setFileExtension(this.fileExtension);
}
```


<span id="9d8c6e38"></span>
### Set the category

Call the `setClassificationId` method to pass the category ID for video classification. You can create categories and obtain category IDs on the [BytePlus VOD console](https://console.byteplus.com/vodpaas) under the **System settings** \> **Categories** page within the specified space. For details, see [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc). The example code is as follows:

```TypeScript
if (this.classificationId > 0) {
  this.videoUploader.setClassificationId(this.classificationId);
}
```


<span id="7ed450cf"></span>
### Upload control

```TypeScript
// Start or resume upload
private async startVideoUploader(): Promise<void> {
  await this.videoUploader?.start();
}

// Pause upload
private async stopVideoUploader(): Promise<void> {
  await this.videoUploader?.stop();
}

// Terminate upload
public async closeVideoUploader(): Promise<void> {
  await this.videoUploader?.close();
  this.videoUploader = undefined;
}
```


<span id="f0811d5d"></span>
### Set the callbacks

```TypeScript
// Set the callbacks
let listener = new UploaderVideoListener(this.videoUploader, this);
this.videoUploader.setVideoInfoListener(listener);

// Listen to the callbacks
export class UploaderVideoListener implements VideoInfoListener {
  private videoUploader?: TTVideoUploader;

  constructor(videoUploader: TTVideoUploader, uploaderPage: UploaderPage) {
    this.videoUploader = videoUploader;
  }

  // Upload progress and upload status callbacks. See [onNotify](https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos#set-the-callbacks)
  async onNotify(what: number, info: BDVideoInfo): Promise<void> {
    hilog.info(0x0000, 'UploaderVideoListener', 'onNotify:%{public}d', what);
    if (what == TTVideoUploadNotifier.MsgIsComplete) {
      await this.uploaderPage.closeVideoUploader();
    } else if (what == TTVideoUploadNotifier.MsgIsFail) {
      await this.uploaderPage.closeVideoUploader();
    } else if (what == TTVideoUploadNotifier.MsgIsUpdateProgress) {
    } else if (what == TTVideoUploadNotifier.MsgIsFlushComplete) {
    } else if (what == TTVideoUploadNotifier.MessageIsDiskResumeInfoError) {
    } 
  }

  // Key log callback, you can upload the callback information to your server, and you can troubleshoot online problems through logs.
  // You can simply leave the implementation empty if you don't want to use it.
  onLog(what: number, info: LogInfo): void {
    hilog.info(0x0000, 'UploaderVideoListener', 'onLog:%{public}s', info);
  }
}
```


<span id="d26d7171"></span>
## Advanced features

<span id="bc7ad356"></span>
### Set frame extraction time for cover image

Use `setPoster` to set the automatic frame extraction time point for the video, in seconds. After successful setup, the upload SDK will capture a video frame at the specified time point as the cover image. The sample code is as follows:

```TypeScript
this.videoUploader.setPoster(this.posterTime); // In seconds, the default value is 0
```


<span id="68d3ffab"></span>
### Set relay information parameters for callback

This parameter value will be returned to your server\-side through the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event's `CallbackArgs` parameter. The sample code is as follows:

```TypeScript
this.videoUploader.setServerParameter(this.serverParam); // Set callback parameters
```


<span id="b5a16664"></span>
### Set the workflow ID

Call the `setTemplateId` method to pass in the workflow ID and trigger the media processing task. You can obtain the workflow ID on the [BytePlus VOD console](https://console.byteplus.com/vodpaas) under the **Media processing** \> **Workflows** page within the specified space. For details, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). The sample code is as follows:

```TypeScript
this.videoUploader.setTemplateId(this.templateId);
```


<span id="52c39ea3"></span>
### Set asynchronous metadata extraction

If your business scenario does not require real\-time metadata extraction, you can use the asynchronous metadata extraction capability to improve upload speed. You need to call `setGetMetaMode` and set the mode to `1`. The sample code is as follows:

```TypeScript
this.videoUploader.setGetMetaMode(this.getMetaMode); // 1 = async, 0 = sync
```


<span id="3711ad88"></span>
### Customize upload configuration

The upload SDK also supports features like fragmentation, often used to upload large files. You can configure the chunk size, set the number of threads for fragmentation, and more. The implementation code example is shown below.

```TypeScript
// Whether to enable HTTPS
this.videoUploader.setEnableHttps(this.enableHttps); 

// Set the chunk size for fragmentation, in bytes, the default value is 512 * 1024
if (this.sliceSize > 0) {
  this.videoUploader.setSliceSize(this.sliceSize);
}

// Set the number of threads for fragmentation, the default value is 1
if (this.socketNum > 0) {
  this.videoUploader.setSocketNum(this.socketNum);
}

// Set the total connection timeout duration for the SDK, in seconds, the default value is 300
if (this.timeoutSec > 0) {
    this.videoUploader.setSDKMaxRetryTimeout(this.timeoutSec);
}
```

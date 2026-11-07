---
title: "Flutter Upload SDK: Uploading audios and videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-upload-sdk-uploading-audios-and-videos"
---

This article introduces how to use the Flutter Upload SDK to upload audio and video files to BytePlus VOD.

<span id="e9480078"></span>
## Prerequisites


* **SDK integration:**  You have already integrated the SDK. See [Flutter Upload SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-upload-sdk-quickstart) for details.

* **Space creation:**  You have already created a space.

* **App ID:**  You have created an application in the VOD console and obtained the App ID. For details, please refer to [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).


<span id="189a9fb8"></span>
## Basic features

<span id="e9a5eefb"></span>
### Initialize the SDK

Refer to the code below to initialize the SDK. You can choose whether to integrate the SDK's log reporting feature based on your actual needs. It is highly recommended to enable this module. If you do not need to use log reporting or do not want privacy data to be collected, please set `openAppLog` to `false` during initialization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The SDK does not collect any user personal information before initialization.</div>


```Dart
EnvOptions options = EnvOptions(
  appID: '<your_app_id>',
  appChannel: 'appChannel',
  appVersion: '1.0.0',
  appName: "FlutterUploadDemo",
  openAppLog: true,
  autoStartAppLog: true,
  debugLogLevel: true,
  enableLocalLogPrint: true,
  enableLogCallback: true,
);

await initEnv(options);
```


A detailed parameter description is shown in the table below.


|Parameter |Type |Default value |Description |
|---|---|---|---|
|appID |String |(Required) NA |The app ID, required. You can get the app ID on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|appChannel |String? |null |App channel number, required. This value should be customized based on your business needs, such as Xiaomi app store (xiaomi), Huawei app market (huawei), etc. |
|appVersion |String? |null |App version number, required. This value should be customized based on your business needs. A valid version number must contain at least two separators, such as `1.3.2`. |
|appName |String? |null |App name, required. You can get the app name on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|openAppLog |bool? |true |Whether to initialize AppLog. |
|autoStartAppLog |bool? |true |Enable AppLog (this setting only applies to Android). It is recommended to set it to false before the user grants privacy permissions, and after the user grants them, call `await Env.startAppLog();` to enable AppLog reporting. |
|debugLogLevel |bool? |false |Set the Debug level. During the debugging phase, it is recommended to enable this setting; in the online environment, please set it to `false`. |
|enableLocalLogPrint |bool? |false |Whether to print Native logs. During the debugging phase, it is recommended to enable this setting; in the online environment, please set it to `false`. |
|enableLogCallback |bool? |false |Whether to enable log callback, used in conjunction with the `setLogCallback(void Function(String?, int?) callback)` interface. |


<span id="55013887"></span>
### **Log callback**

When `enableLogCallback` is enabled, you can call `setLogCallback` to implement log callback.

```Dart
import 'package:byteplus_bd_file_upload/core/upload.dart';

// msg: Log content. level: 0 - 6, the higher the value, the higher the log level.
await setLogCallback((msg, level) {
  print('log callback------------>: $msg, $level');
});
```


<span id="e571d84c"></span>
### Create an uploader instance

Create an uploader instance.

```Dart
import 'package:byteplus_bd_file_upload/bd_file_upload.dart';

VideoUploaderOptions options = VideoUploaderOptions(
  accessKey: "your accessKey",
  secretKey: "your secretKey",
  sessionToken: "your sessionToken",
  serviceID: "your serviceID",
  region: "your region", // For the Asia Pacific Southeast (Johor) region, use "ap-southeast-1"
  filePaths: filePath, // Only supports uploading a single file, so the list length must be 1
  };
  
  BDVideoUploader uploader = await initVideoUploader(options);
```


<span id="389455bb"></span>
### Specify the path of the file to be uploaded

Only supports uploading a single file, so the list length must be 1.

```Dart
VideoUploaderOptions options = VideoUploaderOptions(
...
filePaths: ["filePath1"],
}
```


<span id="6cb799e3"></span>
### Set authentication parameters

Get the authentication parameters from your app server and pass them to the SDK. For more information, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Dart
VideoUploaderOptions options = VideoUploaderOptions(
  accessKey: "your accessKey",
  secretKey: "your secretKey",
  sessionToken: "your token",
  ...
}
```


<span id="d58f2851"></span>
### Specify the space to which the file will be uploaded

Set the space to which the file will be uploaded. To learn about space, see [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).

```Dart
VideoUploaderOptions options = VideoUploaderOptions(
   ...
   serviceID: "your service ID",
}
```


<span id="7aff874a"></span>
### Specify the file path in cloud storage

After the upload is complete, the file path in cloud storage is as follows: `StoreUri={{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}`. Here is an example of a complete cloud storage path: `ASmapleBucketName/path/to/foo/bar/test.mp4`.


|Parameter |Required |Description |
|---|---|---|
|BucketName |No |The bucket name is automatically generated. |
|FilePrefix |No |The file prefix must end with `/`, such as `path/to/foo/bar/`. |
|FileTitle |No |The file name. If not set, the SDK will automatically generate a 32\-bit string as the file name. |
|FileExtension |Yes |The file suffix must be started with `.`, such as `.mp4`, `.mp3`. |


For specific character rules, please refer to the [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).

You can refer to the following example code to set the cloud storage path.


<Tabs>
<Tab zoneid="ZbcwP1zcJG" title="Setting the complete storage path">
<TabTitle>Setting the complete storage path</TabTitle>

```Dart
// FileName = FilePrefix + FileTitle + FileExtension
VideoUploaderOptions options = VideoUploaderOptions(
    // Example 1, the storage path in the cloud: tos-pathxxx/byteplus/test.mp4
    fileName: "byteplus/test.mp4";
);

VideoUploaderOptions options = VideoUploaderOptions(
    // Example 2, the storage path in the cloud: tos-pathxxx/test.mp4
    fileName: "test.mp4";
);
```



</Tab>
<Tab zoneid="OQogAak56w" title="Setting prefix and suffix">
<TabTitle>Setting prefix and suffix</TabTitle>

```Dart
// Example The storage path in the cloud: tos-pathxxx/byteplus/b8bb180086f945709dfda76bc9c6133d.mp4
VideoUploaderOptions options = VideoUploaderOptions(
    // Set suffix, must be set, needs to start with a dot, such as .mp4, .mp3, etc.
    fileExtension: ".mp4",
    // Set prefix, optional setting, needs to end with /
    filePrefix: "byteplus/",
    ...
);
```



</Tab>
</Tabs>


<span id="8db03fc0"></span>
### Set the category

You can set the category ID for categorizing the uploaded videos. You can create categories and get the category ID in the BytePlus VOD console. For details, see [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Materials categorization is not supported.</div>


```Dart
VideoUploaderOptions options = VideoUploaderOptions(
   ...
   classificationId: "xxxxxxxxx",
}
```


<span id="a467d74b"></span>
### Control the upload process

The Upload SDK provides the following methods for controlling the upload process.


<Tabs>
<Tab zoneid="m7HIu640q4" title="Start uploading">
<TabTitle>Start uploading</TabTitle>

When the SDK executes this function internally, it will create a new thread and will not block. The example code is as follows:

```Dart
VideoUploaderOptions options = VideoUploaderOptions(
   ...
};
BDVideoUploader uploader = await initVideoUploader(options);

await uploader.start();
```



</Tab>
<Tab zoneid="x9ympTXY3F" title="Pause uploading">
<TabTitle>Pause uploading</TabTitle>

The example code for pausing uploading is as follows:

```Dart
await uploader.stop();
```



</Tab>
<Tab zoneid="PbmOLHSYXo" title="Terminate uploading">
<TabTitle>Terminate uploading</TabTitle>

Terminate uploading and release the underlying upload object. After release, uploading cannot continue. The example code for terminating uploading is as follows:

```Dart
await uploader.close();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">After the upload is complete, you must call close() to prevent memory leaks.</div>



</Tab>
</Tabs>


<span id="fa34faba"></span>
### Set the callbacks

```Dart
await uploader.setListener(
  VideoUploaderInfoCallback(
    // Callback after video upload is successful, close() method needs to be called in it to avoid leakage. uploadInfo is a BDVideoUploadInfo object
    onUploadSuccess: (uploadInfo) async {
      print(
        '--- [VideoUploaderInfoCallback] onUploadSuccess: ${jsonEncode(uploadInfo)}',
      );
      await uploader.close();
    },
    // Callback after video upload fails, close() method needs to be called in it to avoid leakage.
    onUploadFail: (errorCode, errorMsg, uploadInfo) {
      print(
        '--- [VideoUploaderInfoCallback] onUploadFail: $errorCode, $errorMsg, ${jsonEncode(uploadInfo)}',
      );
      await uploader.close();
    },
    // Callback for video upload progress: [0, 100]
    onUpdateProgress: (progress) {
      print(
        '--- [VideoUploaderInfoCallback] onUpdateProgress: $progress',
      );
    },
  ),
);
```


In the callback, `errorCode` is the error code, `errorMsg` is the error message, for details, please refer to the [Upload SDK error codes](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-error-codes).

The uploadInfo type in the callback is `BDVideoUploadInfo`, the callback description is shown in the table below:


|Parameter |Type |Description |
|---|---|---|
|vid |String? |Video ID, which is the `Vid` generated by the VOD service for audio and video type resources. |
|mid |String? |Material ID, which is the `Mid` generated by the VOD service for material type resources. |
|mCoverUri |String? |Cover URI. |
|oid |String? |TOS storage key. |
|videoMetaInfo |String? |Please refer to the `SourceInfo` parameter in [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) for details of media information.<br><br>Example: `{"Bitrate":463419,"Duration":39.726999999999997,"FileType":"video","Format":"MP4","Height":360,"Md5":"53f62abe3c29d0654b3405af7***7060","Size":2301285,"StoreUri":"tos-vod-cn-v-309be6ba73***b04/cd404e7bef654554b638422***7c0c40","Width":640}` |
|callbackArgs |String? |Passthrough data for server callbacks. |


<span id="8c22f52f"></span>
## Advanced features

<span id="53b3c7b5"></span>
### Set the snapshot time for the cover image

Call `setPoster` to set the time point for automatic snapshot, in seconds. The Upload SDK captures the video frame at the specified time point as the cover image. See the following example code:

```Dart
// Unit is in seconds, default value is 0
VideoUploaderOptions options = VideoUploaderOptions(
   ...
   poster: posterTime,
};
```


<span id="1ff6c078"></span>
### Enable resumable upload

To enable the resumable upload feature, call `setDiskResumeOption`. After enabling resumable upload, the Upload SDK can automatically resume the upload from the interruption point when users upload the same file in your application, thereby saving upload time. If it is for Android, you need to set the storage directory for the resumable upload file (there are two ways to set the storage directory, you can choose one).

See the following example code:

```Dart
// For Android, you need to additionally pass in the storage directory for resumable upload files. That is, set the value of resumeConfigDir. Note that it cannot end with "/".
VideoUploaderOptions options = VideoUploaderOptions(
  ...
  resumeConfigDir: diskResumeFilePath,
);
// In addition to the above method of setting the storage directory for resumable upload files, you can also call the following line of code to set it (choose one of the two).
await uploader.setSDKConfigDirForAndroid(diskResumeFilePath);


// Enable resumable upload, 1 to enable, 0 to disable, default is disabled.
await uploader.setDiskResumeOption(1);
```


<span id="b40e6a07"></span>
### Enable asynchronous meta info extraction

If your business scenario does not require synchronous meta info extraction, you can enable asynchronous meta info extraction to improve upload speed. Call `setEnableAsyncFetchMeta`.

See the following example code:

```Dart
await uploader.setEnableAsyncFetchMeta(true);
```


<span id="bf25d6cb"></span>
### Customize upload configuration

Call the following methods before starting the upload process to customize upload configuration.

```Java
VideoUploaderOptions options = VideoUploaderOptions(
  ...
  // Slice upload settings, slice size in bytes, default is 512 * 1024
  sliceSize: 512 * 512,
  // Number of parallel upload threads, default is 1
  socketNum: 1,
  // Single slice transfer timeout, unit is s, default is 40
  rwTimeout: 40,
  // Total connection timeout, unit is s, default is 70
  maxFailTime: 70,
  // System socket single read and write timeout, unit is s, default is 10
  tranTimeout: 10,
  // Slice retry count, default is 2
  sliceRetryCount: 2,
  // File level retry count, default is 3
  fileRetryCount: 3,
);

BDVideoUploader uploader = await initVideoUploader(options);

// Single TCP connection timeout, unit is ms, default is 5000
await uploader.setTcpOpenTimeOutMs(5000);

// Timeout for reusing the connection, to prevent slow upload speeds caused by poor quality of old connections, unit is s, default is 6
await uploader.setAliveMaxFailTime(6);
```


<span id="023a3b84"></span>
### Set the callback parameters

If you want to relay info as\-is from the client to the server, you can use the `setServerParameter` method. The parameter value will be sent back to your server through the `CallbackArgs` parameter in the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) callback. See the following example code:

```Dart
// Custom parameters to be carried, for example: "appid=123&did=123456&uid=12345&Region=xxx&StoreRegion=xxx"
VideoUploaderOptions options = VideoUploaderOptions(
    ...
    serverParameter: "appid=123&did=123456&uid=12345&Region=xxx&StoreRegion=xxx",
);
```


<span id="8e58e9ed"></span>
### Set the workflow ID

Call the `setTemplateId` method to set the workflow ID, triggering the media processing task. You can obtain the workflow ID from the **Workflows** page within the specified space on the BytePlus VOD console. For more details, refer to [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). Example code:

```Java
// Set the workflow ID
VideoUploaderOptions options = VideoUploaderOptions(
    ...
    templateId: templateId,
);
```

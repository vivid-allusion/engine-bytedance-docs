---
title: "Flutter Upload SDK: Uploading materials"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-upload-sdk-uploading-materials"
---

To upload materials such as subtitles, cover images, trailers, and audio to BytePlus VOD from your Flutter application, you can use the Flutter Upload SDK. This guide provides detailed instructions and code examples for initialization, setting upload parameters, controlling the upload process, and enabling advanced features like resumable uploads.

<span id="108c7138"></span>
## Prerequisites


* **SDK integration:**  You have already integrated the SDK. See [Flutter Upload SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-upload-sdk-quickstart) for details.

* **Space creation:**  You have already created a space.

* **App ID:**  You have created an application in the VOD console and obtained the App ID. For details, please refer to [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management).


<span id="ed2e8358"></span>
## Basic features

<span id="de42e36a"></span>
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
|appChannel |String? |null |The app channel, which is required. Customize this value based on your app's distribution channel, such as Xiaomi app store (xiaomi), Huawei app market (huawei), and more. |
|appVersion |String? |null |App version number, required. This value needs to be customized according to your current business situation, a valid version number must contain at least two separators, such as 1.3.2. |
|appName |String? |null |App name, required. You can get the app name on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|openAppLog |bool? |true |Whether to initialize AppLog. |
|autoStartAppLog |bool? |true |Enable AppLog (this setting only applies to Android). It is recommended to set it to false before the user agrees to the privacy permissions, and after the user agrees to the privacy permissions, call `await Env.startAppLog();` to enable AppLog reporting. |
|debugLogLevel |bool? |false |Enables debug\-level logging. During the debugging phase, it is recommended to enable this setting; in a production environment, please set it to false. |
|enableLocalLogPrint |bool? |false |Whether to print Native logs. During the debugging phase, it is recommended to enable this setting; in a production environment, please set it to false. |
|enableLogCallback |bool? |false |Whether to enable log callback, used in conjunction with the `setLogCallback(void Function(String?, int?) callback)` interface. |


<span id="483ccb0d"></span>
### **Log callback**

When `enableLogCallback` is enabled, you can call `setLogCallback` to implement log callback.

```Dart
import 'package:byteplus_bd_file_upload/core/upload.dart';

// msg: Log content. level: 0 - 6, the higher the value, the higher the log level.
await setLogCallback((msg, level) {
  print('log callback------------>: $msg, $level');
});
```


<span id="ef450465"></span>
### Create an uploader instance

Create an uploader instance.

```Dart
import 'package:byteplus_bd_file_upload/bd_file_upload.dart';

MaterialUploaderOptions options = MaterialUploaderOptions(
  accessKey: "your accessKey",
  secretKey: "your secretKey",
  sessionToken: "your sessionToken",
  serviceID: "your serviceID",
  region: "your region", // For the Asia Pacific Southeast (Johor) region, use "ap-southeast-1"
  filePaths: filePath, // Only supports uploading a single file, so the list length must be 1.
  };
  
BDMaterialUploader uploader = await initMaterialUploader(options);
```


<span id="3b4754b3"></span>
### Specify the path of the file to be uploaded

Only supports uploading a single file, so the list length must be 1.

```Dart
MaterialUploaderOptions options = MaterialUploaderOptions(
...
filePaths: ["filePath1"],
}
```


<span id="9f6e76cd"></span>
### Set authentication parameters

Get the authentication parameters from your app server and pass them to the SDK. For more information, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Dart
MaterialUploaderOptions options = MaterialUploaderOptions(
  accessKey: "your accessKey",
  secretKey: "your secretKey",
  sessionToken: "your token",
  ...
}
```


<span id="20eb05b2"></span>
### Specify the space to which the file will be uploaded

Set the space to which the file will be uploaded. To learn about space, see [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).

```Dart
MaterialUploaderOptions options = MaterialUploaderOptions(
   ...
   serviceID: "your service ID",
}
```


<span id="4d19546a"></span>
### Specify the file path in cloud storage

After the upload is complete, the file path in cloud storage is as follows: `StoreUri={{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}`. Here is an example of a complete cloud storage path: `ASampleBucketName/path/to/foo/bar/test.mp4`.


|Parameter |Required |Description |
|---|---|---|
|BucketName |No |The bucket name is automatically generated. |
|FilePrefix |No |The file prefix must end with `/`, such as `path/to/foo/bar/`. |
|FileTitle |No |The file name. If not set, the SDK will automatically generate a 32\-bit string as the file name. |
|FileExtension |Yes |The file suffix must start with `.`, such as `.mp4`, `.mp3`. |


For specific character rules, please refer to the [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).

You can refer to the following example code to set the cloud storage path.


<Tabs>
<Tab zoneid="XzhZPSIpoV" title="Setting the complete storage path">
<TabTitle>Setting the complete storage path</TabTitle>

```Dart
// FileName = FilePrefix + FileTitle + FileExtension
MaterialUploaderOptions options = MaterialUploaderOptions(
    ...
    // Example 1, the storage path in the cloud: tos-pathxxx/byteplus/test.mp4
    fileName: "byteplus/test.mp4",
    // Example 2, the storage path in the cloud: tos-pathxxx/test.mp4
    // fileName: "test.mp4",
);
```



</Tab>
<Tab zoneid="si6dXzQfYh" title="Setting prefix and suffix">
<TabTitle>Setting prefix and suffix</TabTitle>

```Dart
// Example The storage path in the cloud: tos-pathxxx/byteplus/b8bb180086f945709dfda76bc9c6133d.mp4
MaterialUploaderOptions options = MaterialUploaderOptions(
    // Set suffix, must be set, needs to start with a dot, such as .mp4, .mp3, etc.
    fileExtension: ".mp4",
    // Set prefix, optional setting, needs to end with /
    filePrefix: "byteplus/",
    ...
);
```



</Tab>
</Tabs>


<span id="12e08869"></span>
### Set the material information

Here is a code example of how to set material information:

```Dart
MaterialUploaderOptions options = MaterialUploaderOptions(
    ...
    title: "title",
    tags: "tags",
    description: "description",
    format: formatStr,
);

BDMaterialUploader uploader = await initMaterialUploader(options);

await uploader.setFileType(fileType);

await uploader.setCategory(category);
```


Detailed parameter descriptions are shown in the table below.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileType |String |File type. Supported values: media, image, object. |
|Title |String |File title. |
|Tags |String |Multiple tags separated by commas. |
|Description |String |A description of the material. |
|Category |String |The material category. When uploading material, you can specify the category information. Supported values: video, audio, image, dynamic_img, subtitle, font. |
|Format |String |The file format. If you specify the `Format`, it will be determined by the parameter you provide; otherwise, it will be determined by the format recognized by the system. If the file cannot be automatically identified, the `Format` field might be empty. |


Relationship between `FileType` and `Category` :


|**FileType Value** |**Category Value** |
|---|---|
|media |video, audio |
|image |image, dynamic_img |
|object |subtitle, font |


<span id="56ceb634"></span>
### Control the upload process

The Upload SDK provides the following methods for controlling the upload process.


<Tabs>
<Tab zoneid="E9ZTJ1SBlE" title="Start uploading">
<TabTitle>Start uploading</TabTitle>

When the SDK executes this function internally, it will create a new thread and will not block. The example code is as follows:

```Dart
await uploader.start();
```



</Tab>
<Tab zoneid="JOqTMY6Hha" title="Pause uploading">
<TabTitle>Pause uploading</TabTitle>

The example code for pausing uploading is as follows:

```Dart
await uploader.stop();
```



</Tab>
<Tab zoneid="z3c05WKSPO" title="Terminate uploading">
<TabTitle>Terminate uploading</TabTitle>

Terminate uploading and release the underlying upload object. After release, uploading cannot continue. The example code for terminating uploading is as follows:

```Dart
await uploader.close();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">After uploading is complete, please call <code>await uploader.close()</code>, otherwise it will cause memory leaks.</div>



</Tab>
</Tabs>


<span id="ff39e034"></span>
### Set the callbacks

```Dart
await uploader.setListener(
  MaterialUploaderInfoCallback(
    // Callback for successful asset upload. You need to call the close() method to avoid memory leaks.
    onUploadSuccess: (uploadInfo) async {
      print(
        '--- [MaterialUploaderInfoCallback] onUploadSuccess: ${jsonEncode(uploadInfo)}',
      );
      await uploader.close();
    },
    // Callback for failed asset upload. Call close() to avoid memory leaks.
    onUploadFail: (errorCode, errorMsg, uploadInfo) {
      print(
        '--- [MaterialUploaderInfoCallback] onUploadFail: $errorCode, $errorMsg, ${jsonEncode(uploadInfo)}',
      );
      await uploader.close();
    },
    // Callback for asset upload progress: [0,100]
    onUpdateProgress: (progress) {
      print(
        '--- [MaterialUploaderInfoCallback] onUpdateProgress: $progress',
      );
    },
  ),
);
```


In the callback, `errorCode` is the error code, `errorMsg` is the error message, for details, please refer to the [Upload SDK error codes](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-error-codes).

The uploadInfo type in the callback is `BDVideoUploadInfo`, the callback parameters are described in the table below:


|Parameter |Type |Description |
|---|---|---|
|vid |String? |Video ID, which is the `Vid` generated by the VOD service for audio and video type resources. |
|mid |String? |Material ID, which is the `Mid` generated by the VOD service for material type resources. |
|mCoverUri |String? |Cover URI. |
|oid |String? |TOS storage key. |
|videoMetaInfo |String? |Media information, which includes details like bitrate, format, length, and width. Please refer to the `SourceInfo` parameter in [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) for details of media information.<br><br>Example: `{"Bitrate":463419,"Duration":39.726999999999997,"FileType":"video","Format":"MP4","Height":360,"Md5":"53f62abe3c29d0654b3405af7***7060","Size":2301285,"StoreUri":"tos-vod-cn-v-309be6ba73***b04/cd404e7bef654554b638422***7c0c40","Width":640}` |
|callbackArgs |String? |Transmitted server callback information. |


<span id="fa24307b"></span>
## Advanced features

<span id="e46e3a3c"></span>
### Enable resumable upload

To enable the resumable upload feature, call `setDiskResumeOption`. After enabling resumable upload, the Upload SDK can automatically resume the upload from the interruption point when users upload the same file in your application, thereby saving upload time. If it is for Android, you need to set the storage directory for the resumable upload file (there are two ways to set the storage directory, you can choose one).

See the following example code:

```Dart
// For Android, you need to additionally pass in the storage directory for resumable upload files. That is, set the value of resumeConfigDir. Note that it cannot end with "/".
MaterialUploaderOptions options = MaterialUploaderOptions(
   ...
   resumeConfigDir: diskResumeFilePath,
};
// In addition to the above method of setting the storage directory for resumable upload files, you can also call the following line of code to set it (choose one of the two).
await uploader.setSDKConfigDirForAndroid(diskResumeFilePath);


// Enable resumable upload, 1 to enable, 0 to disable, default is disabled.
await uploader.setDiskResumeOption(1);
```


<span id="064ebed2"></span>
### Customize upload configuration

Call the following methods before starting the upload process to customize upload configuration.

```Java
MaterialUploaderOptions options = MaterialUploaderOptions(
   ...
   // Custom parameters for the client, such as "testkey=testValue"
   serverParameter: "testkey=testValue",
   // Setting slice size for segmented upload, in bytes. The default value is 512 * 1024
   sliceSize: 512 * 512,
   // Number of parallel upload threads to enable. The default value is 1
   socketNum: 1,
   // Timeout for single slice transfer, unit is seconds. The default value is 40
   rwTimeout: 40,
   // Total connection timeout, unit is seconds. The default value is 70
   maxFailTime: 70,
   // System socket read/write timeout per time, unit is seconds. The default value is 10
   tranTimeout: 10,
   // The number of times to retry a failed slice upload. The default is 2
   sliceRetryCount: 2,
   // The number of times to retry a failed file upload. The default is 3
   fileRetryCount:3,
);

BDMaterialUploader uploader = await initMaterialUploader(options);

// Timeout for single TCP connection establishment, unit is milliseconds. The default value is 5000
await uploader.setTcpOpenTimeOutMs(5000);

// Timeout for reusing connections, preventing slow upload speeds due to poor quality of old connections, unit is s, default value is 6
await uploader.setAliveMaxFailTime(6);
```

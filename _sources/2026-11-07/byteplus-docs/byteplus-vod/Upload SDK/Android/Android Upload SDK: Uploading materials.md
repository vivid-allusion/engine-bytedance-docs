---
title: "Android Upload SDK: Uploading materials"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-materials"
---

To integrate file uploading into your Android application, use the BytePlus VOD Upload SDK. This guide walks you through the entire process, from basic initialization and authentication to managing the upload lifecycle and implementing advanced features like resumable uploads and custom configurations.

<span id="df3fee09"></span>
## Prerequisites

Ensure that you have integrated the Android Upload SDK.

<span id="1266b84c"></span>
## Basic features

<span id="8ae16d4a"></span>
### Enable logging

During development, enable logging for debugging and troubleshooting. Remember to disable logging for the release version to reduce performance impact.

```Java
BDUploadLog.turnOn(LOG_DEBUG, 1);
BDUploadUtil.setEnableNativeLog(true);
```


<span id="ebed2c0d"></span>
### Initialize the SDK

We recommend that you initialize the SDK in `Application#onCreate`. See the following sample code:

```Java
Env.start(new Config.Builder()
        .setApplicationContext(context)
        .setAppID("your app id")
        .setAppName("your app English name")
        .setAppVersion(BuildConfig.VERSION_NAME)
        .setAppChannel("channel name")
        .setBizType(BIZ_TYPE_UPLOAD)
        .build());
```


When initializing the SDK, set the following parameters:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|AppId |String |The app ID. You can get the app ID on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|AppName |String |The English name of the app. You can get the app name on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|AppVersion |String |The version number of the app. You can set this parameter as `BuildConfig.VERSION_NAME`. A valid version number should contain two or more delimiters, such as `"1.3.2"`. |
||||
|AppChannel |String |The name of the channel where your app is distributed, such as `googleplay`. |
||||


<span id="d5450a93"></span>
### Create an uploader instance

Create an uploader instance with the `BDMaterialUploader` class, as follows:

```Java
BDMaterialUploader mUploader = new BDMaterialUploader();
```


<span id="b49a75a8"></span>
### Specify the path of the file to be uploaded

Call `setPathName` to specify the absolute path of the file to be uploaded:

```Java
mUploader.setPathName("/data/user/0/xxx/files/test.mp4");
```


<span id="6b87cefd"></span>
### Set authentication parameters

Get the authentication parameters from your app server and pass them to the SDK.

```Java
mUploader.setTopAccessKey("xxx");
mUploader.setTopSecretKey("xxx");
mUploader.setTopSessionToken("xxx");
```


<span id="ceef0a5f"></span>
### Specify the space to which the file will be uploaded

Call `setSpaceName` to specify the space to which the file will be uploaded. To learn about space, see [Space management](https://docs.byteplus.com/en/byteplus-vod/docs/space-management).

```Java
mUploader.setSpaceName("xxx");
```


<span id="7e19d1e0"></span>
### Specify the file path in cloud storage

After the upload is complete, the file path in cloud storage is as follows:

`StoreUri={{BucketName}}/{{FilePrefix}}{{FileTitle}}{{FileExtension}}`


|**Parameter** |**Description** |
|---|---|
|BucketName |The bucket name is automatically generated. |
|FilePrefix |The file prefix must end with `/`, such as `"path/to/foo/bar/"`. |
|FileTitle |The file name. If not set, the SDK will automatically generate a 32\-bit string as the file name. |
|FileExtension |The file suffix must start with `.`, such as `".mp4"`. |


You can either specify the full path or just specify the file prefix and suffix.


* Call `setFileName` to set the full path. Note that the full path must contain a suffix, such as `.mp4` or `.mp3`. Otherwise an error occurs.

   ```Java
   // The file path is tos-pathxxx/volc/test.mp4
   mUploader.setFileName("volc/test.mp4"); 
   // The file path is tos-pathxxx/test.mp4
   mUploader.setFileName("test.mp4");
   ```
   

* Call `setFilePrefix` and `setFileExtension` to set the prefix and suffix:

   ```Java
   // The file path is tos-pathxxx/volc/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4"); 
   mUploader.setFilePrefix("volc/"); 
   // The file path is tos-pathxxx/b8bb180086f945709dfda76bc9c6133d.mp4
   mUploader.setFileExtension(".mp4");
   ```
   


<span id="d0e5fc49"></span>
### Set the material information

To set the material information, call the following APIs:

```Java
// Set the file type as media, image, or object
public void setFileType(String fileType)

// Set the file title
public void setTitle(String title)

// Set the file tag
public void setTags(String tags)

// Set the file description
public void setDescription(String description)

// Set the file category as video, audio, image, dynamic_img, subtitle, or font
public void setCategory(String category)

// Set the file format
public void setFormat(String format)
```


Detailed parameter descriptions are shown in the table below.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|FileType |String |File type. Supported values: media, image, object. |
|Title |String |File title. |
|Tags |String |Multiple tags separated by commas. |
|Description |String |Description information. |
|Category |String |The material category. When uploading material, you can specify the category information. Supported values: video, audio, image, dynamic_img, subtitle, font. |
|Format |String |The file format. If you specify the `Format`, it will be determined by the parameter you provide; otherwise, it will be determined by the format recognized by the system. If unique files cannot be identified, the `Format` field may remain empty. |


Relationship between `FileType` and `Category` :


|**FileType Value** |**Category Value** |
|---|---|
|media |video, audio |
|image |image, dynamic_img |
|object |subtitle, font |


<span id="18f8a230"></span>
### Control the upload process

The Player SDK provides the following methods for controlling the upload process:


* Call `start` to start uploading:

   ```Java
   mUploader.start();
   ```
   

* Call `stop` to pause uploading:

   ```Java
   mUploader.stop();
   ```
   

* After the upload is complete, call `close` to terminate uploading. Otherwise it will cause memory leaks.

   ```Java
   mUploader.close()
   ```
   


<span id="9131e382"></span>
### Set the callbacks

If the `Uploader` instance is created in Thread A and Thread A has a Looper, the callback will be executed in Thread A. Otherwise, the callback will be executed in the main thread.

```Java
public void setListener(BDMaterialUploaderListener listener)

public interface BDMaterialUploaderListener {
    // Callback for upload progress and status. See the table below
    void onNotify(int what, long parameter, BDVideoInfo info);
    
    // Key log callback. You can upload the callback information to your server for troubleshooting online issues.
    // It needs to be enabled by calling mUploader.setEnableLogCallBack(true).
    void onLog(int what, int code, String info);
    
    // Callback for upload error retry. You need to check the network status.
    // Return 1: SDK retries.
    // Return 0: SDK stops retrying.
    // If you do not want to check network status, just return 1, and the SDK will retry within the retry limit and timeout.
    int videoUploadCheckNetState(int errorCode, int tryCount);

    // Not in use
    String getStringFromExtern(int key);
}
```


See the table below for the `onNotify` callback.


|**Message type** |**Description** |**The 'what' value** |**The 'parameter' meaning** |**The 'info' meaning** |
|---|---|---|---|---|
|MsgIsComplete |Notification of video upload completion. Call `close()` to release the upload object. |0 |N/A |See [BDVideoInfo](https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos#bdvideoinfo) |
|MsgIsFlushComplete |Notification of video fast upload completion. Call `close()` to release the upload object. |50 |N/A |See [BDVideoInfo](https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos#bdvideoinfo) |
|MsgIsFail |Notification of video upload failure. If retry is needed, call `start()` to upload again; otherwise, call `close()` to release the upload object. |2 |For details, refer to [Upload SDK error codes](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-error-codes). |See [BDVideoInfo](https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos#bdvideoinfo) |
|MsgIsUpdateProgress |Update on video upload progress. |1 |Upload progress. Range is [0,100]. |N/A |
|MessageIsDiskResumeInfoError |Callback when the SDK cannot resume upload, falling back to normal upload. You will receive a callback indicating success or failure of the upload. |120 |N/A |N/A |


<span id="22d6049f"></span>
## Advanced features

<span id="adbd8c63"></span>
### Enable resumable upload

Call `setDiskResumeOption` to enable the feature of resuming uploading from where it was terminated.

```Java
// Specify the directory for storing the SDK configuration file
BDUploadUtil.setSDKConfigDir(dir)

// Enable the feature of resuming uploading from where it was terminated
mUploader.setDiskResumeOption(1);
```


<span id="3b607016"></span>
### Custom configuration

```Java
// Set the size of each slice for uploading, in bytes. Default value is 512 * 1024
public void setSliceSize(int size)

// Set the number of threads for parallel uploading. Default value is 1
public void setSocketNum(int num)

// Set the TCP connection timeout in milliseconds. Default value is 5000
public void setTcpOpenTimeOutMilliSec(int openTimeOutMilliSec)

// Set the timeout for transferring a single slice, in seconds. Default is 40
public void setRWTimeout(int timeOut)

// Set the total connection timeout, in seconds. Default is 70
public void setMaxFailTime(int maxTime)

// Set the system socket read/write timeout, in seconds. Default is 10
public void setTranTimeOutUnit(int tranTimeOutUnit)

// Set the timeout for reusing connections to prevent a decrease in upload speed due to deterioration in old connection quality, in seconds. Default is 6
public void setAliveMaxFailTime(int maxFailTime)

// Set the number of retry attempts for a single slice. Default value is 2
public void setSliceReTryCount(int retryCount)

// Set the number of retry attempts at the file level. Default value is 3
public void setFileRetryCount(int retryCount)

// Set custom parameters, such as "testkey=testValue"
public void setServerParameter(String value)

// Enable HTTPS, set to 1 to fully enable
public void setEnableHttps(int isEnableHttps)
```

---
title: "Android Upload SDK: Uploading audios and videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos"
---

To upload audio and video files to BytePlus VOD from your Android application, you can use the Android Upload SDK. This guide provides detailed instructions and code examples covering the entire process, from basic initialization and configuration to implementing advanced features like resumable uploads and custom workflows.

<span id="df3fee09"></span>
## Prerequisites

Ensure that you have integrated the Android Upload SDK.

<span id="87585b52"></span>
## Basic features

<span id="ed8be264"></span>
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


|Parameter |Type |Required |Description |
|---|---|---|---|
|AppId |String |Yes |The app ID. You can get the app ID on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|AppName |String |Yes |The app name. You can get the app name on the [Applications](https://console.byteplus.com/vodpaas/sdk/) page in the BytePlus VOD console. For details, see [Applications](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-management). |
|AppVersion |String |Yes |The version number of the app. You can set this parameter as `BuildConfig.VERSION_NAME`. A valid version number should contain two or more delimiters, such as `"1.3.2"`. |
|AppChannel |String |Yes |The name of the channel where your app is distributed, such as `googleplay`. |


<span id="d5450a93"></span>
### Create an uploader instance

Create an uploader instance with the `BDVideoUploader` class, as follows:

```Java
BDVideoUploader mUploader = new BDVideoUploader();
```


<span id="b49a75a8"></span>
### Specify the path of the file to be uploaded

Call `setPathName` to specify the absolute path of the file to be uploaded:

```Java
mUploader.setPathName("/data/user/0/xxx/files/test.mp4");
```


<span id="6b87cefd"></span>
### Set authentication parameters

Get the authentication parameters from your app server and pass them to the SDK. For more information, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```Java
mUploader.setTopAccessKey("xxx");
mUploader.setTopSecretKey("xxx");
mUploader.setTopSessionToken("xxx");
```


<span id="ceef0a5f"></span>
### Specify the space to which the file will be uploaded

Call `setSpaceName` to specify the space to which the file will be uploaded. To learn about space, see [Spaces](https://docs.byteplus.com/docs/byteplus-vod/docs-space-management).

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
|FileTitle |The file name. If not set, the SDK will automatically generate a 32\-character string as the file name. |
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
   


<span id="74023d10"></span>
### Set the category

You can set the category ID for categorizing the uploaded videos. You can create categories and get the category ID in the BytePlus VOD console. For details, see [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc). The following code shows an example:

```Java
public void setClassificationId(long classificationId)
```


<span id="18f8a230"></span>
### Control the upload process

The Upload SDK provides the following methods for controlling the upload process:


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
   


<span id="ff3e7d65"></span>
### Set the callbacks

If the `Uploader` instance is created in Thread A and Thread A has a Looper, the callback will be executed in Thread A. Otherwise, the callback will be executed in the main thread.

```Java
public void setListener(BDVideoUploaderListener listener)

public interface BDVideoUploaderListener {
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
|MsgIsComplete |Notification of video upload completion. Call<br><br>`close()` to release the upload object. |0 |N/A |See [BDVideoInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-uploading-audios-and-videos#590fb4cc) |
|MsgIsFlushComplete |Notification of video fast upload completion. Call<br><br>`close()` to release the upload object. |50 |N/A |See [BDVideoInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-uploading-audios-and-videos#590fb4cc) |
|MsgIsFail |Notification of video upload failure. If retry is needed, call<br><br>`start()` to upload again; otherwise, call<br><br>`close()` to release the upload object. |2 |For details, refer to [Upload SDK error codes](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-error-codes). |See [BDVideoInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-uploading-audios-and-videos#590fb4cc) |
|MsgIsUpdateProgress |Update on video upload progress. |1 |Upload progress. Range is [0,100]. |N/A |
|MessageIsDiskResumeInfoError |Callback when the SDK cannot resume upload, falling back to normal upload. You will receive a callback indicating success or failure of the upload. |120 |N/A |N/A |


<span id="22d6049f"></span>
## Advanced features

<span id="124c6de2"></span>
### Set the snapshot time for the cover image

Call `setPoster` to set the time point for automatic snapshot, in seconds. The Upload SDK captures the video frame at the specified time point as the cover image. See the following example code:

```Java
// Unit: ms
// The default value is 0
public void setPoster(float posterTime)
```


<span id="290f3053"></span>
### Enable resumable upload

To enable the resumable upload feature, call `setSDKConfigDir` and `setDiskResumeOption`. After enabling resumable upload, the Upload SDK can automatically resume the upload from the interruption point when users upload the same file in your application, thereby saving upload time.

See the following example code:

```Java
// Specify the directory for storing the resumable upload configuration file. The Upload SDK requires read and write permissions for this directory. Call this method once after initialization.
BDUploadUtil.setSDKConfigDir(dir)

// To enable resumable upload, call this method for each uploader instance.
mUploader.setDiskResumeOption(1);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Resumable upload is not supported for files uploaded using <code>Reader</code>.</div>


<span id="9cb31a50"></span>
### Enable asynchronous meta info extraction

If your business scenario does not require synchronous meta info extraction, you can enable asynchronous meta info extraction to improve upload speed. Call `setGetMetaMode` and set `mode` to `GET_META_ASYNC`.

See the following example code:

```Java
mUploader.setGetMetaMode(GET_META_ASYNC);
```


<span id="4bed1873"></span>
### Customize upload configuration

Call the following methods before starting the upload process to customize upload configuration.

```Java
// Sets the segment size in bytes. The default value is 512 * 1024.
// When uploading large files, the Upload SDK segments them to mitigate the impact of network fluctuations and enhance upload speed.
public void setSliceSize(int size)

// Sets the number of concurrent connections when uploading file segments. The default value is 1.
public void setSocketNum(int num)  

// Sets the TCP connection timeout in milliseconds. The default value is 5000.
public void setTcpOpenTimeOutMilliSec(int openTimeOutMilliSec) 

// Sets the timeout for transferring a single segment in seconds. The default value is 40.
public void setRWTimeout(int timeOut) 

// Sets the connection establishment timeout in seconds. The default value is 70.
public void setMaxFailTime(int maxTime)

// Sets the timeout for system socket read and write operations in seconds. The default value is 10.
public void setTranTimeOutUnit(int tranTimeOutUnit)

// Sets the timeout for reusing connections in seconds. The default value is 6.
public void setAliveMaxFailTime(int maxFailTime)

// Sets the number of retries allowed for uploading a single segment. The default value is 2.
public void setSliceReTryCount(int retryCount) 

// Sets the number of retries allowed for uploading a file. The default value is 3.
public void setFileRetryCount(int retryCount)

// Sets whether to enable HTTPS. 1: Enable; 0: Disable
public void setEnableHttps(int isEnableHttps)
```


<span id="80813c8e"></span>
### Set the callback parameters

If you want to relay info as\-is from the client to the server, you can use the `setServerParameter` method. The parameter value will be sent back to your server through the `CallbackArgs` parameter in the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) callback. See the following example code:

```Java
// The information that you want to pass, such as "appid=123&did=123456&uid=12345&Region=xxx&StoreRegion=xxx"
public void setServerParameter(String value)
```


<span id="52862099"></span>
### Set the workflow ID

Call the `setTemplateId` method to set the workflow ID, triggering the media processing task. You can obtain the workflow ID from the **Workflows** page within the specified space on the BytePlus VOD console. For more details, refer to [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). Example code:

```Java
// Set the workflow ID
mUploader.setTemplateId(templateId);
```


<span id="488819e9"></span>
## Reference

<span id="590fb4cc"></span>
### **BDVideoInfo**


|**Parameter** |**Description** |
|---|---|
|mVideoId |The video ID generated by BytePlus VOD. |
|mMid |The material ID generated by BytePlus VOD. |
|mCoverUri |The URI of the cover image |
|mTosKey |The TOS storage key |
|mErrorCode |Error code. For details, refer to [Upload SDK error codes](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-sdk-error-codes). |
|mErrorMsg |Error message |
|mVideoMediaInfo |The media information, including bitrate, format, length, resolution. See the `SourceInfo` parameter in [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) for details. Example:<br><br>```JSON```<br>```{"Bitrate":463419,"Duration":39.726999999999997,"FileType":"video","Format":"MP4","Height":360,"Md5":"53f62abe3c29d0654b3405af7***7060","Size":2301285,"StoreUri":"tos-vod-cn-v-309be6ba73***b04/cd404e7bef654554b638422***7c0c40","Width":640}```<br> |
|mCallbackArgs |The data transmitted from the server. |
|mLog |Not in use |
|mProgress |Upload progress. Range is [0,100] |
|mEncryptionMeta |Not in use |

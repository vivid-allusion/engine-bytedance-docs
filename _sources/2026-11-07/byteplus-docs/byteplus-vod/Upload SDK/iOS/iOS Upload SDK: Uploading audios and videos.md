---
title: "iOS Upload SDK: Uploading audios and videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos_1"
---

This article introduces how to use the iOS Upload SDK to upload audio and video files to BytePlus VOD.

<span id="99f24995"></span>
## Prerequisites

Ensure that you have integrated the iOS Upload SDK.

<span id="24a99d52"></span>
## Basic features

<span id="a03e9d3a"></span>
### Initialize the SDK

See the following sample code:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Initialize the SDK
    [self initTTSDK];
    
    return YES;
}
 
- (void)initTTSDK {
    // Enable debug mode for the uploader
#if DEBUG
    [[BDUploadUtilTool sharedInstance] enableNativeLogFunc:YES];
#endif

    // Get the app ID from the BytePlus VOD console
    // NSString *appId = @"you app id";
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:<#appid#> licenseName:licenseName];
    [TTSDKManager startWithConfiguration:configuration];
}
```


<span id="0f242712"></span>
### Create an uploader instance

Create an uploader instance with the `BDVideoUploaderClient` class, as follows:

```objectivec
#import <TTSDK/BDFileUploaderHeader.h>

- (void)initVideoUploader {
    // 1. When initializing the uploader object, specify the path of the file to be uploaded
    // NSString *filePath = @"path/to/upload/file";
    BDVideoUploaderClient *videoUploadClient = [[BDVideoUploaderClient alloc] initWithFilePath:<#filepath#>];
    
    // 2. Get the authentication parameters from your app server and pass them to the SDK 
    //NSDictionary *authParameter = @{
    //    BDFileUploadAccessKey: accessKeyId,
    //    BDFileUploadSecretKey: secretKeyId,
    //    BDFileUploadSessionToken: sessionToken,
    //    Specify the space to which the file will be uploaded
    //    BDFileUploadSpace: uploadSpace,
    //};
    [videoUploadClient setAuthorizationParameter:<#authparameter#>];
    
    // 3. Customize upload configurations
    [videoUploadClient setUploadConfig:@{
        // Set the slice size
        BDFileUploadSliceSize:@(512 * 1024),
    }];
    
    // 4. Set the BDVideoUploadClientDelegate
    //  @see {BDVideoUploadClientDelegate.h}
    videoUploadClient.delegate = self;
    
    // 5. Set the uploader client as a global variable
    self.videoUploadClient = videoUploadClient;
}
```


<span id="cdf71ecd"></span>
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

   ```objectivec
   // FileName = FilePrefix + FileTitle + FileExtension
   [self.videoUploadClient setFileName:<#filename#>];
   ```
   

* Call `setFilePrefix` and `setFileExtension` to set the prefix and suffix:

   ```objectivec
   // The file prefix must end with /
   [self.videoUploadClient setFilePrefix:<#fileprefix#>];
   // The file suffix must start with .
   [self.videoUploadClient setFileExtension:<#fileextension#>];
   ```
   


<span id="994cfec8"></span>
### Set the category

You can set the category ID for categorizing the uploaded videos. You can create categories and get the category ID in the BytePlus VOD console. For details, see [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc). The following code shows an example:

```objectivec
- (void)setClassificationId:(NSInteger)classificationId;
```


<span id="6561c443"></span>
### Control the upload process

The Upload SDK provides the following methods for controlling the upload process:


* Call `start` to start uploading:

   ```objectivec
   [self.videoUploadClient start];
   ```
   

* Call `stop` to pause uploading:

   ```objectivec
   [self.videoUploadClient stop];
   ```
   

* After the upload is complete, call `close` to terminate the upload.

   ```objectivec
   [self.videoUploadClient stop];
   ```
   


<span id="3bd0f36d"></span>
### Set the callbacks

You can set up callbacks to get the video upload results and upload progress. The code example is as follows:

```objectivec
#pragma mark - BDVideoUploadClientDelegate

/// Callback for video upload completion
/// @param uploadClient Video upload instance
/// @param videoInfo Information callback after video upload completion
/// @param error If the upload fails, an error will be returned
- (void)videoUpload:(nonnull BDVideoUploaderClient*)uploadClient didFinish:(nullable BDVideoUploadInfo *)videoInfo error:(nullable NSError *)error {
    if (!error) {
       // Video uploaded successfully
    } else {
       // Video upload failed
       // You can determine the specific reason for upload error based on the detailed information in BDVideoUploadInfo. See explanation below
       NSLog  
    }
    // Release the upload object
    [uploadClient close];
}
 
/// Callback for video upload progress
/// @param uploadClient Video upload object
/// @param progress Progress of the video upload
- (void)videoUpload:(nonnull BDVideoUploaderClient*)uploadClient progressDidUpdate:(NSInteger)progress {
    // NSLog(@"progress update:%ld", progress);
}
```


If the upload fails, an `error` will be returned. SDK error codes and gateway error codes are stored in different locations in `NSError`. The specific locations are as follows:

```objectivec
- (void)videoUpload:(nonnull BDVideoUploaderClient*)uploadClient didFinish:(nullable BDVideoUploadInfo *)videoInfo error:(nullable NSError *)error {
    if (!error) { 
        // Upload successfully
    } else {
        // Upload failed
        // Get the SDK error code
        NSLog(@"SDK error code is: %ld", error.code);
        // If there is a gateway error code, the gateway error code will be included in NSError.userInfo, and can be parsed as needed
        if ([error.userInfo isKindOfClass:NSDictionary.class]) {
            NSLog(@"error message is: %@", error.userInfo[@"message"]);
        }
    }
    // Release the upload object
    [uploadClient close];
}
```


<span id="2f6d8130"></span>
## Advanced features

<span id="deceda56"></span>
### Set the snapshot time for the cover image

Call `setSnapshot` to set the time point for automatic snapshot, in seconds. The Upload SDK captures the video frame at the specified time point as the cover image. See the following example code:

```objectivec
[self.videoUploadClient setSnapshot:<#CGFloat#>];
```


<span id="73da269b"></span>
### Enable resumable upload

To enable the resumable upload feature, call `setUploadConfig` and set `BDFileUploadDiskResumeOption` after initializing the upload object but before starting the upload process. After enabling resumable upload, the Upload SDK can automatically resume the upload from the interruption point when users upload the same file in your application, thereby saving upload time. See the following example code:

```objectivec
- (void)initVideoUploader {
    ......
    [videoUploadClient setUploadConfig:@{ 
        // 1: Enable resumable upload
        // 0: Disable resumable upload
        BDFileUploadDiskResumeOption: @(1),
    }];
    
    ......
}
```


<span id="b1554e86"></span>
### Enable asynchronous meta info extraction

If your business scenario does not require synchronous meta info extraction, you can enable asynchronous meta info extraction to improve upload speed. Call `setGetMetaMode` and set `mode` to `BDVideoUploadGetMetaModeAsync`.

See the following example code:

```objectivec
- (void)setGetMetaMode:(BDVideoUploadGetMetaMode)mode;
```


<span id="e0dcf66a"></span>
### Customize upload configuration

Call `setUploadConfig` before starting the upload process to customize the upload configuration. The prototype of the `setUploadConfig` method is as follows:

```objectivec
- (void)setUploadConfig:(NSDictionary*)config;
```


The following table lists the options and value types for the `config` dictionary.


|**Option** |**Type** |**Description** |
|---|---|---|
|BDFileUploadSliceSize |NSNumber(NSInteger) |Sets the segment size in bytes. The default value is 512 KB. When uploading large files, the Upload SDK segments them to mitigate the impact of network fluctuations and enhance upload speed. |
|BDFileUploadSocketNum |NSNumber(NSInteger) |Sets the number of concurrent connections when uploading file segments. The default value is 1. |
|BDFileUploadTcpOpenTimeOutMilliSec |NSNumber(NSInteger) |Sets the TCP connection timeout in milliseconds. The default value is 5000. |
|BDFileUploadMaxFailTimes |NSNumber(NSInteger) |Sets the maximum number of retries for a failed upload. |
|BDFileUploadRWTimeout |NSNumber(NSInteger) |Sets the timeout for transferring a single segment in seconds. The default value is 40. |
|BDFileUploadSliceRetryCount |NSNumber(NSInteger) |Sets the number of retries allowed for uploading a single segment. |
|BDFileUploadFileRetryCount |NSNumber(NSInteger) |Sets the number of retries allowed for uploading a file. |
|BDFileUploadTranTimeOutUnit |NSNumber(NSInteger) |Sets the timeout for system socket read and write operations in seconds. The default value is 70. |
|BDFileUploadAliveMaxFailTime |NSNumber(NSInteger) |Sets the timeout for reusing connections in seconds. The default value is 10. |
|BDFileUploadHttpsEnable |NSNumber(BDUploadHttpsOpen) |Sets whether to enable HTTPS. |


Taking `BDFileUploadSliceSize` as an example, the following code sets the segment size as 512 KB:

```objectivec
[self.videoUploadClient setUploadConfig:@{
    // Sets the segment size as 512 KB
    BDFileUploadSliceSize:@(512 * 1024),
}];
```


<span id="5d8fe214"></span>
### Set the callback parameters

If you want to relay information as\-is from the client to the server, you can use the `setRequestParameter` method. The parameter value will be sent back to your server through the `CallbackArgs` parameter in the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) callback. See the following example code:

```objectivec
[self.uploader setRequestParameter:@[BDFileUploadCustomedParameter: ""]]
```


<span id="6b9e27b2"></span>
### Set the workflow ID

Call the `setTemplateId` method to set the workflow ID, triggering the media processing task. You can obtain the workflow ID from the **Workflows** page within the specified space on the BytePlus VOD console. For more details, refer to [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow). Example code:

```objectivec
- (void)setTemplateId:(NSString *)templateId;
```


<span id="643279a0"></span>
## Reference

<span id="142c8a2f"></span>
### BDVideoUploadInfo


|**Parameter** |**Description** |
|---|---|
|vid |The video ID generated by BytePlus VOD. |
|mid |The material ID generated by BytePlus VOD. |
|md5 |The MD5 of the file |
|oid |TOS storage key |
|videoMetaInfo |The media information, including bitrate, format, length, resolution. See the `SourceInfo` parameter in [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo) for details. Example:<br><br>```JSON```<br>```{"Bitrate":463419,"Duration":39.726999999999997,"FileType":"video","Format":"MP4","Height":360,"Md5":"53f62abe3c29d0654b3405af7***7060","Size":2301285,"StoreUri":"tos-vod-cn-v-309be6ba73***b04/cd404e7bef654554b638422***7c0c40","Width":640}```<br> |
|encryptionInfo |Not in use |
|coverURI |The URI of the cover image |
|callbackArgs |The data transmitted from the server. |

---
title: "iOS Upload SDK: Uploading materials"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-materials_1"
---

This article introduces how to use the iOS Upload SDK to upload materials to BytePlus VOD.

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
    // Initialize TTSDK
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

Create an uploader instance with the `BDMaterialUploaderClient` class, as follows:

```objectivec
#import <TTSDK/BDFileUploaderHeader.h>

- (void)initMaterialUploader {
    // 1. When initializing the uploader object, specify the path of the file to be uploaded
    // NSString *filePath = @"path/to/upload/file";
    BDMaterialUploaderClient *materialUploadClient = [[BDMaterialUploaderClient alloc] initWithFilePath:<#filepath#>];
    
    // 2. Get the authentication parameters from your app server and pass them to the SDK
    //NSDictionary *authParameter = @{
    //    BDFileUploadAccessKey: accessKeyId,
    //    BDFileUploadSecretKey: secretKeyId,
    //    BDFileUploadSessionToken: sessionToken,
    //    Specify the space to which the file will be uploaded
    //    BDFileUploadSpace: uploadSpace,
    //    BDFileUploadServiceID: serviceId
    //};
    [materialUploadClient setAuthorizationParameter:<#authparameter#>];
    
    // 3. Customize upload configurations
    [materialUploadClient setUploadConfig:@{
        // Set the slice size
        BDFileUploadSliceSize:@(512 * 1024),
    }];
    
    // 4. Set the material information
    [materialUploadClient setRequestParameter:@{
        // Set the file type as media, image, or object
        BDFileUploadFileTypeStr: <#filetype#>,
    }];
    // Set the file category as video, audio, image, dynamic_img, subtitle, or font
    [materialUploadClient setCategory:<#category#>];
    
    // Set the file title
    [materialUploadClient setTitle:<#title#>];
    // Set the file tag
    [materialUploadClient setTags:<#tags#>]; // e.g. @"testMateTag,testMateTagOne"
    // Set the file description
    [materialUploadClient setDescription:<#description#>];
    // Set the file format
    [materialUploadClient setFormat:<#format#>]; // e.g. @"mp4"
    
    // 5. Set the BDVideoUploadClientDelegate
    //  @see {BDVideoUploadClientDelegate.h}
    materialUploadClient.delegate = self;
    
    // 6. Set the uploader client as a global variable
    self.materialUploadClient = materialUploadClient;
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
|FileTitle |The file name. If not set, the SDK will automatically generate a 32\-bit string as the file name. |
|FileExtension |The file suffix must start with `.`, such as `".mp4"`. |


You can either specify the full path or just specify the file prefix and suffix.


* Call `setFileName` to set the full path. Note that the full path must contain a suffix, such as `.mp4` or `.mp3`. Otherwise an error occurs.

   ```objectivec
   // FileName = FilePrefix + FileTitle + FileExtension
   [self.materialUploadClient setFileName:<#filename#>];
   // [self.materialUploadClient setFileName: @"path/to/foo/bar/test.mp4"];
   ```
   

* Call `setFilePrefix` and `setFileExtension` to set the prefix and suffix:

   ```objectivec
   // The file prefix must end with /
   [self.materialUploadClient setFilePrefix:<#fileprefix#>];
   // e.g.: [self.materialUploadClient setFilePrefix:@"path/to/foo/bar/"];
   // The file suffix must start with .
   [self.materialUploadClient setFileExtension:<#fileextension#>];
   // e.g.:  [self.videoUploadClient setFileExtension:@".mp4"];
   ```
   


<span id="6561c443"></span>
### Control the upload process

The Upload SDK provides the following methods for controlling the upload process:


* Call `start` to start uploading:

   ```objectivec
   [self.materialUploadClient start];
   ```
   

* Call `stop` to pause uploading:

   ```objectivec
   [self.materialUploadClient stop];
   ```
   

* After the upload is complete, call `close` to terminate the upload.

   ```objectivec
   [self.materialUploadClient close];
   ```
   


<span id="c696a99e"></span>
### Set the callbacks

You can set up callbacks to get the video upload results and upload progress. The code example is as follows:

```objectivec
#pragma mark - BDVideoUploadClientDelegate

/// Callback for video upload completion
/// @param uploadClient Video upload instance
/// @param videoInfo Information about the completed video upload
/// @param error If the upload fails, an error will be returned
- (void)videoUpload:(nonnull BDVideoUploaderClient*)uploadClient didFinish:(nullable BDVideoUploadInfo *)videoInfo error:(nullable NSError *)error {
    if (!error) {
       // Video uploaded successfully
    } else {
       // Video upload failed
       // You can determine the specific reason for the upload failure based on the detailed information in [BDVideoUploadInfo](https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploading-audios-and-videos_1#bdvideouploadinfo).
       NSLog  
    }
    // Release the upload object
    [uploadClient close];
}
 
/// Callback for video upload progress
/// @param uploadClient Video upload object
/// @param progress The video upload progress
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
        // If there is a gateway error code, the gateway error code is included in NSError.userInfo, which you can parse as needed
        if ([error.userInfo isKindOfClass:NSDictionary.class]) {
            NSLog(@"error message is: %@", error.userInfo[@"message"]);
        }
    }
    // Release the upload object
    [uploadClient close];
}
```


<span id="a5cfd37a"></span>
## Advanced features

<span id="f91af92d"></span>
### Custom configuration

The Uploader SDK supports some custom configurations. You can configure them as needed by calling the `setUploadConfig` method before starting the upload.

```objectivec
- (void)setUploadConfig:(NSDictionary*)config;
```


The fields and value types in the config dictionary are explained in the table below.


|Field name |Type |Description |
|---|---|---|
|BDFileUploadSliceSize |NSNumber(NSInteger) |Set the size of each slice for uploading, in bytes. Default value is 512 \* 1024 |
|BDFileUploadSocketNum |NSNumber(NSInteger) |Set the number of threads for parallel uploading. Default value is 1 |
|BDFileUploadTcpOpenTimeOutMilliSec |NSNumber(NSInteger) |Set the TCP connection timeout in milliseconds. Default value is 5000 |
|BDFileUploadMaxFailTimes |NSNumber(NSInteger) |Set the total connection timeout, in seconds. Default is 70 |
|BDFileUploadRWTimeout |NSNumber(NSInteger) |Set the timeout for transferring a single slice, in seconds. Default is 40 |
|BDFileUploadSliceRetryCount |NSNumber(NSInteger) |Set the number of retry attempts for a single slice. Default value is 2 |
|BDFileUploadFileRetryCount |NSNumber(NSInteger) |Set the number of retry attempts at the file level. Default value is 3 |
|BDFileUploadTranTimeOutUnit |NSNumber(NSInteger) |Set the system socket read/write timeout, in seconds. Default is 10 |
|BDFileUploadAliveMaxFailTime |NSNumber(NSInteger) |Set the timeout for reusing connections, in seconds, to prevent a decrease in upload speed caused by deteriorating connection quality. Default is 6 |
|BDFileUploadHttpsEnable |NSNumber(BDUploadHttpsOpen) |Enable HTTPS, set to 1 to fully enable. Can be progressively enabled based on the upload stage. |


Below is an example of the implementation code:

```objectivec
[self.materialUploadClient setUploadConfig:@{
    // Specify the file slice size, 512 KB
    BDFileUploadSliceSize:@(512 * 1024),
}];
```

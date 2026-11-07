---
title: "iOS Player SDK: Downloading videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-downloading-videos-ios"
---

To allow your users to watch videos offline, you can use the download function of the iOS Player SDK. This guide provides step\-by\-step instructions on how to initialize the feature, create and manage download tasks for different video assets, and handle playback of downloaded content.

## Introduction

The iOS Player SDK supports downloading both DirectUrl and Vid video assets. It also allows users to start, pause, resume, and delete download tasks.

## Prerequisites

Before using the download function, read [SDK management overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management-overview) and [Step 5: Initialize the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#9707a7fa) and ensure the SDK is initialized.

> **说明**

> To download HLS videos, you must integrate iOS Player SDK version 1.36.300.9 or later.

## Initializing the download function

Before you can use the download function, there are some essential settings you must configure during the initialization of the Player SDK, such as whether to enable HLS video download and the download path.

You can also set the maximum concurrency and minimum free disk space.

> **注意**

> Note that the timing of code initialization has a direct impact on whether the download function works properly:

* > If you need to download HLS videos, you must enable the `HLSProxyModule` before initializing the Player SDK. This method must be called **before** the `[TTSDKManager startWithConfiguration:]` method.

* > Set the download file storage path **before** calling the `[TTSDKManager startWithConfiguration:]` method.

* > Other download configurations are set **after** calling the `[TTSDKManager startWithConfiguration:]` method.

Sample code:

```objectivec
- (void)initTTSDK {
    // Enable HLS download functionality. Optional: If your business does not require downloading HLS videos, you can skip this step.    [TTVideoEngine.ls_localServerConfigure setOptionForKey:@(VEKKeyHLSProxyProtocolEnable_BOOL) value:@YES];
    // Required: Set the storage path for downloaded files.    [TTVideoEngine ls_localServerConfigure].downloadDirectory = @"xxxxx";
    
    // Initialize the Video-on-Demand (VOD) SDK.    [TTSDKManager startWithConfiguration:configuration];
    
    // Optional: Set the maximum number of concurrent downloads. The default value is 1.    [TTVideoEngineDownloader shareLoader].maxDownloadOperationCount = 3;
    
    // The current limit is 1 GB. If the available disk space falls below this value, the SDK returns a TTVideoEngineErrorNotEnoughDiskSpace error    [TTVideoEngineDownloader shareLoader].limitFreeDiskSize = 1024 * 1024 * 1024;
    
    // The iOS Video-on-Demand (VOD) SDK defaults to supporting caching for up to 50 videos. If your business requires caching more than this limit, you need to make the following configurations.    [TTVideoEngine setGlobalForKey:VEGSKeyPlayerVideoModelMaxCache_NSInteger value:@(500)];
}
```

## Using the download function

### Creating a download task

The Player SDK supports the playback of DirectUrl video assets and Vid video assets. To this end, the Player SDK also provides the ability to download different data assets. Before creating a new download task, we recommend that you call the `getAllTasksWithCompletionHandler` method to fetch an existing download task. The Player SDK automatically saves unfinished download tasks and automatically retrieves previously interrupted tasks when the app restarts.

You can create download tasks in the `getAllTasksWithCompletionHandler` block to ensure a specific call sequence.

> **说明**

* > For information on the video asset parameters, see [Step 8: Set the playback source](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk#a09b013b).

* > `getAllTasksWithCompletionHandler` must be called on the main thread.

#### Creating a DirectUrl video asset download task

```objectivec
[[TTVideoEngineDownloader shareLoader] getAllTasksWithCompletionHandler:^(NSArray<__kindof TTVideoEngineDownloadTask *> * _Nonnull tasks) {
    TTVideoEngineDownloadURLTask *urlTask = [[TTVideoEngineDownloader shareLoader] urlTask:@[urlString] key:key videoId:nil];
    [urlTask resume];
  }];
```

#### Creating a Vid video asset download task

```objectivec
[[TTVideoEngineDownloader shareLoader] getAllTasksWithCompletionHandler:^(NSArray<__kindof TTVideoEngineDownloadTask *> * _Nonnull tasks) {
    TTVideoEngineDownloadVidTask *vidTask = [[TTVideoEngineDownloader shareLoader] vidTask:videoID playAuthToken:token resolution:TTVideoEngineResolutionTypeSD];
    [vidTask resume];
  }];
```

### Controlling download tasks

Use the following methods to control individual download tasks:

```objectivec
// Start/Resume a single download task.
// Supports resume from breakpoint. [task resume];
// Pauses a single download task. The download can be resumed later.
// This method must be called on the main thread.[task suspend];
// Delete a single download task.
// After a download task is deleted, the task will be stopped, and TTVideoEngineDownloader will no longer manage this task.
// This interface is an asynchronous operation. You need to check if the task has been deleted in the callback of getAllTasksWithCompletionHandler.[task invalidateAndCancel];
```

Use the following methods to control all download tasks:

```objectivec
// Pause all download tasks.
// This method must be called after getAllTasksWithCompletionHandler.- (void)suspendAllTasks;
// Start/Resume all download tasks.
// This method must be invoked after getAllTasksWithCompletionHandler. - (void)resumeAllTasks;
// Delete all download tasks.
// This method must be called after obtaining all tasks via getAllTasksWithCompletionHandler.- (void)removeAllTasks;
```

> **注意**

> Once the download task has been deleted, the corresponding video file is also deleted.

### Setting up monitoring

To obtain information about the completion, progress, and status of the download task, you need to implement the methods in `TTVideoEngineDownloaderDelegate`. Sample code:

```objectivec
// Set callback receiver. [TTVideoEngineDownloader shareLoader].delegate = self;
```

```objectivec
/**
 * Callback for download task completion.
 * @param downloadTask Current download task.
  * @param error. If error is nil, the download was successful; otherwise, the download failed.
 */- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader
         downloadTask:(TTVideoEngineDownloadTask *)downloadTask
     didCompleteWithError:(nullable NSError *)error;
/**
 * Callback for downloading task progress update.
 * @param downloadTask Current download task.
 *                 - downloadTask.countOfBytesReceived Total downloaded data for the current download task (not applicable for HLS, see notes below).
 *                 - downloadTask.countOfBytesExpectedToReceive Total data size that needs to be downloaded for the current download task (not applicable for HLS, see notes below).
 *                 - downloadTask.progress Current download task progress (0.0 to 1.0).
 * @param  bytesWritten The amount of newly downloaded data in this callback, measured in bytes.
 * @param  timeMs current time.
 */- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader
         downloadTask:(TTVideoEngineDownloadTask *)downloadTask
          writeData:(int64_t)bytesWritten
         timeInterval:(double)timeMS;
/**
 * Callback for the start/resume of a download task.
 * @param downloadTask Current download task. 
 * @param  fileOffset Amount of data already downloaded.
 * @param  expectedTotalBytes Total data size to be downloaded for this task.
 */- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader
         downloadTask:(TTVideoEngineDownloadTask *)downloadTask
      didResumeAtOffset:(int64_t)fileOffset
      expectedTotalBytes:(int64_t)expectedTotalBytes;
/**
 * Callback for changes in the download task status.
 * @param downloadTask Current download task.
 * @param  downloadState Current download task status:
 *                     - TTVideoEngineDownloadStateInit(0)：Initialization.
 *                     - TTVideoEngineDownloadStateWaiting(1): Waiting.
 *                     - TTVideoEngineDownloadStateRunning(2): Running.
 *                     - TTVideoEngineDownloadStateSuspended(3): Suspended.
 *                     - TTVideoEngineDownloadStateCanceling(4): Canceling.
 *                     - TTVideoEngineDownloadStateCompleted(5): Completed.
 */- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader
         downloadTask:(TTVideoEngineDownloadTask *)downloadTask
         stateChanged:(TTVideoEngineDownloadState)downloadState;
```

> **注意**

> When downloading HLS (M3U8) videos, the SDK cannot determine the total file size. Consequently, the `countOfBytesReceived` and `countOfBytesExpectedToReceive` values in the callback are inaccurate. Therefore, for HLS (M3U8) you can only fetch the progress of the download using `- [TTVideoEngineDownloadTask progress]`.

### Playing videos

The SDK automatically links the download cache with the playback engine.

The SDK prioritizes the playback of downloaded videos, even if they have not been fully downloaded, so you do not need to configure additional settings during playback.

#### Playing DirectUrl video assets

Refer to the following sample code for the playback of DirectUrl video assets:

```objectivec
// Before playing downloaded HLS videos, the following must be set: option[self.videoEngine setOptionForKey:VEKKeyIsAllowAllExtensions value:@1];
// Note: The cacheKey must be the same as the one used during the download process.TTVideoEngineUrlSource *urlSource = [[TTVideoEngineUrlSource alloc] initWithUrl:videoUrl cacheKey:cacheKey];
[self.videoEngine setVideoEngineVideoSource:urlSource];
[self.videoEngine play];
```

#### Playing Vid video assets

Refer to the following sample code for the playback of Vid video assets:

```objectivec
// Before playing downloaded videos offline, the following options must be set: [self.videoEngine setOptionForKey:VEKKeyModelCacheVideoInfoEnable_BOOL value:@(YES)];
[self.videoEngine setOptionForKey:VEKKeyPlayerVideoModelPriority_ENUM value:@(TTVideoEngineVideoModelUseLocal)];
// Before playing downloaded HLS videos, the following options must be set:[self.videoEngine setOptionForKey:VEKKeyIsAllowAllExtensions value:@1];
// Note: The resolution must match the one used during the download.TTVideoEngineVidSource *vidSource = [[TTVideoEngineVidSource alloc] initWithVid:vid playAuthToken:playAuthToken resolution:resolution];
[self.videoEngine setVideoEngineVideoSource:vidSource];
[self.videoEngine play];
```

## Downloading external subtitles

The iOS Player SDK can download external subtitles together with the video, for both DirectUrl and Vid video assets. The SDK downloads the video first and then downloads one selected subtitle, so that the subtitle can be loaded during offline playback.

> **Note**

> Subtitle download is supported in BytePlus iOS Player SDK 1.51.300.2 and later. Integrate version 1.51.300.2 or a later version.

### Prerequisites

* Subtitle download requires only a valid SDK authorization and a supported SDK version. Both the standard and premium editions can download subtitle files. Loading and displaying external subtitles during playback is also supported in the standard edition. For the integration requirements, see [iOS Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-ios).

* Complete [Initializing the download function](https://docs.byteplus.com/en/docs/25/36394#67a772a9) in this article, and create download tasks in the `getAllTasksWithCompletionHandler` block.

* DirectUrl mode: your app server must provide the video URL and the subtitle information.

* Vid mode: the subtitles are bound to the Vid, and your app server must provide the video playback auth token and the subtitle auth token separately. For how to issue the subtitle auth token, see [iOS Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-ios).

### Url mode

Pass the subtitle information and the ID of the subtitle to download through `urlTask:key:videoId:subtitleInfoModel:subtitleId:`:

```objectivec
[[TTVideoEngineDownloader shareLoader] getAllTasksWithCompletionHandler:^(NSArray<__kindof TTVideoEngineDownloadTask *> * _Nonnull tasks) {
    TTVideoEngineDownloadURLTask *task = [[TTVideoEngineDownloader shareLoader] urlTask:@[urlString] key:key
                                                                                videoId:videoId
                                                                      subtitleInfoModel:subtitleInfoModel
                                                                             subtitleId:subtitleId // Returns the subtitle ID to download
                                                                             ];

    // Optional: a subtitle failure does not block the overall download task. The default value is NO.
    // YES: ignore the subtitle download failure, and the download task status is success; NO: the subtitle download fails, and the download task status is failure.
    task.ignoreSubtitleDownloadFailure = YES;

    // Start the download.
    [task resume];
}];
```

### Vid mode

Pass the subtitle auth token through `vidTask:playAuthToken:resolution:subtitleAuthToken:downloadSubtitleModelBlock:`, and return the subtitle to download in the block:

```objectivec
[[TTVideoEngineDownloader shareLoader] getAllTasksWithCompletionHandler:^(NSArray<__kindof TTVideoEngineDownloadTask *> * _Nonnull tasks) {
    TTVideoEngineDownloadVidTask *task = [[TTVideoEngineDownloader shareLoader] vidTask:videoID
                                                                          playAuthToken:token
                                                                             resolution:resolution
                                                                      subtitleAuthToken:subtitleAuthToken
                                                             downloadSubtitleModelBlock:^id<TTVideoEngineSubProtocol>(NSArray<id<TTVideoEngineSubProtocol>> *subModels) {
       // Return the subtitle to download. If nil is returned, the SDK selects the first subtitle by default.
       return subModels.firstObject;
   }];

    // Optional: a subtitle failure does not block the overall download task. The default value is NO.
    // YES: ignore the subtitle download failure, and the download task status is success; NO: the subtitle download fails, and the download task status is failure.
    task.ignoreSubtitleDownloadFailure = YES;

    // Start the download.
    [task resume];
}];
```

`ignoreSubtitleDownloadFailure` is `NO` by default. If you set it to `YES`, a subtitle download failure does not affect the result of the overall download task.

### Playing subtitles offline

Configure the video playback source as described in [Playing videos](https://docs.byteplus.com/en/docs/25/36394#83968c7d), and keep parameters such as `cacheKey` and `resolution` consistent with the settings used for downloading.

Configure the subtitle feature switch and subtitle source as described in [iOS Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-ios). The SDK returns the subtitle text, and your app displays it with its own UI. After the download task or subtitle cache is deleted, the subtitle must be downloaded again.

## Error codes

The following error codes may be returned during the download task completion callback:

|Enum |Error code |Description |
|---|---|---|
|TTVideoEngineErrorNetworkNotAvailable |\-9960 |The network is unavailable. |
|TTVideoEngineErrorSaveTaskItem |\-9949 |Failed to save the download task due to a database error. We recommend that you delete the download. |
|TTVideoEngineErrorWriteFile |\-9948 |Failed to write file. Check your write permissions for the download directory. If you have the relevant permissions, we recommend that you delete the download item and start the download again. |
|TTVideoEngineErrorNotEnoughDiskSpace |\-9947 |Insufficient disk space. |
|TTVideoEngineErrorURLUnavailable |\-9945 |The download address is not available. Check the URL of the download task. We recommend that you change the URL and try again. |
|TTVideoEngineErrorServiceInaccessible |\-9944 |The URL request returned an error (such as 500) and the asset could not be downloaded. We recommend that you change the URL or prompt that the video cannot be downloaded (the service is not available). |
|TTVideoEngineErrorExistedTask |\-9943 |This download task already exists. |

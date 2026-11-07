---
title: "Android Player SDK: Downloading videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-downloading-videos"
---

To enable offline video playback in your application, you can use the download function of the Android Player SDK. This guide provides comprehensive instructions on how to initialize the download feature, create and manage tasks for both DirectUrl and Vid video assets, monitor download progress, and play the cached content.

## Overview

The Android Player SDK provides a download function that allows users to cache videos for offline playback. With this function, you can download both DirectUrl and Vid video assets and manage the download tasks (start, pause, resume, and delete).

> **说明**

> To download HLS videos, you must integrate Android Player SDK version 1.36.300.9 or later.

## Initializing the download feature

Before using the download function, you must configure essential settings during SDK initialization, such as enabling HLS downloads and setting the download path.

You can also set the maximum concurrency and minimum free disk space.

> **注意**

> Note that the timing of the initialization code is critical for the download function to work correctly:

* > If you need to download HLS videos, you must enable the HLS download function before initializing the Player SDK.

* > Call other download configuration methods after initializing the Player SDK.

Sample code:

```Java
// (Optional) Customize the download file storage path. The default path is "/data/user/0/packname/cache/video_cache/mdlDownload".
// If you need to customize the download file storage path, you must call this function before initializing the Player SDK.
TTVideoEngine.setStringValue(DATALOADER_KEY_STRING_DOWNLOAD_DIR, "mnt/sdcard/testdownload");

// Enable HLS download functionality. This is optional, and can be skipped if your business does not require downloading HLS videos.
TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ENABLE_HLS,1); // Enable HLS
TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_ENABLE_HLS_PROXY,1); // Enable HLS proxy

// Initialization of the player SDK. For details, please refer to "Quick Start".
Env.init(...);

// When downloading Vid videos, there is a limit on the number of downloads. You can adjust this limit through the following two settings:
// Method 1: Remove the download quantity limit and store in the database (db) until disk space is insufficient.
VideoModelDBManager.setEnableSizeLimit(false);
// Method 2: Set a custom download quantity limit based on business requirements.
VideoModelDBManager.setCacheSize(Integer.MAX_VALUE);

//(Optional) Set the maximum number of concurrent downloads, with a default value of 1.
Downloader.getInstance().setMaxDownloadOperationCount(1);

//(Optional) Set the limit for the size of available disk space (in bytes). The default value is 1GB. If the remaining disk space is less than 1GB, an ERROR_CODE_DOWNLOAD_DISK_FULL error will be returned.
Downloader.getInstance().setLimitFreeDiskSize(1024 * 1024 * 1024);
```

## Retrieve existing download tasks

After initialization, call the `loadAllTasks` method to retrieve existing download tasks, including completed and incomplete ones. Once execution is completed, the SDK will trigger the `downloaderDidLoadAllTask` callback.

> **说明**

* > New tasks can only be created and added after the `downloaderDidLoadAllTask` callback is triggered.

```Java
/ Load existing download tasks, including completed and incomplete ones.
// Upon completion, the downloaderDidLoadAllTask callback will be triggered.
// This interface can be called after initialization.
// It can be used for persistence: When the app is exited and then reopened, by calling this interface, you can retrieve the list of both completed and incomplete download tasks.
Downloader.getInstance().loadAllTasks(this.getApplicationContext());
```

## Creating a download task

The Player SDK supports playing video sources from both DirectUrl and Vid. It also provides download capabilities for these data sources.

> **说明**

> For information on the video asset parameters, see [Step 6: Set the playback source](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk#9397be37).

### Creating a DirectUrl video download task

```Java
// video asset
String[] urls = { httpUrl };
// The cache key cannot be empty and must be unique for each video source. For example, you can use the MD5 hash of the HTTP URL.
String cachekey = MD5(httpUrl); 
String vid = "videoID"; 
DownloadTask downloadTask = Downloader.getInstance().urlTask(urls, cachekey, vid);
```

### Creating a Vid video download task

```Java
// Video ID
String videoId = "your video id";
// Playback authorization token
String playAuthToken = "your video id's play auth token";
// Resolution
Resolution resolution = Resolution.High;

DownloadTask downloadTask = Downloader.getInstance().vidTask(videoId, resolution, playAuthToken);
```

## Controlling download tasks

Method for controlling individual download tasks:

```Java
// Start/resume a single download task.
// After execution is completed, the SDK will trigger the downloaderDidResume callback.
// Supports resuming downloads from breakpoints.
downloadTask.resume(); 

// Pause a single download task.
downloadTask.suspend();

// Delete a single download task.
// The deletion process is asynchronous. After the deletion is completed, the SDK will trigger the downloaderDidComplete callback. The callback parameter error will not be empty, and error.code will be -9995. 
downloadTask.invalidateAndCancel();
```

Method for controlling all download tasks:

```Java
// Start/resume all download tasks
Downloader.getInstance().resumeAllTasks();

// Pause all download tasks
Downloader.getInstance().suspendAllTasks();

// Delete all download tasks
Downloader.getInstance().invalidateAndCancelAllTasks();
```

> **注意**

> Once the download task has been deleted, the corresponding video file is also deleted.

## Monitoring download status and progress

To enable your application to react to changes during the download process in real\-time—for example, to display a progress bar in the UI, update a task's status, or handle download results—you need to implement the `IDownloaderListener` interface. The SDK will automatically invoke your implemented callback methods whenever a task's progress is updated, its state changes, or when it ultimately completes or fails.

```Java
Downloader.getInstance().setListener(new IDownloaderListener() {
    /**
     * Callback for download task completion.
     *
     * @param task The current download task.
     * @param error An error object. If `error` is null, the download was successful; otherwise, it failed.
     */
    @Override
    public void downloaderDidComplete(Downloader downloader, DownloadTask task, @Nullable Error error) {
        // Handle the download completion or failure logic here.
    }

    /**
     * @deprecated This callback is deprecated. Please use downloaderOnProgress() instead.
     *             For HLS videos, its receivedSize/totalSize parameters represented the count of TS segments.
     */
    @Deprecated
    @Override
    public void downloaderProgress(Downloader downloader, DownloadTask task, long receivedSize, long totalSize) {
    
    }

    /**
     * (Added in v1.48.2) Callback for download task progress.
     *
     * @param task The current download task.
     * @param receivedSize The size of the downloaded file in bytes. For HLS, this value now correctly represents the downloaded byte size.
     * @param totalSize The total size of the file in bytes. For HLS, this value will be -1 during the download process as the total size is unknown until completion.
     */
    @Override
    public void downloaderOnProgress(Downloader downloader, DownloadTask task, long receivedSize, long totalSize) {
        // It is recommended to call task.getProgress() to get the precise download percentage for all video formats (including HLS).
        float progress = task.getProgress(); // The 'progress' value ranges from 0.0 to 1.0.
        int percent = (int) (progress * 100);
        
        // You can now use the `receivedSize` parameter to display the actual downloaded size (e.g., in MB) for HLS videos to the user.
        // Update your progress bar UI here.
        // Log.d("Downloader", String.format("Task %s progress: %d%%, Downloaded: %.2f MB", 
        //        task.getVid(), percent, receivedSize / 1024.0 / 1024.0));
    }

    /**
     * Called when a download task starts or resumes.
     *
     * @param task The current download task.
     * @param fileOffset The file offset, representing the amount of data already downloaded.
     * @param expectedTotalBytes The total amount of data expected to be downloaded for this task.
     */
    @Override
    public void downloaderDidResume(Downloader downloader, DownloadTask task, long fileOffset, long expectedTotalBytes) {
        // Handle the task start or resume logic here.
    }

    /**
     * Callback for when all existing download tasks have been loaded.
     *
     * @param allTasks A list of all tasks, including completed and incomplete ones.
     */
    @Override
    public void downloaderDidLoadAllTask(Downloader downloader, @Nullable List<DownloadTask> allTasks, @Nullable Error error) {
        // You can get the list of persisted download tasks here.
    }

    /**
     * Callback for download task state changes.
     *
     * @param task The current download task.
     * @param state The current state of the download task:
     *              - DOWNLOAD_TASK_STATE_INIT(0): Initializing.
     *              - DOWNLOAD_TASK_STATE_WAITING(1): Waiting.
     *              - DOWNLOAD_TASK_STATE_RUNNING(2): Running.
     *              - DOWNLOAD_TASK_STATE_SUSPENDED(3): Suspended.
     *              - DOWNLOAD_TASK_STATE_COMPLETED(4): Completed.
     *              - DOWNLOAD_TASK_STATE_FAILED(5): Failed.
     */
    @Override
    public void downloaderTaskStateDidChange(Downloader downloader, DownloadTask task, int state) {
        // You can update the UI based on the task state here.
    }
});
```

## Playing videos

The SDK automatically uses cached content for playback. The SDK automatically prioritizes playing downloaded video content, including partially downloaded files, so no extra playback configuration is needed.

### DirectUrl mode

Refer to the following sample code to play DirectUrl videos:

```Java
// The following option must be set before playing a downloaded HLS video:
ttVideoEngine.setIntOption(PLAYER_OPTION_INT_ALLOW_ALL_EXTENSIONS, 1);

final String vid = "video id"; // The video source must correspond one-to-one with the vid.
final String url = "http://www.example.com/h264.mp4";
// The playback cacheKey must be consistent with the download cacheKey.
final String cacheKey = TTVideoEngine.computeMD5(url);

// 1.Assemble a DirectUrl video source
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(url)
                .setCacheKey(cacheKey)
                .build())
        .build();
       
// 2.Set the playback source
ttVideoEngine.setStrategySource(directUrlSource);
// 3.Play
ttVideoEngine.play()
```

### Vid mode

```Java
// Before playing a downloaded HLS video, the following option must be set:
ttVideoEngine.setIntOption(PLAYER_OPTION_INT_ALLOW_ALL_EXTENSIONS, 1);

// To play downloaded files offline, the following option needs to be set:
ttVideoEngine.setIntOption(PLAYER_OPTION_USE_VIDEOMODEL_CACHE, 1);
ttVideoEngine.setIntOption(PLAYER_OPTION_USE_VIDEOMODEL_CACHE_FORCE, 1); // Set the option to force playback of locally cached videos

final String vid = "your video id"; // appServer distribution
final String playAuthToken = "your video id's play auth token"; // appServer distribution

final int encodeType = TTVideoEngine.CODEC_TYPE_H264;
// final int encodeType = TTVideoEngine.CODEC_TYPE_H265;
// final int encodeType = TTVideoEngine.CODEC_TYPE_H266;

// 1.Assemble a Vid playback source
StrategySource vidSource = new VidPlayAuthTokenSource.Builder()
        .setVid(vid)
        .setPlayAuthToken(playAuthToken)
        // Set the Codec type (h264, h265, h266). If not specified, the default value h264 will be used.
        .setEncodeType(encodeType)
        // The expected playback resolution should be consistent with the resolution set during downloading.
        .setResolution(Resolution.High)
        .build();
// 2.Set the playback source 
ttVideoEngine.setStrategySource(vidSource);
// 3.Play
ttVideoEngine.play()
```

## Downloading external subtitles

The Android Player SDK can download external subtitles together with the video, for both DirectUrl and Vid video assets. The SDK downloads the video first and then downloads one selected subtitle, so that the subtitle can be loaded during offline playback.

> **Note**

> Subtitle download is supported in BytePlus Android Player SDK 1.51.300.2 and later. Integrate version 1.51.300.2 or a later version.

### Prerequisites

* Subtitle download requires only a valid SDK authorization and a supported SDK version. Both the standard and premium editions can download subtitle files. Loading and displaying external subtitles during playback is also supported in the standard edition. For the integration requirements, see [Android Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-android).

* Complete [Initializing the download feature](https://docs.byteplus.com/en/docs/25/36436#c4204ca7) and [Retrieve existing download tasks](https://docs.byteplus.com/en/docs/25/36436#9ab78e54) in this article. If you download HLS videos, also complete the HLS download configuration.

* DirectUrl mode: your app server must provide the video URL and the subtitle information. WebVTT and SRT subtitle files are supported.

* Vid mode: the subtitles are bound to the Vid, and your app server must provide the video playback auth token and the subtitle auth token separately. For how to issue the subtitle auth token, see [Android Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-android).

### Subtitle information

In DirectUrl mode, the subtitle information delivered by your app server uses the following structure. Replace the URL in the example with the subtitle file address that can be downloaded.

```json
{
  "list": [
    {
      "language_id": 1,
      "language": "cmn-Hans-CN",
      "format": "webvtt",
      "url": "https://example.com/subtitles/chinese.vtt",
      "sub_id": 128934090
    }
  ]
}
```

|Field |Type |Description |
|---|---|---|
|list |Array |The subtitle list. It can contain multiple subtitles, and a download task downloads one of them. |
|list[].language_id |Integer |Required. The subtitle language ID. For the values, refer to [Subtitle languages](https://docs.byteplus.com/docs/byteplus-vod/docs-subtitle-language). |
|list[].language |String |Optional. The language identifier. |
|list[].format |String |Required. The subtitle format. Valid values: `webvtt` and `srt`. |
|list[].url |String |Required. The address of the subtitle file that can be downloaded. |
|list[].sub_id |Integer |Required. The subtitle ID, which is used to select the subtitle to download. It is different from the language ID and the position in the list. |
|list[].cache_key |String |Optional. The subtitle cache identifier. If this field is not provided or is an empty string, the SDK generates the value. If you set a custom value, use the same value for downloading and playback. |

### Creating a DirectUrl download task with subtitles

Build the subtitle source with `SubDesInfoModel`, and then call the `urlTask` method with the subtitle parameters to create the task. Run the following code after existing download tasks are loaded successfully. `subtitleInfoJson` is the subtitle information JSON string delivered by your app server. If it is `null` or an empty string, only the video is downloaded.

```Java
String videoUrl = "YOUR_VIDEO_URL";
String videoId = "YOUR_VIDEO_ID";
// The video cache identifier must be the same as the cacheKey used for playback.
String cacheKey = TTVideoEngine.computeMD5(videoUrl);

SubDesInfoModel subtitleModel = null;
if (!TextUtils.isEmpty(subtitleInfoJson)) {
    try {
        subtitleModel = new SubDesInfoModel(new JSONObject(subtitleInfoJson));
    } catch (JSONException e) {
        // The subtitle information is not valid JSON. Notify the user or fetch the data again.
        return;
    }
}

// null: download the first subtitle in the list.
// To download a specific subtitle, pass its sub_id. If it is not found, the first subtitle is still used.
Integer subtitleId = null;

DownloadURLTask task = Downloader.getInstance().urlTask(
        new String[] {videoUrl},
        cacheKey,
        videoId,
        subtitleModel,
        subtitleId);
if (task == null) {
    // The task failed to be created. Check the video URL, cacheKey, and SDK authorization.
    return;
}

// The default value is false, which means a subtitle download failure affects the overall task result.
// Optional: allow the overall task to succeed even if the subtitle fails. To do so, uncomment the following line.
// task.setIgnoreSubtitleDownloadFailure(true);
task.resume();
```

If `subtitleModel` is `null` or the subtitle list is empty, only the video is downloaded. Setting only `subtitleId` does not trigger a subtitle download.

When you use a VideoModel data source, obtain the URL and the video `cacheKey` of the selected video stream first, and then call the same `urlTask` method with the subtitle model. The subtitle is still downloaded by `DownloadURLTask`.

### Creating a Vid download task with subtitles

Pass the video playback auth token and the subtitle auth token to `vidTask`. After the SDK obtains the subtitle list, it downloads one subtitle based on `subtitleId`. Run the following code after existing download tasks are loaded successfully.

```Java
String videoId = "YOUR_VIDEO_ID";
String playAuthToken = "YOUR_PLAY_AUTH_TOKEN";
String subtitleAuthToken = "YOUR_SUBTITLE_AUTH_TOKEN";
Resolution resolution = Resolution.High;

// If the sub_id of the target subtitle is known, pass this ID.
// If it is null or not found, the SDK downloads the first subtitle in the list.
Integer subtitleId = null;

DownloadVidTask task = Downloader.getInstance().vidTask(
        videoId,
        resolution,
        playAuthToken,
        subtitleAuthToken,
        subtitleId);
if (task == null) {
    // The task failed to be created. Check the video parameters and SDK authorization.
    return;
}

// The default value is false. To ignore subtitle download failures, uncomment the following line.
// task.setIgnoreSubtitleDownloadFailure(true);
task.resume();
```

`playAuthToken` is used for video authentication, and `subtitleAuthToken` is used for subtitle authentication. Both are issued by your app server. If `subtitleAuthToken` is `null` or an empty string, only the video is downloaded.

The five\-parameter method downloads H.264 videos by default and disables `baseDashEnable`. To specify the codec, enable DASH, or use HTTPS, use the following overload and keep the settings consistent with the resolution and codec used for playback:

```Java
DownloadVidTask task = Downloader.getInstance().vidTask(
        videoId,
        resolution,
        TTVideoEngine.CODEC_TYPE_H265, // The example uses H.265. Select the codec based on your playback settings.
        false,                         // baseDashEnable. Configure it based on the video source.
        true,                          // httpsEnable.
        playAuthToken,
        subtitleAuthToken,
        subtitleId);
if (task != null) {
    task.resume();
}
```

### Handling download results

`downloaderSubtitleDidComplete` reports the result of the subtitle stage, and `downloaderDidComplete` reports the result of the overall download. Handle them separately. Add the following methods to your existing `IDownloaderListener` implementation:

```Java
@Override
public void downloaderSubtitleDidComplete(
        Downloader downloader, DownloadTask task, Error error) {
    if (error == null) {
        // The selected subtitle was downloaded successfully.
    } else if (error.code == Error.SubNoSubtitle) {
        // No subtitle is available for this video. This is normal, and the overall task still succeeds.
    } else {
        // The subtitle download failed.
        // The real error is returned here even if you have enabled ignoring subtitle download failures.
    }
}

@Override
public void downloaderDidComplete(
        Downloader downloader, DownloadTask task, Error error) {
    if (error == null) {
        // The overall download succeeded.
        // To check whether the subtitle was downloaded, use the result in the subtitle completion callback.
    } else {
        // Handle the task failure or the reason why the task ended based on the error information.
    }
}
```

|Scenario |Subtitle completion callback |Overall completion callback |Next steps |
|---|---|---|---|
|The video and the selected subtitle are both downloaded |error == null |error == null |The video and the subtitle can be played offline. |
|No subtitle is configured, or the DirectUrl subtitle list is empty |The subtitle callback is not triggered |error == null after the video is downloaded |Only the video is downloaded. |
|The VID subtitle API returns no available subtitle |error.code == Error.SubNoSubtitle |error == null |Handle it as no subtitle. |
|The subtitle download fails with the default false |A subtitle error is returned |An error is returned |After handling the error, call `task.resume()` to retry the subtitle download. |
|The subtitle download fails with true |A subtitle error is still returned |error == null |The video is available, but the failed subtitle is not. Calling `resume()` again on the finished task does not download the subtitle. |
|The video download fails |The subtitle stage is not reached, and the subtitle callback is not triggered |A video download error is returned |Handle the video download error. |

Set `setIgnoreSubtitleDownloadFailure` after the task is created and before `resume()`. It only affects the overall task result when the subtitle fails. It does not ignore video download errors.

To distinguish the video and subtitle download stages, listen to `downloaderVideoDidComplete` and `downloaderSubtitleWriteData`. The former is triggered only after the video is downloaded successfully and before the SDK attempts to download the subtitle, and the latter provides the bytes and time interval of the subtitle download. When a non\-empty subtitle token is passed in VID mode, the video completion callback is triggered first even if the video has no subtitle. In DirectUrl mode, the callback is not triggered when the subtitle model is `null` or the list is empty.

After the video progress reaches 100%, the subtitle may still be downloading. The overall result is determined by `downloaderDidComplete`.

### Playing subtitles offline

Configure the video playback source as described in [Playing videos](https://docs.byteplus.com/en/docs/25/36436#801a2999). For DirectUrl, keep the video `cacheKey` consistent. For Vid, keep the resolution and codec settings used for downloading, and enable video information caching.

Configure the subtitle feature switch, subtitle source, and content callback as described in [Android Player SDK: Adding external subtitles](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-android). The SDK returns the subtitle text, and your app displays it with its own UI. Note the following:

* You can use `DownloadURLTask.getSubtitleModel()` or `DownloadVidTask.getSubtitleModel()` to obtain the subtitle list saved by the task, and set it to the player with `setSubDesInfoModel` after setting the video playback source and before calling `play()`. For a VID task, the subtitle list is available only after the subtitle information is obtained successfully. A non\-null model does not mean that the subtitle file was downloaded successfully.

* Before playback, enable `PLAYER_OPTION_ENABLE_OPEN_SUB_THREAD` and `PLAYER_OPTION_SUB_ENABLE_MDL`. To output subtitles, enable `PLAYER_OPTION_ENABLE_OPEN_SUB`. Use `PLAYER_OPTION_SWITCH_SUB_ID` to select the `sub_id` that was actually downloaded.

* If `subtitleId` is `null` or not found during downloading, the first subtitle in the list is downloaded. Select the same subtitle for offline playback. The other subtitles in the list are not downloaded by this task.

* The subtitle `cacheKey` used for downloading and playback must be the same. If the subtitle model contains a non\-empty `cache_key`, both sides use this value first. If the field is missing or empty, the download side generates the value with `MD5(subtitle URL path) + "_sub"`.

* If `cache_key` is not provided, the player's default subtitle cacheKey generation method is used. If you customize the playback\-side algorithm with `setMDLCacheKeyGeneratorForSubModel`, the download side does not automatically use the algorithm, and offline playback may not hit the subtitle cache. For DirectUrl or VideoModel, you can provide a consistent `cache_key` in the subtitle model. This is especially important for Vid models that do not have this field.

* After the download task or subtitle cache is deleted, the subtitle must be downloaded again.

## Error codes

The following error codes may be returned during the download task completion callback:

|Enum |Error code |Description |
|---|---|---|
|UserCancel |\-9995 |When a user calls the `invalidateAndCancel` method to delete a download task, the deletion process is asynchronous. After the deletion is completed, the SDK will trigger the `downloaderDidComplete` callback. The callback parameter `error` will not be empty, and `error.code` will be \-9995. |
|NetworkNotAvailable |\-9960 |The user's current network is not available. |
|SaveTaskItem |\-9949 |Your application should handle this by deleting the download task. |
|SaveTaskWriteFile |\-9948 |A disk write error occurred. It is recommended that the user delete this download task and restart the download. |
|NotEnoughDiskSpace |\-9947 |When the SDK initiates a download task, it checks the available space. If it is less than `LimitFreeDiskSize`, this error will occur. It is recommended that the user clear some space before downloading. |
|MediaLoaderNeedStart |\-9946 |When calling `loadAllTasks`, if the SDK's data module has not been started first, this error will be returned in the `downloaderDidLoadAllTask` callback. |
|URLUnavailable |\-9945 |The URL is not available. It is recommended to try again with a different URL. |
|ServiceInaccessible |\-9944 |The URL request returned an error such as 500, making it impossible to download the resource. It is recommended to change the URL or display a message indicating that the download is not available (service unavailable). |
|ParameterNull |\-9999 |(VID download\-related error) The parameter is empty. |
|InvalidVideoInfoRequest |\-9990 |(VID download\-related error) Authentication failed. The `playAuthToken` needs to be updated. |
|ResultEmpty |\-9997 |The server returned an empty result. |
|HTTPNotOK |\-9994 |A network issue occurred. You can retry the operation. |

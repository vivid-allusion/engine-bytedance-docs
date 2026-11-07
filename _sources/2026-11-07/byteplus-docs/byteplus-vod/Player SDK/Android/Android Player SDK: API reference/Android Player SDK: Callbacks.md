---
title: "Android Player SDK: Callbacks"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-callbacks"
---

<span id="VideoEngineCallback"></span>
# VideoEngineCallback

```java
public interface com.ss.ttvideoengine.VideoEngineCallback
```


This interface provides callbacks for events related to video playback state.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**default void** |[onPlaybackStateChanged](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onplaybackstatechanged) |
|**default void** |[onLoadStateChanged](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onloadstatechanged) |
|**default void** |[onVideoSizeChanged](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onvideosizechanged) |
|**default void** |[onBufferingUpdate](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onbufferingupdate) |
|**default void** |[onPrepare](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onprepare) |
|**default void** |[onPrepared](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onprepared) |
|**default void** |[onRenderStart](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onrenderstart) |
|**default void** |[onReadyForDisplay](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onreadyfordisplay) |
|**default void** |[onCompletion](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-oncompletion) |
|**default void** |[onError](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onerror) |
|**default void** |[onBufferStart](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onbufferstart) |
|**default void** |[onBufferEnd](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onbufferend) |
|**default void** |[onVideoStreamBitrateChanged](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-onvideostreambitratechanged) |
|**default void** |[onCurrentPlaybackTimeUpdate](https://docs.byteplus.com/en/docs/25/7958#VideoEngineCallback-oncurrentplaybacktimeupdate) |


<span id="Function details"></span>
## Function details

<span id="VideoEngineCallback-onplaybackstatechanged"></span>
### onPlaybackStateChanged

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onPlaybackStateChanged(
    TTVideoEngine engine,
    int playbackState)
```


Occurs when the playback state changes.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|playbackState |**int** |The current playback state:<br><br><br>* `PLAYBACK_STATE_STOPPED`: The playback is stopped.<br><br>* `PLAYBACK_STATE_PLAYING`: The playback is in progress.<br><br>* `PLAYBACK_STATE_PAUSED`: The playback is paused.<br><br>* `PLAYBACK_STATE_ERROR`: An error occurred during playback. |


<span id="VideoEngineCallback-onloadstatechanged"></span>
### onLoadStateChanged

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onLoadStateChanged(
    TTVideoEngine engine,
    int loadState)
```


Occurs when the load state changes.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|loadState |**int** |The current load state:<br><br><br>* `LOAD_STATE_PLAYABLE`: The player has finished loading and can start or resume playback.<br><br>* `LOAD_STATE_STALLED`: The player is buffering and loading data.<br><br>* `LOAD_STATE_ERROR`: The player encountered an error while loading data. |


<span id="VideoEngineCallback-onvideosizechanged"></span>
### onVideoSizeChanged

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onVideoSizeChanged(
    TTVideoEngine engine,
    int width,
    int height)
```


Occurs when the video resolution changes.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|width |**int** |The current video width. |
|height |**int** |The current video height. |


<span id="VideoEngineCallback-onbufferingupdate"></span>
### onBufferingUpdate

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onBufferingUpdate(
    TTVideoEngine engine,
    int percent)
```


Occurs when the video buffering progress updates.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|percent |**int** |The buffering progress, ranging from 0 to 100. |


<span id="VideoEngineCallback-onprepare"></span>
### onPrepare

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onPrepare(
    TTVideoEngine engine)
```


Occurs when the player is preparing for playback.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |


<span id="VideoEngineCallback-onprepared"></span>
### onPrepared

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onPrepared(
    TTVideoEngine engine)
```


Occurs when the playback preparation is completed.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |


<span id="VideoEngineCallback-onrenderstart"></span>
### onRenderStart

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onRenderStart(
    TTVideoEngine engine)
```


Occurs when the video rendering starts.

**Parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |


**Note**

When receiving this callback, you can assume that the video frame has been displayed.

<span id="VideoEngineCallback-onreadyfordisplay"></span>
### onReadyForDisplay

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onReadyForDisplay(
    TTVideoEngine engine)
```


Occurs when the first frame of the video is rendered.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |


**Note**

This callback is triggered when the SDK finishes rendering the first frame of the video after calling [prepare](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-prepare).

<span id="VideoEngineCallback-oncompletion"></span>
### onCompletion

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onCompletion(
    TTVideoEngine engine)
```


Occurs when the video playback is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |


<span id="VideoEngineCallback-onerror"></span>
### onError

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onError(
    Error error)
```


Occurs when an error is encountered during video playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|error |**Error** |The error encountered during playback. Refer to the [Player SDK error codes](https://docs.byteplus.com/en/byteplus-vod/docs/upload-sdk-error-codes) for more details. |


<span id="VideoEngineCallback-onbufferstart"></span>
### onBufferStart

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onBufferStart(
    int reason,
    int afterFirstFrame,
    int action)
```


Occurs when buffering starts during video playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|reason |**int** |The reason for buffering:<br><br><br>* `BUFFERING_TYPE_NET`: Network buffering<br><br>* `BUFFERING_TYPE_DECODER`: Decoder buffering |
|afterFirstFrame |**int** |The timing of buffering:<br><br><br>* `BEFORE_FIRST_FRAME`: Buffering before the first frame<br><br>* `AFTER_FIRST_FRAME`: Buffering after the first frame |
|action |**int** |The action that caused buffering:<br><br><br>* `BUFFER_START_ACTION_NONE`: Buffering during normal playback<br><br>* `BUFFER_START_ACTION_SEEK`: Buffering after a seek operation<br><br>* `BUFFER_START_ACTION_CHANG_RESOLUTION`: Buffering after a resolution change |


<span id="VideoEngineCallback-onbufferend"></span>
### onBufferEnd

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onBufferEnd(
    int code)
```


Occurs when buffering ends during video playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|code |**int** |The reason for buffering:<br><br><br>* `BUFFERING_TYPE_NET`: Network buffering<br><br>* `BUFFERING_TYPE_DECODER`: Decoder buffering |


<span id="VideoEngineCallback-onvideostreambitratechanged"></span>
### onVideoStreamBitrateChanged

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onVideoStreamBitrateChanged(
    Resolution resolution,
    int bitrate)
```


Occurs when the video bitrate or resolution changes during video playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolution |**Resolution** |The changed resolution. |
|bitrate |**int** |The changed bitrate. |


**Note**

This callback is only triggered when using the smooth switching feature.

<span id="VideoEngineCallback-oncurrentplaybacktimeupdate"></span>
### onCurrentPlaybackTimeUpdate

```java
default void com.ss.ttvideoengine.VideoEngineCallback.onCurrentPlaybackTimeUpdate(
    TTVideoEngine engine,
    int currentPlaybackTime)
```


Occurs when the playback position of the video is updated.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|currentPlaybackTime |**int** |The current playback position in milliseconds. |


**Note**

You can use this callback to update the progress bar.

Before using this callback, you need to set the trigger interval for this callback using `setIntOption(TTVideoEngine.PLAYER_OPTION_POSITION_UPDATE_INTERVAL, 200)`.

<span id="IDownloaderListener"></span>
# IDownloaderListener

```java
public interface com.ss.ttvideoengine.download.IDownloaderListener
```


This interface provides callbacks related to downloading.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[downloaderDidComplete](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderdidcomplete) |
|**void** |[downloaderWriteData](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderwritedata) |
|**default void** |[downloaderProgress](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderprogress) |
|**void** |[downloaderDidResume](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderdidresume) |
|**void** |[downloaderDidLoadAllTask](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderdidloadalltask) |
|**void** |[downloaderStateChanged](https://docs.byteplus.com/en/docs/25/7958#IDownloaderListener-downloaderstatechanged) |


<span id="Function details"></span>
## Function details

<span id="IDownloaderListener-downloaderdidcomplete"></span>
### downloaderDidComplete

```java
void com.ss.ttvideoengine.download.IDownloaderListener.downloaderDidComplete(
    Downloader downloader,
    DownloadTask task,
    @Nullable Error error)
```


Occurs when a downloading task is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|task |**DownloadTask** |The current downloading task. |
|error | **@Nullable Error** |The error message or reason for completion. `error` is null if there was no error and the task has completed successfully. |


<span id="IDownloaderListener-downloaderwritedata"></span>
### downloaderWriteData

```java
void com.ss.ttvideoengine.download.IDownloaderListener.downloaderWriteData(
    Downloader downloader,
    DownloadTask task,
    long bytesWritten,
    long timeMS)
```


Occurs when the download speed updates.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|task |**DownloadTask** |The current downloading task. |
|bytesWritten |**long** |The number of bytes downloaded within the `timeMS` interval. |
|timeMS |**long** |The time interval. |


**Note**


* You can calculate the download speed for this time interval using `bytesWritten` and `timeMS`.

* The `bytesWritten` value may not be accurate when playing HLS videos.


<span id="IDownloaderListener-downloaderprogress"></span>
### downloaderProgress

```java
default void com.ss.ttvideoengine.download.IDownloaderListener.downloaderProgress(
    Downloader downloader,
    DownloadTask task,
    long receivedSize,
    long totalSize)
```


Occurs when the progress of a downloading task updates.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|task |**DownloadTask** |The current downloading task. |
|receivedSize |**long** |The size of the downloaded task received, in bytes. |
|totalSize |**long** |The total size of the downloading task, in bytes. |


**Note**


* Download progress = receivedSize / totalSize

* The `receivedSize` and `totalSize` in the `downloaderProgress` callback are not the byte size of the file if the value of `getMediaType` in `DownloadTask` is HLS (M3U8). This is because the SDK cannot know the total size of the entire HLS (M3U8) file. You can only calculate the download progress using the above formula.


<span id="IDownloaderListener-downloaderdidresume"></span>
### downloaderDidResume

```java
void com.ss.ttvideoengine.download.IDownloaderListener.downloaderDidResume(
    Downloader downloader,
    DownloadTask task,
    long fileOffset,
    long expectedTotalBytes)
```


Occurs when a downloading task starts or resumes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|task |**DownloadTask** |The current downloading task. |
|fileOffset |**long** |The file offset. |
|expectedTotalBytes |**long** |The expected total number of bytes. |


<span id="IDownloaderListener-downloaderdidloadalltask"></span>
### downloaderDidLoadAllTask

```java
void com.ss.ttvideoengine.download.IDownloaderListener.downloaderDidLoadAllTask(
    Downloader downloader,
    @Nullable List<DownloadTask> allTasks,
    @Nullable Error error)
```


Occurs when all downloading tasks are completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|allTasks | **@Nullable List** |All downloading tasks. |
|error | **@Nullable Error** |The error message or reason. |


<span id="IDownloaderListener-downloaderstatechanged"></span>
### downloaderStateChanged

```java
void com.ss.ttvideoengine.download.IDownloaderListener.downloaderStateChanged(
    Downloader downloader,
    DownloadTask task,
    int state)
```


Occurs when the state of a downloading task changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**Downloader** |The downloading task manager. |
|task |**DownloadTask** |The current downloading task. |
|state |**int** |The current state of the downloading task:<br><br><br>* `DOWNLOAD_TASK_STATE_INIT`: Initialization.<br><br>* `DOWNLOAD_TASK_STATE_WAITING`: Waiting.<br><br>* `DOWNLOAD_TASK_STATE_RUNNING`: Running.<br><br>* `DOWNLOAD_TASK_STATE_SUSPENDED`: Suspended.<br><br>* `DOWNLOAD_TASK_STATE_CANCELING`: Cancelling.<br><br>* `DOWNLOAD_TASK_STATE_COMPLETED`: Completed. |


<span id="MaskInfoListener"></span>
# MaskInfoListener

```java
public interface com.ss.ttvideoengine.MaskInfoListener
```


The interface provides callbacks for masking bullet comment information.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onMaskInfoCallback](https://docs.byteplus.com/en/docs/25/7958#MaskInfoListener-onmaskinfocallback) |


<span id="Function details"></span>
## Function details

<span id="MaskInfoListener-onmaskinfocallback"></span>
### onMaskInfoCallback

```java
void com.ss.ttvideoengine.MaskInfoListener.onMaskInfoCallback(
    int code,
    int pts,
    String info)
```


Occurs when the SDK receives a single piece of masking bullet comment.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|code |**int** |This parameter is not used. |
|pts |**int** |The timestamp of the masking bullet comment, in milliseconds. |
|info |**String** |The content of the masking bullet comment. |


<span id="IPreLoaderItemCallBackListener"></span>
# IPreLoaderItemCallBackListener

```java
public interface com.ss.ttvideoengine.IPreLoaderItemCallBackListener
```


The interface provides callbacks related to preload tasks.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[preloadItemInfo](https://docs.byteplus.com/en/docs/25/7958#IPreLoaderItemCallBackListener-preloaditeminfo) |


<span id="Function details"></span>
## Function details

<span id="IPreLoaderItemCallBackListener-preloaditeminfo"></span>
### preloadItemInfo

```java
void com.ss.ttvideoengine.IPreLoaderItemCallBackListener.preloadItemInfo(
    PreLoaderItemCallBackInfo info)
```


Occurs when the SDK receives information about a preload task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|info |**PreLoaderItemCallBackInfo** |Information about the preload task. See [PreLoaderItemCallBackInfo](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#preloaderitemcallbackinfo) for details. |


<span id="VideoEngineInfoListener"></span>
# VideoEngineInfoListener

```java
public interface com.ss.ttvideoengine.VideoEngineInfoListener
```


The interface provides general callbacks of the player.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onVideoEngineInfos](https://docs.byteplus.com/en/docs/25/7958#VideoEngineInfoListener-onvideoengineinfos) |


<span id="Function details"></span>
## Function details

<span id="VideoEngineInfoListener-onvideoengineinfos"></span>
### onVideoEngineInfos

```java
void com.ss.ttvideoengine.VideoEngineInfoListener.onVideoEngineInfos(
    VideoEngineInfos videoEngineInfos)
```


The general callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngineInfos |**VideoEngineInfos** |Information related to the `videoEngine` class. See [VideoEngineInfos](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-type-definitions?version=v1.0#videoengineinfos) for details. |


**Note**

Pay attention to the following callbacks:

`videoEngineInfos.getKey() == VideoEngineInfos.USING_RENDER_SEEK_COMPLETE`: This callback occurs when rendering is complete following a seek operation.

`videoEngineInfos.getKey() == VideoEngineInfos.USING_MDL_HIT_CACHE_SIZE`: This callback occurs when the preloading task hits the cashed video. If greater than `0`, it indicates the size of the cached video that was hit.

<span id="VideoInfoListener"></span>
# VideoInfoListener

```java
public interface com.ss.ttvideoengine.VideoInfoListener
```


This interface provides callbacks related to video information.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**boolean** |[onFetchedVideoInfo](https://docs.byteplus.com/en/docs/25/7958#VideoInfoListener-onfetchedvideoinfo) |


<span id="Function details"></span>
## Function details

<span id="VideoInfoListener-onfetchedvideoinfo"></span>
### onFetchedVideoInfo

```java
boolean com.ss.ttvideoengine.VideoInfoListener.onFetchedVideoInfo(
    VideoModel model)
```


Occurs when the SDK receives the video model returned by the server.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|model |**VideoModel** |The video model returned by the server after you call `GetPlayInfo`. |


**Returns**

Whether to handle the returned video model yourself. You should return `false` to indicate that you will not handle it.

<span id="SeekCompletionListener"></span>
# SeekCompletionListener

```java
public interface com.ss.ttvideoengine.SeekCompletionListener
```


This interface provides callbacks related to the seek operation.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onCompletion](https://docs.byteplus.com/en/docs/25/7958#SeekCompletionListener-oncompletion) |


<span id="Function details"></span>
## Function details

<span id="SeekCompletionListener-oncompletion"></span>
### onCompletion

```java
void com.ss.ttvideoengine.SeekCompletionListener.onCompletion(
    boolean success)
```


Occurs when a seek operation is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|success |**boolean** |Whether the seek operation was successful. |


<span id="SubInfoSimpleCallBack"></span>
# SubInfoSimpleCallBack

```java
public class com.ss.ttvideoengine.SubInfoSimpleCallBack
```


This interface provides callbacks related to subtitles.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onSubInfoCallback](https://docs.byteplus.com/en/docs/25/7958#SubInfoSimpleCallBack-onsubinfocallback) |
|**void** |[onSubSwitchCompleted](https://docs.byteplus.com/en/docs/25/7958#SubInfoSimpleCallBack-onsubswitchcompleted) |
|**void** |[onSubLoadFinished](https://docs.byteplus.com/en/docs/25/7958#SubInfoSimpleCallBack-onsubloadfinished) |


<span id="Function details"></span>
## Function details

<span id="SubInfoSimpleCallBack-onsubinfocallback"></span>
### onSubInfoCallback

```java
public void com.ss.ttvideoengine.SubInfoSimpleCallBack.onSubInfoCallback(
    int code,
    String info)
```


Occurs when the SDK receives a single piece of subtitle.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|code |**int** |The timestamp corresponding to the subtitle piece, in milliseconds. |
|info |**String** |The content of the subtitle piece. |


<span id="SubInfoSimpleCallBack-onsubswitchcompleted"></span>
### onSubSwitchCompleted

```java
public void com.ss.ttvideoengine.SubInfoSimpleCallBack.onSubSwitchCompleted(
    int success,
    int subId)
```


Occurs when the subtitle language is switched.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|success |**int** |Whether the subtitle language switch is successful:<br><br><br>* `1`: Switch successful.<br><br>* `0`: Switch failed. |
|subId |**int** |The subtitle ID. |


<span id="SubInfoSimpleCallBack-onsubloadfinished"></span>
### onSubLoadFinished

```java
public void com.ss.ttvideoengine.SubInfoSimpleCallBack.onSubLoadFinished(
    int success)
```


Occurs when the subtitle file download is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|success |**int** |Whether the subtitle file is downloaded successfully:<br><br><br>* `1`: Download successful.<br><br>* `0`: Download failed. |


<span id="EngineStrategyListener"></span>
# EngineStrategyListener

```java
public interface com.ss.ttvideoengine.strategy.EngineStrategyListener
```


This interface provides callbacks related to the playback strategy.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**default void** |[onPreRenderEngineCreated](https://docs.byteplus.com/en/docs/25/7958#EngineStrategyListener-onprerenderenginecreated) |


<span id="Function details"></span>
## Function details

<span id="EngineStrategyListener-onprerenderenginecreated"></span>
### onPreRenderEngineCreated

```java
default void com.ss.ttvideoengine.strategy.EngineStrategyListener.onPreRenderEngineCreated(
    TTVideoEngine engine,
    StrategySource source)
```


Occurs when the `engine` object for pre\-rendering is created.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|engine |**TTVideoEngine** |The `TTVideoEngine` object. |
|source |**StrategySource** |The playback source. |


**Note**

When the SDK constructs the `engine` object for pre\-rendering, this callback will be triggered. You can configure the `engine` object after receiving this callback, for example, to enable Texture Render with `engine.setIntOption(PLAYER_OPTION_USE_TEXTURE_RENDER, 1)`.

<span id="SnapshotListener"></span>
# SnapshotListener

```java
public interface com.ss.ttvideoengine.SnapshotListener
```


This interface provides callbacks related to snapshots.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onSnapShot](https://docs.byteplus.com/en/docs/25/7958#SnapshotListener-onsnapshot) |


<span id="Function details"></span>
## Function details

<span id="SnapshotListener-onsnapshot"></span>
### onSnapShot

```java
void com.ss.ttvideoengine.SnapshotListener.onSnapShot(
    Bitmap bitmap,
    int with,
    int height)
```


Occurs when the SDK receives a snapshot.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|bitmap |**Bitmap** |The image data of the snapshot. |
|with |**int** |The width of the current video. |
|height |**int** |The height of the current video. |


<span id="DataLoaderListener2"></span>
# DataLoaderListener2

```java
public interface com.ss.ttvideoengine.DataLoaderListener2
```


This interface provides callbacks related to data loading.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onNotify](https://docs.byteplus.com/en/docs/25/7958#DataLoaderListener2-onnotify) |


<span id="Function details"></span>
## Function details

<span id="DataLoaderListener2-onnotify"></span>
### onNotify

```java
void com.ss.ttvideoengine.DataLoaderListener2.onNotify(
    int what,
    long code,
    long parameter,
    String info)
```


Occurs when data is loaded for playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|what |**int** |The event name. |
|code |**long** |The data code. |
|parameter |**long** |The data parameter. |
|info |**String** |Information about the loading process. |


**Note**

The `DataLoaderListener2` callback is defined to be more flexible, and the meanings of the parameters vary depending on the event.

<span id="SubInfoListener"></span>
# SubInfoListener

```java
public interface com.ss.ttvideoengine.SubInfoListener
```


This interface provides callbacks related to the subtitle source.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[onSubPathInfo](https://docs.byteplus.com/en/docs/25/7958#SubInfoListener-onsubpathinfo) |
|**void** |[onSubInfoCallback](https://docs.byteplus.com/en/docs/25/7958#SubInfoListener-onsubinfocallback) |


<span id="Function details"></span>
## Function details

<span id="SubInfoListener-onsubpathinfo"></span>
### onSubPathInfo

```java
void com.ss.ttvideoengine.SubInfoListener.onSubPathInfo(
    String subPathInfo,
    Error error)
```


Occurs when the SDK receives subtitle information of all languages.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subPathInfo |**String** |All language subtitle information. |
|error |**Error** |Error information for subtitle retrieval. If `error` is not empty, it indicates a failure in retrieving subtitles. |


<span id="SubInfoListener-onsubinfocallback"></span>
### onSubInfoCallback

```java
void com.ss.ttvideoengine.SubInfoListener.onSubInfoCallback(
    int code,
    int pts,
    String info)
```


Occurs when the SDK receives a single piece of subtitle.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|code |**int** |This parameter is not used. |
|pts |**int** |The timestamp corresponding to the subtitle piece, in milliseconds. |
|info |**String** |The content of the subtitle piece. |

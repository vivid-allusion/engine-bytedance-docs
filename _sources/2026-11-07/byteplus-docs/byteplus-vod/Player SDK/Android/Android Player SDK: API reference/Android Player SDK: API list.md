---
title: "Android Player SDK: API list"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-list"
---

<span id="Methods"></span>
# Methods

<span id="Playback"></span>
## Playback


|**Method** |**Description** |
|---|---|
|[setStrategySource](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-setstrategysource) |Sets the playback source. |
|[prepare](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-prepare) |Prepares for playback. |
|[play](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-play) |Starts playback. |
|[pause](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-pause) |Pauses playback. |
|[stop](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-stop) |Stops playback. |
|[seekTo](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-seekto) |Jumps to a specified position for playback. |
|[releaseAsync](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-releaseasync) |Asynchronously releases the player. |
|[setStartTime](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-setstarttime) |Sets the starting playback time. |


<span id="Preloading and pre-rendering strategies"></span>
## Preloading and pre\-rendering strategies


|**Method** |**Description** |
|---|---|
|[enableEngineStrategy](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-enableenginestrategy) |Enables the strategy. The SDK supports preloading and pre\-rendering strategies. |
|[setStrategySources](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-setstrategysources) |Sets the list of playback sources for the current page. |
|[addStrategySources](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-addstrategysources) |Adds playback source data to the current list of playback sources. |
|[setEngineStrategyListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-setenginestrategylistener) |Sets the callback for strategy\-related events. |
|[getPreRenderEngine](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-getprerenderengine) |Gets the `TTVideoEngine` object that has finished pre\-rendering using the `StrategySource`. |
|[getPreRenderEngine](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-getprerenderengine) |Gets the `TTVideoEngine` object that has finished pre\-rendering using the `vid`. |
|[clearAllStrategy](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-clearallstrategy) |Clears all strategies and releases resources. |


<span id="Custom preloading"></span>
## Custom preloading


|**Method** |**Description** |
|---|---|
|[addTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-addtask) |Adds a preloading task for the VID playback source. |
|[addTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-addtask) |Adds a preloading task for the URL playback source. |
|[cancelPreloadTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-cancelpreloadtask) |Cancels the preloading task based on the cache key. |
|[cancelPreloadTaskByVideoId](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-cancelpreloadtaskbyvideoid) |Cancels the preloading task based on the video ID. |
|[cancelAllPreloadTasks](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#TTVideoEngine-cancelallpreloadtasks) |Cancels all preloading tasks. |


<span id="Download"></span>
## Download


|**Method** |**Description** |
|---|---|
|[urlTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#Downloader-urltask) |Creates a downloading task for the URL playback source. |
|[vidTask](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#Downloader-vidtask) |Creates a downloading task for the VID playback source. |
|[suspendAllTasks](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#Downloader-suspendalltasks) |Suspends all downloading tasks. |
|[getState](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#DownloadTask-getstate) |Gets the state of a downloading task. |
|[resume](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#DownloadTask-resume) |Starts or resumes a downloading task. |
|[suspend](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#DownloadTask-suspend) |Suspends a downloading task. |
|[invalidateAndCancel](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#DownloadTask-invalidateandcancel) |Deletes a downloading task. |
|[invalidateAndCancelAllTasks](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-api-details?version=v1.0#Downloader-invalidateandcancelalltasks) |Deletes all downloading tasks. |


<span id="Callbacks"></span>
# Callbacks

<span id="Playback"></span>
## Playback


|**Callback** |**Description** |
|---|---|
|[onPlaybackStateChanged](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onplaybackstatechanged) |Occurs when the playback state changes. |
|[onLoadStateChanged](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onloadstatechanged) |Occurs when the load state changes. |
|[onBufferingUpdate](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onbufferingupdate) |Occurs when the video buffering progress updates. |
|[onPrepare](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onprepare) |Occurs when the playback is being prepared. |
|[onPrepared](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onprepared) |Occurs when the preparation is completed and playback can begin. |
|[onRenderStart](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onrenderstart) |Occurs when rendering starts. |
|[onBufferStart](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onbufferstart) |Occurs when buffering starts. |
|[onBufferEnd](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onbufferend) |Occurs when buffering ends. |
|[onCompletion](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-oncompletion) |Occurs when playback is completed. |
|[onError](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onerror) |Occurs when a playback error occurs. |
|[onCurrentPlaybackTimeUpdate](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-oncurrentplaybacktimeupdate) |Occurs when the current playback position updates. |


<span id="Preloading and Pre-rendering Strategies"></span>
## Preloading and Pre\-rendering Strategies


|**Callback** |**Description** |
|---|---|
|[onReadyForDisplay](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#VideoEngineCallback-onreadyfordisplay) |Occurs when the first frame is pre\-rendered. |


<span id="Download"></span>
## Download


|**Callback** |**Description** |
|---|---|
|[downloaderDidComplete](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderdidcomplete) |Occurs when a downloading task is completed. |
|[downloaderWriteData](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderwritedata) |Occurs when the download speed is updated. |
|[downloaderProgress](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderprogress) |Occurs when the progress of a downloading task updates. |
|[downloaderDidResume](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderdidresume) |Occurs when a downloading task starts or resumes. |
|[downloaderStateChanged](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#IDownloaderListener-downloaderstatechanged) |Occurs when the state of a downloading task changes. |

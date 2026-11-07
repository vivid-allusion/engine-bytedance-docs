---
title: "iOS Player SDK: API list"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-list"
---

<span id="Methods"></span>
# Methods

<span id="Playback"></span>
## Playback


|**Method** |**Description** |
|---|---|
|[initWithOwnPlayer:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-initwithownplayer) |Initializes a player instance. |
|[setVideoEngineVideoSource:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-setvideoenginevideosource) |Sets the playback source. |
|[prepareToPlay](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-preparetoplay) |Prepares for playback. |
|[play](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-play) |Starts playback. |
|[pause](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-pause) |Pauses playback. |
|[stop](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-stop) |Stops playback. |
|[closeAysnc](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-closeaysnc) |Asynchronously closes and destroys the player. |
|[setCurrentPlaybackTime:complete:renderComplete:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-setcurrentplaybacktime-complete-rendercomplete) |Jumps to the specified timestamp to play. |


<span id="Preloading and pre-rendering strategy"></span>
## Preloading and pre\-rendering strategy


|**Method** |**Description** |
|---|---|
|[enableEngineStrategy:scene:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-enableenginestrategy-scene) |Enables the strategy. The SDK supports preloading and pre\-rendering strategies. |
|[setStrategyVideoSources:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-setstrategyvideosources) |Sets the list of playback sources for the current page. |
|[addStrategyVideoSources:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-addstrategyvideosources) |Adds playback sources to the current list of playback sources. |
|[setPreRenderVideoEngineDelegate:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-setprerendervideoenginedelegate) |Sets the delegate for the pre\-rendering strategy. |
|[getPreRenderFinishedPlayerViewWithVideoSource:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-getprerenderfinishedplayerviewwithvideosource) |Gets the player view of the pre\-rendered `TTVideoEngine` with the given playback source. |
|[getPreRenderFinishedVideoEngineWithVideoSource:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-getprerenderfinishedvideoenginewithvideosource) |Gets the pre\-rendered `TTVideoEngine` object with the given playback source. |
|[getVideoEngineStrategyUniqueId](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-getvideoenginestrategyuniqueid) |Gets the unique identifier for the current `TTVideoEngine` object. |


<span id="Custom preloading"></span>
## Custom preloading


|**Method** |**Description** |
|---|---|
|[ls_addTaskWithURLItem:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_addtaskwithurlitem) |Adds a preloading task for the URL playback source. |
|[ls_addTaskWithVidItem:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_addtaskwithviditem) |Adds a preloading task for the VID playback source. |
|[ls_cancelTaskByKey:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_canceltaskbykey) |Cancels the preloading task based on the cache key. |
|[ls_cancelTaskByVideoId:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_canceltaskbyvideoid) |Cancels the preloading task based on the video ID. |
|[ls_cancelAllTasks](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_cancelalltasks) |Cancels all preloading tasks. |
|[ls_cancelAllIdlePreloadTasks](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-ls_cancelallidlepreloadtasks) |Cancels all idle preloading tasks. |


<span id="Downloading"></span>
## Downloading


|**Method** |**Description** |
|---|---|
|[urlTask:key:videoId:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-urltask-key-videoid) |Creates a downloading task for the URL playback source. |
|[vidTask:playAuthToken:resolution:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-vidtask-playauthtoken-resolution) |Creates a downloading task for the VID playback source. |
|[getAllTasksWithCompletionHandler:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-getalltaskswithcompletionhandler) |Gets all downloading tasks. |
|[downloadSize](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-downloadsize) |Gets the total size of all downloading tasks, in bytes. |
|[resumeAllTasks](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-resumealltasks) |Resumes all downloading tasks. |
|[suspendAllTasks](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-suspendalltasks) |Suspends all downloading tasks. |
|[removeAllTasks](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloader-removealltasks) |Removes all downloading tasks. |
|[resume](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloadTask-resume) |Starts or resumes a downloading task. |
|[suspend](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloadTask-suspend) |Suspends a downloading task. |
|[invalidateAndCancel](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngineDownloadTask-invalidateandcancel) |Removes a downloading task. |


<span id="Debug tool"></span>
## Debug tool


|**Method** |**Description** |
|---|---|
|[showDebugTool:inRect:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-showdebugtool-inrect) |Adds a debug tool. |
|[debugToolIsShowing](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-debugtoolisshowing) |Checks if the debug tool is currently being displayed. |
|[refreshCurrentVideoEngine:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-refreshcurrentvideoengine) |Refreshes the `TTVideoEngine` instance associated with the current debug tool. |
|[removeDebugTool](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-api-details?version=v1.0#TTVideoEngine-removedebugtool) |Removes the debug tool. |


<span id="Callbacks"></span>
# Callbacks

<span id="Playback"></span>
## Playback


|**Callback** |**Description** |
|---|---|
|[videoEngine:playbackStateDidChanged:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengine-playbackstatedidchanged) |Occurs when the playback state changes. |
|[videoEngine:loadStateDidChanged:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengine-loadstatedidchanged) |Occurs when the load state changes. |
|[videoEngine:fetchedVideoModel:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengine-fetchedvideomodel) |Occurs when the video information is fetched. |
|[videoEngine:usingUrlInfos:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengine-usingurlinfos) |Occurs when the array of playback information is obtained. |
|[videoEnginePrepared:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengineprepared) |Occurs when the player module is prepared and ready for playback. |
|[videoEngineReadyToDisPlay:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoenginereadytodisplay) |Occurs when the first frame of the video is ready to be displayed. |
|[videoEngineReadyToPlay:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoenginereadytoplay) |Occurs when the video loading is completed and the player is ready to play. |
|[videoEngineAudioRendered:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengineaudiorendered) |Occurs when the audio rendering is complete. |
|[videoEngineStalledExcludeSeek:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoenginestalledexcludeseek) |Occurs when a freeze occurs that is not caused by a seek operation. |
|[videoEngineUserStopped:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoengineuserstopped) |Occurs when playback is stopped. |
|[videoEngineDidFinish:error:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoenginedidfinish-error) |Occurs when playback is finished. |
|[videoEngineCloseAysncFinish:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDelegate-videoenginecloseaysncfinish) |Occurs when the player instance is destroyed. |


<span id="Preloading and pre-rendering strategy"></span>
## Preloading and pre\-rendering strategy


|**Callback** |**Description** |
|---|---|
|[videoEngineWillPrepare:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEnginePreRenderDelegate-videoenginewillprepare) |Occurs when the `TTVideoEngine` instance is about to call the play method. You can adjust the playback parameters through the `videoEngine` at this time. |


<span id="Downloading"></span>
## Downloading


|**Callback** |**Description** |
|---|---|
|[VideoEngineDownloader:downloadTask:didCompleteWithError:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didcompletewitherror) |Occurs when a downloading task is completed. |
|[VideoEngineDownloader:downloadTask:writeData:timeInterval:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-writedata-timeinterval) |Occurs when there is progress in a downloading task. |
|[VideoEngineDownloader:downloadTask:didResumeAtOffset:expectedTotalBytes:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didresumeatoffset-expectedtotalbytes) |Occurs when a downloading task is about to start or resume. |
|[VideoEngineDownloader:downloadTask:stateChanged:](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-statechanged) |Occurs when the state of a downloading task changes. |

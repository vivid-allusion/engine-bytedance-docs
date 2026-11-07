---
title: "iOS Player SDK: Callbacks"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-callbacks"
---

<span id="TTVideoEngineDelegate"></span>
# TTVideoEngineDelegate

```objectivec
@protocol TTVideoEngineDelegate <NSObject>
```


Callbacks for events related to video playback state.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[videoEngine:playbackStateDidChanged:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-playbackstatedidchanged) |
|**void** |[videoEngine:loadStateDidChanged:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-loadstatedidchanged) |
|**void** |[videoEngine:loadStateDidChanged:extra:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-loadstatedidchanged-extra) |
|**void** |[videoEngine:fetchedVideoModel:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-fetchedvideomodel) |
|**void** |[videoEngine:usingUrlInfos:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-usingurlinfos) |
|**void** |[videoEngineReadyToDisPlay:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginereadytodisplay) |
|**void** |[videoEnginePrepared:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengineprepared) |
|**void** |[videoEngineReadyToPlay:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginereadytoplay) |
|**void** |[videoEngineAudioRendered:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengineaudiorendered) |
|**void** |[videoEngine:retryForError:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-retryforerror) |
|**void** |[videoEngineStalledExcludeSeek:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginestalledexcludeseek) |
|**void** |[videoEngine:mdlKey:hitCacheSze:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengine-mdlkey-hitcachesze) |
|**void** |[videoEngineDeviceOpened:streamType:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginedeviceopened-streamtype) |
|**void** |[videoEngineBeforeViewRemove:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginebeforeviewremove) |
|**nullable NSString** |[videoEngineGetEncryptedLocalTime:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginegetencryptedlocaltime) |
|**void** |[videoEngineUserStopped:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoengineuserstopped) |
|**void** |[videoEngineDidFinish:error:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginedidfinish-error) |
|**void** |[videoEngineDidFinish:videoStatusException:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginedidfinish-videostatusexception) |
|**void** |[videoEngineCloseAysncFinish:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDelegate-videoenginecloseaysncfinish) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineDelegate-videoengine-playbackstatedidchanged"></span>
### videoEngine:playbackStateDidChanged:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine playbackStateDidChanged:(TTVideoEnginePlaybackState)playbackState;
```


Occurs when the playback state changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|playbackState |**TTVideoEnginePlaybackState** |The current playback state. See [TTVideoEnginePlaybackState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineplaybackstate) for details. |


<span id="TTVideoEngineDelegate-videoengine-loadstatedidchanged"></span>
### videoEngine:loadStateDidChanged:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine loadStateDidChanged:(TTVideoEngineLoadState)loadState;
```


Occurs when the load state changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|loadState |**TTVideoEngineLoadState** |The current load state. See [TTVideoEngineLoadState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineloadstate) for details. |


**Note**

You can show or hide the loading view based on this callback.

<span id="TTVideoEngineDelegate-videoengine-loadstatedidchanged-extra"></span>
### videoEngine:loadStateDidChanged:extra:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine loadStateDidChanged:(TTVideoEngineLoadState)loadState extra:(nullable NSDictionary<NSString *,id> *)extraInfo;
```


Occurs when the load state changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|loadState |**TTVideoEngineLoadState** |The current load state. See [TTVideoEngineLoadState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineloadstate) for details. |
|extraInfo |\*\*nullable NSDictionary<NSString \*,id\> \*\*\* |Extra information:<br><br><br>* `TTVideoEngineBufferStartAction:@(TTVideoEngineStallActionNone)`: The action that caused buffering. See [TTVideoEngineStallAction](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestallaction) for details.<br><br>* `TTVideoEngineBufferStartReason:@(TTVideoEngineStallReasonNetwork)`: The specific reason that caused buffering. See [TTVideoEngineStallReason](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestallreason) for details. |


**Note**

You can show or hide the loading view based on this callback

<span id="TTVideoEngineDelegate-videoengine-fetchedvideomodel"></span>
### videoEngine:fetchedVideoModel:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine fetchedVideoModel:(TTVideoEngineModel *)videoModel;
```


Occurs when the video information is fetched.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|videoModel |**TTVideoEngineModel** |The detailed video source information returned by the server. |


**Note**

When playing VID video sources, this callback returns detailed information about the video source, including the `urls` for all resolutions.

<span id="TTVideoEngineDelegate-videoengine-usingurlinfos"></span>
### videoEngine:usingUrlInfos:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine usingUrlInfos:(NSArray<TTVideoEngineURLInfo *> *)urlInfos;
```


Occurs when the array of playback information is obtained.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|urlInfos |\*\*NSArray<TTVideoEngineURLInfo \*\> \*\*\* |The URL information for all resolutions of the video. |


**Note**

This callback returns all resolutions of the video when playing VID video sources.

<span id="TTVideoEngineDelegate-videoenginereadytodisplay"></span>
### videoEngineReadyToDisPlay:

```objectivec
- (void)videoEngineReadyToDisPlay:(TTVideoEngine *)videoEngine;
```


Occurs when the first frame of the video is ready to be displayed.

**Inputparameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


**Note**

You can hide the cover image and display the video frame based on this callback.

<span id="TTVideoEngineDelegate-videoengineprepared"></span>
### videoEnginePrepared:

```objectivec
- (void)videoEnginePrepared:(TTVideoEngine *)videoEngine;
```


Occurs when the player is ready for playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineDelegate-videoenginereadytoplay"></span>
### videoEngineReadyToPlay:

```objectivec
- (void)videoEngineReadyToPlay:(TTVideoEngine *)videoEngine;
```


Occurs when the video loading is completed and the player is ready to play.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineDelegate-videoengineaudiorendered"></span>
### videoEngineAudioRendered:

```objectivec
- (void)videoEngineAudioRendered:(TTVideoEngine *)videoEngine;
```


Occurs when the audio rendering is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineDelegate-videoengine-retryforerror"></span>
### videoEngine:retryForError:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine retryForError:(NSError *)error;
```


Occurs when an internal error occurs in the SDK and a retry is initiated.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|error |**NSError** |The internal error information. |


**Note**

This callback indicates that an internal error has occurred in the SDK and a retry will be initiated, rather than a final playback failure.

<span id="TTVideoEngineDelegate-videoenginestalledexcludeseek"></span>
### videoEngineStalledExcludeSeek:

```objectivec
- (void)videoEngineStalledExcludeSeek:(TTVideoEngine *)videoEngine;
```


Occurs when a freeze occurs that is not caused by a seek operation.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineDelegate-videoengine-mdlkey-hitcachesze"></span>
### videoEngine:mdlKey:hitCacheSze:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine mdlKey:(NSString *)key hitCacheSze:(NSInteger)cacheSize;
```


Occurs when the preloading task hits the cashed video.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|key |**NSString** |The unique identifier of the video cache. |
|cacheSize |**NSInteger** |The size of the cached video that is hit. |


<span id="TTVideoEngineDelegate-videoenginedeviceopened-streamtype"></span>
### videoEngineDeviceOpened:streamType:

```objectivec
- (void)videoEngineDeviceOpened:(TTVideoEngine *)videoEngine streamType:(TTVideoEngineStreamType)streamType;
```


Occurs when the audio and video devices are successfully opened.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|streamType |**TTVideoEngineStreamType** |The stream type. See [TTVideoEngineStreamType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestreamtype) for details. |


<span id="TTVideoEngineDelegate-videoenginebeforeviewremove"></span>
### videoEngineBeforeViewRemove:

```objectivec
- (void)videoEngineBeforeViewRemove:(TTVideoEngine *)videoEngine;
```


Occurs before the playback view is removed from its parent view. If the playback view is removed, the screen will display black.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineDelegate-videoenginegetencryptedlocaltime"></span>
### videoEngineGetEncryptedLocalTime:

```objectivec
- (nullable NSString *)videoEngineGetEncryptedLocalTime:(TTVideoEngine *)videoEngine;
```


Returns the encrypted local timestamp.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


**Returns**

This callback is used for private DRM encryption. You need to pass the encrypted local timestamp to the SDK.

<span id="TTVideoEngineDelegate-videoengineuserstopped"></span>
### videoEngineUserStopped:

```objectivec
- (void)videoEngineUserStopped:(TTVideoEngine *)videoEngine;
```


Occurs when the playback is stopped.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


**Note**

This callback is triggered when the `stop` method is called and completed by the SDK.

<span id="TTVideoEngineDelegate-videoenginedidfinish-error"></span>
### videoEngineDidFinish:error:

```objectivec
- (void)videoEngineDidFinish:(TTVideoEngine *)videoEngine error:(nullable NSError *)error;
```


Occurs when the playback is finished.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|error |**nullable NSError** |The error information. |


<span id="TTVideoEngineDelegate-videoenginedidfinish-videostatusexception"></span>
### videoEngineDidFinish:videoStatusException:

```objectivec
- (void)videoEngineDidFinish:(TTVideoEngine *)videoEngine videoStatusException:(NSInteger)status;
```


Occurs when the playback is finished abnormally.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|status |**NSInteger** |The status code of the abnormal playback. |


<span id="TTVideoEngineDelegate-videoenginecloseaysncfinish"></span>
### videoEngineCloseAysncFinish:

```objectivec
- (void)videoEngineCloseAysncFinish:(TTVideoEngine *)videoEngine;
```


Occurs when the player instance is destroyed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


**Note**

This callback is triggered when the `closeAysnc` method is called and completed by the SDK.

<span id="TTVideoEngineResolutionDelegate"></span>
# TTVideoEngineResolutionDelegate

```objectivec
@protocol TTVideoEngineResolutionDelegate <NSObject>
```


Resolution\-related callbacks.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[videoBitrateDidChange:resolution:bitrate:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineResolutionDelegate-videobitratedidchange-resolution-bitrate) |
|**void** |[videoSizeDidChange:videoWidth:videoHeight:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineResolutionDelegate-videosizedidchange-videowidth-videoheight) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineResolutionDelegate-videobitratedidchange-resolution-bitrate"></span>
### videoBitrateDidChange:resolution:bitrate:

```objectivec
- (void)videoBitrateDidChange:(TTVideoEngine *)videoEngine resolution:(TTVideoEngineResolutionType)resolution bitrate:(NSInteger)bitrate;
```


Occurs when the video bitrate changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|resolution |**TTVideoEngineResolutionType** |The current video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details. |
|bitrate |**NSInteger** |The current video bitrate. |


<span id="TTVideoEngineResolutionDelegate-videosizedidchange-videowidth-videoheight"></span>
### videoSizeDidChange:videoWidth:videoHeight:

```objectivec
- (void)videoSizeDidChange:(TTVideoEngine *)videoEngine videoWidth:(NSInteger)videoWidth videoHeight:(NSInteger)videoHeight;
```


Occurs when the video resolution changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|videoWidth |**NSInteger** |The current video width. |
|videoHeight |**NSInteger** |The current video height. |


<span id="TTVideoEngineSubtitleDelegate"></span>
# TTVideoEngineSubtitleDelegate

```objectivec
@protocol TTVideoEngineSubtitleDelegate <NSObject>
```


Callbacks related to subtitles.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[videoEngine:onSubtitleInfoCallBack:pts:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinfocallback-pts) |
|**void** |[videoEngine:onSubtitleInfoCallBack:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinfocallback) |
|**void** |[videoEngine:onSubtitleInfoRequested:error:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinforequested-error) |
|**void** |[videoEngine:onSubSwitchCompleted:currentSubtitleId:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineSubtitleDelegate-videoengine-onsubswitchcompleted-currentsubtitleid) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinfocallback-pts"></span>
### videoEngine:onSubtitleInfoCallBack:pts:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoCallBack:(NSString *)content pts:(NSUInteger)pts;
```


Occurs when the SDK receives a single piece of subtitle.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|content |**NSString** |The content of the subtitle piece. |
|pts |**NSUInteger** |The timestamp corresponding to the subtitle piece, in milliseconds. |


<span id="TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinfocallback"></span>
### videoEngine:onSubtitleInfoCallBack:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoCallBack:(TTVideoEngineSubInfo *)subInfo;
```


Occurs when the SDK receives a single piece of subtitle.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|subInfo |**TTVideoEngineSubInfo** |The subtitle piece. See [TTVideoEngineSubInfo](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginesubinfo) for details. |


<span id="TTVideoEngineSubtitleDelegate-videoengine-onsubtitleinforequested-error"></span>
### videoEngine:onSubtitleInfoRequested:error:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubtitleInfoRequested:(id _Nullable)info error:(NSError * _Nullable)error;
```


Occurs when the SDK receives subtitle information of all languages.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|info |**id** |The JSON object containing all language subtitle information. |
|error |**NSError** |Error information for the subtitle request. `error` is `nil` if the request is successful. |


<span id="TTVideoEngineSubtitleDelegate-videoengine-onsubswitchcompleted-currentsubtitleid"></span>
### videoEngine:onSubSwitchCompleted:currentSubtitleId:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine onSubSwitchCompleted:(BOOL)success currentSubtitleId:(NSInteger)currentSubtitleId;
```


Occurs when the subtitle language is switched.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |
|success |**BOOL** |Indicates whether the subtitle language switch is successful:<br><br><br>* YES: Successful.<br><br>* NO: Failed. |
|currentSubtitleId |**NSInteger** |The ID of the current subtitle. |


<span id="TTVideoEnginePreRenderDelegate"></span>
# TTVideoEnginePreRenderDelegate

```objectivec
@protocol TTVideoEnginePreRenderDelegate <NSObject>
```


Callbacks related to the pre\-rendering strategy.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[videoEngineWillPrepare:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEnginePreRenderDelegate-videoenginewillprepare) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEnginePreRenderDelegate-videoenginewillprepare"></span>
### videoEngineWillPrepare:

```objectivec
- (void)videoEngineWillPrepare:(TTVideoEngine *)videoEngine;
```


Indicates that the `TTVideoEngine` instance is about to call the play method. You can use this callback to adjust playback parameters through the `videoEngine`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


<span id="TTVideoEngineExternDNSParserDelegate"></span>
# TTVideoEngineExternDNSParserDelegate

```objectivec
@protocol TTVideoEngineExternDNSParserDelegate<NSObject>
```


This protocol describes the delegate for using an external DNS parser.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[setUrl:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineExternDNSParserDelegate-seturl) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineExternDNSParserDelegate-seturl"></span>
### setUrl:

```objectivec
- (void)setUrl:(NSString *)urlString;
```


Provides the URL to be resolved.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urlString |**NSString** |The URL to be resolved. |


<span id="TTVideoEngineDownloaderDelegate"></span>
# TTVideoEngineDownloaderDelegate

```objectivec
@protocol TTVideoEngineDownloaderDelegate <NSObject>
```


Callbacks related to downloading.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[VideoEngineDownloader:downloadTask:didCompleteWithError:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didcompletewitherror) |
|**void** |[VideoEngineDownloader:downloadTask:writeData:timeInterval:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-writedata-timeinterval) |
|**void** |[VideoEngineDownloader:downloadTask:didResumeAtOffset:expectedTotalBytes:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didresumeatoffset-expectedtotalbytes) |
|**void** |[VideoEngineDownloader:downloadTask:stateChanged:](https://docs.byteplus.com/en/docs/25/7969#TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-statechanged) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didcompletewitherror"></span>
### VideoEngineDownloader:downloadTask:didCompleteWithError:

```objectivec
- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader downloadTask:(TTVideoEngineDownloadTask *)downloadTask didCompleteWithError:(nullable NSError *)error;
```


Occurs when a downloading task is completed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**TTVideoEngineDownloader** |The downloading task manager. |
|downloadTask |**TTVideoEngineDownloadTask** |The current downloading task. |
|error |**nullable NSError** |The error information or the reason for completion. |


<span id="TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-writedata-timeinterval"></span>
### VideoEngineDownloader:downloadTask:writeData:timeInterval:

```objectivec
- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader downloadTask:(TTVideoEngineDownloadTask *)downloadTask writeData:(int64_t)bytesWritten timeInterval:(double)timeMS;
```


Indicates the progress of the downloading task .

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**TTVideoEngineDownloader** |The downloading task manager. |
|downloadTask |**TTVideoEngineDownloadTask** |The current downloading task. |
|bytesWritten |**int64_t** |The number of bytes downloaded in the `timeMS` time interval, which can be used to calculate the download speed. |
|timeMS |**double** |The time interval. |


**Note**

When playing HLS videos, the `bytesWritten` value may not be accurate. To get the download progress, it is recommended to directly use the `TTVideoEngineDownloadTask.progress` property.

<span id="TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-didresumeatoffset-expectedtotalbytes"></span>
### VideoEngineDownloader:downloadTask:didResumeAtOffset:expectedTotalBytes:

```objectivec
- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader downloadTask:(TTVideoEngineDownloadTask *)downloadTask didResumeAtOffset:(int64_t)fileOffset expectedTotalBytes:(int64_t)expectedTotalBytes;
```


Occurs when a downloading task is about to start or resume.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**TTVideoEngineDownloader** |The downloading task manager. |
|downloadTask |**TTVideoEngineDownloadTask** |The current downloading task. |
|fileOffset |**int64_t** |The starting or resuming position. |
|expectedTotalBytes |**int64_t** |The total size in bytes. Note: When playing HLS videos, the `expectedTotalBytes` value may not be accurate. |


<span id="TTVideoEngineDownloaderDelegate-videoenginedownloader-downloadtask-statechanged"></span>
### VideoEngineDownloader:downloadTask:stateChanged:

```objectivec
- (void)VideoEngineDownloader:(TTVideoEngineDownloader *)downloader downloadTask:(TTVideoEngineDownloadTask *)downloadTask stateChanged:(TTVideoEngineDownloadState)downloadState;
```


Occurs when the state of the downloading task changes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|downloader |**TTVideoEngineDownloader** |The downloading task manager. |
|downloadTask |**TTVideoEngineDownloadTask** |The current downloading task. |
|downloadState |**TTVideoEngineDownloadState** |The current download state. See [TTVideoEngineDownloadState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginedownloadstate) for details. |

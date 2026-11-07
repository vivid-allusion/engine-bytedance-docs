---
title: "iOS Player SDK: API details"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details"
---

<span id="TTVideoEngine"></span>
# TTVideoEngine

```objectivec
@interface TTVideoEngine : NSObject
```


The video engine. `TTVideoEngine` is the core class of the Player SDK, providing the core playback functions.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**CGFloat** |[playbackSpeed](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-playbackspeed) |
|**BOOL** |[muted](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-muted) |
|**BOOL** |[radioMode](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-radiomode) |
|**BOOL** |[hardwareDecode](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-hardwaredecode) |
|**BOOL** |[looping](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-looping) |
|**UIView** |[playerView](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-playerview) |
|**NSTimeInterval** |[currentPlaybackTime](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-currentplaybacktime) |
|**NSTimeInterval** |[duration](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-duration) |
|**NSTimeInterval** |[playableDuration](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-playableduration) |
|**NSTimeInterval** |[durationWatched](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-durationwatched) |
|**TTVideoEngineState** |[state](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-state) |
|**TTVideoEnginePlaybackState** |[playbackState](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-playbackstate) |
|**TTVideoEngineLoadState** |[loadState](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-loadstate) |
|**TTVideoEngineStallReason** |[stallReason](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-stallreason) |
|**TTVideoEngineResolutionType** |[currentResolution](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-currentresolution) |
|**id** |[subtitleDelegate](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-subtitledelegate) |
|**id** |[subDecInfoModel](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-subdecinfomodel) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**void** |[setLogFlag:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setlogflag) |
|**BOOL** |[isSupportMetal](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-issupportmetal) |
|**BOOL** |[enableEngineStrategy:scene:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-enableenginestrategy-scene) |
|**void** |[clearAllEngineStrategy](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-clearallenginestrategy) |
|**void** |[setStrategyVideoSources:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setstrategyvideosources) |
|**void** |[addStrategyVideoSources:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-addstrategyvideosources) |
|**void** |[setPreRenderVideoEngineDelegate:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setprerendervideoenginedelegate) |
|**TTVideoEngine** |[getPreRenderVideoEngineWithVideoSource:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-getprerendervideoenginewithvideosource) |
|**UIView** |[getPreRenderFinishedPlayerViewWithVideoSource:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-getprerenderfinishedplayerviewwithvideosource) |
|**TTVideoEngine** |[getPreRenderFinishedVideoEngineWithVideoSource:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-getprerenderfinishedvideoenginewithvideosource) |
|**BOOL** |[debugToolIsShowing](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-debugtoolisshowing) |
|**void** |[showDebugTool:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-showdebugtool) |
|**void** |[showDebugTool:inRect:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-showdebugtool-inrect) |
|**void** |[refreshCurrentVideoEngine:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-refreshcurrentvideoengine) |
|**void** |[removeDebugTool](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-removedebugtool) |
|**TTVideoEngineLocalServerConfigure** |[ls_localServerConfigure](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_localserverconfigure) |
|**void** |[ls_setCustomDNSParser:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_setcustomdnsparser) |
|**void** |[ls_addTaskWithURLItem:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_addtaskwithurlitem) |
|**void** |[ls_addTaskWithVidItem:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_addtaskwithviditem) |
|**void** |[ls_cancelTaskByKey:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_canceltaskbykey) |
|**void** |[ls_cancelTaskByVideoId:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_canceltaskbyvideoid) |
|**void** |[ls_cancelAllTasks](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_cancelalltasks) |
|**void** |[ls_cancelAllIdlePreloadTasks](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_cancelallidlepreloadtasks) |
|**void** |[ls_clearAllCaches](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_clearallcaches) |
|**void** |[ls_clearAllCaches:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_clearallcaches) |
|**void** |[ls_removeFileCacheByKey:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_removefilecachebykey) |
|**int64_t** |[ls_getAllCacheSize](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_getallcachesize) |
|**void** |[ls_getAllCacheSizeWithCompletion:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_getallcachesizewithcompletion) |
|**int64_t** |[ls_getCacheSizeByKey:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_getcachesizebykey) |
|**void** |[ls_getCacheSizeByKey:result:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_getcachesizebykey-result) |
|**nullable TTVideoEngineLocalServerCacheInfo** |[ls_getCacheFileInfoByKey:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-ls_getcachefileinfobykey) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[initWithOwnPlayer:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-initwithownplayer) |
|**void** |[setCustomHeaderValue:forKey:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setcustomheadervalue-forkey) |
|**void** |[setLocalURL:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setlocalurl) |
|**void** |[setBarrageMaskURL:fileHash:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setbarragemaskurl-filehash) |
|**void** |[prepareToPlay](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-preparetoplay) |
|**void** |[play](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-play) |
|**void** |[pause](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-pause) |
|**void** |[stop](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-stop) |
|**void** |[close](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-close) |
|**void** |[closeAysnc](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-closeaysnc) |
|**void** |[setCurrentPlaybackTime:complete:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setcurrentplaybacktime-complete) |
|**void** |[setCurrentPlaybackTime:complete:renderComplete:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setcurrentplaybacktime-complete-rendercomplete) |
|**void** |[addPeriodicTimeObserverForInterval:queue:usingBlock:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-addperiodictimeobserverforinterval-queue-usingblock) |
|**void** |[removeTimeObserver](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-removetimeobserver) |
|**nullable NSArray** |[supportedResolutionTypes](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-supportedresolutiontypes) |
|**nullable NSArray** |[supportedQualityInfos](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-supportedqualityinfos) |
|**BOOL** |[configResolution:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-configresolution) |
|**void** |[configResolution:completion:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-configresolution-completion) |
|**NSInteger** |[videoSizeForType:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-videosizefortype) |
|**nullable CVPixelBufferRef** |[copyPixelBuffer](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-copypixelbuffer) |
|**BOOL** |[isSupportHDR](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-issupporthdr) |
|**BOOL** |[isSupportSR](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-issupportsr) |
|**void** |[setFFmpegProtocol:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setffmpegprotocol) |
|**void** |[snapshot:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-snapshot) |
|**void** |[setVideoEngineVideoSource:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setvideoenginevideosource) |
|**NSString** |[getVideoEngineStrategyUniqueId](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-getvideoenginestrategyuniqueid) |
|**void** |[setSubtitleAuthToken:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-setsubtitleauthtoken) |
|**NSArray** |[subtitleIDs](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-subtitleids) |
|**NSArray** |[subtitleDescriptions](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-subtitledescriptions) |
|**NSDictionary** |[requestedSubtitleInfo](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-requestedsubtitleinfo) |
|**NSArray** |[subtitleInfos](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-subtitleinfos) |
|**BOOL** |[hasEmbeddedSubtitle](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-hasembeddedsubtitle) |
|**void** |[switchNewSubtitleModel:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-switchnewsubtitlemodel) |
|**TTVideoEngineSubInfo** |[getSubtitleInfo:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngine-getsubtitleinfo) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngine-playbackspeed"></span>
### playbackSpeed

```objectivec
@property (nonatomic, assign) CGFloat playbackSpeed;
```


Sets the playback speed. The default value is 1, and the value range is (0,3].

<span id="TTVideoEngine-muted"></span>
### muted

```objectivec
@property (nonatomic, assign) BOOL muted;
```


Sets whether to mute the video:

YES: Mute the video.

NO: (Default) Do not mute the video.

<span id="TTVideoEngine-radiomode"></span>
### radioMode

```objectivec
@property (nonatomic, assign) BOOL radioMode;
```


Sets whether to enable radio mode:

YES: Enable radio mode.

NO: (Default) Disable radio mode.

<span id="TTVideoEngine-hardwaredecode"></span>
### hardwareDecode

```objectivec
@property (nonatomic, assign) BOOL hardwareDecode;
```


Sets whether to enable hardware decoding:

YES: (Default) Enable hardware decoding.

NO: Disable hardware decoding.

<span id="TTVideoEngine-looping"></span>
### looping

```objectivec
@property (nonatomic, assign) BOOL looping;
```


Sets whether to enable looping playback:

YES: Enable looping playback.

NO: (default) Disable looping playback.

<span id="TTVideoEngine-playerview"></span>
### playerView

```objectivec
@property (nonatomic, strong, readonly) UIView *playerView;
```


The display view of the player.

<span id="TTVideoEngine-currentplaybacktime"></span>
### currentPlaybackTime

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval currentPlaybackTime;
```


The current playback position, in seconds.

<span id="TTVideoEngine-duration"></span>
### duration

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval duration;
```


The total duration of the video, in seconds.

<span id="TTVideoEngine-playableduration"></span>
### playableDuration

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval playableDuration;
```


The current playable duration (the cache progress), in seconds.

<span id="TTVideoEngine-durationwatched"></span>
### durationWatched

```objectivec
@property (nonatomic, assign, readonly) NSTimeInterval durationWatched;
```


The total duration watched, in seconds.

<span id="TTVideoEngine-state"></span>
### state

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineState state;
```


The current player state. See [TTVideoEngineState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestate) for details.

<span id="TTVideoEngine-playbackstate"></span>
### playbackState

```objectivec
@property (nonatomic, assign, readonly) TTVideoEnginePlaybackState playbackState;
```


The current playback state. See [TTVideoEnginePlaybackState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineplaybackstate) for details.

<span id="TTVideoEngine-loadstate"></span>
### loadState

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineLoadState loadState;
```


The current player load state. See [TTVideoEngineLoadState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineloadstate) for details.

<span id="TTVideoEngine-stallreason"></span>
### stallReason

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineStallReason stallReason;
```


The reason for player freeze. See [TTVideoEngineStallReason](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestallreason) for details.

<span id="TTVideoEngine-currentresolution"></span>
### currentResolution

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineResolutionType currentResolution;
```


The current video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details.

<span id="TTVideoEngine-subtitledelegate"></span>
### subtitleDelegate

```objectivec
@property (nonatomic, weak, nullable) id<TTVideoEngineSubtitleDelegate> subtitleDelegate;
```


Sets the subtitle\-related callback. See [TTVideoEngineSubtitleDelegate](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#ttvideoenginesubtitledelegate) for details.

<span id="TTVideoEngine-subdecinfomodel"></span>
### subDecInfoModel

```objectivec
@property (nonatomic, weak) id<TTVideoEngineSubDecInfoProtocol> subDecInfoModel;
```


Sets the subtitle source. See [TTVideoEngineSubDecInfoProtocol](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginesubdecinfoprotocol) for details.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngine-setlogflag"></span>
### setLogFlag:

```objectivec
+ (void)setLogFlag:(TTVideoEngineLogFlag)flag;
```


Sets log output mode.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|flag |**TTVideoEngineLogFlag** |Log output mode. See [TTVideoEngineLogFlag](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginelogflag) for details. |


**Note**

It is recommended to set `TTVideoEngineLogFlagDefault` for debugging and `TTVideoEngineLogFlagNone` for the online environment.

If you enable log output for debugging, make sure to disable it before your app goes live.

<span id="TTVideoEngine-issupportmetal"></span>
### isSupportMetal

```objectivec
+ (BOOL)isSupportMetal;
```


Checks whether the current device supports Metal rendering.

**Returns**

Whether Metal rendering is supported:

YES: Supported.

NO: Not supported.

<span id="TTVideoEngine-enableenginestrategy-scene"></span>
### enableEngineStrategy:scene:

```objectivec
+ (BOOL)enableEngineStrategy:(TTVideoEngineStrategyType)strategyType scene:(NSString *)scene;
```


Enables the playback strategy. The Player SDK supports preloading and prerendering strategies.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|strategyType |**TTVideoEngineStrategyType** |The strategy type. See [TTVideoEngineStrategyType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginestrategytype) for details. |
|scene |**NSString** |The use scenario. The strategy should be used with scenarios to achieve the best result. The SDK supports the following scenarios:<br><br><br>* `TTVEngineStrategySceneSmallVideo`: The short video scenario.<br><br>* `TTVEngineStrategySceneShortVideo`: The medium\-length video scenario. |


**Returns**

The result of enabling the strategy:

YES: Success.

NO: Failure.

**Note**

It is recommended to enable the strategy after a user entering the page.

<span id="TTVideoEngine-clearallenginestrategy"></span>
### clearAllEngineStrategy

```objectivec
+ (void)clearAllEngineStrategy;
```


Clears all strategies and releases resources.

**Note**

Call this method when the user exiting the current page or switching to another page.

<span id="TTVideoEngine-setstrategyvideosources"></span>
### setStrategyVideoSources:

```objectivec
+ (void)setStrategyVideoSources:(NSArray<id<TTVideoEngineMediaSource>> *)videoSources;
```


Sets the list of playback sources for the current page.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoSources |**NSArray** |The playback sources. See [TTVideoEngineMediaSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginemediasource) for details. |


**Note**

Use this method for preloading or prerendering strategies.

Calling this method will reset the current list of playback sources, which is used for setting the playback sources for the first time or when refreshing the page to display new data.

<span id="TTVideoEngine-addstrategyvideosources"></span>
### addStrategyVideoSources:

```objectivec
+ (void)addStrategyVideoSources:(NSArray<id<TTVideoEngineMediaSource>> *)videoSources;
```


Adds playback sources to the current list of playback sources.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoSources |**NSArray** |The playback sources. See [TTVideoEngineMediaSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginemediasource) for details. |


**Note**

Use this method for preloading or prerendering strategies.

This method is suitable for scenarios that load more data.

<span id="TTVideoEngine-setprerendervideoenginedelegate"></span>
### setPreRenderVideoEngineDelegate:

```objectivec
+ (void)setPreRenderVideoEngineDelegate:(id<TTVideoEnginePreRenderDelegate>)delegate;
```


Sets the delegate for the prerendering strategy.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|delegate |**id** |The delegate object for the prerendering strategy. See [TTVideoEnginePreRenderDelegate](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#ttvideoengineprerenderdelegate) for details. |


<span id="TTVideoEngine-getprerendervideoenginewithvideosource"></span>
### getPreRenderVideoEngineWithVideoSource:

```objectivec
+ (TTVideoEngine * _Nullable)getPreRenderVideoEngineWithVideoSource:(id<TTVideoEngineMediaSource>)source;
```


Gets the `TTVideoEngine` object that has been prerendered with the given playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The playback source. See [TTVideoEngineMediaSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginemediasource) for details. |


**Returns**

Te prerendered `TTVideoEngine` object.

<span id="TTVideoEngine-getprerenderfinishedplayerviewwithvideosource"></span>
### getPreRenderFinishedPlayerViewWithVideoSource:

```objectivec
+ (UIView * _Nullable)getPreRenderFinishedPlayerViewWithVideoSource:(id<TTVideoEngineMediaSource>)source;
```


Gets the player view of the pre\-rendered `TTVideoEngine` with the given playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The playback source. For more information, see [TTVideoEngineMediaSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginemediasource). |


**Returns**

The pre\-rendered `TTVideoEngine` player view.

**Note**

You can check if the player view is `nil` to determine if the pre\-rendering is finished.

<span id="TTVideoEngine-getprerenderfinishedvideoenginewithvideosource"></span>
### getPreRenderFinishedVideoEngineWithVideoSource:

```objectivec
+ (TTVideoEngine * _Nullable)getPreRenderFinishedVideoEngineWithVideoSource:(id<TTVideoEngineMediaSource>)source;
```


Gets the pre\-rendered `TTVideoEngine` object with the given playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The playback source. For more information, see [TTVideoEngineMediaSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginemediasource). |


**Returns**

The pre\-rendered `TTVideoEngine` object.

**Note**

You can check if the `TTVideoEngine` object is `nil` to determine if the pre\-rendering is finished.

<span id="TTVideoEngine-debugtoolisshowing"></span>
### debugToolIsShowing

```objectivec
+ (BOOL)debugToolIsShowing;
```


Checks if the debug tool is currently being displayed.

<span id="TTVideoEngine-showdebugtool"></span>
### showDebugTool:

```objectivec
+ (void)showDebugTool:(UIView *)containerView;
```


Adds the debug tool.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|containerView |**UIView** |The `containerView` used to display the debug tool. |


**Note**

After calling this method, the player will automatically add the current `TTVideoEngine` instance to the debug tool, so you don't need to frequently set the `TTVideoEngine` instance.

This method is suitable for scenarios which require frequent video switching, such as short videos or medium\-length videos.

<span id="TTVideoEngine-showdebugtool-inrect"></span>
### showDebugTool:inRect:

```objectivec
+ (void)showDebugTool:(UIView *)containerView inRect:(CGRect)rect;
```


Adds the debug tool.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|containerView |**UIView** |The `containerView` used to display the debug tool. |
|rect |**CGRect** |Sets the display area of the debug view in the container view. |


**Note**

After calling this method, the player will automatically add the current `TTVideoEngine` instance to the debug tool, so you don't need to frequently set the `TTVideoEngine` instance.

This method is suitable for scenarios which require frequent video switching, such as short videos or medium\-length videos.

<span id="TTVideoEngine-refreshcurrentvideoengine"></span>
### refreshCurrentVideoEngine:

```objectivec
+ (void)refreshCurrentVideoEngine:(TTVideoEngine *)videoEngine;
```


Refreshes the `TTVideoEngine` instance associated with the current debug tool.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoEngine |**TTVideoEngine** |The `videoEngine` object. |


**Note**

By default, the SDK automatically associates the currently playing `TTVideoEngine` instance with the debug tool.

<span id="TTVideoEngine-removedebugtool"></span>
### removeDebugTool

```objectivec
+ (void)removeDebugTool;
```


Removes the debug tool.

<span id="TTVideoEngine-ls_localserverconfigure"></span>
### ls_localServerConfigure

```objectivec
+ (TTVideoEngineLocalServerConfigure *)ls_localServerConfigure;
```


Configures the data loading module. For more information, see [TTVideoEngineLocalServerConfigure](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginelocalserverconfigure).

<span id="TTVideoEngine-ls_setcustomdnsparser"></span>
### ls_setCustomDNSParser:

```objectivec
+ (void)ls_setCustomDNSParser:(nonnull id<TTVideoEngineExternDNSParserDataSource, TTVideoEngineExternDNSParserDelegate>)parser;
```


Sets a custom DNS parser.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|parser |**id<TTVideoEngineExternDNSParserDataSource, TTVideoEngineExternDNSParserDelegate\>**  |An instance that implements the `<TTVideoEngineExternDNSParserDataSource, TTVideoEngineExternDNSParserDelegate>` protocol. |


**Note**

Call this method before `[TTSDKManager startWithConfiguration:configuration]`.

<span id="TTVideoEngine-ls_addtaskwithurlitem"></span>
### ls_addTaskWithURLItem:

```objectivec
+ (void)ls_addTaskWithURLItem:(TTVideoEnginePreloaderURLItem *)urlItem;
```


Adds a URL preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urlItem |**TTVideoEnginePreloaderURLItem** |The URL preloading task. For more information, see [TTVideoEnginePreloaderURLItem](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginepreloaderurlitem). |


<span id="TTVideoEngine-ls_addtaskwithviditem"></span>
### ls_addTaskWithVidItem:

```objectivec
+ (void)ls_addTaskWithVidItem:(TTVideoEnginePreloaderVidItem *)vidItem;
```


Adds a VID preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vidItem |**TTVideoEnginePreloaderVidItem** |The VID preloading task. For more information, see [TTVideoEnginePreloaderVidItem](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginepreloaderviditem). |


<span id="TTVideoEngine-ls_canceltaskbykey"></span>
### ls_cancelTaskByKey:

```objectivec
+ (void)ls_cancelTaskByKey:(NSString *)key;
```


Cancels a preloading task based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The cache key, which is the unique identifier of the URL preloading task. |


<span id="TTVideoEngine-ls_canceltaskbyvideoid"></span>
### ls_cancelTaskByVideoId:

```objectivec
+ (void)ls_cancelTaskByVideoId:(NSString *)vid;
```


Cancels a preloading task based on the video ID.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |**NSString** |The video ID. |


<span id="TTVideoEngine-ls_cancelalltasks"></span>
### ls_cancelAllTasks

```objectivec
+ (void)ls_cancelAllTasks;
```


Cancels all preloading tasks.

<span id="TTVideoEngine-ls_cancelallidlepreloadtasks"></span>
### ls_cancelAllIdlePreloadTasks

```objectivec
+ (void)ls_cancelAllIdlePreloadTasks;
```


Cancels all idle preloading tasks.

<span id="TTVideoEngine-ls_clearallcaches"></span>
### ls_clearAllCaches

```objectivec
+ (void)ls_clearAllCaches;
```


Deletes cached data from the data loading module.

**Note**

To optimize the playback experience, calling this method does not delete all cached data. Instead, it keeps about the last 10 data items according to the Least Recently Used (LRU) algorithm.

<span id="TTVideoEngine-ls_clearallcaches"></span>
### ls_clearAllCaches:

```objectivec
+ (void)ls_clearAllCaches:(BOOL)force;
```


Deletes all cached data from the data loading module.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|force |**BOOL** |Whether to forcefully delete all cached data:<br><br><br>* YES: Deletes all cached data.<br><br>* NO: Similar to calling the `ls_clearAllCaches` method, it does not delete all cached data. Instead, it keeps about the last 10 data items using the Least Recently Used (LRU) algorithm, optimizing the playback experience. |


<span id="TTVideoEngine-ls_removefilecachebykey"></span>
### ls_removeFileCacheByKey:

```objectivec
+ (void)ls_removeFileCacheByKey:(NSString *)key;
```


Deletes cached data from the data loading module based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The unique identifier for the cached data in the data loading module. |


<span id="TTVideoEngine-ls_getallcachesize"></span>
### ls_getAllCacheSize

```objectivec
+ (int64_t)ls_getAllCacheSize;
```


Gets the total size of the cached data in the data loading module, in bytes.

**Returns**

The total size of the cached data in the data loading module.

<span id="TTVideoEngine-ls_getallcachesizewithcompletion"></span>
### ls_getAllCacheSizeWithCompletion:

```objectivec
+ (void)ls_getAllCacheSizeWithCompletion:(void(^)(int64_t cacheSize))block;
```


Asynchronously gets the total size of the cached data in the data loading module, in bytes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|block |**void(^)(int64_t cacheSize)**  |The asynchronous callback. |


<span id="TTVideoEngine-ls_getcachesizebykey"></span>
### ls_getCacheSizeByKey:

```objectivec
+ (int64_t)ls_getCacheSizeByKey:(NSString *)key;
```


Gets the size of the cached data based on the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The unique identifier for the cached data in the data loading module. |


**Returns**

The size of the cached data, in bytes.

<span id="TTVideoEngine-ls_getcachesizebykey-result"></span>
### ls_getCacheSizeByKey:result:

```objectivec
+ (void)ls_getCacheSizeByKey:(NSString *)key result:(void(^)(int64_t size))result;
```


Asynchronously gets the size of the cached data based on the cache key, in bytes.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The unique identifier for the cached data in the data loading module. |
|result |**void(^)(int64_t size)**  |The asynchronous callback. |


<span id="TTVideoEngine-ls_getcachefileinfobykey"></span>
### ls_getCacheFileInfoByKey:

```objectivec
+ (nullable TTVideoEngineLocalServerCacheInfo *)ls_getCacheFileInfoByKey:(NSString *)key;
```


Gets detailed information about the cached data based on the cache key. For more information, see [TTVideoEngineLocalServerCacheInfo](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginelocalservercacheinfo).

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The unique identifier for the cached data in the data loading module. |


<span id="TTVideoEngine-initwithownplayer"></span>
### initWithOwnPlayer:

```objectivec
- (instancetype)initWithOwnPlayer:(BOOL)isOwnPlayer;
```


Initializes the player instance.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|isOwnPlayer |**BOOL** |Whether to use the BytePlus player.<br><br>• `YES`: The BytePlus player.<br><br>• `NO`: The system player. |


**Returns**

After a successful call, returns the player instance.

**Note**

It is strongly recommended to set this parameter to `YES` to use the BytePlus player. If you use the system player, you will not be able to use features such as preloading and local caching.

<span id="TTVideoEngine-setcustomheadervalue-forkey"></span>
### setCustomHeaderValue:forKey:

```objectivec
- (void)setCustomHeaderValue:(NSString *)value forKey:(NSString *)key;
```


Sets the custom header for player requests.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|value |**NSString** |The value. |
|key |**NSString** |The key. |


<span id="TTVideoEngine-setlocalurl"></span>
### setLocalURL:

```objectivec
- (void)setLocalURL:(NSString *)url;
```


Sets the local video source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|url |**NSString** |The local video URL, for example, `file://xxx.xx`. |


**Note**

Call this method to play a local video resource.

<span id="TTVideoEngine-setbarragemaskurl-filehash"></span>
### setBarrageMaskURL:fileHash:

```objectivec
- (void)setBarrageMaskURL:(NSString *)url fileHash:(nullable NSString *)fileHash;
```


Sets the URL of the masking bullet comments.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|url |**NSString** |The URL of the masking bullet comments. |
|fileHash |**nullable NSString** |The unique identifier of the file. It is recommended to use the hash value of the file or the MD5 value of the URL. |


<span id="TTVideoEngine-preparetoplay"></span>
### prepareToPlay

```objectivec
- (void)prepareToPlay;
```


Prepares for playback.

**Note**

This method is used for the pre\-rendering strategy. After setting the playback source, you need to call this method. The SDK will render the first frame of the video but will not start playing immediately.

<span id="TTVideoEngine-play"></span>
### play

```objectivec
- (void)play;
```


Starts playback.

<span id="TTVideoEngine-pause"></span>
### pause

```objectivec
- (void)pause;
```


Pauses playback.

<span id="TTVideoEngine-stop"></span>
### stop

```objectivec
- (void)stop;
```


Stops playback.

<span id="TTVideoEngine-close"></span>
### close

```objectivec
- (void)close;
```


Destroys the player.

**Note**

After destroying the player instance, no further methods can be called. You can set the `engine` instance to `nil` to prevent further calls.

<span id="TTVideoEngine-closeaysnc"></span>
### closeAysnc

```objectivec
-(void)closeAysnc;
```


Asynchronously releases the player.

**Note**

This method asynchronously destroys the player instance without affecting the main thread.

Asynchronous release helps to avoid UI freezes when user scrolling videos up and down.

After destroying the player instance, no further methods can be called. You can set the `engine` instance to `nil` to prevent further calls.

<span id="TTVideoEngine-setcurrentplaybacktime-complete"></span>
### setCurrentPlaybackTime:complete:

```objectivec
- (void)setCurrentPlaybackTime:(NSTimeInterval)currentPlaybackTime complete:(void(^)(BOOL success))finised;
```


Jumps to the specified timestamp and starts playing.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|currentPlaybackTime |**NSTimeInterval** |The specified timestamp. |
|finised |**void(^)(BOOL success)**  |Callback for completion of the jump. |


**Note**

You can call this method to implement the functionality of dragging the progress bar to start playing at a specific time.

<span id="TTVideoEngine-setcurrentplaybacktime-complete-rendercomplete"></span>
### setCurrentPlaybackTime:complete:renderComplete:

```objectivec
- (void)setCurrentPlaybackTime:(NSTimeInterval)currentPlaybackTime complete:(void(^)(BOOL success))finised renderComplete:(void(^)(void)) renderComplete;
```


Jumps to the specified timestamp and starts playing.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|currentPlaybackTime |**NSTimeInterval** |The specified timestamp. |
|finised |**void(^)(BOOL success)**  |Callback for completion of the jump. |
|renderComplete |**void(^)(void)**  |Callback for render completion. |


**Note**

You can call this method to implement the functionality of dragging the progress bar to start playing at a specific time.

<span id="TTVideoEngine-addperiodictimeobserverforinterval-queue-usingblock"></span>
### addPeriodicTimeObserverForInterval:queue:usingBlock:

```objectivec
- (void)addPeriodicTimeObserverForInterval:(NSTimeInterval)interval queue:(dispatch_queue_t)queue usingBlock:(void (^)(void))block;
```


Adds a periodic time observer, which encapsulates an NSTimer timer for convenient updating of the playback progress in the block callback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|interval |**NSTimeInterval** |The interval of the callback, in seconds. |
|queue |**dispatch_queue_t** |The specified dispatch queue. |
|block |**void (^)(void)**  |The callback block. |


<span id="TTVideoEngine-removetimeobserver"></span>
### removeTimeObserver

```objectivec
- (void)removeTimeObserver;
```


Removes the periodic time observer.

**Note**

This method is used together with `addPeriodicTimeObserverForInterval:queue:usingBlock`.

Call this method after destroying the player to avoid memory leaks.

<span id="TTVideoEngine-supportedresolutiontypes"></span>
### supportedResolutionTypes

```objectivec
- (nullable NSArray<NSNumber *> *)supportedResolutionTypes;
```


Gets all the supported resolution types when playing videos with VIDs.

**Returns**

An array of all the supported resolution types.

<span id="TTVideoEngine-supportedqualityinfos"></span>
### supportedQualityInfos

```objectivec
- (nullable NSArray<NSString *> *)supportedQualityInfos;
```


Gets all the descriptions of the supported resolution types when playing videos with VIDs.

**Returns**

An array of all the descriptions of the supported resolution types.

<span id="TTVideoEngine-configresolution"></span>
### configResolution:

```objectivec
- (BOOL)configResolution:(TTVideoEngineResolutionType)resolution;
```


Sets the initial resolution when playback starts or switches to a specific resolution during playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolution |**TTVideoEngineResolutionType** |The video resolution. Refer to [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details. |


**Returns**

The result of the method call:

YES: Success.

NO: Failure.

<span id="TTVideoEngine-configresolution-completion"></span>
### configResolution:completion:

```objectivec
- (void)configResolution:(TTVideoEngineResolutionType)resolution completion:(void(^)(BOOL success, TTVideoEngineResolutionType completeResolution))completion;
```


Sets the initial resolution when playback starts or switches to a specific resolution during playback.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolution |**TTVideoEngineResolutionType** |The video resolution. Refer to [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details. |
|completion |**void(^)(BOOL success, TTVideoEngineResolutionType completeResolution)**  |Callback for resolution switching completion. |


**Returns**

The result of the method call:

YES: Success.

NO: Failure.

<span id="TTVideoEngine-videosizefortype"></span>
### videoSizeForType:

```objectivec
- (NSInteger)videoSizeForType:(TTVideoEngineResolutionType)type;
```


Gets the video size in bytes for a specific resolution.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|type |**TTVideoEngineResolutionType** |The resolution type. Refer to [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details. |


**Returns**

The video size in bytes.

<span id="TTVideoEngine-copypixelbuffer"></span>
### copyPixelBuffer

```objectivec
- (nullable CVPixelBufferRef)copyPixelBuffer;
```


Gets the current rendering CVPixelBufferRef.

**Returns**

The current rendering CVPixelBufferRef.

**Note**

You can use this method for custom rendering.

<span id="TTVideoEngine-issupporthdr"></span>
### isSupportHDR

```objectivec
- (BOOL)isSupportHDR;
```


Check if the current device supports HDR playback.

**Returns**

Whether HDR is supported:

YES: Supported.

NO: Not supported.

**Note**

The SDK has a whitelist of devices that support HDR playback. The SDK will check if the current device is in the whitelist to determine if HDR playback is supported.

<span id="TTVideoEngine-issupportsr"></span>
### isSupportSR

```objectivec
- (BOOL)isSupportSR;
```


Checks if the current device supports super resolution.

**Returns**

Whether super resolution is supported:

YES: Supported.

NO: Not supported.

**Note**

The SDK has a whitelist of devices that support super resolution. The SDK will check if the current device is in the whitelist to determine if super resolution is supported.

<span id="TTVideoEngine-setffmpegprotocol"></span>
### setFFmpegProtocol:

```objectivec
- (void)setFFmpegProtocol:(id<TTVideoEngineFFmpegProtocol>) obj;
```


Sets the `TTVideoEngineFFmpegProtocol` object for supporting private FFmpeg encryption protocols.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|obj |**id** |The `TTVideoEngineFFmpegProtocol` object. |


<span id="TTVideoEngine-snapshot"></span>
### snapshot:

```objectivec
- (void)snapshot:(void(^)(UIImage *))completion;
```


Takes a snapshot.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|completion |**void(^)(UIImage )**  |Callback for snapshot completion. |


<span id="TTVideoEngine-setvideoenginevideosource"></span>
### setVideoEngineVideoSource:

```objectivec
- (void)setVideoEngineVideoSource:(id<TTVideoEngineMediaSource>)source;
```


Sets the playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The playback source, which supports the following types:<br><br><br>* If you want to play videos with VIDs, set this parameter to [TTVideoEngineVidSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginevidsource).<br><br>* If you want to play videos with URLs, set this parameter to [TTVideoEngineUrlSource](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineurlsource). |


<span id="TTVideoEngine-getvideoenginestrategyuniqueid"></span>
### getVideoEngineStrategyUniqueId

```objectivec
- (NSString *)getVideoEngineStrategyUniqueId;
```


Gets the unique identifier for the current `TTVideoEngine` object.

**Returns**

The unique identifier for the current `TTVideoEngine` object, which is the `uniqueId` property of the `TTVideoEngineMediaSource` object.

<span id="TTVideoEngine-setsubtitleauthtoken"></span>
### setSubtitleAuthToken:

```objectivec
- (void)setSubtitleAuthToken:(NSString *)auth;
```


Sets the subtitle token.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|auth |**NSString** |The subtitle token. |


<span id="TTVideoEngine-subtitleids"></span>
### subtitleIDs

```objectivec
- (NSArray * _Nullable)subtitleIDs;
```


Gets the list of supported subtitle IDs.

**Returns**

The list of supported subtitle IDs.

<span id="TTVideoEngine-subtitledescriptions"></span>
### subtitleDescriptions

```objectivec
- (NSArray<TTVideoEngineSubModel *> *)subtitleDescriptions;
```


Gets the list of subtitle information in supported languages.

**Returns**

The list of [TTVideoEngineSubModel](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginesubmodel).

<span id="TTVideoEngine-requestedsubtitleinfo"></span>
### requestedSubtitleInfo

```objectivec
- (NSDictionary * _Nullable)requestedSubtitleInfo;
```


Gets the detailed information of the subtitle requested with the VID.

**Returns**

The detailed information of the subtitle.

<span id="TTVideoEngine-subtitleinfos"></span>
### subtitleInfos

```objectivec
- (NSArray * _Nullable)subtitleInfos;
```


Gets the detailed information of all requested subtitle sources for the VID playback source.

**Returns**

The detailed information of all requested subtitle sources.

<span id="TTVideoEngine-hasembeddedsubtitle"></span>
### hasEmbeddedSubtitle

```objectivec
- (BOOL)hasEmbeddedSubtitle;
```


Checks if the current video source has embedded subtitles.

**Returns**

Whether the video has embedded subtitles:

YES: Embedded subtitles are available.

NO: No embedded subtitles.

<span id="TTVideoEngine-switchnewsubtitlemodel"></span>
### switchNewSubtitleModel:

```objectivec
- (void)switchNewSubtitleModel:(id<TTVideoEngineSubProtocol>)subModel;
```


Switches to the subtitle source in another language.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subModel |**id** |The subtitle data source for a single language. See [TTVideoEngineSubProtocol](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginesubprotocol). |


<span id="TTVideoEngine-getsubtitleinfo"></span>
### getSubtitleInfo:

```objectivec
- (TTVideoEngineSubInfo *)getSubtitleInfo:(NSInteger)queryTime;
```


Gets the subtitle of a specified playback position.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|queryTime |**NSInteger** |The specified playback position. |


**Returns**

The subtitle of the specified playback position. See [TTVideoEngineSubInfo](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginesubinfo).

<span id="TTVideoEngineDownloader"></span>
# TTVideoEngineDownloader

```objectivec
@interface TTVideoEngineDownloader : NSObject
```


The downloader interface, which can be used for managing downloading tasks.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSUInteger** |[maxDownloadOperationCount](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-maxdownloadoperationcount) |
|**int64_t** |[limitFreeDiskSize](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-limitfreedisksize) |
|**id** |[delegate](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-delegate) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[shareLoader](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-shareloader) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[getAllTasksWithCompletionHandler:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-getalltaskswithcompletionhandler) |
|**NSInteger** |[downloadSize](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-downloadsize) |
|**void** |[suspendAllTasks](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-suspendalltasks) |
|**void** |[resumeAllTasks](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-resumealltasks) |
|**void** |[removeAllTasks](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-removealltasks) |
|**nullable TTVideoEngineDownloadURLTask** |[urlTask:key:videoId:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-urltask-key-videoid) |
|**nullable TTVideoEngineDownloadVidTask** |[vidTask:playAuthToken:resolution:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloader-vidtask-playauthtoken-resolution) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineDownloader-maxdownloadoperationcount"></span>
### maxDownloadOperationCount

```objectivec
@property (nonatomic, assign) NSUInteger maxDownloadOperationCount;
```


Sets the maximum number of concurrent downloading tasks. The default value is 1.

<span id="TTVideoEngineDownloader-limitfreedisksize"></span>
### limitFreeDiskSize

```objectivec
@property (nonatomic, assign) int64_t limitFreeDiskSize;
```


Sets the limit on remaining disk size for caching. The unit is bytes, and the default value is 1024 \* 1024 \* 1024 \* 1, which represents 1 GB. If the remaining disk size is less than the specified value, the SDK throws the `TTVideoEngineErrorNotEnoughDiskSpace` error.

<span id="TTVideoEngineDownloader-delegate"></span>
### delegate

```objectivec
@property (nonatomic, weak) id<TTVideoEngineDownloaderDelegate> delegate;
```


Sets the delegate for download\-related callbacks. See [TTVideoEngineDownloaderDelegate](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-callbacks?version=v1.0#ttvideoenginedownloaderdelegate).

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineDownloader-shareloader"></span>
### shareLoader

```objectivec
+ (instancetype)shareLoader;
```


Singleton method.

<span id="TTVideoEngineDownloader-getalltaskswithcompletionhandler"></span>
### getAllTasksWithCompletionHandler:

```objectivec
- (void)getAllTasksWithCompletionHandler:(void (^)(NSArray<__kindof TTVideoEngineDownloadTask *> * _Nonnull))completionHandler;
```


Gets all downloading tasks.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|completionHandler |\**void (^)(NSArray<__kindof TTVideoEngineDownloadTask \> \* _Nonnull)*  |The block callback. |


<span id="TTVideoEngineDownloader-downloadsize"></span>
### downloadSize

```objectivec
- (NSInteger)downloadSize;
```


Gets the total size of all downloading tasks, in bytes.

**Returns**

The total size of all downloading tasks.

**Note**

This method must be called in the block callback of `getAllTasksWithCompletionHandler`.

The value returned by this method may not be accurate when playing HLS videos. If you want to gets the download progress, it is recommended to directly use the `TTVideoEngineDownloadTask.progress` property.

<span id="TTVideoEngineDownloader-suspendalltasks"></span>
### suspendAllTasks

```objectivec
- (void)suspendAllTasks;
```


Suspends all downloading tasks.

**Note**

This method must be called in the block callback of `getAllTasksWithCompletionHandler`.

<span id="TTVideoEngineDownloader-resumealltasks"></span>
### resumeAllTasks

```objectivec
- (void)resumeAllTasks;
```


Resumes all downloading tasks.

**Note**

This method must be called in the block callback of `getAllTasksWithCompletionHandler`.

<span id="TTVideoEngineDownloader-removealltasks"></span>
### removeAllTasks

```objectivec
- (void)removeAllTasks;
```


Removes all downloading tasks.

**Note**

This method must be called in the block callback of `getAllTasksWithCompletionHandler`.

<span id="TTVideoEngineDownloader-urltask-key-videoid"></span>
### urlTask:key:videoId:

```objectivec
- (nullable TTVideoEngineDownloadURLTask *)urlTask:(NSArray *)urls key:(NSString *)key videoId:(nullable NSString *)videoId;
```


Creates a downloading task for URL\-based media sources.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls |**NSArray** |The URLs of the media sources. Supports primary and backup URLs. |
|key |**NSString** |The cache key, which is the unique identifier for the downloading task. |
|videoId |**nullable NSString** |(Optional) The video ID . |


**Returns**

An instance of [TTVideoEngineDownloadURLTask](https://docs.byteplus.com/en/docs/25/7968#ttvideoenginedownloadurltask).

<span id="TTVideoEngineDownloader-vidtask-playauthtoken-resolution"></span>
### vidTask:playAuthToken:resolution:

```objectivec
- (nullable TTVideoEngineDownloadVidTask *)vidTask:(NSString *)videoId playAuthToken:(NSString *)token resolution:(TTVideoEngineResolutionType)resolution;
```


Creates a downloading task for VID\-based media sources.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|videoId |**NSString** |The video ID. |
|token |**NSString** |The video playback auth token. |
|resolution |**TTVideoEngineResolutionType** |The video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details. |


**Returns**

An instance of [TTVideoEngineDownloadVidTask](https://docs.byteplus.com/en/docs/25/7968#ttvideoenginedownloadvidtask).

<span id="TTVideoEngineDownloadTask"></span>
# TTVideoEngineDownloadTask

```objectivec
@interface TTVideoEngineDownloadTask : NSObject
```


The interface of a downloading task.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[taskDescription](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-taskdescription) |
|**int64_t** |[countOfBytesReceived](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-countofbytesreceived) |
|**int64_t** |[countOfBytesExpectedToReceive](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-countofbytesexpectedtoreceive) |
|**double** |[progress](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-progress) |
|**TTVideoEngineDownloadState** |[state](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-state) |
|**NSError** |[error](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-error) |
|**NSString** |[availableLocalFilePath](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-availablelocalfilepath) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[invalidateAndCancel](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-invalidateandcancel) |
|**void** |[suspend](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-suspend) |
|**void** |[resume](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadTask-resume) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineDownloadTask-taskdescription"></span>
### taskDescription

```objectivec
@property (nullable, copy) NSString *taskDescription;
```


Sets the description for the downloading task.

<span id="TTVideoEngineDownloadTask-countofbytesreceived"></span>
### countOfBytesReceived

```objectivec
@property (readonly) int64_t countOfBytesReceived;
```


The current number of bytes received by the downloading task.

<span id="TTVideoEngineDownloadTask-countofbytesexpectedtoreceive"></span>
### countOfBytesExpectedToReceive

```objectivec
@property (readonly) int64_t countOfBytesExpectedToReceive;
```


The total number of bytes in the video. Note that this value may not be accurate when playing HLS videos. If you want to get the download progress, it is recommended to directly use the `TTVideoEngineDownloadTask.progress` property.

<span id="TTVideoEngineDownloadTask-progress"></span>
### progress

```objectivec
@property (nonatomic, readonly) double progress;
```


The current download progress as a percentage.

<span id="TTVideoEngineDownloadTask-state"></span>
### state

```objectivec
@property (readonly) TTVideoEngineDownloadState state;
```


Gets the current download state. See [TTVideoEngineDownloadState](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoenginedownloadstate) for details.

<span id="TTVideoEngineDownloadTask-error"></span>
### error

```objectivec
@property (nullable, readonly, copy) NSError *error;
```


The error information for the downloading task, including the error code and description.

<span id="TTVideoEngineDownloadTask-availablelocalfilepath"></span>
### availableLocalFilePath

```objectivec
@property (nullable, readonly, copy) NSString *availableLocalFilePath;
```


Gets the local file path for the downloading task.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineDownloadTask-invalidateandcancel"></span>
### invalidateAndCancel

```objectivec
- (void)invalidateAndCancel;
```


Delete the downloading task.

**Note**

This method can be called on a background thread.

<span id="TTVideoEngineDownloadTask-suspend"></span>
### suspend

```objectivec
- (void)suspend;
```


Suspends the downloading taskask.

**Note**

This method should be called on the main thread.

<span id="TTVideoEngineDownloadTask-resume"></span>
### resume

```objectivec
- (void)resume;
```


Starts or resumes the downloading task.

<span id="TTVideoEngineDownloadURLTask"></span>
# TTVideoEngineDownloadURLTask

```objectivec
@interface TTVideoEngineDownloadURLTask : TTVideoEngineDownloadTask
```


The interface of a URL downloading task.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSArray** |[urls](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadURLTask-urls) |
|**NSString** |[key](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadURLTask-key) |
|**NSString** |[videoId](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadURLTask-videoid) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[updateUrls:](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadURLTask-updateurls) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineDownloadURLTask-urls"></span>
### urls

```objectivec
@property (nonatomic, copy, readonly) NSArray *urls;
```


A list of URLs. Supports primary and backup URLs.

<span id="TTVideoEngineDownloadURLTask-key"></span>
### key

```objectivec
@property (nonatomic, copy, readonly) NSString *key;
```


The cache key that corresponds to the video source. It is recommended to use the MD5 of the URL as the cache key.

<span id="TTVideoEngineDownloadURLTask-videoid"></span>
### videoId

```objectivec
@property (nonatomic, copy, readonly, nullable) NSString *videoId;
```


The video ID. It is a unique identifier for the video and must correspond to the video source.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineDownloadURLTask-updateurls"></span>
### updateUrls:

```objectivec
- (void)updateUrls:(NSArray *)urls;
```


Updates the list of URLs.

<span id="TTVideoEngineDownloadVidTask"></span>
# TTVideoEngineDownloadVidTask

```objectivec
@interface TTVideoEngineDownloadVidTask : TTVideoEngineDownloadTask
```


The interface of a VID downloading task.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[videoId](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-videoid) |
|**TTVideoEngineResolutionType** |[resolution](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-resolution) |
|**TTVideoEngineEncodeType** |[codecType](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-codectype) |
|**BOOL** |[h265Enable](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-h265enable) |
|**BOOL** |[baseDashEnable](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-basedashenable) |
|**BOOL** |[httpsEnable](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-httpsenable) |
|**NSDictionary<NSString, NSNumber\>**  |[resolutionMap](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-resolutionmap) |
|**TTVideoEngineResolutionType** |[currentResolution](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-currentresolution) |
|**TTVideoEngineModel** |[videoModel](https://docs.byteplus.com/en/docs/25/7968#TTVideoEngineDownloadVidTask-videomodel) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineDownloadVidTask-videoid"></span>
### videoId

```objectivec
@property (nonatomic,   copy, readonly) NSString *videoId;
```


The video ID.

<span id="TTVideoEngineDownloadVidTask-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineResolutionType resolution;
```


The video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineresolutiontype) for details.

<span id="TTVideoEngineDownloadVidTask-codectype"></span>
### codecType

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineEncodeType codecType;
```


The codec type. See [TTVideoEngineEncodeType](https://docs.byteplus.com/byteplus-vod/docs/ios-player-sdk-type-definitions?version=v1.0#ttvideoengineencodetype) for details.

<span id="TTVideoEngineDownloadVidTask-h265enable"></span>
### h265Enable

```objectivec
@property (nonatomic, assign, readonly) BOOL h265Enable;
```


Whether to enable H.265:

YES: Enable H.265.

NO: Disable H.265..

<span id="TTVideoEngineDownloadVidTask-basedashenable"></span>
### baseDashEnable

```objectivec
@property (nonatomic, assign, readonly) BOOL baseDashEnable;
```


Whether to enable DASH:

YES: Enable DASH.

NO: Disable DASH.

<span id="TTVideoEngineDownloadVidTask-httpsenable"></span>
### httpsEnable

```objectivec
@property (nonatomic, assign, readonly) BOOL httpsEnable;
```


Whether to enable HTTPS:

YES: Enable HTTPS.

NO: Disable HTTPS.

<span id="TTVideoEngineDownloadVidTask-resolutionmap"></span>
### resolutionMap

```objectivec
@property (nonatomic, strong, nullable) NSDictionary<NSString *, NSNumber *> *resolutionMap;
```


The video resolution map.

<span id="TTVideoEngineDownloadVidTask-currentresolution"></span>
### currentResolution

```objectivec
@property (nonatomic, assign, readonly) TTVideoEngineResolutionType currentResolution;
```


The video resolution corresponding to the downloading task.

<span id="TTVideoEngineDownloadVidTask-videomodel"></span>
### videoModel

```objectivec
@property (nonatomic, strong, nullable, readonly) TTVideoEngineModel *videoModel;
```


The video information for the downloading task.

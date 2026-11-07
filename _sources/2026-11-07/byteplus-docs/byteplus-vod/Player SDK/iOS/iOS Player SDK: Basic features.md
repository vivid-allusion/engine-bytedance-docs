---
title: "iOS Player SDK: Basic features"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-ios"
---

To build a full\-featured video player in your iOS app, this guide provides the essential code examples and instructions. You will learn how to implement core playback controls, adjust video layout and resolution, play various formats like DASH and encrypted HLS, and listen for key playback events.

<span id="0ded4672"></span>
## Prerequisites

To create the environment necessary to implement the basic features in your app, ensure that you have integrated the SDK and implemented the playback feature in [Getting Started with the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk).

<span id="b06aa682"></span>
## Control playback

The `TTVideoEngine` class provides the following methods for controlling video playback:


* Call `play` to start or resume playback.

   ```objectivec
   [self.engine play];
   ```
   

* Call `pause` to pause playback. Call `play` to resume.

   ```objectivec
   [self.engine pause:YES]; 
   [self.engine play];
   ```
   

* Call `setCurrentPlaybackTime:complete:` to seek to a specified time position. This method enables users to drag the video progress bar to forward or rewind the video.

   ```objectivec
   // `currentTime` is the time you want to seek to, in seconds
   [self.engine setCurrentPlaybackTime:currentTime complete:^(BOOL success) {
       // Indicates whether the seek operation was successful
       NSLog(@"seek complete %@", @(success));
   } renderComplete:^{
       // The renderComplete callback indicates whether the rendering operation completes
       NSLog(@"seek render complete");
   }];
   ```
   

* Set `StartTime` before calling `play` to specify the time position at which the playback starts. This can be used for the "Skip Intro" feature.

   ```objectivec
   CGFloat startTime = 5.0f;
   [engine setOptionForKey:VEKKeyPlayerStartTime_CGFloat value:@(startTime)];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Combining pre\-rendering with a specified playback start time requires the iOS Player SDK <code>1.52.100.4</code> or later. Set the start time before calling <code>prepareToPlay</code> and enable <code>VEKKeyPlayerEnableStartTimeSkipAVSkipSerial</code>. For configuration details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-ios-player-short-video-best-practices#prerender-with-start-time">Pre\-rendering with a specified start time</a>.   </div>
   

* Call `stop` to stop the playback.

   ```objectivec
   [self.engine stop];
   ```
   


<span id="6265e9c6"></span>
## Play only audio

For audio\-only scenarios, the Player SDK can decode and play only audio from a video file. Compared to implementing audio\-only playback in your own business logic, letting the SDK decode only audio is more power\-efficient.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


See the following sample:

```objectivec
// Play only audio
self.videoEngine.radioMode = YES;
// Play both audio and video
self.videoEngine.radioMode = NO;
```


<span id="ac0f04f0"></span>
## Play DASH videos

To play DASH videos smoothly, enable the following options before playing:

```objectivec
[self.videoEngine setOptionForKey:VEKKeyPlayerBashEnabled_BOOL value:@(YES)];
[self.videoEngine setOptionForKey:VEKKeyPlayerDashEnabled_BOOL value:@(YES)];
```


To play standard DASH videos, enable the following options before playing:

```objectivec
// Global setting. Must be called before initializing the SDK.
[TTVideoEngine ls_localServerConfigure].isEnableDashProxy = YES;
[TTVideoEngine ls_start];

// Per-instance setting to enable the DASH proxy for this specific playback.
[self.videoEngine setOptionForKey:VEKKeyEnableDashProxyForVV_BOOL value:@(1)];
```


<span id="796ff499"></span>
## Adjust video layout

The `TTVideoEngine` class provides the following methods for adjusting video layout:

<span id="e303279b"></span>
### Set display mode

Use the `ScaleMode` property to set the video display mode. This is useful when the disparity between the video's aspect ratio and the display view's aspect ratio causes the video to be resized. See the following sample code:

```objectivec
// Use TTVideoEngineScalingModeNone
[self.engine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeNone)]; 
// Use TTVideoEngineScalingModeAspectFit
[self.engine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeAspectFit)]; 
// Use TTVideoEngineScalingModeAspectFill
[self.engine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeAspectFill)]; 
// Use TTVideoEngineScalingModeFill
[self.engine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeFill)];
```


See the following table for the description of video display modes:


|**Enum** |**Description** |
|---|---|
|TTVideoEngineScalingModeNone |The video is not resized at all. If the video is smaller than the display view, black bars may appear. |
|TTVideoEngineScalingModeAspectFit |Resizes the video to fit the box while maintaining its aspect ratio. Any unfilled areas are displayed as black bars. |
|TTVideoEngineScalingModeAspectFill |Resizes the video to fill the box, while maintaining its aspect ratio but often cropping the video in the process. |
|TTVideoEngineScalingModeFill |Resizes the video to fill the box, regardless of its aspect ratio. The video may be distorted as a result. |


<span id="5252182c"></span>
### Rotate the video

Use the `RotateType` property to set the rotation angle. The SDK rotates the video clockwise. You can set the rotation degree as `0`, `90`, `180`, or `270`.

The following sample code shows how to rotate the video:

```objectivec
// Do not rotate the video
[self.engine setOptionForKey:VEKKeyViewRotateType_ENUM value:@(TTVideoEngineRotateTypeNone)]; 
// Rotate the video 90 degrees
[self.engine setOptionForKey:VEKKeyViewRotateType_ENUM value:@(TTVideoEngineRotateType90)]; 
// Rotate the video 180 degrees
[self.engine setOptionForKey:VEKKeyViewRotateType_ENUM value:@(TTVideoEngineRotateType180)]; 
// Rotate the video 270 degrees
[self.engine setOptionForKey:VEKKeyViewRotateType_ENUM value:@(TTVideoEngineRotateType270)];
```


<span id="081c8fef"></span>
### Set mirror mode

Set `MirrorType` to mirror the video horizontally and vertically.

```objectivec
// Do not mirror the video
[self.engine setOptionForKey:VEKKeyViewMirrorType_ENUM value:@(TTVideoEngineMirrorTypeNone)]; 
// Mirror the video horizontally
[self.engine setOptionForKey:VEKKeyViewMirrorType_ENUM value:@(TTVideoEngineMirrorTypeHorizontal)]; 
// Mirror the video vertically
[self.engine setOptionForKey:VEKKeyViewMirrorType_ENUM value:@(TTVideoEngineMirrorTypeVertical)];
```


<span id="a8f03f5c"></span>
## Get playback information

The `TTVideoEngine` class provides the following methods for getting playback information:


* Use the `currentPlaybackTime` property to get the current playback position in seconds.

   ```objectivec
   // In seconds
   NSTimeInterval currentPlaybackTime = self.engine.currentPlaybackTime;
   ```
   

* Use the `duration` property to get the duration of the file in seconds.

   ```objectivec
   // In seconds
   NSTimeInterval duration = self.engine.duration;
   ```
   

* Call `playableDuration` to get the buffering progress.

   ```objectivec
   // In seconds
   NSTimeInterval playableDuration = self.engine.playableDuration; 
   ```
   

* Get the playback progress:

   ```objectivec
   // The SDK implements NSTimer internally for you to get the playback progress
   // You can implement your own NSTimer
   [self.engine addPeriodicTimeObserverForInterval:0.5  queue:dispatch_get_main_queue() usingBlock:^{
       // After getting the current playback progress, playable duration, and whole duration, you can display these information in the progress bar
   }];
   
   // Remove the time observer when the playback finishes
   [self.engine removeTimeObserver];
   ```
   


<span id="d5ac855d"></span>
## Loop the video

To loop the video, set the `looping` property to `YES`.

```objectivec
self.engine.looping = YES;
```


<span id="3b833a62"></span>
## Set playback speed

Set the `playbackSpeed` property to set playback speed. The default value is `1`, and the value range is (0, 3].

```objectivec
self.engine.playbackSpeed = 1.0;
```


<span id="25af64dc"></span>
## Configure audio behavior

<span id="5484eee0"></span>
### Mute

Set the `muted` property as `YES` to mute the video.

```objectivec
// Mute
self.engine.muted = YES;
// Unmute
self.engine.muted = NO;
```


<span id="dd83338d"></span>
### Adjust the volume

We suggest that you call the [system methods](https://developer.apple.com/documentation/avfoundation/avplayer/1390127-volume?language=objc) to adjust the volume. If you want to adjust the volume of the video, set `AudioDevice` before calling `play`.

```objectivec
[self.engine setOptionForKey:VEKKeyPlayerAudioDevice_ENUM value:@(TTVideoEngineDeviceAudioGraph)];
self.engine.volume = 1.0f;
```


<span id="60e86b22"></span>
## Resolution configuration

When you play videos with the Video IDs, the BytePlus VOD server sends the addresses of videos with multiple resolutions to the player. Once the player receives the `videoEngine:fetchedVideoModel:` callback, you can use the `supportedResolutionTypes` property to get the resolution array. The resolution array can be used for implementing the resolution drop\-down menu, which allows viewers to toggle between different resolutions of the videos.

<span id="ef87e3cf"></span>
### Fetching the current resolution

Use the `currentResolution` property to get the resolution that is being used.

```objectivec
TTVideoEngineResolutionType currentType = self.engine.currentResolution;
```


<span id="b5cefbb9"></span>
### Fetching the resolution list

Use the `supportedResolutionTypes` attribute to get the resolution array.

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine fetchedVideoModel:(TTVideoEngineModel *)videoModel {
    // Get the array of available resolutions
    NSArray<NSNumber *> *allResolutions = [self.engine supportedResolutionTypes];
}
```


<span id="1a8ce6ea"></span>
### Switching the resolution


1. Call `configResolution` to set the resolution before starting the playback. If the specified resolution is not supported, the SDK automatically finds the closest resolution.

   ```objectivec
   [self.engine configResolution:TTVideoEngineResolutionTypeFullHD];
   ```
   

2. After starting the playback, you can use the `supportedResolutionTypes` property to get the resolution array and then use the resolution array to implement the resolution drop\-down menu.

   ```objectivec
   NSArray<NSNumber *> *allResolutions = [engine supportedResolutionTypes];
   TTVideoEngineResolutionType useResolution = [[allResolutions objectAtIndex:0] integerValue]; 
   [self.engine configResolution:type withCompletion:^(BOOL success, NSError * _Nullable err, TTVideoEngineResolutionType completeResolution) {
       if (success) {
           NSLog(@"Resolution switch successful");
       } else {
           // The NSError code contains the specific error code.
           // Refer to the error code meanings: https://docs.byteplus.com/en/docs/byteplus-vod/docs-error-code
           // Special case: If resolution switching fails due to an abnormal player state, the error code is -1
           // The callback might trigger on a non-UI thread, so avoid directly executing UI operations within the callback. It's recommended to perform UI operations on the UI thread.
           NSLog(@"Resolution switch failed, error code: %ld", err.code);
       }
   }];
   ```
   


See the following table for the resolutions supported by the player:


|Enum |Video quality |Audio quality |
|---|---|---|
|TTVideoEngineResolutionTypeSD |360p, SD (Standard Definition) |Normal |
|TTVideoEngineResolutionTypeHD |480p, HD (High Definition) |High |
|TTVideoEngineResolutionTypeFullHD |720p, Full HD (Full High Definition) |Very high |
|TTVideoEngineResolutionType1080P |1080p |Original |
|TTVideoEngineResolutionType2K |2K |This enum does not have effect on audio quality. |
|TTVideoEngineResolutionType4K |4K |This enum does not have effect on audio quality. |
|TTVideoEngineResolutionTypeAuto |For DASH videos, the player automatically decides the best resolution based on the viewer's network connection and adjusts the quality of the video throughout playback to minimize the risk of buffering. |This enum does not have effect on audio quality. |


<span id="89dccfee"></span>
## Enabling seamless switching

For frame\-aligned MP4 and HLS videos generated by the VOD service, seamless switching between multiple resolutions during playback is supported to enhance the user experience. The following example code demonstrates how to enable seamless switching in Vid mode:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For information on encoding frame\-aligned videos and enabling seamless switching in DirectUrl mode, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">submit a ticket</a> to our technical support team.</div>


```objectivec
// Seamless switching for HLS playback sources
[self.videoEngine setOptionForKey:VEKKeyPlayerHLSSeamlessSwitchEnable_BOOL value:@(YES)];
[self.videoEngine setOptionForKey:VEKKeyMasterm3u8OptimizeEnable_BOOL value:@(YES)];

// Seamless switching for MP4 playback sources
[self.videoEngine setOptionForKey:VEKKeyPlayerBashEnabled_BOOL value:@(YES)];
[self.videoEngine setOptionForKey:VEKeyPlayerSegmentFormatFlag value:@(TTVideoEngineDashSegmentFlagFormatMp4 | TTVideoEngineDashSegmentFlagFormatFMP4)];
```


<span id="d9fa839e"></span>
## Playing HLS standard encrypted videos

<span id="38f74c9e"></span>
### Server\-side configuration

Before implementing the client\-side playback logic, ensure you have completed the following server\-side configurations.


* **Complete server\-side configuration:**  Set the decryption service, encrypted transcoding and all other preparatory work. For more details, please refer to [HLS standard encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption).

* **Set the correct** \*\*`FileType`: \*\*Different from playing regular videos, your application server must set the `FileType` \*\*\*\* parameter to `standard_evideo` (encrypted video) or `standard_eaudio` (encrypted audio) when calling the `GetPlayInfo` interface to retrieve the playback URL or when issuing a `PlayAuthToken`.


<span id="758fcd38"></span>
### Client\-side implementation


<Tabs>
<Tab zoneid="OPaKu5kw07" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

In this scenario, the client\-side playback code is largely the same as for playing regular Vid videos. The SDK automatically handles the decryption process internally. If you have enabled the[ HLS encryption rewrite](https://docs.byteplus.com/en/docs/byteplus-vod/docs-standard-encryption#step-3-configuring-hls-encryption-rewrite-recommended) feature, you need to additionally set the `urlExtendParams` property to pass the authentication parameter `AppAuthToken`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you enable the HLS encryption rewrite feature, you can pass the <code>AppAuthToken</code> via the <code>urlExtendParams</code> parameter throughout the entire lifecycle of playback, download, and preloading:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Playback</strong>: Set on the <code>TTVideoEngineVidSource</code> object.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Download:</strong> Set on the <code>TTVideoEngineDownloadVidTask</code> object.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Preloading</strong>:</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Custom preloading</strong>: Set the <code>urlExtendParams</code> property on the <code>TTVideoEnginePreloaderVidItem</code> object.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Preload strategy:</strong> Set the <code>urlExtendParams</code> property to the <code>TTVideoEngineVidSource</code> instance and pass to the preload strategy. The strategy reads and applies the property to the internal preload tasks.</div>



```objectivec
// 1. Prepare basic parameters
NSString *vid = @"your_hls_encrypted_vid";
NSString *playAuthToken = @"your_play_auth_token";

// 2. Construct the Vid playback source
TTVideoEngineVidSource *vidSource = [[TTVideoEngineVidSource alloc] initWithVid:vid playAuthToken:playAuthToken resolution:TTVideoEngineResolutionTypeAuto];

// 3. (Configure as needed) Handle the HLS encryption rewrite scenario
// If "HLS encryption rewrite" is enabled, you must pass your authentication parameters.
// The SDK automatically appends these parameters to the end of the M3U8 file's request URL.
// NSDictionary *authParams = @{ @"AppAuthToken": @"<your_token>" };
// vidSource.urlExtendParams = authParams; 

// 4. Set the playback source and play
[self.engine setVideoEngineVideoSource:vidSource];
[self.engine play];
```



</Tab>
<Tab zoneid="eLQJimiCUb" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

You can directly use `DirectUrlSource` to set the HLS standard encrypted video's M3U8 address. If you have enabled the [HLS encryption rewrite](https://docs.byteplus.com/en/docs/byteplus-vod/docs-standard-encryption#step-3-configuring-hls-encryption-rewrite-recommended) feature, you need to manually append the authentication parameters to the end of the URL and set the URL to the player.

```objectivec
// 1. Obtain the required playback information from your application server
// If "HLS encryption rewrite" is enabled, your application server must append authentication parameters (such as AppAuthToken) and send a complete URL to the client.
// --- URL example ---
// Original URL: https://www.example.com/encrypted_master.m3u8
// The URL sent to the client after enabling "URL encryption rewrite": https://www.example.com/encrypted_master.m3u8?AppAuthToken=<your_token>
NSString *finalUrlFromServer = @"https://www.example.com/encrypted_master.m3u8?AppAuthToken=<your_token>";

NSString *cacheKey = [finalUrlFromServer md5];

// 2. Construct the Url playback source
TTVideoEngineUrlSource *urlSource = [[TTVideoEngineUrlSource alloc] initWithUrl:finalUrlFromServer cacheKey:cacheKey];

// 3. Set the playback source and play
[self.engine setVideoEngineVideoSource:urlSource];
[self.engine play];
```



</Tab>
</Tabs>


<span id="761cabed"></span>
## Setting business tags

Business tags (tag) are used to distinguish between different types of audio and video within the same app (appid). They can be categorized according to business needs, based on video scenario and video duration—for example, immersive feed, short video, or long video. The example code is shown below.

```objectivec
[videoEngine setOptionForKey:VEKKeyLogTag_NSString value:@"tag"];
```


<span id="5717f6fa"></span>
## Setting business subtags

Business subtags (subtag) are used to further distinguish different audio and video types under the same business tag, such as encrypted video, unencrypted video, and audio. The example code is shown below.

```objectivec
[videoEngine setOptionForKey:VEKKeyLogSubTag_NSString value:@"subtag"];
```


<span id="configure-reporting-domain"></span>
## Configure the reporting domain

Player SDK 1.51.300 and later supports configuring the event reporting domain. If you do not configure the reporting domain, the SDK uses its built\-in default reporting domain.


* To use the SDK's built\-in dual\-stack reporting domain, set `builtInIPv6ReportURLEnabled` to `YES`.

* To use a custom IPv4 or IPv6 reporting URL, specify the URL through `customReportURL`. The URL must start with `http://` or `https://`.

* If both settings are configured, the custom reporting URL specified by `customReportURL` takes precedence.


The following sample code shows how to configure the reporting domain:

```objectivec
- (void)initTTSDK {
    // 1. Initialize the configuration.
    TTSDKConfiguration *configuration = nil;

    // 2. Configure the event reporting domain. If you do not configure it, the SDK uses its built-in default reporting domain.
    //    - To use the built-in dual-stack reporting domain, enable builtInIPv6ReportURLEnabled.
    //    - To use a custom IPv4 or IPv6 reporting URL, specify it through customReportURL. The URL must start with http:// or https://.
    //    - If both settings are configured, customReportURL takes precedence.
    configuration.reportConfiguration = [TTSDKReportConfiguration defaultReportConfigurationWithBuiltInIPv6ReportURLEnabled:YES customReportURL:@"https://custom-report-url.com"];

    // 3. Start TTSDK.
    [TTSDKManager startWithConfiguration:configuration];
}
```


<span id="b58bc08a"></span>
## Keep the screen on

To keep the screen on while video playback is occurring, use either of the following approaches:


* Approach one: Set the [idleTimerDisabled](https://developer.apple.com/documentation/uikit/uiapplication/1623070-idletimerdisabled) property of the `UIApplication` class.

   ```objectivec
   [UIApplication sharedApplication].idleTimerDisabled = YES;
   ```
   

* Approach two: Set the `IdleTimerAuto` property of the `TTVideoEngine` class.

   ```objectivec
   [self.videoEngine setOptionForKey:VEKKeyPlayerIdleTimerAuto_NSInteger value:@(YES)];
   ```
   


<span id="9bf3ef7b"></span>
## Playback status callbacks

The following are the key delegate methods for monitoring the player's status.

```objectivec
/**
 * Called when the playback state changes.
 * @param videoEngine The player instance.
 * @param playbackState The new playback state (e.g., playing, paused, stopped).
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine playbackStateDidChanged:(TTVideoEnginePlaybackState)playbackState;

/**
 * Called when playback has actually started and the playhead is advancing.
 */
- (void)videoEngineReadyToPlay:(TTVideoEngine *)videoEngine;

/**
 * Called when playback finishes.
 * @param videoEngine The player instance.
 * @param error An error object if playback failed, or `nil` if it completed successfully.
 */
- (void)videoEngineDidFinish:(TTVideoEngine *)videoEngine error:(nullable NSError *)error;

/**
 * Called after the `stop` method has been called and the player has fully stopped.
 */
- (void)videoEngineUserStopped:(TTVideoEngine *)videoEngine;

/**
 * @brief Called when the loading state changes.
 * @note The SDK calls this method when its internal loading state changes. You can use this callback to show or hide a loading indicator.
 * @param videoEngine The player instance.
 * @param loadState The current loading state. See `TTVideoEngineLoadState`.
 * @param extraInfo A dictionary containing additional details:
 *        - `TTVideoEngineBufferStartAction`: The action that caused the buffering. See `TTVideoEngineStallAction`.
 *        - `TTVideoEngineBufferStartReason`: The specific reason for the buffering. See `TTVideoEngineStallReason`.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine
loadStateDidChanged:(TTVideoEngineLoadState)loadState
              extra:(nullable NSDictionary<NSString *,id> *)extraInfo {
    if (loadState == TTVideoEngineLoadStateStalled) {
        // Buffering has started. You can show a loading indicator here.
    } else if (loadState == TTVideoEngineLoadStatePlayable) {
        // Buffering has ended and playback is smooth. You can hide the loading indicator.
    }              
}

/**
 * @brief Reports the progress of the video buffer.
 * @note The SDK calls this method periodically as the buffer fills. You can use this to display a more detailed loading progress indicator.
 * @param videoEngine The player instance.
 * @param progress The current buffer progress, ranging from 0.0 to 1.0.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine
    loadingProgress:(CGFloat)progress {
    // Update your loading progress UI with the new progress value.    
}

/**
 * Called when playback has stalled due to buffering (this excludes stalls caused by seeking).
 */
- (void)videoEngineStalledExcludeSeek:(TTVideoEngine *)videoEngine;

/**
 * Called when the player has finished preparing all necessary components and is ready to start playing.
 */
- (void)videoEnginePrepared:(TTVideoEngine *)videoEngine;
  
/**
 * Called when the first frame of the video is rendered. This is the ideal time to hide any cover images or thumbnails.
 */
- (void)videoEngineReadyToDisplay:(TTVideoEngine *)videoEngine;

/**
 * For Vid playback, this is called when the video model (containing URLs and metadata) has been fetched successfully.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine fetchedVideoModel:(TTVideoEngineModel *)videoModel;  

/**
 * For Vid playback, this notifies the delegate which specific `TTVideoEngineURLInfo` from the video model is currently being used for playback.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine usingUrlInfos:(NSArray<TTVideoEngineURLInfo *> *)urlInfos;

/**
 * Provides information about a cache hit for the current playback.
 * A `cacheSize` greater than 0 often indicates that preloaded content is being used.
 * @param key A unique identifier for the cached content.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine mdlKey:(NSString *)key hitCacheSize:(NSInteger)cacheSize;

/**
 * Called when the SDK encounters a recoverable error and is attempting to retry playback internally.
 * @param error The internal error that triggered the retry attempt.
 */
- (void)videoEngine:(TTVideoEngine *)videoEngine retryForError:(NSError *)error;

/**
 * Called after the asynchronous `closeAsync` operation has completed.
 */
- (void)videoEngineCloseAsyncFinish:(TTVideoEngine *)videoEngine;
```


<span id="7fbb7acf"></span>
## Display download speed

The download speed is the speed at which the player fetches video data from the original source. You can display the download speed when the video playback is about to start, the video is seeking to a specified time position, or the video is stuttering.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


See the following sample code:

```objectivec
// 1. Set the delegate
- (void)setPreloadDelegate {
    [TTVideoEngine ls_setPreloadDelegate:self];
}

// 2. The callback for the download speed test
- (void)localServerTestSpeedInfo:(NSTimeInterval)timeInternalMs size:(NSInteger)sizeByte {
    // The time interval of the download speed test, in seconds
    NSTimeInterval time = timeInternalMs / 1000;
    // The size of the data downloaded within the specified time interval, in KB
    CGFloat dataSize = sizeByte / 1024;
    // The calculated download speed (KBps)
    CGFloat downloadSpeed = dataSize / time;
    NSLog(@"localServerTestSpeedInfo callback, timeInternalMs: %@, size: %@, speed: %.1f KB/s", @(timeInternalMs), @(sizeByte), downloadSpeed);
}
```


<span id="5da903f8"></span>
## **Setting network timeout** duration

Refer to the following code snippet to set the network timeout duration for the SDK. It is recommended to set it to 10 seconds.

```objectivec
// 1. Enable network timeout detection
// Set VEGSKeyAlgoOptionUseEngineNetworkTimeout to 1
[TTVideoEngine setGlobalForKey:VEGSKeyAlgoOptionUseEngineNetworkTimeout 
    value:@(1)];

TTVideoEngine* engine = [[TTVideoEngine alloc] initWithOwnPlayer:YES];
// 2. Set network timeout duration (in seconds) for the engine instance
// This example sets it to 10 seconds
[engine setOptionForKey:VEKKeyPlayerOpenTimeOut_NSInteger value:@(10)];
// 3. Disable engine playback failure retry. When playback fails, no retry will be attempted
[engine setOptionForKey:VEKKeyPlayerMaxAccumulatedErrCount_NSInteger value:@(0)];
```


<span id="c9c49314"></span>
## Fetching the device ID

The Player SDK automatically generates a unique device ID by default. You can track the playback records of the device ID on the [Endpoint tracker](https://docs.byteplus.com/docs/byteplus-vod/docs-end-point-tracker). Refer to the following code to fetch the device ID:

```objectivec
// Get device ID
[TTSDKManager getRangersDeviceID];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you have your own user system and want to track the play behavior of individual users using the user ID, you can <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-device-id-ios">iOS Player SDK: Customizing device ID</a>.</div>


<span id="cd004a73"></span>
## 5.1 channel audio playback

To enable playback of 5.1 channel audio, you must enable the following options:

```objectivec
[self.videoEngine setOptionForKey:VEKKeyIsEnableAudioSpatialMixer value:@(1)];
[self.videoEngine setOptionForKey:VEKKeyIsEnableVoiceBlockOpt value:@(2)];
[self.videoEngine setOptionForKey:VEKKeyIsSpatialMixerFullRetryCount value:@(2000)]
```

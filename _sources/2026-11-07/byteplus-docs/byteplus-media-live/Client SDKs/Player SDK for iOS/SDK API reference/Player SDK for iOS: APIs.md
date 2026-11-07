---
title: "Player SDK for iOS: APIs"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api"
---

<span id="TVLManager(VeLivePlayer)"></span>
# TVLManager(VeLivePlayer)

```objectivec
@interface TVLManager (VeLivePlayer)
```


The live player.

<span id="member-property"></span>
## Member Property


|Type |Name |
|---|---|
|id |[observer](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-observer) |
|UIView\* |[playerView](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-playerview) |
|float |[volume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-volume) |
|BOOL |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-isplaying) |


<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|void |[setLogLevel:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setloglevel) |
|NSString\* |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getversion) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|instancetype |[init](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-init) |
|instancetype |[initWithType:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-initwithtype) |
|void |[setConfig:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig) |
|void |[setObserver:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver) |
|void |[setRenderFillMode:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderfillmode) |
|void |[setPlayUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl) |
|void |[setUrlHostIP:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-seturlhostip) |
|void |[setProperty:value:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) |
|void |[setPlayStreamData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) |
|void |[play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) |
|void |[stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop) |
|void |[destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy) |
|int |[isSupportResolutionSwitch:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-issupportresolutionswitch) |
|void |[switchResolution:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) |
|void |[setMute:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setmute) |
|BOOL |[isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-ismute) |
|void |[setRenderRotation:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrenderrotation) |
|void |[setRenderMirror:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) |
|int |[snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-snapshot) |
|void |[enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) |
|void |[enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) |
|void |[setEnableSuperResolution:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) |
|void |[setEnableSharpen:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) |
|VeLivePlayerStreamInfo |[getStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-getstreamlist) |


<span id="instructions"></span>
## Instructions

<span id="TVLManager(VeLivePlayer)-observer"></span>
### observer

```objectivec
@property (nonatomic, weak, readonly, nullable) id<VeLivePlayerObserver> observer;
```


The player observer.

<span id="TVLManager(VeLivePlayer)-playerview"></span>
### playerView

```objectivec
@property (nonatomic, strong, readonly) UIView *playerView;
```


The view used by the player to render video. Add `playerView` to the view hierarchy of your app to display the video content.

<span id="TVLManager(VeLivePlayer)-volume"></span>
### volume

```objectivec
@property (nonatomic, assign) float volume;
```


The player volume. The default value is `1.0`. The value range is [0.0, 1.0].

<span id="TVLManager(VeLivePlayer)-isplaying"></span>
### isPlaying

```objectivec
@property (nonatomic, assign, readonly) BOOL isPlaying;
```


Checks whether the player is playing.

<span id="instructions"></span>
## Instructions

<span id="TVLManager(VeLivePlayer)-setloglevel"></span>
### setLogLevel:

```objectivec
+ (void)setLogLevel:(VeLivePlayerLogLevel)logLevel;
```


Sets the level of the output log.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|logLevel |VeLivePlayerLogLevel |The level of the output log. See [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerLogLevel) for details. |


<span id="TVLManager(VeLivePlayer)-getversion"></span>
### getVersion

```objectivec
+ (NSString *_Nonnull )getVersion;
```


Gets the version number of the Player SDK.

**Return Value**

The version number of the Player SDK.

<span id="TVLManager(VeLivePlayer)-init"></span>
### init

```objectivec
- (instancetype)init;
```


Initializes the player.

<span id="TVLManager(VeLivePlayer)-initwithtype"></span>
### initWithType:

```objectivec
- (instancetype)initWithType:(VeLivePlayerType)type;
```


Initializes the specified type of player.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|type |VeLivePlayerType |The player type. Refer to [VeLivePlayerType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerType) for details. |


<span id="TVLManager(VeLivePlayer)-setconfig"></span>
### setConfig:

```objectivec
- (void)setConfig:(VeLivePlayerConfiguration *_Nonnull)config;
```


Configures player settings, including whether to turn on SEI messaging, hardware decoding, and local DNS prefetch.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |VeLivePlayerConfiguration\* |Player configurations. Refer to [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration) for details. |


**Notes**

Call this method before calling play.

<span id="TVLManager(VeLivePlayer)-setobserver"></span>
### setObserver:

```objectivec
- (void)setObserver:(id<VeLivePlayerObserver> _Nullable)observer;
```


Sets the player observer to listen to the VeLivePlayer's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |id |The player observer. See [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) for details. |


**Notes**

Call this method before calling play.

<span id="TVLManager(VeLivePlayer)-setrenderfillmode"></span>
### setRenderFillMode:

```objectivec
- (void)setRenderFillMode:(VeLivePlayerFillMode)fillMode;
```


Sets the fill mode of the player screen.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|fillMode |VeLivePlayerFillMode |The fill mode of SurfaceView. The default value is `VeLivePlayerFillModeAspectFill`. See [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFillMode) for details. |


**Notes**


* Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) to set the initial fill mode of the player.

* You can call this method during playback to dynamically adjust the fill mode.

    &nbsp;


<span id="setplayurl"></span>
### setPlayUrl:

```objectivec
- (void)setPlayUrl:(NSString *_Nonnull)url;
```


Sets a pull stream address.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|url |NSString\* |The pull stream address. |


**Notes**

Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play).

<span id="TVLManager(VeLivePlayer)-seturlhostip"></span>
### setUrlHostIP:

```objectivec
- (void)setUrlHostIP:(NSDictionary *_Nonnull)hostIpMap;
```


Sets the mapping of domain names to server IP addresses.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|hostIpMap |NSDictionary\* |The mapping of domain names to server IP addresses. The `Map` object uses the domain name as the key, and the corresponding value is a list of IP addresses for the servers associated with that domain. The value is of the `List` type. |


<span id="TVLManager(VeLivePlayer)-setproperty-value"></span>
### setProperty:value:

```objectivec
- (void)setProperty:(NSString *_Nonnull)key value:(id _Nonnull)value;
```


Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |NSString\* |The parameter name of the advanced setting. |
|value |id |The parameter value of the advanced setting. |


<span id="TVLManager(VeLivePlayer)-setplaystreamdata"></span>
### setPlayStreamData:

```objectivec
- (void)setPlayStreamData:(VeLivePlayerStreamData *_Nonnull)streamData;
```


Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamData |VeLivePlayerStreamData\* |Configurations for multiple pull stream addresses. See [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData) for details. |


**Notes**

Call this method before calling play.

<span id="TVLManager(VeLivePlayer)-play"></span>
### play

```objectivec
- (void)play;
```


Starts or resumes playback.

**Notes**

After you call this method, the [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) callback is triggered both when the player finishes preparing for stream pulling and when the first frame is rendered.

<span id="TVLManager(VeLivePlayer)-stop"></span>
### stop

```objectivec
- (void)stop;
```


Stops playback. This method does not destroy the player.

**Notes**

When playback stops after you call this method, the [onPlayerStatusUpdate:status:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) callback is triggered.

<span id="TVLManager(VeLivePlayer)-destroy"></span>
### destroy

```objectivec
- (void)destroy;
```


Stops playback and destroys the player.

<span id="TVLManager(VeLivePlayer)-issupportresolutionswitch"></span>
### isSupportResolutionSwitch:

```objectivec
- (int)isSupportResolutionSwitch:(VeLivePlayerResolution)resolution;
```


Check whether the player currently supports the specified resolution level.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolution |VeLivePlayerResolution |Resolution levels. For details, please refer to [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution). |


**Return Value**


* 0: Supported;

* Others: Not supported. For details of other return values, please refer to [VeLivePlayerSupportResolutionSwitchError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerSupportResolutionSwitchError).

    &nbsp;


<span id="switchresolution"></span>
### switchResolution:

```objectivec
- (void)switchResolution:(VeLivePlayerResolution)resolution;
```


Changes the video resolution.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolution |VeLivePlayerResolution |The video resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution) for details. |


**Return Value**


* `YES`: Success;

* `NO`: Failure.


**Notes**


* Call [setPlayStreamData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplaystreamdata) to set multiple resolutions before calling this method.

* Once the player switches to the new resolution after you call this method, the [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) callback is triggered.

* To avoid black screens or lag when switching resolutions, set [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) to `YES`.

    &nbsp;


<span id="setmute"></span>
### setMute:

```objectivec
- (void)setMute:(BOOL)mute;
```


Sets whether to mute playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |BOOL |Whether to mute playback. The default value is `NO`.<br><br><br>* `YES`: Mute;<br><br>* `NO`: Do not mute. |


<span id="TVLManager(VeLivePlayer)-ismute"></span>
### isMute

```objectivec
- (BOOL)isMute;
```


Checks whether playback is muted.

**Return Value**

Whether playback is muted.


* `YES`: Muted;

* `NO`: Not muted.

    &nbsp;


<span id="setrenderrotation"></span>
### setRenderRotation:

```objectivec
- (void)setRenderRotation:(VeLivePlayerRotation)rotation;
```


Sets the clockwise rotation angle of the video.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rotation |VeLivePlayerRotation |The clockwise rotation angle of the video. Rotation is disabled by default. See [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerRotation) for details. |


**Notes**


* You can change the rotation angle before and during playback.

* Each time this method is called, the player rotates the video based on the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.

    &nbsp;


<span id="setrendermirror"></span>
### setRenderMirror:

```objectivec
- (void)setRenderMirror:(VeLivePlayerMirror)mirror;
```


Configures mirroring settings.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mirror |VeLivePlayerMirror |Mirroring settings. Mirroring is disabled by default. See [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerMirror) for details. |


**Notes**


* You can change the mirroring settings before and during playback.

* Each time this method is called, the player applies the mirroring settings to the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.

    &nbsp;


<span id="snapshot"></span>
### snapshot

```objectivec
- (int)snapshot;
```


Takes a screenshot of the video.

**Return Value**


* 0: Screenshot capturing is allowed;

* VeLivePlayerErrorRefused: Screenshot capturing is not allowed.


**Notes**


* This method only takes effect during playback.

* When a screenshot is captured after you call this method, the [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) callback is triggered containing the `UIImage` object of the screenshot.

    &nbsp;


<span id="enablevideoframeobserver-pixelformat-buffertype"></span>
### enableVideoFrameObserver:pixelFormat:bufferType:

```objectivec
- (void)enableVideoFrameObserver:(BOOL)enable pixelFormat:(VeLivePlayerPixelFormat)pixelFormat bufferType:(VeLivePlayerVideoBufferType)bufferType;
```


Sets the video frame observer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable the video frame callback. The default value is `NO`.<br><br><br>* `YES`: Enable;<br><br>* `NO`: Disable. |
|pixelFormat |VeLivePlayerPixelFormat |The pixel format of the video frame in the callback. See [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerPixelFormat) for details. |
|bufferType |VeLivePlayerVideoBufferType |The encapsulation format of the video data in the callback. See [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoBufferType) for details. |


**Notes**


* You can call this method to subscribe to decoded video data for external rendering.

* After you call this method, the onRenderVideoFrame:videoFrame:is triggered once the SDK receives a video frame. The callback contains detailed information of the video frame.

* If you use external rendering, you need to make sure the video and audio are synchronized.

    &nbsp;


<span id="enableaudioframeobserver-enablerendering"></span>
### enableAudioFrameObserver:enableRendering:

```objectivec
- (void)enableAudioFrameObserver:(BOOL)enable enableRendering:(BOOL)enableRendering;
```


Sets the audio frame observer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable the audio frame callback. The default value is `NO`.<br><br><br>* `YES`: Enable;<br><br>* `NO`: Disable. |
|enableRendering |BOOL |Whether to enable player rendering. The default value is `NO`.<br><br><br>* `YES`: Enable;<br><br>* `NO`: Disable. |


**Notes**


* You can call this method to subscribe to decoded audio data for external rendering.

* After you call this method, the [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) callback is triggered once the SDK receives a audio frame. The callback contains detailed information of the audio frame.

* If you use external rendering, you need to make sure the video and audio are synchronized.

    &nbsp;


<span id="setenablesuperresolution"></span>
### setEnableSuperResolution:

```objectivec
- (void)setEnableSuperResolution:(BOOL)enable;
```


Enables or disables super resolution.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable super resolution. The default value is `NO`.<br><br><br>* `YES`: Turn on;<br><br>* `NO`: Turn off. |


**Notes**


* Call this method after receiving the onFirstVideoFrameRender:isFirstFrame:callback, or during playback.

* Support calling this method during playback to turn on or off super\-resolution.

* If the SDK fails to enable super resolution due to device model, video resolution or frame rate, you will receive the [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error).

    &nbsp;


<span id="setenablesharpen"></span>
### setEnableSharpen:

```objectivec
- (void)setEnableSharpen:(BOOL)enable;
```


Sets whether to enable video sharpening. If enabled, the edges and details in the video become more pronounced, making the visuals appear clearer and more vivid.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |BOOL |Whether to enable video sharpening. The default value is `NO`. Valid values:<br><br><br>* `YES`: Enable.<br><br>* `NO`: Disable. |


<span id="TVLManager(VeLivePlayer)-getstreamlist"></span>
### getStreamList

```objectivec
- (NSArray<VeLivePlayerStreamInfo *> *)getStreamList;
```


Gets the stream information.

**Return Value**

The stream information.

**Notes**


* Call this method when the [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus) (player status) is `VeLivePlayerStatusPrepared`.

* This method is currently only applicable to HLS format streams.


<span id="TVLManager(PictureInPicture)"></span>
# TVLManager(PictureInPicture)

```objective-c
@interface TVLManager (PictureInPicture)
```


Picture\-in\-Picture (PiP) capability for the live player.

<span id="Member Variables"></span>
## Member Variables


|Name |Type |
|---|---|
|[enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) |BOOL |
|[pictureInPictureRequiresLinearPlayback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturerequireslinearplayback) |BOOL |
|[canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) |BOOL |
|[avPictureInPictureController](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-avpictureinpicturecontroller) |AVPictureInPictureController \* |
|[pictureInPictureDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpicturedelegate) |id |
|[pictureInPicturePlaybackDelegate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-pictureinpictureplaybackdelegate) |id |


<span id="Static Functions"></span>
## Static Functions


|Name |Return |
|---|---|
|[isPictureInPictureSupported](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturesupported) |BOOL |
|[isPictureInPictureStarted](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-ispictureinpicturestarted) |BOOL |


<span id="Member Functions"></span>
## Member Functions


|Name |Return |
|---|---|
|[startPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-startpictureinpicture) |void |
|[stopPictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-stoppictureinpicture) |void |
|[invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate) |void |


<span id="Variable Description"></span>
## Variable Description

<span id="TVLManager(PictureInPicture)-enablepictureinpicture"></span>
### enablePictureInPicture

```objective-c
@property (nonatomic, assign) BOOL enablePictureInPicture;
```


Whether to enable the PiP feature. The default value is `NO`.


* `YES`: Enables the PiP feature. Then, you can call PiP\-related methods or set PiP\-related properties.

* `NO`: Disables the PiP feature.


**Note**

Before setting this property to `YES`, make sure the following conditions are met:


* The system is running iOS 15.0 or later.

* The app has enabled **Audio, AirPlay, and Picture in Picture** in **Background Modes**.


<span id="TVLManager(PictureInPicture)-pictureinpicturerequireslinearplayback"></span>
### pictureInPictureRequiresLinearPlayback

```objective-c
@property (nonatomic, assign) BOOL pictureInPictureRequiresLinearPlayback;
```


Whether fast\-forward and rewind buttons are hidden in the PiP window. The default value is `YES`. Valid values:


* `YES`: Fast\-forward and rewind buttons are hidden.

* `NO`: Fast\-forward and rewind buttons are shown.


<span id="TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline"></span>
### canStartPictureInPictureAutomaticallyFromInline

```objective-c
@property (nonatomic, assign) BOOL canStartPictureInPictureAutomaticallyFromInline;
```


Whether PiP can start automatically when the app moves to the background. The default value is `YES`. Valid values:


* `YES`: Allows the system to attempt to start PiP automatically when the app moves to the background.

* `NO`: Prevents the system from starting PiP automatically when the app moves to the background.


<span id="TVLManager(PictureInPicture)-avpictureinpicturecontroller"></span>
### avPictureInPictureController

```objective-c
@property (nonatomic, strong, readonly, nullable) AVPictureInPictureController *avPictureInPictureController;
```


The [AVPictureInPictureController](https://developer.apple.com/documentation/AVKit/AVPictureInPictureController) instance associated with the current player, which can be used to read system\-level PiP state and related information.

<span id="TVLManager(PictureInPicture)-pictureinpicturedelegate"></span>
### pictureInPictureDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate API_AVAILABLE(ios(15.0));
```


The delegate object that implements [AVPictureInPictureControllerDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturecontrollerdelegate), which is used to receive PiP lifecycle callbacks, such as start, stop, and failure events.

**Note**

The SDK provides basic PiP features. To customize the handling of related delegate callbacks, set this property to your delegate object. This property takes effect only when the following conditions are met at the same time:


* The system is running iOS 15.0 or later.

* The [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) property is set to `YES`.


<span id="TVLManager(PictureInPicture)-pictureinpictureplaybackdelegate"></span>
### pictureInPicturePlaybackDelegate

```objective-c
@property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate API_AVAILABLE(ios(15.0));
```


The delegate object that implements [AVPictureInPictureSampleBufferPlaybackDelegate](https://developer.apple.com/documentation/avkit/avpictureinpicturesamplebufferplaybackdelegate), which is used to handle play and pause requests in PiP, determine whether the playback controls in the PiP window should display Play or Pause, and provide the playable time range.

**Note**

The SDK provides basic PiP features. To customize the handling of related delegate callbacks, set this property to your delegate object. This property takes effect only when the following conditions are met at the same time:


* The system is running iOS 15.0 or later.

* The [enablePictureInPicture](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-enablepictureinpicture) property is set to `YES`.


<span id="Function Description"></span>
## Function Description

<span id="TVLManager(PictureInPicture)-ispictureinpicturesupported"></span>
### isPictureInPictureSupported

```objective-c
+ (BOOL) isPictureInPictureSupported;
```


Whether PiP is supported on the current device.

**Return Value**


* `YES`: Supported.

* `NO`: Not supported.


<span id="TVLManager(PictureInPicture)-ispictureinpicturestarted"></span>
### isPictureInPictureStarted

```objective-c
+ (BOOL) isPictureInPictureStarted;
```


Whether PiP has started successfully.

**Return Value**


* `YES`: PiP has started successfully.

* `NO`: PiP has not started.


<span id="TVLManager(PictureInPicture)-startpictureinpicture"></span>
### startPictureInPicture

```objective-c
- (void) startPictureInPicture;
```


Manually start PiP.

<span id="TVLManager(PictureInPicture)-stoppictureinpicture"></span>
### stopPictureInPicture

```objective-c
- (void) stopPictureInPicture;
```


Manually stop PiP and close the PiP window.

<span id="TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate"></span>
### invalidatePictureInPicturePlaybackState

```objective-c
- (void) invalidatePictureInPicturePlaybackState;
```


Manually update the play/pause button state and progress display in the PiP window.

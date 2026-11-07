---
title: "Player SDK for iOS: Callbacks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback"
---

 &nbsp;

<span id="veliveplayerobserver"></span>
# VeLivePlayerObserver

```objectivec
@protocol VeLivePlayerObserver <NSObject>
```


The live player observer.

 &nbsp;

<span id="member-functions"></span>
## Member Functions

&nbsp;


|Return |Name |
|---|---|
|void |[onError:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) |
|void |[onInfo:info:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info) |
|void |[onFirstVideoFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstvideoframerender-isfirstframe) |
|void |[onFirstAudioFrameRender:isFirstFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onfirstaudioframerender-isfirstframe) |
|void |[onStallStart:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallstart) |
|void |[onStallEnd:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstallend) |
|void |[onVideoRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideorenderstall-stalltime) |
|void |[onAudioRenderStall:stallTime:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onaudiorenderstall-stalltime) |
|void |[onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) |
|void |[onVideoSizeChanged:width:height:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onvideosizechanged-width-height) |
|void |[onReceiveSeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) |
|void |[onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) |
|void |[onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error) |
|void |[onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo) |
|void |[onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status) |
|void |[onPlayerStatusUpdate:status:extraInfo:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status-extrainfo) |
|void |[onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) |
|void |[onSnapshotComplete:image:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onsnapshotcomplete-image) |
|void |[onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) |
|void |[onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) |
|void |[onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) |
|nullable NSData\* |[getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloadercertificatedata) |
|nullable NSString\* |[getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-getdrmresourceloaderlicenseurl) |


 &nbsp;

<span id="instructions"></span>
## Instructions

 &nbsp;

<span id="onerror:error:"></span>
### onError:error:

```objectivec
- (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
```


Occurs when a player error occurs.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|error |VeLivePlayerError\* |The error message. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError) for details. |


 &nbsp;

<span id="oninfo:info:"></span>
### onInfo:info:

```objectivec
- (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
```


Triggered when the player encounters an internal error.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback. See [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)) for details. |
|info |VeLivePlayerError\* |The player information. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError) for details. |


 &nbsp;

<span id="onfirstvideoframerender:isfirstframe:"></span>
### onFirstVideoFrameRender:isFirstFrame:

```objectivec
- (void)onFirstVideoFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```


Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|isFirstFrame |BOOL |Whether the video frame is the first video frame rendered at the beginning of playback.<br><br><br>* `YES`: The video frame is the first video frame rendered at the beginning of playback;<br><br>* `NO`: The video frame is the first video frame rendered after a retry during playback. |


 &nbsp;

<span id="onfirstaudioframerender:isfirstframe:"></span>
### onFirstAudioFrameRender:isFirstFrame:

```objectivec
- (void)onFirstAudioFrameRender:(TVLManager *_Nonnull)player isFirstFrame:(BOOL)isFirstFrame;
```


Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|isFirstFrame |BOOL |Whether the audio frame is the first audio frame rendered at the beginning of playback.<br><br><br>* `YES`: The audio frame is the first audio frame rendered at the beginning of playback;<br><br>* `NO`: The audio frame is the first audio frame rendered after a retry during playback. |


 &nbsp;

<span id="onstallstart:"></span>
### onStallStart:

```objectivec
- (void)onStallStart:(TVLManager *_Nonnull)player;
```


Occurs when a playback stutter starts.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |


 &nbsp;

<span id="onstallend:"></span>
### onStallEnd:

```objectivec
- (void)onStallEnd:(TVLManager *_Nonnull)player;
```


Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |


 &nbsp;

<span id="onvideorenderstall:stalltime:"></span>
### onVideoRenderStall:stallTime:

```objectivec
- (void)onVideoRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```


Occurs when video rendering stutters.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|stallTime |int64_t |The stutter duration, in milliseconds. |


 &nbsp;

<span id="onaudiorenderstall:stalltime:"></span>
### onAudioRenderStall:stallTime:

```objectivec
- (void)onAudioRenderStall:(TVLManager *_Nonnull)player stallTime:(int64_t)stallTime;
```


Occurs when audio rendering stutters.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|stallTime |int64_t |The stutter duration, in milliseconds. |


 &nbsp;

<span id="onresolutionswitch:resolution:error:reason:"></span>
### onResolutionSwitch:resolution:error:reason:

```objectivec
- (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
```


Occurs when the video resolution changes.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|resolution |VeLivePlayerResolution |The updated resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolution) for details. |
|error |VeLivePlayerError\* |Whether an error occurred during resolution switching. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError) for details. |
|reason |VeLivePlayerResolutionSwitchReason |The reason for resolution switching. See [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerResolutionSwitchReason) for details. |


 &nbsp;

<span id="onvideosizechanged:width:height:"></span>
### onVideoSizeChanged:width:height:

```objectivec
- (void)onVideoSizeChanged:(TVLManager *_Nonnull)player width:(int)width height:(int)height;
```


Occurs when the video size changes.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|width |int |The updated width of the video, in pixels. |
|height |int |The updated height of the video, in pixels. |


 &nbsp;

<span id="onreceiveseimessage:message:"></span>
### onReceiveSeiMessage:message:

```objectivec
- (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message;
```


String SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableSei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|message |NSString\* |The SEI message. |


 &nbsp;

<span id="onreceivebinaryseimessage:message:"></span>
### onReceiveBinarySeiMessage:message:

```objectivec
- (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message;
```


Binary SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableBinarySei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|message |NSData\* |The SEI message. |


 &nbsp;

<span id="onmainbackupswitch:streamtype:error:"></span>
### onMainBackupSwitch:streamType:error:

```objectivec
- (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
```


Occurs when the player switches between the primary stream and the backup stream.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|streamType |VeLivePlayerStreamType |The type of the updated stream. See [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamType) for details. |
|error |VeLivePlayerError\* |The reason for the switch. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError) for details. |


 &nbsp;

<span id="onstreamformatswitch:fromstreamformat:tostreamformat:error:extrainfo:"></span>
### onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:

```objectivec
- (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(nullable NSDictionary *)extraInfo;
```


Triggered when the player switches the stream format.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback. See [TVLManager](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)) for details. |
|fromStreamType |VeLivePlayerFormat |The stream format before switching. See [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat) for details. |
|toStreamType |VeLivePlayerFormat |The stream format after switching. See [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerFormat) for details. |
|error |VeLivePlayerError\* |The reason for the stream format switching. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerError) for details. |
|extraInfo |nullable NSDictionary\* |Additional information containing detailed data related to the switching. |


 &nbsp;

<span id="onplayerstatusupdate:status:"></span>
### onPlayerStatusUpdate:status:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status;
```


Occurs when the playback status changes.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player whose playback status changes. |
|status |VeLivePlayerStatus |The updated status of the player. See [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus) for details. |


 &nbsp;

<span id="onplayerstatusupdate:status:extrainfo:"></span>
### onPlayerStatusUpdate:status:extraInfo:

```objectivec
- (void)onPlayerStatusUpdate:(TVLManager *_Nonnull)player status:(VeLivePlayerStatus)status extraInfo:(nullable NSDictionary *)extraInfo;
```


Occurs when the playback status changes. Compared with [onPlayerStatusUpdate:status:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onplayerstatusupdate-status), this callback returns supplemental information about the current playback stream through `extraInfo`.

**Input Parameters**

&nbsp;


|Parameter Name |Type |Description |
|---|---|---|
|player |TVLManager\* |The player whose playback status changes. |
|status |VeLivePlayerStatus |The updated status of the player. See [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatus) for details. |
|extraInfo |nullable NSDictionary\* |A dictionary of supplemental information about the current playback stream. The dictionary may contain the following keys:<br><br><br>* `url` (NSString): The URL of the stream that is currently playing.<br><br>* `all_resolution_urls` (NSDictionary<NSString \*, NSString \*\>): Playback address mapping for all resolutions. The `Key` is the resolution identifier, and the `Value` is the corresponding playback URL. This key is present only when the current stream is a multi\-resolution stream.<br><br>* `resolution` (NSString): The resolution identifier of the currently playing stream. This key is present only when the current stream is a multi\-resolution stream.<br><br>* `enable_abr` (NSNumber): Whether Adaptive Bitrate (ABR) is enabled. This key is present only when the current stream is a multi\-resolution stream. Valid values:<br><br>   * `YES`: Enabled.<br><br>   * `NO`: Disabled.<br><br>* `enable_smooth_switch_resolution` (NSNumber): Whether smooth resolution switching is enabled. This key is present only when the current stream is a multi\-resolution stream. Valid values:<br><br>   * `YES`: Enabled.<br><br>   * `NO`: Disabled.<br><br>* `max_retry_count` (NSNumber, NSInteger): The maximum retry count of the current stream.<br><br>* `retry_interval_time_ms` (NSNumber, NSInteger): The retry interval of the current stream, in milliseconds.<br><br>* `priority` (NSNumber, NSInteger): The priority of the current stream in the pull\-stream list. |


 &nbsp;

<span id="onstatistics:statistics:"></span>
### onStatistics:statistics:

```objectivec
- (void)onStatistics:(TVLManager *_Nonnull)player statistics:(VeLivePlayerStatistics *_Nonnull)statistics;
```


Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|statistics |VeLivePlayerStatistics\* |The playback statistics. See [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics) for details. |


 &nbsp;

<span id="onsnapshotcomplete:image:"></span>
### onSnapshotComplete:image:

```objectivec
- (void)onSnapshotComplete:(TVLManager *_Nonnull)player image:(UIImage *_Nonnull)image;
```


Occurs when a screenshot is taken after snapshot is called.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|image |UIImage\* |The UIImage object of the screenshot. |


 &nbsp;

<span id="onrendervideoframe:videoframe:"></span>
### onRenderVideoFrame:videoFrame:

```objectivec
- (void)onRenderVideoFrame:(TVLManager *_Nonnull)player videoFrame:(VeLivePlayerVideoFrame *_Nonnull)videoFrame;
```


Occurs when the player decodes a video frame. Call [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enablevideoframeobserver-pixelformat-buffertype) to enable video frame callback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|videoFrame |VeLivePlayerVideoFrame\* |The video frame, including the pixel format, encapsulation format, width and height of the video, and other information. See [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerVideoFrame) for details. |


**Notes**

If you use the texture format for external rendering, we recommend that you render the video in the callback thread.

 &nbsp;

<span id="onrenderaudioframe:audioframe:"></span>
### onRenderAudioFrame:audioFrame:

```objectivec
- (void)onRenderAudioFrame:(TVLManager *_Nonnull)player audioFrame:(VeLivePlayerAudioFrame *_Nonnull)audioFrame;
```


Occurs when the player decodes an audio frame. Call [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-enableaudioframeobserver-enablerendering) to enable audio frame callback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|audioFrame |VeLivePlayerAudioFrame\* |The audio frame. See [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-type-definition#VeLivePlayerAudioFrame) for details. |


**Notes**

The audio data returned by the callback is of type Float32 and in big\-endian byte order.

 &nbsp;

<span id="onstreamfailedopensuperresolution:error:"></span>
### onStreamFailedOpenSuperResolution:error:

```objectivec
- (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
```


Occurs when the SDK fails to enable super resolution after [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesuperresolution) is called.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player object that triggers the callback function. |
|error |VeLivePlayerError\* |The reason of the failure. See [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-sdk-for-ios-api-error-code#VeLivePlayerErrorCode) for details. |


 &nbsp;

<span id="getdrmresourceloadercertificatedata:"></span>
### getDrmResourceLoaderCertificateData:

```objectivec
- (nullable NSData *)getDrmResourceLoaderCertificateData:(nonnull TVLManager *_Nonnull)player;
```


You need to return the FairPlay certificate in NSData format in this callback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player instance that triggers the callback. |


 &nbsp;

<span id="getdrmresourceloaderlicenseurl:"></span>
### getDrmResourceLoaderLicenseUrl:

```objectivec
- (nullable NSString *)getDrmResourceLoaderLicenseUrl:(nonnull TVLManager *_Nonnull)player;
```


You need to return the URL of the DRM license in this callback.

**Input Parameters**

&nbsp;


|Name |Type |Instructions |
|---|---|---|
|player |TVLManager\* |The player instance that triggers the callback. |

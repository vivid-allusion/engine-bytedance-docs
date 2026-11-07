---
title: "Player SDK for Android: Callbacks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback"
---

<span id="VeLivePlayerObserver"></span>
# VeLivePlayerObserver

```java
public interface com.ss.videoarch.liveplayer.VeLivePlayerObserver
```


The live player observer.

<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|default void |[onError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onerror) |
|default void |[onInfo](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-oninfo) |
|default void |[onFirstVideoFrameRender](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) |
|default void |[onFirstAudioFrameRender](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onfirstaudioframerender) |
|default void |[onStallStart](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstallstart) |
|default void |[onStallEnd](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstallend) |
|default void |[onVideoRenderStall](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onvideorenderstall) |
|default void |[onAudioRenderStall](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onaudiorenderstall) |
|default void |[onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) |
|default void |[onVideoSizeChanged](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onvideosizechanged) |
|default void |[onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) |
|default void |[onReceiveBinarySeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) |
|default void |[onMainBackupSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch) |
|default void |[onStreamFormatSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch) |
|default void |[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) |
|default void |[onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate-2) |
|default void |[onStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) |
|default void |[onSnapshotComplete](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) |
|default void |[onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) |
|default void |[onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) |
|default void |[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) |
|default void |[onStreamFailedOpenSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayerObserver-onerror"></span>
### onError

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onError(
    VeLivePlayer player,
    VeLivePlayerError error
)
```


Occurs when a player error occurs.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|error |VeLivePlayerError |The error message. Refer to [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError) for details. |


<span id="VeLivePlayerObserver-oninfo"></span>
### onInfo

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onInfo(
    VeLivePlayer player,
    VeLivePlayerError error
)
```


Triggered when the player encounters an internal error.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback. See [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer) for details. |
|error |VeLivePlayerError |The player information. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError) for details. |


<span id="VeLivePlayerObserver-onfirstvideoframerender"></span>
### onFirstVideoFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstVideoFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```


Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|isFirstFrame |boolean |Whether the video frame is the first video frame rendered at the beginning of playback.<br><br><br>* true: The video frame is the first video frame rendered at the beginning of playback;<br><br>* false: The video frame is the first video frame rendered after a retry during playback. |


<span id="VeLivePlayerObserver-onfirstaudioframerender"></span>
### onFirstAudioFrameRender

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onFirstAudioFrameRender(
    VeLivePlayer player,
    boolean isFirstFrame
)
```


Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|isFirstFrame |boolean |Whether the audio frame is the first audio frame rendered at the beginning of playback.<br><br><br>* true: The audio frame is the first audio frame rendered at the beginning of playback;<br><br>* false: The audio frame is the first audio frame rendered after a retry during playback. |


<span id="VeLivePlayerObserver-onstallstart"></span>
### onStallStart

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallStart(VeLivePlayer player)
```


Occurs when a playback stutter starts.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |


<span id="VeLivePlayerObserver-onstallend"></span>
### onStallEnd

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStallEnd(VeLivePlayer player)
```


Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |


<span id="VeLivePlayerObserver-onvideorenderstall"></span>
### onVideoRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoRenderStall(
    VeLivePlayer player,
    long stallTime
)
```


Occurs when video rendering stutters.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|stallTime |long |The stutter duration, in milliseconds. |


<span id="VeLivePlayerObserver-onaudiorenderstall"></span>
### onAudioRenderStall

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onAudioRenderStall(
    VeLivePlayer player,
    long stallTime
)
```


Occurs when audio rendering stutters.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|stallTime |long |The stutter duration, in milliseconds. |


<span id="VeLivePlayerObserver-onresolutionswitch"></span>
### onResolutionSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onResolutionSwitch(
    VeLivePlayer player,
    VeLivePlayerResolution resolution,
    VeLivePlayerError error,
    VeLivePlayerResolutionSwitchReason reason
)
```


Occurs when the video resolution changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|resolution |VeLivePlayerResolution |The updated resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolution) for details. |
|error |VeLivePlayerError |Whether an error occurred during resolution switching. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError) for details. |
|reason |VeLivePlayerResolutionSwitchReason |The reason for resolution switching. See [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerResolutionSwitchReason) for details. |


<span id="VeLivePlayerObserver-onvideosizechanged"></span>
### onVideoSizeChanged

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onVideoSizeChanged(
    VeLivePlayer player,
    int width,
    int height
)
```


Occurs when the video size changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|width |int |The updated width of the video, in pixels. |
|height |int |The updated height of the video, in pixels. |


<span id="VeLivePlayerObserver-onreceiveseimessage"></span>
### onReceiveSeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveSeiMessage(
    VeLivePlayer player,
    String message
)
```


String SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableSei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|message |String |The SEI message. |


<span id="VeLivePlayerObserver-onreceivebinaryseimessage"></span>
### onReceiveBinarySeiMessage

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onReceiveBinarySeiMessage(
    VeLivePlayer player,
    byte[] message
)
```


Binary SEI message callback. This callback is triggered when the player SDK receives an SEI message. It is necessary to enable the `enableBinarySei` property in `VeLivePlayerConfiguration`. When the `enableBinarySei` property is enabled, the string SEI message will no longer be sent.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|message |byte[] |The SEI message. |


<span id="VeLivePlayerObserver-onmainbackupswitch"></span>
### onMainBackupSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onMainBackupSwitch(
    VeLivePlayer player,
    VeLivePlayerStreamType streamType,
    VeLivePlayerError error
)
```


Occurs when the player switches between the primary stream and the backup stream.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|streamType |VeLivePlayerStreamType |The type of the updated stream. For details, see [VeLivePlayerStreamType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamType). |
|error |VeLivePlayerError |The reason for the switch. For details, see [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError). |


<span id="VeLivePlayerObserver-onstreamformatswitch"></span>
### onStreamFormatSwitch

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFormatSwitch(
    VeLivePlayer player,
    VeLivePlayerFormat fromStreamFormat,
    VeLivePlayerFormat toStreamFormat,
    VeLivePlayerError error,
    Bundle extraInfo
)
```


Triggered when the player switches the stream format.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback. See [VeLivePlayer](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer) for details. |
|fromStreamFormat |VeLivePlayerFormat |The stream format before switching. See [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat) for details. |
|toStreamFormat |VeLivePlayerFormat |The stream format after switching. See [VeLivePlayerFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFormat) for details. |
|error |VeLivePlayerError |The reason for the stream format switching. See [VeLivePlayerError](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerError) for details. |
|extraInfo |Bundle |Additional information containing detailed data related to the switching. |


<span id="VeLivePlayerObserver-onplayerstatusupdate"></span>
### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status
)
```


Occurs when the playback status changes.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player whose playback status changes. |
|status |VeLivePlayerStatus |The updated status of the player. See [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus) for details. |


<span id="VeLivePlayerObserver-onplayerstatusupdate-2"></span>
### onPlayerStatusUpdate

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onPlayerStatusUpdate(
    VeLivePlayer player,
    VeLivePlayerStatus status,
    Bundle extraInfo
)
```


Occurs when the playback status changes. Compared with [onPlayerStatusUpdate](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate), this callback returns supplemental information about the current playback stream through `extraInfo`.

**Input Parameters**


|Parameter Name |Type |Description |
|---|---|---|
|player |VeLivePlayer |The player whose playback status changes. |
|status |VeLivePlayerStatus |The updated status of the player. See [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus) for details. |
|extraInfo |Bundle |A Bundle of supplemental information about the current playback stream. The Bundle may contain the following keys:<br><br><br>* `url` (String): The URL of the stream that is currently playing.<br><br>* `all_resolution_urls` (Bundle): Playback address mapping for all resolutions. The `Key` is the resolution identifier, and the `Value` is the corresponding playback URL. This key is present only when the current stream is a multi\-resolution stream.<br><br>* `resolution` (String): The resolution identifier of the currently playing stream. This key is present only when the current stream is a multi\-resolution stream.<br><br>* `enable_abr` (boolean): Whether Adaptive Bitrate (ABR) is enabled. This key is present only when the current stream is a multi\-resolution stream. Valid values:<br><br>   * `true`: Enabled.<br><br>   * `false`: Disabled.<br><br>* `enable_smooth_switch_resolution` (boolean): Whether smooth resolution switching is enabled. This key is present only when the current stream is a multi\-resolution stream. Valid values:<br><br>   * `true`: Enabled.<br><br>   * `false`: Disabled.<br><br>* `max_retry_count` (int): The maximum retry count of the current stream.<br><br>* `retry_interval_time_ms` (int): The retry interval of the current stream, in milliseconds.<br><br>* `priority` (int): The priority of the current stream in the pull\-stream list. |


<span id="VeLivePlayerObserver-onstatistics"></span>
### onStatistics

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStatistics(
    VeLivePlayer player,
    VeLivePlayerStatistics statistics
)
```


Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|statistics |VeLivePlayerStatistics |The playback statistics. For details, see [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatistics). |


<span id="VeLivePlayerObserver-onsnapshotcomplete"></span>
### onSnapshotComplete

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onSnapshotComplete(
    VeLivePlayer player,
    Bitmap bitmap
)
```


Occurs when a screenshot is taken after [snapshot](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-snapshot) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|bitmap |Bitmap |The Bitmap object of the screenshot. |


<span id="VeLivePlayerObserver-onrendervideoframe"></span>
### onRenderVideoFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderVideoFrame(
    VeLivePlayer player,
    VeLivePlayerVideoFrame videoFrame
)
```


Occurs when the player decodes a video frame. Call [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) to enable video frame callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|videoFrame |VeLivePlayerVideoFrame |The video frame, including the pixel format, encapsulation format, width and height of the video, and other information. See [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoFrame) for details. |


**Notes**

If you use the texture format for external rendering, we recommend that you render the video in the callback thread.

<span id="VeLivePlayerObserver-onrenderaudioframe"></span>
### onRenderAudioFrame

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onRenderAudioFrame(
    VeLivePlayer player,
    VeLivePlayerAudioFrame audioFrame
)
```


Occurs when the player decodes an audio frame. Call [enableAudioFrameObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) to enable audio frame callback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|audioFrame |VeLivePlayerAudioFrame |The audio frame. See [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioFrame) for details. |


**Notes**

The audio data returned by the callback is of type Float32 and in big\-endian byte order.

<span id="VeLivePlayerObserver-onstreamfailedopensuperresolution"></span>
### onStreamFailedOpenSuperResolution

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSuperResolution(
    VeLivePlayer player,
    VeLivePlayerError error
)
```


Occurs when the SDK fails to enable super resolution after [setEnableSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|error |VeLivePlayerError |The reason of the failure. See [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode) for details. |


<span id="VeLivePlayerObserver-onstreamfailedopensharpen"></span>
### onStreamFailedOpenSharpen

```java
default void com.ss.videoarch.liveplayer.VeLivePlayerObserver.onStreamFailedOpenSharpen(
    VeLivePlayer player,
    VeLivePlayerError error
)
```


Occurs when the SDK fails to enable sharpen after [setEnableSharpen](https://docs.byteplus.com/en/docs/24/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) is called.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|player |VeLivePlayer |The player object that triggers the callback function. |
|error |VeLivePlayerError |The reason of the failure. See VeLivePlayerErrorCode for details. |

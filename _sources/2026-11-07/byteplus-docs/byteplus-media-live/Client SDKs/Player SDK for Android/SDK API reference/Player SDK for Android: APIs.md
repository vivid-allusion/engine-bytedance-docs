---
title: "Player SDK for Android: APIs"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference"
---

<span id="VeLivePlayer"></span>
# VeLivePlayer

```java
public abstract class com.ss.videoarch.liveplayer.VeLivePlayer
```


The live player.

<span id="static-functions"></span>
## Static Functions


|Return |Name |
|---|---|
|static String |[getVersion](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getversion) |
|static void |[setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) |


<span id="member-functions"></span>
## Member Functions


|Return |Name |
|---|---|
|abstract void |[setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) |
|abstract void |[setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) |
|abstract void |[setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) |
|abstract void |[setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) |
|abstract void |[setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) |
|abstract void |[setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) |
|abstract void |[setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) |
|abstract void |[play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) |
|abstract void |[stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) |
|abstract void |[destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) |
|abstract boolean |[switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) |
|abstract boolean |[isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) |
|abstract void |[setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) |
|abstract void |[setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) |
|abstract boolean |[isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute) |
|abstract void |[setUrlHostIP](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) |
|abstract void |[setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) |
|abstract int |[snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) |
|abstract void |[enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) |
|abstract void |[enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) |
|abstract void |[setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) |
|abstract void |[setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) |
|abstract void |[setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) |
|abstract void |[setEnableSharpen](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) |
|abstract ArrayList |[getStreamList](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-getstreamlist) |


<span id="instructions"></span>
## Instructions

<span id="VeLivePlayer-getversion"></span>
### getVersion

```java
public static String com.ss.videoarch.liveplayer.VeLivePlayer.getVersion()
```


Gets the version number of the Player SDK.

**Return Value**

The version number of the Player SDK.

<span id="VeLivePlayer-setloglevel"></span>
### setLogLevel

```java
public static void com.ss.videoarch.liveplayer.VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel logLevel)
```


Sets the level of the output log.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|logLevel |VeLivePlayerLogConfig.VeLivePlayerLogLevel |The level of the output log. For details, see [VeLivePlayerLogLevel](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerLogLevel). |


<span id="VeLivePlayer-setconfig"></span>
### setConfig

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setConfig(VeLivePlayerConfiguration config)
```


Initializes the player and configures whether to turn on SEI messaging, hardware decoding, local DNS prefetch, and other configurations.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|config |VeLivePlayerConfiguration |Player configurations. Refer to [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration) for details. |


**Notes**

Call this method to initialize the player before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) .

<span id="VeLivePlayer-setobserver"></span>
### setObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setObserver(VeLivePlayerObserver observer)
```


Sets the player observer to listen to the live player's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|observer |VeLivePlayerObserver |The player observer. See [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver) for details. |


**Notes**

Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play).

<span id="VeLivePlayer-setrenderfillmode"></span>
### setRenderFillMode

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderFillMode(VeLivePlayerFillMode fillMode)
```


Sets the fill mode of the player screen.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|fillMode |VeLivePlayerFillMode |The fill mode of SurfaceView. The default value is `VeLivePlayerFillModeAspectFill`. For details, see [VeLivePlayerFillMode](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerFillMode). |


**Notes**


* Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) to set the initial fill mode of the player.

* You can call this method during playback to dynamically adjust the fill mode.

    &nbsp;


<span id="setsurfaceholder"></span>
### setSurfaceHolder

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurfaceHolder(SurfaceHolder surfaceHolder)
```


Sets the `SurfaceHolder` object for video rendering and playback. Use this method if you use `SurfaceView` for playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|surfaceHolder |SurfaceHolder |The `SurfaceHolder` object. |


**Notes**

If you call both setSurfaceHolder and [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) to set the `Surface` object, the player will prioritize the configurations of `surfaceHolder`.

<span id="VeLivePlayer-setsurface"></span>
### setSurface

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setSurface(Surface surface)
```


Sets the `Surface` object for video rendering and playback. Use this method if you use `SurfaceView` or `TextureView` for playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|surface |Surface |The `Surface` object. |


**Notes**

If you call both [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) and `setSurface` to set the `Surface` object, the player will prioritize the configurations of `surfaceHolder`.

<span id="VeLivePlayer-setplayurl"></span>
### setPlayUrl

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayUrl(String url)
```


Sets a pull stream address.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|url |String |The pull stream address. |


**Notes**

Call this method before calling play.

<span id="VeLivePlayer-setplaystreamdata"></span>
### setPlayStreamData

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayStreamData(VeLivePlayerStreamData streamData)
```


Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|streamData |VeLivePlayerStreamData |Configurations for multiple pull stream addresses. For details, see [VeLivePlayerStreamData](https://docs.byteplus.com/en/docs/24/player-android-api-keytype#VeLivePlayerStreamData). |


**Notes**

Call this method before calling play.

<span id="VeLivePlayer-play"></span>
### play

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.play()
```


Starts or resumes playback.

**Notes**

After you call this method, the [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) callback is triggered both when the player finishes preparing for stream pulling and when the first frame is rendered.

<span id="VeLivePlayer-stop"></span>
### stop

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.stop()
```


Stops playback. This method does not destroy the player.

**Notes**

When playback stops after you call this method, the [onPlayerStatusUpdate](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onplayerstatusupdate) callback is triggered.

<span id="VeLivePlayer-destroy"></span>
### destroy

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.destroy()
```


Stops playback and destroys the player.

<span id="VeLivePlayer-switchresolution"></span>
### switchResolution

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.switchResolution(VeLivePlayerResolution resolution)
```


Changes the video resolution.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|resolution |VeLivePlayerResolution |The video resolution. For details, refer to VeLivePlayerResolution. |


**Return Value**


* true: Success;

* false: Failure.


**Notes**


* Call [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) to set multiple resolutions before calling this method.

* Once the player switches to the new resolution after you call this method, the [onResolutionSwitch](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) callback is triggered.

* To avoid black screens or lag when switching resolutions, set [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) to `true`.

    &nbsp;


<span id="isplaying"></span>
### isPlaying

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isPlaying()
```


Checks whether the player is playing.

**Return Value**

Whether the player is playing.


* true: The player is playing;

* false: The player is not playing.

    &nbsp;


<span id="setplayervolume"></span>
### setPlayerVolume

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setPlayerVolume(float volume)
```


Sets the player volume.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|volume |float |The volume. The default value is `1.0`. The value range is [0.0, 1.0]. |


<span id="VeLivePlayer-setmute"></span>
### setMute

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setMute(boolean mute)
```


Sets whether to mute playback.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mute |boolean |Whether to mute playback. The default value is `false`.<br><br><br>* true: Mute;<br><br>* false: Do not mute. |


<span id="VeLivePlayer-ismute"></span>
### isMute

```java
public abstract boolean com.ss.videoarch.liveplayer.VeLivePlayer.isMute()
```


Checks whether playback is muted.

**Return Value**

Whether playback is muted.


* true: Muted;

* false: Not muted.

    &nbsp;


<span id="seturlhostip"></span>
### setUrlHostIP

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setUrlHostIP(Map<String, List<String>> hostIpMap)
```


Sets the mapping of domain names to server IP addresses.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|hostIpMap |Map<String, List\> |The mapping of domain names to server IP addresses. The `Map` object uses the domain name as the key, and the corresponding value is a list of IP addresses for the servers associated with that domain. The value is of the `List` type. |


**Notes**


* When using setUrlHostIP to map domain names and IP addresses, disable the DNS pre\-resolution feature in the initial configuration by setting [enableLiveDNS](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablelivedns) to false.

* Call this method to set the mapping of domain names and IP addresses before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) to start playback.

    &nbsp;


<span id="setproperty"></span>
### setProperty

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setProperty(
    String key,
    Object value
)
```


Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|key |String |The parameter name of the advanced setting. |
|value |Object |The parameter value of the advanced setting. |


<span id="VeLivePlayer-snapshot"></span>
### snapshot

```java
public abstract int com.ss.videoarch.liveplayer.VeLivePlayer.snapshot()
```


Takes a screenshot of the video.

**Return Value**


* 0: Screenshot capturing is allowed.

* [VeLivePlayerErrorRefused](https://docs.byteplus.com/en/docs/24/docs-player-android-api-errorcode#VeLivePlayerErrorCode-veliveplayererrorrefused) : Screenshot capturing is not allowed.


**Notes**


* This method only takes effect during playback.

* When a screenshot is captured after you call this method, the [onSnapshotComplete](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) callback is triggered containing the Bitmap object of the screenshot.

    &nbsp;


<span id="enablevideoframeobserver"></span>
### enableVideoFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableVideoFrameObserver(
    boolean enable,
    VeLivePlayerPixelFormat pixelFormat,
    VeLivePlayerVideoBufferType bufferType
)
```


Sets the video frame observer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable the video frame callback. The default value is `false`.<br><br><br>* true: Enable;<br><br>* false: Disable. |
|pixelFormat |VeLivePlayerPixelFormat |The pixel format of the video frame in the callback. See [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerPixelFormat) for details. |
|bufferType |VeLivePlayerVideoBufferType |The encapsulation format of the video data in the callback. For details, see [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerVideoBufferType). |


**Notes**


* You can call this method to subscribe to decoded video data for external rendering.

* After you call this method, the [onRenderVideoFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) callback is triggered once the SDK receives a video frame. The callback contains detailed information about the video frame.

* If you use external rendering, you need to make sure the video and audio are synchronized.

    &nbsp;


<span id="enableaudioframeobserver"></span>
### enableAudioFrameObserver

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.enableAudioFrameObserver(
    boolean enable,
    boolean enableRendering,
    VeLivePlayerAudioBufferType bufferType
)
```


Sets the audio frame observer.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable the audio frame callback. The default value is `false`.<br><br><br>* true: Enable;<br><br>* false: Disable. |
|enableRendering |boolean |Whether to enable player rendering. The default value is `false`.<br><br><br>* true: Enable;<br><br>* false: Disable. |
|bufferType |VeLivePlayerAudioBufferType |Audio buffer type. For details, please refer to [VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerAudioBufferType). |


**Notes**


* You can call this method to subscribe to decoded audio data if you want to use external rendering.

* After you call this method, the [onRenderAudioFrame](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) callback is triggered once the SDK receives an audio frame. The callback contains detailed information about the audio frame.

* If you use external rendering, you need to make sure the video and audio are synchronized.

    &nbsp;


<span id="setrenderrotation"></span>
### setRenderRotation

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderRotation(VeLivePlayerRotation rotation)
```


Sets the clockwise rotation angle of the video.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|rotation |VeLivePlayerRotation |The clockwise rotation angle of the video. Rotation is disabled by default. See [VeLivePlayerRotation](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerRotation) for details. |


**Notes**


* You can change the rotation angle before and during playback.

* Each time this method is called, the player rotates the video based on the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.

    &nbsp;


<span id="setrendermirror"></span>
### setRenderMirror

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setRenderMirror(VeLivePlayerMirror mirror)
```


Configures mirroring settings.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|mirror |VeLivePlayerMirror |Mirroring settings. Mirroring is disabled by default. See [VeLivePlayerMirror](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerMirror) for details. |


**Notes**


* You can change the mirroring settings before and during playback.

* Each time this method is called, the player applies the mirroring settings to the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.

    &nbsp;


<span id="setenablesuperresolution"></span>
### setEnableSuperResolution

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSuperResolution(boolean enable)
```


Enables or disables super resolution. You must first contact BytePlus [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to activate the feature before using it.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Whether to enable super resolution. The default value is false.<br><br><br>* true: enable;<br><br>* false: disable. |


**Notes**


* Call this method after receiving the [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onfirstvideoframerender) callback, or during playback.

* Support dynamically enabling and disabling super\-resolution by calling this interface during playback.

* If the SDK fails to enable super resolution due to device model, video resolution or frame rate, you will receive the [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/24/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) callback.

    &nbsp;


<span id="setenablesharpen"></span>
### setEnableSharpen

```java
public abstract void com.ss.videoarch.liveplayer.VeLivePlayer.setEnableSharpen(boolean enable)
```


Set whether to enable video sharpening.

**Input Parameters**


|Name |Type |Instructions |
|---|---|---|
|enable |boolean |Set whether to enable video sharpening. The default value is `false`.<br><br><br>* true: Enable;<br><br>* false: Disable. |


<span id="VeLivePlayer-getstreamlist"></span>
### getStreamList

```java
public abstract ArrayList<VeLivePlayerStreamInfo> com.ss.videoarch.liveplayer.VeLivePlayer.getStreamList()
```


Gets the stream information.

**Return Value**

The stream information. For more information, see [VeLivePlayerStreamInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype?lang=en#veliveplayerstreaminfo).

**Notes**


* Call this method when the [VeLivePlayerStatus](https://docs.byteplus.com/en/docs/24/docs-player-android-api-keytype#VeLivePlayerStatus) (player status) is `VeLivePlayerStatusPrepared`.

* This method is currently only applicable to HLS format streams.

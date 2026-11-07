---
title: "Player SDK for React Native: APIs"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api"
---

<span id="veliveplayer"></span>
## VeLivePlayer  

Type：`class`

The live player.

<span id="setconfig"></span>
### setConfig()  

Initializes the player and configures whether to turn on SEI messaging, hardware decoding, local DNS prefetch, and other configurations.

**Notes**

Call this method to initialize the player before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) .

**Type**

```ts
(config: VeLivePlayerConfiguration) => void
```



* **Parameters**

   * **config**

      Type：`VeLivePlayerConfiguration`

      Player configurations. Refer to [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerConfiguration) for details.


<span id="setobserver"></span>
### setObserver()  

Sets the player observer to listen to the live player's events, such as playback errors or status updates, rendering of the first audio and video frame, and resolution switching.

**Notes**

Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play).

**Type**

```ts
(observer: VeLivePlayerObserver) => void
```



* **Parameters**

   * **observer**

      Type：`VeLivePlayerObserver`

      The player observer. See [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerObserver) for details.


<span id="setrenderfillmode"></span>
### setRenderFillMode()  

Sets the fill mode of the player screen.

**Notes**


* Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) to set the initial fill mode of the player.

* You can call this method during playback to dynamically adjust the fill mode.


**Type**

```ts
(fillMode: VeLivePlayerFillMode) => Promise<void>
```



* **Parameters**

   * **fillMode**

      Type：`VeLivePlayerFillMode`

      The fill mode of SurfaceView. The default value is `VeLivePlayerFillModeAspectFill`. For details, see [VeLivePlayerFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerFillMode).


**Return Value**

`Promise<void>`

<span id="setplayurl"></span>
### setPlayUrl()  

Sets a pull stream address.

**Notes**

Call this method before calling play.

**Type**

```ts
(url: string) => void
```



* **Parameters**

   * **url**

      Type：`string`

      The pull stream address.


<span id="setplaystreamdata"></span>
### setPlayStreamData()  

Sets multiple live streams. Call this method if you need to enable features requiring multiple live streams, such as adaptive bitrate (ABR), manual resolution switching, and primary and backup streams.

**Notes**

Call this method before calling play.

**Type**

```ts
(streamData: VeLivePlayerStreamData) => void
```



* **Parameters**

   * **streamData**

      Type：`VeLivePlayerStreamData`

      Configurations for multiple pull stream addresses. For details, see [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerStreamData).


<span id="play"></span>
### play()  

Starts or resumes playback.

**Notes**

After you call this method, the `onPlayerStatusUpdate` callback is triggered both when the player finishes preparing for stream pulling and when the first frame is rendered.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="pause"></span>
### pause()  

Pauses playback.

**Notes**

When playback is paused after you call this method, the `onPlayerStatusUpdate` callback is triggered.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="stop"></span>
### stop()  

Stops playback. This method does not destroy the player.

**Notes**

When playback stops after you call this method, the `onPlayerStatusUpdate` callback is triggered.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="destroy"></span>
### destroy()  

Stops playback and destroys the player.

**Type**

```ts
() => void
```


<span id="switchresolution"></span>
### switchResolution()  

Changes the video resolution.

**Notes**


* Call [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) to set multiple resolutions before calling this method.

* Once the player switches to the new resolution after you call this method, the [onResolutionSwitch](https://docs.byteplus.com/en/docs/24/player-android-api-1317627#veliveplayerobserver-onresolutionswitch) callback is triggered.


**Type**

```ts
(resolution: VeLivePlayerResolution) => void
```



* **Parameters**

   * **resolution**

      Type：`VeLivePlayerResolution`

      The video resolution. For details, refer to [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerResolution).


**Return Value**


* true: Success;

* false: Failure.


<span id="isplaying"></span>
### isPlaying()  

Checks whether the player is playing.

**Type**

```ts
() => boolean
```


**Return Value**

`boolean` Whether the player is playing.


* true: The player is playing;

* false: The player is not playing.


<span id="setplayervolume"></span>
### setPlayerVolume()  

Sets the player volume.

**Type**

```ts
(volume: number) => void
```



* **Parameters**

   * **volume**

      Type：`number`

      The volume. The default value is `1.0`. The value range is [0.0, 1.0].


<span id="setmute"></span>
### setMute()  

Sets whether to mute playback.

**Type**

```ts
(mute: boolean) => void
```



* **Parameters**

   * **mute**

      Type：`boolean`

      Whether to mute playback. The default value is `false`.

      * true: Mute;

      * false: Do not mute.


<span id="ismute"></span>
### isMute()  

Checks whether playback is muted.

**Type**

```ts
() => boolean
```


**Return Value**

`boolean` Whether playback is muted.


* true: Muted;

* false: Not muted.


<span id="setproperty"></span>
### setProperty()  

Configures advanced settings for the player, including offscreen rendering, maximum buffer duration, and adaptive bitrate (ABR) algorithms. Contact BytePlus technical support if you need further information.

**Type**

```ts
(key: string, value: Object) => void
```



* **Parameters**

   * **key**

      Type：`string`

      The parameter name of the advanced setting.

   * **value**

      Type：`Object`

      The parameter value of the advanced setting.


<span id="setrenderrotation"></span>
### setRenderRotation()  

Sets the clockwise rotation angle of the video.

**Notes**


* You can change the rotation angle before and during playback.

* Each time this method is called, the player rotates the video based on the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.


**Type**

```ts
(rotation: VeLivePlayerRotation) => Promise<void>
```



* **Parameters**

   * **rotation**

      Type：`VeLivePlayerRotation`

      The clockwise rotation angle of the video. Rotation is disabled by default. See [VeLivePlayerRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerRotation) for details.


**Return Value**

`Promise<void>`

<span id="setrendermirror"></span>
### setRenderMirror()  

Configures mirroring settings.

**Notes**


* You can change the mirroring settings before and during playback.

* Each time this method is called, the player applies the mirroring settings to the original video.

* When you apply both rotation and mirroring to the video, the player will mirror the video and then rotate it.


**Type**

```ts
(mirror: VeLivePlayerMirror) => Promise<void>
```



* **Parameters**

   * **mirror**

      Type：`VeLivePlayerMirror`

      Mirroring settings. Mirroring is disabled by default. See [VeLivePlayerMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerMirror) for details.


**Return Value**

`Promise<void>`

<span id="setenablesuperresolution"></span>
### setEnableSuperResolution()  

Enables or disables super resolution. You must first contact the BytePlus [technical support](https://www.byteplus.com/en/support) to activate the feature before using it.

**Notes**


* Call this method after receiving the [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/24/1317627#veliveplayerobserver-onFirstVideoFrameRender) callback, or during playback.

* If the SDK fails to enable super resolution due to device model, video resolution or frame rate, you will receive the [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution) callback.


**Type**

```ts
(enable: boolean) => void
```



* **Parameters**

   * **enable**

      Type：`boolean`

      Whether to enable super resolution.


<span id="3bbd9dbc"></span>
### startPictureInPicture()

Starts picture\-in\-picture (PiP) mode and displays the player in a floating window.

**Type**

```TypeScript
(aspectRatio?: number, x?: number, y?: number) => Promise<void>
```



* **Parameters**

   * **aspectRatio**

      Type: `number`

      The aspect ratio (width / height) of the PiP window.

   * **x**

      Type: `number`

      The horizontal offset (in pixels) from the top\-left corner of the screen.

   * **y**

      Type: `number`

      The vertical offset (in pixels) from the top\-left corner of the screen.


**Return Value**

`Promise<void>`

<span id="fb3447d5"></span>
### stopPictureInPicture()

Exits picture\-in\-picture (PiP) mode.

**Typepe**

```TypeScript
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="4b3e1343"></span>
### isPictureInPictureSupported()

Checks whether the current environment supports picture\-in\-picture (PiP) mode.

**Typepe**

```TypeScript
() => boolean
```


**Return Value**

`boolean` Whether PiP is supported.


* true: Supported.

* false: Not supported.


<span id="9727b950"></span>
### setPictureInPictureListener()

Sets the listener for PiP\-related events, such as PiP started, stopped, or errors.

**Type**

```TypeScript
(listener: PictureInPictureManagerListener) => void
```



* **Parameters**

   * **listener**

      Type: `PictureInPictureManagerListener`

      The listener for PiP events.


<span id="a1f76572"></span>
### enablePictureInPicture()

 **(iOS only)**  Enables automatic PiP mode when the app goes into the background.

**Type**

```TypeScript
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="1b8b5910"></span>
### disablePictureInPicture()

 **(iOS only)**  Disables automatic PiP mode.

**Type**

```TypeScript
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="static-getversion"></span>
### `static` getVersion()  

Gets the version number of the Player SDK.

**Type**

```ts
() => string
```


**Return Value**

`string` The version number of the Player SDK.

<span id="static-setloglevel"></span>
### `static` setLogLevel()  

Sets the level of the output log.

**Type**

```ts
(logLevel: VeLivePlayerLogLevel) => void
```



* **Parameters**

   * **logLevel**

      Type：`VeLivePlayerLogLevel`

      The level of the output log. For details, see [VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerLogLevel).

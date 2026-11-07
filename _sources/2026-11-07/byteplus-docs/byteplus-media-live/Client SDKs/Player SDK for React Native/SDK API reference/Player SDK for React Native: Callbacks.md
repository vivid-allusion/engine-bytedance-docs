---
title: "Player SDK for React Native: Callbacks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback"
---

<span id="veliveplayerobserver"></span>
## VeLivePlayerObserver  

Type：`interface`

The live player observer.

<span id="onerror"></span>
### onError  

Occurs when a player error occurs.

**Type**

```ts
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **error**

      Type：`VeLivePlayerError`

      The error message. Refer to [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError) for details.


<span id="onfirstvideoframerender"></span>
### onFirstVideoFrameRender  

Occurs when the first video frame is rendered at the beginning of playback or after a retry during playback.

**Type**

```ts
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **isFirstFrame**

      Type：`boolean`

      Whether the video frame is the first video frame rendered at the beginning of playback.

      * true: The video frame is the first video frame rendered at the beginning of playback;

      * false: The video frame is the first video frame rendered after a retry during playback.


<span id="onfirstaudioframerender"></span>
### onFirstAudioFrameRender  

Occurs when the first audio frame is rendered at the beginning of playback or after a retry during playback.

**Type**

```ts
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **isFirstFrame**

      Type：`boolean`

      Whether the audio frame is the first audio frame rendered at the beginning of playback.

      * true: The audio frame is the first audio frame rendered at the beginning of playback;

      * false: The audio frame is the first audio frame rendered after a retry during playback.


<span id="onstallstart"></span>
### onStallStart  

Occurs when a playback stutter starts.

**Type**

```ts
((player: VeLivePlayer) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.


<span id="onstallend"></span>
### onStallEnd  

Occurs when a playback stutter stops, that is, when playback resumes after there is enough audio buffer.

**Type**

```ts
((player: VeLivePlayer) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.


<span id="onvideorenderstall"></span>
### onVideoRenderStall  

Occurs when video rendering stutters.

**Type**

```ts
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **stallTime**

      Type：`number`

      The stutter duration, in milliseconds.


<span id="onaudiorenderstall"></span>
### onAudioRenderStall  

Occurs when audio rendering stutters.

**Type**

```ts
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **stallTime**

      Type：`number`

      The stutter duration, in milliseconds.


<span id="onresolutionswitch"></span>
### onResolutionSwitch  

Occurs when the video resolution changes.

**Type**

```ts
((player: VeLivePlayer, resolution: VeLivePlayerResolution, error: VeLivePlayerError, reason: VeLivePlayerResolutionSwitchReason) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **resolution**

      Type：`VeLivePlayerResolution`

      The updated resolution. See [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolution) for details.

   * **error**

      Type：`VeLivePlayerError`

      Whether an error occurred during resolution switching. See [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError) for details.

   * **reason**

      Type：`VeLivePlayerResolutionSwitchReason`

      The reason for resolution switching. See [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolutionSwitchReason) for details.


<span id="onvideosizechanged"></span>
### onVideoSizeChanged  

Occurs when the video size changes.

**Type**

```ts
((player: VeLivePlayer, width: number, height: number) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **width**

      Type：`number`

      The updated width of the video, in pixels.

   * **height**

      Type：`number`

      The updated height of the video, in pixels.


<span id="onreceiveseimessage"></span>
### onReceiveSeiMessage  

Occurs when the Player SDK receives an SEI message.

**Type**

```ts
((player: VeLivePlayer, message: string) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **message**

      Type：`string`

      The SEI message.


<span id="onmainbackupswitch"></span>
### onMainBackupSwitch  

Occurs when the player switches between the primary stream and the backup stream.

**Type**

```ts
((player: VeLivePlayer, streamType: VeLivePlayerStreamType, error: VeLivePlayerError) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **streamType**

      Type：`VeLivePlayerStreamType`

      The type of the updated stream. For details, see [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStreamType).

   * **error**

      Type：`VeLivePlayerError`

      The reason for the switch. For details, see [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError).


<span id="onplayerstatusupdate"></span>
### onPlayerStatusUpdate  

Occurs when the playback status changes.

**Type**

```ts
((player: VeLivePlayer, status: VeLivePlayerStatus) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **status**

      Type：`VeLivePlayerStatus`

      The updated status of the player. See [VeLivePlayerStatus](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatus) for details.


<span id="onstatistics"></span>
### onStatistics  

Occurs periodically to report information such as the current pull stream address, bitrate, and frame rate.

**Type**

```ts
((player: VeLivePlayer, statistics: VeLivePlayerStatistics) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **statistics**

      Type：`VeLivePlayerStatistics`

      The playback statistics. For details, see [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatistics).


<span id="onsnapshotcomplete"></span>
### onSnapshotComplete  

Occurs when a screenshot is taken after snapshot is called.

**Type**

```ts
((player: VeLivePlayer, bitmap: any) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **bitmap**

      Type：`any`

      The Bitmap object of the screenshot.


<span id="onrendervideoframe"></span>
### onRenderVideoFrame  

Occurs when the player decodes a video frame. Call [enableVideoFrameObserver](https://docs.byteplus.com/en/docs/24/player-android-api-reference#veliveplayer-enablevideoframeobserver) to enable video frame callback.

**Notes**

If you use the texture format for external rendering, we recommend that you render the video in the callback thread.

**Type**

```ts
((player: VeLivePlayer, videoFrame: VeLivePlayerVideoFrame) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **videoFrame**

      Type：`VeLivePlayerVideoFrame`

      The video frame, including the pixel format, encapsulation format, width and height of the video, and other information. See [VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerVideoFrame) for details.


<span id="onrenderaudioframe"></span>
### onRenderAudioFrame  

Occurs when the player decodes an audio frame. Call enableAudioFrameObserver to enable audio frame callback.

**Notes**

The audio data returned by the callback is of type Float32 and in big\-endian byte order.

**Type**

```ts
((player: VeLivePlayer, audioFrame: VeLivePlayerAudioFrame) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **audioFrame**

      Type：`VeLivePlayerAudioFrame`

      The audio frame. See [VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerAudioFrame) for details.


<span id="onstreamfailedopensuperresolution"></span>
### onStreamFailedOpenSuperResolution

Occurs when the SDK fails to enable super resolution after setEnableSuperResolution is called.

**Type**

```ts
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **Parameters**

   * **player**

      Type：[VeLivePlayer](https://docs.byteplus.com/en/docs/24/1317626#veliveplayer)

      The player object that triggers the callback function.

   * **error**

      Type：`VeLivePlayerError`

      The reason of the failure. See [VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/24/player-android-api-1317628#veliveplayererror-veliveplayererrorcode) for details.


<span id="3668cd54"></span>
## PictureInPictureManagerListener

Type：`interface`

An interface that listens for picture\-in\-picture (PiP) related events, such as status changes or user interactions.

<span id="5c6ba1f3"></span>
### onStartPictureInPicture

Occurs when picture\-in\-picture mode is started.

You can use this callback to update UI status or add analytics tracking.

**Type**

```TypeScript
(() => void) | undefined
```


<span id="b33d5937"></span>
### onStopPictureInPicture

Occurs when picture\-in\-picture mode is exited, either by user action or programmatically.

**Type**

```TypeScript
(() => void) | undefined
```


<span id="a2f98e10"></span>
### onClickPictureInPicture

 **(Android only)**  Occurs when the picture\-in\-picture window is clicked. Use this callback to respond to user interaction with the PiP window.

**Type**

```TypeScript
(() => void) | undefined
```


<span id="a9a4d317"></span>
### onError

Occurs when an error related to picture\-in\-picture mode occurs. Use this callback for error reporting or fallback handling.

**Type**

```TypeScript
((code: number, extraData: any) => void) | undefined
```



* **Parameters**

   * **code**

      Type: `number`

      The error code.

      \* 0: Success

      \* 1: Unsupported

      \* 2: Invalid parameters

      \* 3: PiP is already active

   * **extraData**

      Type: `any`

      Additional data for debugging or error handling.

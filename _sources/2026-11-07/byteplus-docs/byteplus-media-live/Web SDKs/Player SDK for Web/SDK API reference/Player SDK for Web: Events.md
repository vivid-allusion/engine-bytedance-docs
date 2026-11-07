---
title: "Player SDK for Web: Events"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158676"
---

<span id="liveevents"></span>
## LiveEvents  

Type：`enum`


|Name |Value |Description |
|---|---|---|
|PLAY |`'play'` |Video playback starts. |
|PLAYING |`'playing'` |Video playback resumes after a pause or freeze. |
|ENDED |`'ended'` |Video playback ends. |
|PAUSE |`'pause'` |Video playback pauses. |
|ERROR |`'error'` |An error occurs during video playback. |
|TIME_UPDATE |`'timeupdate'` |The video playback time is updated. |
|WAITING |`'waiting'` |The player is loading data. |
|CANPLAY |`'canplay'` |Sufficient data are buffered for video playback. |
|CANPLAY_THROUGH |`'canplaythrough'` |The video can be played smoothly. |
|DURATION_CHANGE |`'durationchange'` |The video duration changes. |
|VOLUME_CHANGE |`'volumechange'` |The video volume changes. |
|LOADED_DATA |`'loadeddata'` |The playback data is loaded. |
|LOAD_START |`'loadstart'` |The video content starts to load. |
|PLAYER_FOCUS |`'focus'` |The player has focus. |
|PLAYER_BLUR |`'blur'` |The player loses focus. |
|READY |`'ready'` |The player is instantiated. |
|AUTOPLAY_STARTED |`'autoplayStarted'` |Autoplay starts successfully. |
|AUTOPLAY_PREVENTED |`'autoplayWasPrevented'` |Autoplay fails to start. |
|COMPLETE |`'complete'` |The player has created the video and the playback is ready to start. |
|REPLAY |`'replay'` |Replay starts. |
|DESTROY |`'destroy'` |The player is destroyed. |
|URL_CHANGE |`'urlchange'` |The playback address changes. |
|FULLSCREEN_CHANGE |`'fullscreenChange'` |The player switches to or from full\-window mode, in which the player covers the entire desktop. |
|CSS_FULLSCREEN_CHANGE |`'cssFullscreenChange'` |The player switches to or from full\-screen mode, in which the player covers the browser window. |
|DEFINITION_CHANGE |`'definitionChange'` |The video resolution changes. |
|VIDEO_RESIZE |`'videoResize'` |The size of the player container changes. |
|PIP_CHANGE |`'pipChange'` |The player switches to or from Picture\-in\-Picture (PIP) mode. |
|ROTATE |`'rotate'` |The player is rotated. |
|USER_ACTION |`'userAction'` |A user event occurs within a built\-in plug\-in. This event applies to all built\-in plug\-ins and can be used for tracking user behaviors. |
|SHORTCUT |`'shortcut'` |A built\-in shortcut event occurs within the player. |
|FALLBACK_ERROR |`'fallbackError'` |The player fails to switch to a backup stream. |
|FALLBACK |`'fallback'` |The player switches to the backup address. |
|AUTOPLAY_UNMUTE |`'autoplayUnmute'` |The user clicks the "Unmute" button. |
|LONG_WAITING |`'longWaiting'` |Long wait. |
|DEFINITION_FALLBACK |`'definitionFallback'` |A resolution downgrade. |
|ERROR_REFRESH_CLICK |`'errorRefreshClick'` |The user clicks the refresh button after an error occurs. |
|SOURCE_CHANGE |`'sourceChange'` |The player switches to another playback source. |
|SEI |`'sei'` |The player parses the SEI information. |
|TIME_SHIFT_CHANGE |`'timeShiftChange'` |The time\-shift state changes. |
|REFRESH_CLICK |`'refreshClick'` |The user clicks the Refresh button. |
|ABR_SWITCH_START |`'abrSwitchStart'` |Event for switching Adaptive Bitrate (ABR) streams. |
|ABR_SWITCH_SUCCESS |`'abrSwitchedSuccess'` |Event of successfully switching Adaptive Bitrate (ABR) live stream. |
|ABR_SWITCH_FAILED |`'abrSwitchFailed'` |Event of failing to switch Adaptive Bitrate (ABR) live stream. |


<span id="liveeventspayload"></span>
## LiveEventsPayload  

Type：`interface`

The data structure for live event callbacks, including playback status, error details, and network updates.

**Example**

```js
VePlayer.createLivePlayer({
 height: 360,
 url: 'https://livepull.example.com/appname/streamname.flv',
}).then(function (veplayer) {
 veplayer.on(VePlayer.live.Events.PLAYER_FOCUS, function (data) {
   console.log('The returned data of the PLAYER_FOCUS event is', data);
 });
 veplayer.once(VePlayer.live.Events.PLAYER_FOCUS, function (data) {
   console.log('The returned data of the PLAYER_FOCUS event is', data);
 });
}).catch(error => {
 console.log('Fails to create the player. The error message:', error);
});
```


<span id="play"></span>
### play  

The playback starts.

**Type**

```ts
() => void
```


<span id="playing"></span>
### playing  

The playback resumes after a pause or freeze.

**Type**

```ts
() => void
```


<span id="ended"></span>
### ended  

The playback ends.

**Type**

```ts
() => void
```


<span id="pause"></span>
### pause  

The playback pauses.

**Type**

```ts
() => void
```


<span id="error"></span>
### error  

An error occurs during the playback.

**Type**

```ts
(error: VeError) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/24/docs-1158675#veerror) |The error object. |


<span id="timeupdate"></span>
### timeupdate  

The video playback time is updated.

**Type**

```ts
() => void
```


<span id="waiting"></span>
### waiting  

The player is loading data.

**Type**

```ts
() => void
```


<span id="canplay"></span>
### canplay  

Sufficient data are buffered for video playback.

**Type**

```ts
() => void
```


<span id="canplaythrough"></span>
### canplaythrough  

The video can be played smoothly.

**Type**

```ts
() => void
```


<span id="durationchange"></span>
### durationchange  

The video duration changes.

**Type**

```ts
() => void
```


<span id="volumechange"></span>
### volumechange  

The video volume changes.

**Type**

```ts
() => void
```


<span id="loadeddata"></span>
### loadeddata  

The playback data is loaded.

**Type**

```ts
() => void
```


<span id="loadstart"></span>
### loadstart  

The video content starts to load.

**Type**

```ts
() => void
```


<span id="focus"></span>
### focus  

The player has focus.

**Type**

```ts
(data: { paused: boolean; ended: boolean; autoHide: boolean; delay: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |Information about the event. |
|paused |boolean |Whether the playback pauses. |
|ended |boolean |Whether the playback ends. |
|autoHide |boolean |Whether to enable auto hiding. |
|delay |number |The latency of auto hiding, in milliseconds. |


<span id="blur"></span>
### blur  

The player loses focus.

**Type**

```ts
(data: { paused: boolean; ended: boolean;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |Information about the event. |
|paused |boolean |Whether the playback pauses. |
|ended |boolean |Whether the playback ends. |


<span id="ready"></span>
### ready  

The player is instantiated.

**Type**

```ts
() => void
```


<span id="autoplaystarted"></span>
### autoplayStarted  

Autoplay starts successfully.

**Type**

```ts
() => void
```


<span id="autoplaywasprevented"></span>
### autoplayWasPrevented  

Autoplay fails to start.

**Type**

```ts
() => void
```


<span id="complete"></span>
### complete  

The player has created the video and the playback is ready to start.

**Type**

```ts
() => void
```


<span id="replay"></span>
### replay  

Replay starts.

**Type**

```ts
() => void
```


<span id="destroy"></span>
### destroy  

The player is destroyed.

**Type**

```ts
() => void
```


<span id="urlchange"></span>
### urlchange  

The playback address changes.

**Type**

```ts
(url: string) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|url |string |The updated playback address. |


<span id="fullscreenchange"></span>
### fullscreenChange  

The player switches to or from full\-window mode, in which the player covers the entire desktop.

**Type**

```ts
(isFullscreen: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isFullscreen |boolean |Whether the player is in full\-window mode. |


<span id="cssfullscreenchange"></span>
### cssFullscreenChange  

The player switches to or from full\-screen mode, in which the player covers the browser window.

**Type**

```ts
(isFullscreen: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isFullscreen |boolean |Whether the player is in full\-screen mode. |


<span id="definitionchange"></span>
### definitionChange  

The video resolution changes.

**Type**

```ts
(data: { from: Definition; to: Definition;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |The resolution information. |
|from |[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition) |The previous resolution. |
|to |[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition) |The updated resolution. |


<span id="videoresize"></span>
### videoResize  

The size of the player container changes.

**Type**

```ts
(data: any) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |any |The updated player size. |


<span id="pipchange"></span>
### pipChange  

The player switches to or from Picture\-in\-Picture (PIP) mode.

**Type**

```ts
(isPIP: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isPIP |boolean |Whether the player is in PiP mode. |


<span id="rotate"></span>
### rotate  

The player is rotated.

**Type**

```ts
(rotateDeg: number) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|rotateDeg |number |The rotation angle. |


<span id="useraction"></span>
### userAction  

A user event occurs within a built\-in plug\-in. This event applies to all built\-in plug\-ins and can be used for tracking user behaviors.

**Type**

```ts
(data: any) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |any |The user event information. |


<span id="shortcut"></span>
### shortcut  

A built\-in shortcut event occurs within the player.

**Type**

```ts
(data: any) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |any |The shortcut information. |


<span id="fallbackerror"></span>
### fallbackError  

The player fails to switch to a backup stream.

**Type**

```ts
(error: VeError) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/24/docs-1158675#veerror) |The error message. |


<span id="fallback"></span>
### fallback  

The player downgrades to the backup address.

**Type**

```ts
(data: { from: { url: string; }; to: { url: string; };}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |The information about the primary and backup playback addresses. |
|from |*  |The information before the downgrade. |
|url |string |The playback address used before the downgrade. |
|to |*  |The information after the downgrade. |
|url |string |The playback address used after the downgrade. |


<span id="autoplayunmute"></span>
### autoplayUnmute  

The user clicks the "Unmute" button.

**Type**

```ts
() => void
```


<span id="longwaiting"></span>
### longWaiting  

Long wait.

**Type**

```ts
() => void
```


<span id="definitionfallback"></span>
### definitionFallback  

A resolution downgrade.

**Type**

```ts
(data: { from: Definition; to: Definition;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |The information about the downgrade. |
|from |[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition) |The previous resolution. |
|to |[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition) |The updated resolution. |


<span id="errorrefreshclick"></span>
### errorRefreshClick  

The user clicks the refresh button after an error occurs.

**Type**

```ts
() => void
```


<span id="sourcechange"></span>
### sourceChange  

The player switches to another playback source.

**Type**

```ts
() => void
```


<span id="sei"></span>
### sei  

The player parses the SEI information.

**Type**

```ts
(data: { originPts: number; pts: number; time: number; data: { payload: Uint8Array; type: number; size: number; uuid: string; };}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |*  |The SEI information |
|originPts |number |The actual presentation timestamp (PTS) of the video frame. |
|pts |number |The adjusted presentation timestamp (PTS). The player adjusts the presentation timestamp based on the time the audience enters the live room. |
|time |number |The timestamp of the SEI message in the current live stream, in seconds. |
|data |*  |The SEI data. |
|payload |Uint8Array |The SEI data. |
|type |number |The SEI type. |
|size |number |The SEI size. |
|uuid |string |The SEI UUID or an empty string if the SEI UUID doesn't exist. |


<span id="timeshiftchange"></span>
### timeShiftChange  

The time\-shift state changes.

**Type**

```ts
(isTimeShift: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isTimeShift |boolean |Whether the live stream is time\-shifted. |


<span id="refreshclick"></span>
### refreshClick  

The user clicks the Refresh button.

**Type**

```ts
() => void
```


<span id="abrswitchstart"></span>
### abrSwitchStart  

Event callback for switching Adaptive Bitrate (ABR) streams.

**Type**

```ts
(data: { bitrate: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |\- |\- |
|bitrate |number |Bitrate after switching. |


<span id="abrswitchedsuccess"></span>
### abrSwitchedSuccess  

Event callback of successfully switching Adaptive Bitrate (ABR) live stream.

**Type**

```ts
(data: { bitrate: number; url: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |\- |\- |
|bitrate |number |Bitrate after switching. |
|url |string |The playback address after the switch. |


<span id="abrswitchfailed"></span>
### abrSwitchFailed  

Event callback of failing to switch Adaptive Bitrate (ABR) live stream.

**Type**

```ts
(data: { bitrate: number; url: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |\- |\- |
|bitrate |number |Bitrate after switching. |
|url |string |The playback address after the switch. |

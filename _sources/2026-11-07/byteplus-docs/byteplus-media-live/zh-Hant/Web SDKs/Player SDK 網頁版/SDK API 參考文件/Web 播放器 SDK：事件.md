---
title: "Web 播放器 SDK：事件"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158676-zh-TW"
---

<span id="liveevents"></span>
## LiveEvents

類型：`enum`


|名稱 |值 |描述 |
|---|---|---|
|PLAY |`'play'` |影片播放開始。 |
|PLAYING |`'playing'` |影片播放在暫停或凍結後恢復。 |
|ENDED |`'ended'` |影片播放結束。 |
|PAUSE |`'pause'` |影片播放暫停。 |
|ERROR |`'error'` |影片播放過程中發生錯誤。 |
|TIME_UPDATE |`'timeupdate'` |影片播放時間已更新。 |
|WAITING |`'waiting'` |播放器正在載入資料。 |
|CANPLAY |`'canplay'` |已緩衝足夠資料以供影片播放。 |
|CANPLAY_THROUGH |`'canplaythrough'` |影片可順暢播放。 |
|DURATION_CHANGE |`'durationchange'` |影片時長發生變化。 |
|VOLUME_CHANGE |`'volumechange'` |影片音量發生變化。 |
|LOADED_DATA |`'loadeddata'` |播放資料已載入。 |
|LOAD_START |`'loadstart'` |影片內容開始載入。 |
|PLAYER_FOCUS |`'focus'` |播放器取得焦點。 |
|PLAYER_BLUR |`'blur'` |播放器失去焦點。 |
|READY |`'ready'` |播放器已實例化。 |
|AUTOPLAY_STARTED |`'autoplayStarted'` |自動播放啟動成功。 |
|AUTOPLAY_PREVENTED |`'autoplayWasPrevented'` |自動播放啟動失敗。 |
|COMPLETE |`'complete'` |播放器已建立影片，播放已準備就緒。 |
|REPLAY |`'replay'` |重新播放開始。 |
|DESTROY |`'destroy'` |播放器已銷毀。 |
|URL_CHANGE |`'urlchange'` |播放位址發生變更。 |
|FULLSCREEN_CHANGE |`'fullscreenChange'` |播放器切換至或離開全視窗模式（播放器覆蓋整個桌面）。 |
|CSS_FULLSCREEN_CHANGE |`'cssFullscreenChange'` |播放器切換至或離開全螢幕模式（播放器覆蓋瀏覽器視窗）。 |
|DEFINITION_CHANGE |`'definitionChange'` |影片解析度發生變更。 |
|VIDEO_RESIZE |`'videoResize'` |播放器容器大小發生變更。 |
|PIP_CHANGE |`'pipChange'` |播放器切換至或離開子母畫面（PIP）模式。 |
|ROTATE |`'rotate'` |播放器已旋轉。 |
|USER_ACTION |`'userAction'` |內建外掛中發生使用者事件。此事件適用於所有內建外掛，可用於追蹤使用者行為。 |
|SHORTCUT |`'shortcut'` |播放器內發生內建快捷鍵事件。 |
|FALLBACK_ERROR |`'fallbackError'` |播放器切換至備用串流失敗。 |
|FALLBACK |`'fallback'` |播放器切換至備用位址。 |
|AUTOPLAY_UNMUTE |`'autoplayUnmute'` |使用者點擊「取消靜音」按鈕。 |
|LONG_WAITING |`'longWaiting'` |長時間等待。 |
|DEFINITION_FALLBACK |`'definitionFallback'` |解析度降級。 |
|ERROR_REFRESH_CLICK |`'errorRefreshClick'` |發生錯誤後，使用者點擊重新整理按鈕。 |
|SOURCE_CHANGE |`'sourceChange'` |播放器切換至其他播放來源。 |
|SEI |`'sei'` |播放器解析 SEI 資訊。 |
|TIME_SHIFT_CHANGE |`'timeShiftChange'` |時移狀態發生變更。 |
|REFRESH_CLICK |`'refreshClick'` |使用者點擊重新整理按鈕。 |
|ABR_SWITCH_START |`'abrSwitchStart'` |切換自適應碼率（ABR）串流的事件。 |
|ABR_SWITCH_SUCCESS |`'abrSwitchedSuccess'` |自適應碼率（ABR）直播流切換成功事件。 |
|ABR_SWITCH_FAILED |`'abrSwitchFailed'` |自適應碼率（ABR）直播流切換失敗事件。 |


<span id="3d310222"></span>
## LiveEventsPayload

類型：`interface`

用於即時事件回調的資料結構，包括播放狀態、錯誤細節及網路更新。

**範例**

```JavaScript
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


<span id="5fad64ab"></span>
### play

播放開始。

**類型**

```TypeScript
() => void
```


<span id="11041b0f"></span>
### playing

播放在暫停或凍結後恢復。

**類型**

```TypeScript
() => void
```


<span id="b23aa1e0"></span>
### ended

播放結束。

**類型**

```TypeScript
() => void
```


<span id="55656a67"></span>
### pause

播放暫停。

**類型**

```TypeScript
() => void
```


<span id="feba0d28"></span>
### error

播放過程中發生錯誤。

**類型**

```TypeScript
(error: VeError) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#veerror) |錯誤物件。 |


<span id="08ce6577"></span>
### timeupdate

影片播放時間已更新。

**類型**

```TypeScript
() => void
```


<span id="1fe1be49"></span>
### waiting

播放器正在載入資料。

**類型**

```TypeScript
() => void
```


<span id="1cb38462"></span>
### canplay

已緩衝足夠資料以供影片播放。

**類型**

```TypeScript
() => void
```


<span id="dcd63017"></span>
### canplaythrough

影片可順暢播放。

**類型**

```TypeScript
() => void
```


<span id="3829b5e7"></span>
### durationchange

影片時長發生變化。

**類型**

```TypeScript
() => void
```


<span id="e3486166"></span>
### volumechange

影片音量發生變化。

**類型**

```TypeScript
() => void
```


<span id="72692d16"></span>
### loadeddata

播放資料已載入。

**類型**

```TypeScript
() => void
```


<span id="57b78017"></span>
### loadstart

影片內容開始載入。

**類型**

```TypeScript
() => void
```


<span id="614b9d5b"></span>
### focus

播放器獲得焦點。

**類型**

```TypeScript
(data: { paused: boolean; ended: boolean; autoHide: boolean; delay: number;}) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |*  |事件相關資訊。 |
|paused |boolean |播放是否暫停。 |
|ended |boolean |播放是否結束。 |
|autoHide |boolean |是否啟用自動隱藏。 |
|delay |number |自動隱藏延遲時間（毫秒）。 |


<span id="ac69beea"></span>
### blur

播放器失去焦點。

**類型**

```TypeScript
(data: { paused: boolean; ended: boolean;}) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |*  |事件相關資訊。 |
|paused |boolean |播放是否暫停。 |
|ended |boolean |播放是否結束。 |


<span id="40f213c6"></span>
### ready

播放器已實例化。

**類型**

```TypeScript
() => void
```


<span id="f3da2673"></span>
### autoplayStarted

自動播放成功啟動。

**類型**

```TypeScript
() => void
```


<span id="87d7c738"></span>
### autoplayWasPrevented

自動播放啟動失敗。

**類型**

```TypeScript
() => void
```


<span id="afc0125d"></span>
### complete

播放器已建立影片並準備開始播放。

**類型**

```TypeScript
() => void
```


<span id="27bd048c"></span>
### replay

重播開始。

**類型**

```TypeScript
() => void
```


<span id="0297ad40"></span>
### destroy

播放器已銷毀。

**類型**

```TypeScript
() => void
```


<span id="7064f7ff"></span>
### urlchange

播放地址發生變化。

**類型**

```TypeScript
(url: string) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|url |string |更新後的播放位址。 |


<span id="51877f4f"></span>
### fullscreenChange

播放器切換至或離開全視窗模式，該模式下播放器覆蓋整個桌面。

**類型**

```TypeScript
(isFullscreen: boolean) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|isFullscreen |boolean |播放器是否處於全視窗模式。 |


<span id="0184d506"></span>
### cssFullscreenChange

播放器切換至或離開全螢幕模式，該模式下播放器覆蓋瀏覽器視窗。

**類型**

```TypeScript
(isFullscreen: boolean) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|isFullscreen |boolean |播放器是否處於全螢幕模式。 |


<span id="e709925e"></span>
### definitionChange

影片解析度發生變化。

**類型**

```TypeScript
(data: { from: Definition; to: Definition;}) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |*  |解析度資訊。 |
|from |[Definition](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |先前的解析度。 |
|to |[Definition](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |更新後的解析度。 |


<span id="e604d50e"></span>
### videoResize

播放器容器大小發生變化。

**類型**

```TypeScript
(data: any) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |any |更新後的播放器大小。 |


<span id="08e117a6"></span>
### pipChange

播放器切換至或離開子母畫面（PIP）模式。

**類型**

```TypeScript
(isPIP: boolean) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|isPIP |boolean |播放器是否處於子母畫面模式。 |


<span id="d3b3cac4"></span>
### rotate

播放器已旋轉。

**類型**

```TypeScript
(rotateDeg: number) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|rotateDeg |number |旋轉角度。 |


<span id="5436fbea"></span>
### userAction

內建插件中發生使用者事件。此事件適用於所有內建插件，可用於追蹤使用者行為。

**類型**

```TypeScript
(data: any) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |any |使用者事件資訊。 |


<span id="c6526470"></span>
### shortcut

播放器內發生內建快捷鍵事件。

**類型**

```TypeScript
(data: any) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |any |快捷鍵資訊。 |


<span id="1d3a23bc"></span>
### fallbackError

播放器切換至備用串流失敗。

**類型**

```TypeScript
(error: VeError) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#veerror) |錯誤訊息。 |


<span id="80cbf506"></span>
### fallback

播放器降級至備用地址。

**類型**

```TypeScript
(data: { from: { url: string; }; to: { url: string; };}) => void
```


**參數**


|名稱 |類型 |說明 |
|---|---|---|
|data |*  |主、備播放位址相關資訊。 |
|from |*  |降級前的資訊。 |
|url |string |降級前使用的播放位址。 |
|to |*  |降級後的資訊。 |
|url |string |降級後使用的播放地址。 |


<span id="ad2eb761"></span>
### autoplayUnmute

使用者點擊「取消靜音」按鈕。

**類型**

```TypeScript
() => void
```


<span id="9ac86e7d"></span>
### longWaiting

長時間等待。

**類型**

```TypeScript
() => void
```


<span id="5478b8c0"></span>
### definitionFallback

解析度降級。

**類型**

```TypeScript
(data: { from: Definition; to: Definition;}) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|data |*  |關於降級的資訊。 |
|from |[定義](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |先前的解析度。 |
|to |[定義](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |更新後的解析度。 |


<span id="c834f96d"></span>
### errorRefreshClick

使用者在發生錯誤後點擊重新整理按鈕。

**類型**

```TypeScript
() => void
```


<span id="83085b0d"></span>
### sourceChange

播放器切換至其他播放來源。

**類型**

```TypeScript
() => void
```


<span id="bd675273"></span>
### sei

播放器解析 SEI 資訊。

**類型**

```TypeScript
(data: { originPts: number; pts: number; time: number; data: { payload: Uint8Array; type: number; size: number; uuid: string; };}) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|data |*  |SEI 資訊 |
|originPts |number |影片幀的實際顯示時間戳（PTS）。 |
|pts |number |調整後的顯示時間戳（PTS）。播放器會根據觀眾進入直播間的時間調整顯示時間戳。 |
|time |number |當前直播流中 SEI 訊息的時間戳，單位為秒。 |
|data |*  |SEI 數據。 |
|payload |Uint8Array |SEI 數據。 |
|type |number |SEI 類型。 |
|size |number |SEI 大小。 |
|uuid |string |SEI UUID，若不存在則為空字串。 |


<span id="c073f460"></span>
### timeShiftChange

時移狀態發生變化。

**類型**

```TypeScript
(isTimeShift: boolean) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|isTimeShift |boolean |直播流是否為時移。 |


<span id="901f038b"></span>
### refreshClick

使用者點擊重新整理按鈕。

**類型**

```TypeScript
() => void
```


<span id="53c349b3"></span>
### abrSwitchStart

切換自適應比特率（ABR）串流的事件回調。

**類型**

```TypeScript
(data: { bitrate: number;}) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|data |*  |*  |
|bitrate |number |切換後的碼率。 |


<span id="5c0bf27e"></span>
### abrSwitchedSuccess

成功切換自適應比特率（ABR）直播串流的事件回調。

**類型**

```TypeScript
(data: { bitrate: number; url: string;}) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|data |*  |*  |
|bitrate |number |切換後的碼率。 |
|url |string |切換後的播放地址。 |


<span id="e5b7a31d"></span>
### abrSwitchFailed

切換自適應比特率（ABR）直播串流失敗的事件回調。

**類型**

```TypeScript
(data: { bitrate: number; url: string;}) => void
```


**參數**


|名稱 |類型 |描述 |
|---|---|---|
|data |*  |*  |
|bitrate |number |切換後的碼率。 |
|url |string |切換後的播放地址。 |

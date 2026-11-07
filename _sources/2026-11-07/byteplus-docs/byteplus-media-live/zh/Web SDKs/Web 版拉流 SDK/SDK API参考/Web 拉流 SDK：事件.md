---
title: "Web 拉流 SDK：事件"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158676-zh-CN"
---

<span id="liveevents"></span>
## LiveEvents

类型：`enum`


|名称 |值 |接口行为 |
|---|---|---|
|PLAY |`'play'` |视频回放开始。 |
|PLAYING |`'playing'` |暂停或卡顿后视频回放恢复。 |
|ENDED |`'ended'` |视频回放结束。 |
|PAUSE |`'pause'` |视频回放暂停。 |
|ERROR |`'error'` |视频回放过程中发生错误。 |
|TIME_UPDATE |`'timeupdate'` |视频回放时间已更新。 |
|WAITING |`'waiting'` |播放器正在加载数据。 |
|CANPLAY |`'canplay'` |已缓冲足够数据以进行视频回放。 |
|CANPLAY_THROUGH |`'canplaythrough'` |视频可流畅播放。 |
|DURATION_CHANGE |`'durationchange'` |视频时长发生变化。 |
|VOLUME_CHANGE |`'volumechange'` |视频音量发生变化。 |
|LOADED_DATA |`'loadeddata'` |回放数据已加载。 |
|LOAD_START |`'loadstart'` |视频内容开始加载。 |
|PLAYER_FOCUS |`'focus'` |播放器获得焦点。 |
|PLAYER_BLUR |`'blur'` |播放器失去焦点。 |
|READY |`'ready'` |播放器已实例化。 |
|AUTOPLAY_STARTED |`'autoplayStarted'` |自动播放成功启动。 |
|AUTOPLAY_PREVENTED |`'autoplayWasPrevented'` |自动播放启动失败。 |
|COMPLETE |`'complete'` |播放器已创建视频，回放已准备好开始。 |
|REPLAY |`'replay'` |重新播放开始。 |
|DESTROY |`'destroy'` |播放器已销毁。 |
|URL_CHANGE |`'urlchange'` |回放地址发生变化。 |
|FULLSCREEN_CHANGE |`'fullscreenChange'` |播放器切换至或退出全窗口模式，此模式下播放器覆盖整个桌面。 |
|CSS_FULLSCREEN_CHANGE |`'cssFullscreenChange'` |播放器切换至或退出全屏模式，此模式下播放器覆盖浏览器窗口。 |
|DEFINITION_CHANGE |`'definitionChange'` |视频分辨率发生变化。 |
|VIDEO_RESIZE |`'videoResize'` |播放器容器尺寸发生变化。 |
|PIP_CHANGE |`'pipChange'` |播放器切换至或退出画中画（PiP）模式。 |
|ROTATE |`'rotate'` |播放器被旋转。 |
|USER_ACTION |`'userAction'` |内置插件内发生用户事件。该事件适用于所有内置插件，可用于追踪用户行为。 |
|SHORTCUT |`'shortcut'` |播放器内发生内置快捷键事件。 |
|FALLBACK_ERROR |`'fallbackError'` |播放器切换至备流失败。 |
|FALLBACK |`'fallback'` |播放器切换至备份地址。 |
|AUTOPLAY_UNMUTE |`'autoplayUnmute'` |用户点击“取消静音”按钮。 |
|LONG_WAITING |`'longWaiting'` |长时间等待。 |
|DEFINITION_FALLBACK |`'definitionFallback'` |分辨率降级。 |
|ERROR_REFRESH_CLICK |`'errorRefreshClick'` |用户在发生错误后点击刷新按钮。 |
|SOURCE_CHANGE |`'sourceChange'` |播放器切换至其他回放源。 |
|SEI |`'sei'` |播放器解析 SEI 信息。 |
|TIME_SHIFT_CHANGE |`'timeShiftChange'` |时移状态发生变化。 |
|REFRESH_CLICK |`'refreshClick'` |用户点击刷新按钮。 |
|ABR_SWITCH_START |`'abrSwitchStart'` |切换自适应码率（ABR）流的事件。 |
|ABR_SWITCH_SUCCESS |`'abrSwitchedSuccess'` |成功切换自适应码率（ABR）直播流的事件。 |
|ABR_SWITCH_FAILED |`'abrSwitchFailed'` |切换自适应码率（ABR）直播流失败的事件。 |


<span id="3d310222"></span>
## LiveEventsPayload

类型：`interface`

用于直播事件回调的数据结构，包括回放状态、错误详情和网络更新。

**示例**

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

回放开始。

**类型**

```TypeScript
() => void
```


<span id="11041b0f"></span>
### playing

暂停或卡顿后回放恢复。

**类型**

```TypeScript
() => void
```


<span id="b23aa1e0"></span>
### ended

回放结束。

**类型**

```TypeScript
() => void
```


<span id="55656a67"></span>
### pause

回放暂停。

**类型**

```TypeScript
() => void
```


<span id="feba0d28"></span>
### error

回放过程中发生错误。

**类型**

```TypeScript
(error: VeError) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#veerror) |错误对象。 |


<span id="08ce6577"></span>
### timeupdate

视频回放时间已更新。

**类型**

```TypeScript
() => void
```


<span id="1fe1be49"></span>
### waiting

播放器正在加载数据。

**类型**

```TypeScript
() => void
```


<span id="1cb38462"></span>
### canplay

已缓冲足够数据以进行视频回放。

**类型**

```TypeScript
() => void
```


<span id="dcd63017"></span>
### canplaythrough

视频可流畅播放。

**类型**

```TypeScript
() => void
```


<span id="3829b5e7"></span>
### durationchange

视频时长发生变化。

**类型**

```TypeScript
() => void
```


<span id="e3486166"></span>
### volumechange

视频音量发生变化。

**类型**

```TypeScript
() => void
```


<span id="72692d16"></span>
### loadeddata

回放数据已加载。

**类型**

```TypeScript
() => void
```


<span id="57b78017"></span>
### loadstart

视频内容开始加载。

**类型**

```TypeScript
() => void
```


<span id="614b9d5b"></span>
### focus

播放器获得焦点。

**类型**

```TypeScript
(data: { paused: boolean; ended: boolean; autoHide: boolean; delay: number;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |事件相关信息。 |
|paused |boolean |回放是否暂停。 |
|ended |boolean |回放是否结束。 |
|autoHide |boolean |是否启用自动隐藏。 |
|delay |number |自动隐藏的延迟，单位为毫秒。 |


<span id="ac69beea"></span>
### blur

播放器失去焦点。

**类型**

```TypeScript
(data: { paused: boolean; ended: boolean;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |事件相关信息。 |
|paused |boolean |回放是否暂停。 |
|ended |boolean |回放是否结束。 |


<span id="40f213c6"></span>
### ready

播放器实例化。

**类型**

```TypeScript
() => void
```


<span id="f3da2673"></span>
### autoplayStarted

自动播放成功启动。

**类型**

```TypeScript
() => void
```


<span id="87d7c738"></span>
### autoplayWasPrevented

自动播放启动失败。

**类型**

```TypeScript
() => void
```


<span id="afc0125d"></span>
### complete

播放器已创建视频，回放准备开始。

**类型**

```TypeScript
() => void
```


<span id="27bd048c"></span>
### replay

重新播放开始。

**类型**

```TypeScript
() => void
```


<span id="0297ad40"></span>
### destroy

播放器已销毁。

**类型**

```TypeScript
() => void
```


<span id="7064f7ff"></span>
### urlchange

回放地址发生变化。

**类型**

```TypeScript
(url: string) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|url |string |更新后的回放地址。 |


<span id="51877f4f"></span>
### fullscreenChange

播放器切换至或退出全窗口模式（覆盖整个桌面）。

**类型**

```TypeScript
(isFullscreen: boolean) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isFullscreen |boolean |播放器是否处于全窗口模式。 |


<span id="0184d506"></span>
### cssFullscreenChange

播放器切换至或退出全屏模式（覆盖浏览器窗口）。

**类型**

```TypeScript
(isFullscreen: boolean) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isFullscreen |boolean |播放器是否处于全屏模式。 |


<span id="e709925e"></span>
### definitionChange

视频分辨率发生变化。

**类型**

```TypeScript
(data: { from: Definition; to: Definition;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |分辨率信息。 |
|from |[Definition](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |之前的分辨率。 |
|to |[Definition](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |更新后的分辨率。 |


<span id="e604d50e"></span>
### videoResize

播放器容器尺寸发生变化。

**类型**

```TypeScript
(data: any) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |any |更新后的播放器尺寸。 |


<span id="08e117a6"></span>
### pipChange

播放器切换至或退出画中画模式。

**类型**

```TypeScript
(isPIP: boolean) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isPIP |boolean |播放器是否处于画中画模式。 |


<span id="d3b3cac4"></span>
### rotate

播放器已旋转。

**类型**

```TypeScript
(rotateDeg: number) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|rotateDeg |number |旋转角度。 |


<span id="5436fbea"></span>
### userAction

内置插件内发生用户事件。该事件适用于所有内置插件，可用于追踪用户行为。

**类型**

```TypeScript
(data: any) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |any |用户事件信息。 |


<span id="c6526470"></span>
### shortcut

播放器内发生内置快捷键事件。

**类型**

```TypeScript
(data: any) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |any |快捷键信息。 |


<span id="1d3a23bc"></span>
### fallbackError

播放器切换至备流失败。

**类型**

```TypeScript
(error: VeError) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|error |[VeError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675#veerror) |错误信息。 |


<span id="80cbf506"></span>
### fallback

播放器降级至备地址。

**类型**

```TypeScript
(data: { from: { url: string; }; to: { url: string; };}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |主回放地址和备份回放地址的信息。 |
|from |*  |降级前的信息。 |
|url |string |降级前使用的回放地址。 |
|to |*  |降级后的信息。 |
|url |string |降级后使用的回放地址。 |


<span id="ad2eb761"></span>
### autoplayUnmute

用户点击“取消静音”按钮。

**类型**

```TypeScript
() => void
```


<span id="9ac86e7d"></span>
### longWaiting

长时间等待。

**类型**

```TypeScript
() => void
```


<span id="5478b8c0"></span>
### definitionFallback

分辨率降级。

**类型**

```TypeScript
(data: { from: Definition; to: Definition;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |关于降级的信息。 |
|from |[定义](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |之前的分辨率。 |
|to |[定义](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#definition) |更新后的分辨率。 |


<span id="c834f96d"></span>
### errorRefreshClick

用户在发生错误后点击刷新按钮。

**类型**

```TypeScript
() => void
```


<span id="83085b0d"></span>
### sourceChange

播放器切换至其他回放源。

**类型**

```TypeScript
() => void
```


<span id="bd675273"></span>
### sei

播放器解析 SEI 信息。

**类型**

```TypeScript
(data: { originPts: number; pts: number; time: number; data: { payload: Uint8Array; type: number; size: number; uuid: string; };}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |SEI 信息 |
|originPts |number |视频帧的实际显示时间戳（PTS）。 |
|pts |number |调整后的显示时间戳（PTS）。播放器会根据观众进入直播间的时间调整显示时间戳。 |
|time |number |当前直播流中 SEI 消息的时间戳，单位为秒。 |
|data |*  |SEI 数据。 |
|payload |Uint8Array |SEI 数据。 |
|type |number |SEI 类型。 |
|size |number |SEI 大小。 |
|uuid |string |SEI UUID，如果不存在则为空字符串。 |


<span id="c073f460"></span>
### timeShiftChange

时移状态发生变化。

**类型**

```TypeScript
(isTimeShift: boolean) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|isTimeShift |boolean |直播流是否为时移流。 |


<span id="901f038b"></span>
### refreshClick

用户点击刷新按钮。

**类型**

```TypeScript
() => void
```


<span id="53c349b3"></span>
### abrSwitchStart

自适应码率流切换事件回调。

**类型**

```TypeScript
(data: { bitrate: number;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |*  |
|码率 |number |切换后的码率。 |


<span id="5c0bf27e"></span>
### abrSwitchedSuccess

自适应码率直播流切换成功事件回调。

**类型**

```TypeScript
(data: { bitrate: number; url: string;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |*  |
|码率 |number |切换后的码率。 |
|url |string |切换后的回放地址。 |


<span id="e5b7a31d"></span>
### abrSwitchFailed

自适应码率直播流切换失败事件回调。

**类型**

```TypeScript
(data: { bitrate: number; url: string;}) => void
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|data |*  |*  |
|码率 |number |切换后的码率。 |
|url |string |切换后的回放地址。 |

---
title: "Web 拉流 SDK：API 参考"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-api-reference-zh-CN"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文适用于 BytePlus MediaLive Web 拉流 SDK 的 1.x 版本。强烈建议升级到最新版本，以获得更优的播放器体验。</div>


本主题介绍 BytePlus MediaLive Web 拉流 SDK（也称为 VePlayer）的方法、回调和参数。

<span id="Parameters"></span>
## **参数**

创建 VePlayer 实例时，可以通过设置 `options` 配置播放器：

```javascript
var player = new VePlayer(options);
```


以下列表包含播放器支持的部分配置项：


* 拉流地址和协议

* 语言设置

* 软解和硬解

* 回放控制


<span id="options"></span>
### **options**

VePlayer 的配置项。


|**参数** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|isLive |Boolean |false |是否播放直播流。请始终设置为 `true`。 |
|id |String |无 |VePlayer 插入的容器 ID。必须设置 `id` 或 `root`。若同时设置两个参数，VePlayer 将插入 `root` 指定的容器。 |
|root |HTMLElement |无 |VePlayer 插入的容器 ID。必须设置 `id` 或 `root`。若同时设置两个参数，VePlayer 将插入 `root` 指定的容器。 |
|url |String |无 |拉流地址。可以手动拼接地址或使用 [地址生成器](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)生成地址。必须设置 `url` 或 `playList`。 |
|playList |Array |无 |拉流地址列表。详情请参见 [playListItem](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#playListItem)。必须设置 `url` 或 `playList`。 |
|plugins |Any |无 |自定义插件。可传入多个插件，用逗号分隔。 |
|languages |Object |无 |播放器在用户界面显示文本时所引用的字典。与`lang`参数配合使用，该参数用于设置播放器语言。你可以自定义字典，也可以使用[默认字典](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary)。请按照如下格式定义你的字典：`{[key: string]: object;}`。例如，`{ zh: { PIP: '画中画' }, en: { PIP: 'pip' }}`。 |
|useSoftDecoding |Boolean |false |是否使用软解。<br><br><br>* `true`：使用软解。<br><br>* `false`：不使用软解。<br><br><br>播放器在部分 Android 浏览器中可能被劫持，导致部分功能不可用。你可以通过软解来解决该问题。<br><br>移动端浏览器不支持播放 FLV 格式的流。如需播放该格式，请使用软解。<br><br>[部分浏览器](https://caniuse.com/?search=HEVC)不支持 H.265 编码格式。如需播放该编码格式的视频，请使用软解。<br><br>软解依赖于设备的 CPU。播放高码率、高分辨率视频时会导致 CPU 占用率较高。 |
|enableH265Degrade |Boolean |false |是否开启自动降级至 H.265 软解。开启后，若浏览器不支持 H.265 硬解，SDK 会自动切换为 H.265 软解。<br><br><br>* `true`：开启自动降级。<br><br>* `false`：关闭自动降级。 |
|codec |String |'h265' |视频流的编码格式。若通过设置`enableH265Degrade`为`true`开启自动降级至 H.265 软解，建议设置该参数。 |
|sdkErrorPlugin |[SdkErrorConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#SdkErrorConfig) |None |错误信息。播放器发生错误时，你可以配置文本、图片和刷新按钮。 |
|rtm |[RtmConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#RtmConfig) |None |实时媒体（RTM）配置。仅当`url`设置为 RTM 拉流地址时，该参数才生效。 |
|width |String｜Number |100% |播放器的宽度。<br><br>若`width`设置为包含百分号的字符串，例如`'30%'`，SDK 会将该值作为播放器相对于容器的宽度。若字符串不包含百分号，例如`'300'`或`'300px'`，SDK 会将该值作为播放器的绝对宽度（单位：像素）。<br><br>若`width`设置为数字，例如`300`，SDK 会将该值作为播放器的绝对宽度（单位：像素）。 |
|height |String｜Number |100% |播放器的高度。<br><br>若`height`设置为包含百分号的字符串，例如`'30%'`，SDK 会将该值作为播放器相对于容器的高度。若字符串不包含百分号，例如`'300'`或`'300px'`，SDK 会将该值作为播放器的绝对高度（单位：像素）。<br><br>若`height`设置为数字，例如`300`，SDK 会将该值作为播放器的绝对高度（单位：像素）。 |
|volume |Number |0.6 |播放器的默认音量。支持范围：[0, 1] |
|autoplay |Boolean |true |是否开启自动回放。<br><br><br>* `true`：开启自动回放。<br><br>* `false`：关闭自动回放。仅当终端用户点击播放按钮时才会开始回放。 |
|autoplayMuted |Boolean |true |是否在自动回放时静音音频。仅当你将`autoplay`设置为`true`时，该参数才生效。<br><br><br>* `true`：自动回放时静音音频。<br><br>* `false`：自动回放时不静音音频。 |
|poster |String |None |封面图的 URL。 |
|pip |Boolean |true |是否启用画中画（PiP）。<br><br><br>* `true`：启用画中画。<br><br>* `false`：禁用画中画。 |
|fullscreen |[fullscreen](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#fullscreen) |None |与全屏模式相关的配置。 |
|lang |String |zh |播放器的显示语言。默认语言包括：<br><br><br>* `zh`<br><br>* `en`<br><br>* `jp`<br><br>* `zh-hk` |
|liveInfoPanel |[LiveInfoPanel](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#LiveInfoPanel) |None |用于展示流信息的面板。SDK 支持展示 HLS 和 FLV 流的信息。在使用该面板前，需先添加 LiveInfoPanel 插件：`plugins: [window.VePlayer.LiveInfoPanel]`。 |
|timeShiftPlugin |[timeShiftPlugin](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#2f07a993) |None |直播时移相关配置。关于直播时移功能的实现方式，请参见[Time shifting](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-features#cc924516)。 |
|liveLogger |[liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) |None |日志相关配置。 |
|Subtitle |[Subtitle](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#subtitle) |None |字幕相关配置。仅在指定该参数时，播放器才会显示字幕。 |


<span id="fullscreen"></span>
### **fullscreen**

与全屏模式相关的配置项。


|**Name** |**Data Type** |**Default Value** |**接口行为** |
|---|---|---|---|
|rotateFullscreen |Boolean |false |是否启用自动旋转至横屏模式。启用后，若用户以竖屏持握手机并切换播放器至全屏模式，SDK 会将播放器旋转 90 度至横屏模式。该功能常用于移动设备。该参数会覆盖`useCssFullscreen`的设置。<br><br><br>* `true`：启用自动旋转至横屏模式。<br><br>* `false`：禁用自动旋转至横屏模式。 |
|useCssFullscreen |Boolean |false |是否使用全窗口或全屏模式。<br><br><br>* `true`：全窗口模式，播放器覆盖浏览器窗口。<br><br>* `false`：全屏模式，播放器覆盖整个桌面。 |
|needBackIcon |Boolean |false |播放器处于全屏模式时，是否在右上角显示返回按钮。该功能常用于移动设备。<br><br><br>* `true`：显示按钮。<br><br>* `false`：不显示按钮。 |


<span id="playListItem"></span>
### **playListItem**

拉流地址的详细信息。可以配置多个不同分辨率的地址。


|**Name** |**Data Type** |**Default Value** |**接口行为** |
|---|---|---|---|
|streamType |String |None |拉流协议。若你在`playList`中指定的拉流地址无后缀，则必须设置`streamType`。支持的取值包括：<br><br><br>* `rtm`<br><br>* `flv`<br><br>* `mp4`<br><br>* `hls` |
|url |String |None |拉流地址。你可以手动拼接地址或使用[地址生成器](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)生成地址。该参数为必填项。 |
|definition |String |None |流的视频分辨率，对应你在 BytePlus MediaLive 控制台配置的[转码模版](https://docs.byteplus.com/byteplus-media-live/docs/configuring-transcoding)。你可以传入同一源 ID（`lineId`）下不同分辨率的多个拉流地址。建议取值包括：<br><br><br>* `uhd`<br><br>* `hd`<br><br>* `sd`<br><br>* `ld`<br><br>* `ao` |
|definitionTextKey |String |`definition`的值 |流的视频分辨率的语言键。默认情况下，播放器会显示`definition`的值。需与`languages`配合使用。例如，若你将`definitionTextKey`设置为`HD_TEXT_KEY`，并将`languages`设置为`{ en: { HD_TEXT_KEY: 'High definition' }}`，播放器会将**High definition**作为流的分辨率显示。 |
|lineId |String |None |源 ID。你可以传入同一源 ID 下不同分辨率（`definition`）的多个拉流地址。 |
|lineTextKey |String |None |流 ID 的语言键。例如，如果你将`lineTextKey`设置为`LINE_ONE`，并将`languages`设置为`{ en: { LINE_ONE: 'Line one' }}`，播放器会将**Line one**显示为流的 ID。 |
|backUrlList |数组 |无 |备拉流地址。如果你将`sdkErrorPlugin.isNeedDemoteBack`设置为`true`，当主流发生错误时，播放器会自动切换到备流。 |


<span id="SdkErrorConfig"></span>
### **SdkErrorConfig**

播放器的错误信息。当播放器遇到错误时，可以配置文本、图片和刷新按钮。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|errorImg |布尔值 |true |发生错误时是否显示图片。<br><br><br>* `true`：显示图片。<br><br>* `false`：不显示图片。 |
|errorTips |布尔值 |true |报错时是否显示错误信息。默认错误信息为“播放时发生错误，点击刷新重试”，可通过在`languages`中配置`errorTips`进行自定义。<br><br>例如，你可以将`languages`设置为 { en: { errorTips: 'Player error' } }。 |
|isNeedRefreshButton |布尔值 |true |发生错误时是否显示刷新按钮。<br><br><br>* `true`：显示按钮。<br><br>* `false`：不显示按钮。 |
|retryLoopNum |数字 |1 |在播放器用户界面显示错误前的重试次数。 |
|isNeedDemoteBack |布尔值 |false |回放过程中发生错误时是否降级到备流。<br><br><br>* `false`：不降级。播放器显示错误信息。<br><br>* `true`：发生错误时，切换到由`playListItem.backUrlList`定义的备流。 |


<span id="RtmConfig"></span>
### **RtmConfig**

拉取 RTM 流的配置项


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|loadTimeout |数字 |5000 |重试拉流的最大等待时间，单位为毫秒。 |
|retryDelay |数字 |1000 |每次重试拉流的间隔时间，单位为毫秒。 |
|retryCount |数字 |0 |拉流的最大重试次数。 |
|backupURL |字符串 |无 |当拉取 RTM 流失败时，播放器切换到备 FLV 或 HLS 流。<br><br>如果指定了`backupURL`，播放器会启用自动切换。<br><br>如果未指定`backupURL`，播放器在 RTM 流播放失败时会报错，不会切换到备流。 |
|backupStreamType |字符串 |无 |备拉流地址的协议，需要与`backupURL`配合配置。支持的值包括：<br><br><br>* flv<br><br>* hls |
|delayHint |数字 |0 |音视频的缓冲时间，单位为秒。 |


<span id="LiveInfoPanel"></span>
### **LiveInfoPanel**

用于在播放器中展示流信息面板的配置项。流信息包括流的格式、码率和帧率，在播放器中显示。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|visible |布尔值 |true |是否显示面板。<br><br><br>* `true`：显示面板。<br><br>* `false`：不显示面板。 |
|showH265Info |布尔值 |false |是否显示 H.265 相关信息，如解码效率和 CPU 消耗。<br><br><br>* `true`：显示信息。<br><br>* `false`：不显示信息。<br><br><br>仅当`showH265Info`为`true`且浏览器使用软解时，播放器才会显示 H.265 相关信息。 |


<span id="2f07a993"></span>
### timeShiftPlugin

直播时移的配置项。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|livingStartTime |数字 |当前时间 |直播流会话开始的时间。Unix 时间戳（单位为秒）。时间必须根据浏览器的时区指定。 |
|maxMoveTime |数字 |604800 |回放过程中支持的最大直播时移时长，单位为秒。例如，如果你将`maxMoveTime`设置为`60`，则表示超过 60 秒前的内容将无法回放。支持范围：[6,604800]。 |


<span id="liveLogger"></span>
### **liveLogger**

日志上传的配置项。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|appId |String |None |应用ID，即您的应用的唯一标识符。请联系[BytePlus技术支持](https://console.byteplus.com/workorder/create)获取您的应用ID。 |
|enable |Boolean |true |是否启用日志上传至BytePlus MediaLive服务器。<br><br><br>* `true`：启用日志上传。<br><br>* `false`：关闭日志上传。 |
|userId |String |None |用户ID。强烈建议您将其设置为能够唯一标识用户的值。技术支持可能需要该信息来定位问题。如果您未定义`userId`和`deviceId`，SDK将生成随机的用户ID和设备ID，并存储在浏览器缓存中。 |
|deviceId |String |None |设备ID。强烈建议您将其设置为能够唯一标识用户设备的值。技术支持可能需要该信息来定位问题。如果您未定义`userId`和`deviceId`，SDK将生成随机的用户ID和设备ID，并存储在浏览器缓存中。 |


<span id="200897d1"></span>
### **Subtitle**

视频字幕的配置项。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|isDefaultOpen |Boolean |None |是否默认显示字幕。<br><br><br>* `true`：默认显示字幕。<br><br>* `false`：默认不显示字幕。 |
|mode |"external" |"native" |None |
|updateMode |String |'live' |始终将其设置为`'live'`。 |
|style |[style](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference-zh-CN#d1c656ee) |None |字幕样式的配置。 |


<span id="d1c656ee"></span>
### **style**

字幕样式的配置项。


|**名称** |**数据类型** |**默认值** |**接口行为** |
|---|---|---|---|
|follow |Boolean |true |是否根据播放器控制面板调整字幕位置。<br><br><br>* `true`：调整。<br><br>* `false`：不调整。 |
|mode |String |'stroke' |字体显示模式。<br><br><br>* `'stroke'`：为文本添加描边。<br><br>* `'bg'`：为文本添加阴影。 |
|followBottom |Boolean |true |是否根据播放器控制面板的垂直位置调整字幕位置。<br><br><br>* `true`：调整。<br><br>* `false`：不调整。 |
|fitVideo |Boolean |true |是否根据视频尺寸调整字体大小。<br><br><br>* `true`：调整。<br><br>* `false`：不调整。 |
|offsetBottom |Integer |4 |字幕与视频底部距离占视频高度的百分比。 |
|baseSizeX |Integer |49 |用户横屏持手机时的默认字体大小。 |
|baseSizeY |Integer |28 |用户竖屏持手机时的默认字体大小。 |
|minSize |Integer |16 |PC设备上的最小字体大小。 |
|minMobileSize |Integer |13 |移动设备上的最小字体大小。 |
|line |'single' |'double' |'three' |
|fontColor |String |'#fff' |字体颜色。 |


<span id="Methods"></span>
## **方法**

本节将介绍 VePlayer 的方法，以 `player.on()` 为例，调用示例如下。

```javascript
var player = new VePlayer(options)

player.on('player_create_finish', () => {
    console.log('The player is created.')
})
```


方法列表如下。


|**名称** |**接口行为** |
|---|---|
|[on()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#on()) |监听事件。 |
|[once()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#once()) |仅监听一次事件。 |
|[off()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#off()) |停止监听事件。 |
|[destroy()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#destroy()) |销毁播放器。 |
|[player.play()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#play()) |开始回放。 |
|[player.pause()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#pause()) |暂停回放。 |
|[player.retry()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#retry()) |刷新播放器。 |
|[player.switchURL()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#switchURL()) |切换到其他拉流地址。 |


<span id="on()"></span>
### **on()** 

监听事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**参数**


* `Action`：类型为 `string`

* `Func`：类型为 `(... args: any []) => void`


<span id="once()"></span>
### **once()** 

仅监听一次事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**参数**


* `Action`：类型为 `string`

* `Func`：类型为 `(... args: any []) => void`


<span id="off()"></span>
### **off()** 

停止监听事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**参数**


* `Action`：类型为 `string`

* `Func`：类型为 `(... args: any []) => void`


<span id="destroy()"></span>
### **destroy()** 

销毁当前播放器实例。

```typescript
() => Promise<void>
```


<span id="play()"></span>
### **play()** 

开始回放。

```typescript
() => Promise<void>
```


**示例代码**

示例 1

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play()
```


示例 2

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play().then(() => {
    // Actions to take if the playback starts successfully.
}).catch(() => {
    // Actions to take if the playback fails to start.通常发生在自动回放且无用户交互时。
})
```


<span id="pause()"></span>
### **pause()** 

暂停回放。

```typescript
() => void
```


**示例代码**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.pause()
```


<span id="retry()"></span>
### **retry()** 

刷新播放器。

```TypeScript
() => void
```


**示例代码**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.retry()
```


<span id="switchURL()"></span>
### **switchURL()** 

切换到另一个拉流地址。

```TypeScript
(src: string) => void
```


**参数**


* `src`：类型为 `string`


**示例代码**

```javascript
var veplayer = new VePlayer(options)
veplayer.switchURL('http://example.com');
```


<span id="Events"></span>
## **事件**

SDK 可监听以下事件：


|**事件** |**事件值** |**接口行为** |
|---|---|---|
|PLAYER_CREATED_FINISH |'player_create_finish' |播放器已创建。 |
|PLAYER_REBUILD |'player_rebuild' |播放器销毁后重新创建。 |
|CANCEL_UNMUTE |'cancel_unmute' |取消静音。 |
|REFRESH_CLICK |'refresh_click' |用户点击刷新按钮。 |
|PLAY_BACKUP_CHANGE |'play_backup_change' |发生错误后触发降级。 |
|PLAY_BACKUP_CHANGE_FINISH |'play_backup_change_finish' |发生错误后，降级已完成。 |
|PLAY_ERROR_BUTTON_CLICK |'play_error_button_click' |发生错误后触发重试。 |
|PlAY_URL_CHANGE |'play_url_change' |播放器切换到新的拉流地址。 |
|SHOW_PLAY_ERROR |'show_play_error' |播放器显示错误。 |
|LONG_WAITING |'long_waiting' |超过最大等待时间，之后可能发生降级。 |
|INNER_DEFINITION_CHANGE |'inner_definition_change' |播放器切换到其他分辨率。 |
|LINE_CHANGE |'line_change' |播放器切换到其他流。 |
|ENDED |'ended' |直播流已结束。 |

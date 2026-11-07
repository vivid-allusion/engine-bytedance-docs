---
title: "Web 端播放器 SDK：方法和属性"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178-zh-CN"
---

## VePlayerLive

类型：`class`

### 属性

|属性 |类型 |描述 |
|---|---|---|
|playTime |number |`Readonly` 获取已播放时长，不包括暂停和等待时间，单位为秒。 |
|readyState |0 \| 2 \| 1 \| 3 \| 4 |`Readonly` 获取视频的就绪状态。<br><br><br>* `0`: HAVE_NOTHING，表示没有媒体资源信息。<br><br>* `1`: HAVE_METADATA，表示已获取足够的媒体资源来初始化元数据，快进/快退不会引发异常。<br><br>* `2`: HAVE_CURRENT_DATA，表示当前播放位置的数据可用，但没有足够数据播放下一帧。<br><br>* `3`: HAVE_FUTURE_DATA，表示当前播放位置和未来短时间内（至少后续两帧）有足够数据。<br><br>* `4`: HAVE_ENOUGH_DATA，表示数据充足，且下载速率足以让视频无中断播放至结束。 |
|buffered |TimeRanges |`Readonly` 获取当前已缓冲的时间范围。 |
|played |TimeRanges |`Readonly` 获取已播放的音频/视频时间范围。 |
|cumulateTime |number |`Readonly` 设置或获取视频的当前播放位置，单位为秒。 |
|isFocused |boolean |`Readonly` 获取播放器是否获得焦点。播放器获得焦点时显示控制栏。 |
|isFullscreen |boolean |`Readonly` 获取播放器是否处于全屏模式。在该模式下，播放器覆盖整个桌面。 |
|isCssFullscreen |boolean |`Readonly` 获取播放器是否处于全窗口模式。在该模式下，播放器覆盖整个浏览器窗口。 |
|networkState |0 \| 2 \| 1 \| 3 |`Readonly` 获取视频的网络状态。<br><br><br>* `0`: NETWORK_EMPTY，表示尚无数据，且 `readyState` 为 `HAVE_NOTHING`。<br><br>* `1`: NETWORK_IDLE，表示 `HTMLMediaElement` 元素处于活动状态，且已选择资源，但未使用网络。<br><br>* `2`: NETWORK_LOADING，表示浏览器正在下载 `HTMLMediaElement` 元素的数据。<br><br>* `3`: NETWORK_NO_SOURCE，根据 `HTMLMediaElement` 元素的 `src` 属性未找到媒体源。 |
|paused |boolean |`Readonly` 获取当前视频是否已暂停。 |
|ended |boolean |`Readonly` 获取当前视频是否已播放结束。 |
|state |number |`Readonly` 获取播放器的当前状态。<br><br><br>* `0`: ERROR，表示发生播放错误<br><br>* `1`: INITIAL，表示初始化<br><br>* `2`: READY，表示配置/事件/插件已初始化/绑定/实例化<br><br>* `3`: ATTACHING，表示正在挂载媒体对象。<br><br>* `4`: ATTACHED，表示媒体对象已挂载到 DOM 中<br><br>* `5`: NOTALLOW，表示播放被阻止<br><br>* `6`: RUNNING，表示播放已成功开始<br><br>* `7`: ENDED，表示播放已结束<br><br>* `8`: DESTROYED，表示播放器实例已销毁 |
|url |string |`Readonly` 获取当前拉流地址。 |
|source |string |`Readonly` 获取当前播放源 ID。 |
|playerVersion |string |`Readonly` 获取播放器 SDK 版本号。 |
|definition |string |`Readonly` 获取当前分辨率 ID。 |
|crossOrigin |string |获取播放器的跨域配置。更多信息，请参见 [crossorigin](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin)。 |
|volume |number |获取视频音量。取值范围为 [0,1]。 |
|muted |boolean |获取视频是否静音。<br><br><br>* `true`: 已静音。<br><br>* `false`: 未静音。 |
|lang |string |获取当前语言。 |

### openLog()

启用日志上传。

**类型**

```ts
() => void
```

### closeLog()

禁用日志上传。

**类型**

```ts
() => void
```

### openInfoPanel()

开启信息面板。该面板显示流格式、帧率、码率、GOP、视频分辨率、编码格式、缓冲时间和播放进度等基本信息。如果使用软件解码，还会显示软件解码效率和 CPU 消耗。

**类型**

```ts
() => void
```

### closeInfoPanel()

关闭信息面板。

**类型**

```ts
() => void
```

### openAbr()

启用自适应码率（ABR）切换功能。

**类型**

```ts
() => void
```

### closeAbr()

禁用自适应码率（ABR）切换功能。

**类型**

```ts
() => void
```

### updateDrmConfig()

使用此方法更新 DRM 配置。

**类型**

```ts
(config: Drm) => Promise<void | undefined>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[Drm](https://docs.byteplus.com/en/docs/24/docs-1155423#drm) |Yes |None |A configuration object containing settings for Fairplay DRM. |

**返回值**

`Promise<void | undefined>`

### switchAbr()

修改 ABR 配置，包括启用或禁用 ABR 功能，以及调整其他分辨率。

**类型**

```ts
(options: { enable: boolean; bitrate: number;}) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |*  |Yes |*  |Configuration of ABR. |
|enable |boolean |Yes |`-` |Whether to enable the ABR function.<br><br><br>* `true`: Enabled ;<br><br>* `false`: Disabled |
|bitrate |number |Yes |None |Switch the bitrate corresponding to the Adaptive Bitrate (ABR) live stream. |

### getRTMNetWorkInfo()

获取 RTM 拉流的网络评估信息。

**类型**

```ts
() => RTMNetWorkInfo
```

**返回值**

[RTMNetWorkInfo](https://docs.byteplus.com/en/docs/24/docs-1155423#rtmnetworkinfo)

### getRTMStats()

获取 RTM 拉流的播放信息。

**类型**

```ts
() => Promise<StatsSnapShoot>
```

**返回值**

`Promise<`[StatsSnapShoot](https://docs.byteplus.com/en/docs/24/docs-1155423#statssnapshoot)`>`

### getFLVStats()

获取 FLV 拉流的播放信息。

**类型**

```ts
() => FlvStats
```

**返回值**

[FlvStats](https://docs.byteplus.com/en/docs/24/docs-1155423#flvstats)

### updatePlaylist()

此方法用于更新播放列表，支持更新源、分辨率和相关信息。

**类型**

```ts
(playlist: Source[], target?: string | { definition?: string; source?: string;}, needUpdateProtocol?: boolean) => Promise<void>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|playlist |[Source](https://docs.byteplus.com/en/docs/24/docs-1155423#source)[] |Yes |None |The playlist, consisting of multiple `Source` type elements. |
|target |*  |No |*  |An optional target configuration, which can specify the resolution or source. Providing this information helps update the playback source for a specific resolution or stream. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback resource ID. |
|needUpdateProtocol |boolean |Yes |`true` |Whether the protocol needs to be updated.<br><br><br>* `true`: Forces the protocol update to ensure compatibility with the playback configuration or source.<br><br>* `false`: Does not update the protocol and continues to use the current configuration. |

**返回值**

`Promise<void>`

### switch()

切换拉流地址、播放源或分辨率。

**类型**

```ts
(target: string | { definition?: string; source?: string;}, options?: { fallbackToFirstDefinition?: boolean; seamless?: boolean;}) => Promise<Definition>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|target |*  |Yes |*  |The target pull stream address, playback source, or resolution. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback source ID. |
|options |*  |No |*  |More configurations. |
|fallbackToFirstDefinition |boolean \| undefined |No |`false` |Whether to downgrade to the first resolution in the playlist when the player cannot play with the specified resolution. |
|seamless |boolean \| undefined |No |None |Whether seamless switching is enabled.<br><br><br>* `true`: Enables seamless switching, ensuring no interruption during playback.<br><br>* `false`: Disables seamless switching, which may cause interruptions during playback. |

**返回值**

`Promise<`[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition)`>`

### once()

调用此方法监听指定事件。事件处理函数仅执行一次。

**类型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The name representing the event. |
|callback |(data?: any) =\> any |Yes |None |Callback functions representing events. |

### off()

停止监听指定事件。

**类型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### emit()

触发指定事件。

**类型**

```ts
(event: string, data?: any) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|data |any |Yes |None |The event information. |

### offAll()

停止监听任何播放器事件。

**类型**

```ts
() => void
```

### on()

监听指定事件。

**类型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### play()

开始播放。

**类型**

```ts
() => any
```

**返回值**

`any`

### pause()

暂停播放。

**类型**

```ts
() => void
```

### requestPIP()

开启画中画（PIP）。

**类型**

```ts
() => void
```

### exitPIP()

关闭画中画（PIP）。

**类型**

```ts
() => void
```

### retry()

重试拉流。

**类型**

```ts
() => void
```

### focus()

播放器获得焦点。调用该方法后，`veplayer.isFocused` 将变为 `true`，并触发 `PLAYER_FOCUS` 事件。

**类型**

```ts
(data?: { autoHide?: boolean; delay?: number;}) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |Related configurations. |
|autoHide |boolean \| undefined |No |`true` |Whether auto\-blur is enabled.<br><br><br>* `true`: Enables auto\-blur, meaning `blur()` will be automatically called after the specified delay time.<br><br>* `false`: Disables auto\-blur, meaning `blur()` will not be automatically called after the delay. |
|delay |number \| undefined |No |`3000` |Delay duration (in milliseconds) before auto\-blur is triggered. This takes effect only when `autoHide` is set to `true`. |

### blur()

播放器失去焦点。调用该方法后，`veplayer.isFocused` 将变为 `false`，并触发 `PLAYER_BLUR` 事件。

**类型**

```ts
(data?: { ignorePaused?: boolean;}) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |The related configurations. |
|ignorePaused |boolean \| undefined |No |`false` |Whether the player retains focus when paused. The default is `true`, meaning the player will not automatically lose focus during pause. |

### canPlayType()

判断浏览器是否支持该播放格式。

**类型**

```ts
(type: string) => boolean
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|type |string |Yes |None |The playback format. |

**返回值**

`boolean`

### requestFullscreen()

将播放器切换到全屏模式。在该模式下，播放器覆盖整个桌面。如果调用该方法时播放器处于全窗口模式，则会自动退出全窗口模式，并触发 `Events.FULLSCREEN_CHANGE` 事件。

**类型**

```ts
(el?: HTMLElement) => Promise<void>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-screen mode. |

**返回值**

`Promise<void>`

### exitFullscreen()

退出全屏模式。调用该方法后，`veplayer.isFullscreen` 将变为 `false`，并触发 `Events.FULLSCREEN_CHANGE` 事件。

**类型**

```ts
(el?: HTMLElement) => Promise<void>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node of the full screen effect. |

**返回值**

`Promise<void>`

### requestCssFullscreen()

将播放器切换到全窗口模式。在该模式下，播放器覆盖整个浏览器窗口。如果调用该方法时播放器处于全屏模式，则会自动退出全屏模式，并触发 `Events.CSS_FULLSCREEN_CHANGE` 事件。

**类型**

```ts
(el?: HTMLElement) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-window mode. |

### exitCssFullscreen()

退出全窗口模式。调用该方法时，`veplayer.isFullscreen` 将变为 `false`，并触发 `Events.CSS_FULLSCREEN_CHANGE` 事件。

**类型**

```ts
() => void
```

### registerPlugin()

将指定插件注册到当前播放器。

**类型**

```ts
(plugin: Function | { plugin: Function; options: object;}, config?: { [propName: string]: any; } | undefined) => any
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |*  |Yes |*  |The plugin constructor. |
|plugin |Function |Yes |None |The plugin constructor. |
|options |object |Yes |None |The plugin configurations. |
|config |{ [propName: string]: any; } \| undefined |No |None |The plugin configurations. |

**返回值**

`any`

### unRegisterPlugin()

从播放器销毁或取消注册指定插件。

**类型**

```ts
(plugin: any) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |any |Yes |None |The plugin instance or name. |

### showIcon()

显示指定插件的图标。

**类型**

```ts
(pluginNames: string[]) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### hideIcon()

隐藏指定插件的图标。

**类型**

```ts
(pluginNames: string[]) => void
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### destroy()

销毁播放器实例。

**类型**

```ts
() => void
```

## createLivePlayer()

创建直播播放器。

**类型**

```ts
(options?: LiveVePlayerOptions) => Promise<VePlayerLive>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[LiveVePlayerOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#liveveplayeroptions) \| undefined |No |None |The player settings. |

**返回值**

`Promise<`[VePlayerLive](https://docs.byteplus.com/en/docs/24/106648#veplayerlive)`>` 播放器实例。

**示例**

```js
VePlayer.createLivePlayer({
 height: 360,
 url: options.url,
}).then(function (veplayer) {
 veplayer.on(VePlayer.live.Events.CANPLAY, function () {
   console.log('An canplay event has occurred')
 });
}).catch(error => {
 console.log('Fails to create the player. Error message:', error);
});;
```

## prepare()

初始化播放器策略。

**类型**

```ts
(options: PrepareOptions) => Promise<VeStrategyManager | undefined>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[PrepareOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#prepareoptions) |Yes |None |Configure strategy parameters. |

**返回值**

`Promise<`[VeStrategyManager](https://docs.byteplus.com/en/docs/24/ref#vestrategymanager)` | undefined>`

**示例**

```js
live.prepare({
 appId: '***',
 userId: '***',
 strategies: {
  rtmAdaptiveBuffer: true,
 },
}).then(function () {
 VePlayer.createLivePlayer({
  height: '300px',
  url: 'https://pulldomain.com/appname/streamname.sdp',
  logger: {
    userId: '***',
    appId: '***',
  },
 });
});
```

## isRTMSupported()

检查当前浏览器是否支持播放 RTM 流。

**类型**

```ts
() => Promise<boolean>
```

**返回值**

`Promise<boolean>`

## isRTMSupportCodec()

当前浏览器是否支持播放 H.264 编码的 RTM 流。

**类型**

```ts
(codec?: string) => Promise<boolean>
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string |Yes |`'h264'` |The stream codec. Supports `H264` currently. |

**返回值**

`Promise<boolean>`

## isMseSupported()

检查当前浏览器是否支持 MSE (MediaSource Extends) API，并检查 MSE API 是否支持传入的视频编码信息（MIME 格式）。

> **说明**

> 使用场景：检查 PC 端浏览器和 Android 端浏览器是否支持传入的编码信息。

**类型**

```ts
(codec?: string | undefined) => boolean
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MSE supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MSE supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**返回值**

`boolean`

## isSoftDecodeSupported()

检查当前浏览器是否支持软件解码。

**类型**

```ts
() => Promise<boolean>
```

**返回值**

`Promise<boolean>`

## isMMSSupported()

检查当前浏览器是否支持 MMS (ManagedMediaSource) API，并检查 MMS API 是否支持传入的视频编码信息（MIME 格式）。

> **说明**

* > 使用场景：检查 iOS 端 Safari 浏览器和 Chrome 浏览器是否支持传入的编码信息。

* > iOS 17.1 或以上版本的浏览器开始支持 MMS。

**类型**

```ts
(codec?: string | undefined) => any
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MMS supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MMS supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**返回值**

`any`

## isFLVSupported()

检查当前浏览器是否支持 FLV 格式流的编码信息。

> **说明**

* > 在 PC 或 Android 设备的浏览器中调用此方法时，其效果与使用默认编码格式调用 isMseSupported 方法相同。

* > 在 iOS 设备的浏览器中调用此方法时，其效果与实现 isMMSSupported 方法相同。

**类型**

```ts
(codec?: string | undefined) => boolean
```

**参数**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if the H.264 encoding format is supported. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if the H.265 encoding format is supported. If supported, it can meet the playback requirements of most H.265 videos. |

**返回值**

`boolean`

## isRTMSeiSupported()

检查当前浏览器是否支持从 RTM 流接收 SEI (Supplemental Enhancement Information) 消息。

**类型**

```ts
() => Promise<boolean>
```

**返回值**

`Promise<boolean>`

* `true`: 支持从 RTM 流接收 SEI 消息。

* `false`: 不支持从 RTM 流接收 SEI 消息。

## setLicenseConfig()

配置 SDK 许可证。

**类型**

```ts
(params: LicenseConfig) => Promise<void>
```

**参数**

|参数名称 |类型 |描述 |
|---|---|---|
|`params` |[LicenseConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#licenseconfig) |许可证配置参数。 |

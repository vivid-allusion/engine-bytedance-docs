---
title: "Web 版 Player SDK：方法與屬性"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178-zh-TW"
---

## VePlayerLive

類型：`class`

### 屬性

|屬性 |類型 |說明 |
|---|---|---|
|playTime |number |`Readonly` 取得已播放時長，不包含暫停與等待時間，單位為秒。 |
|readyState |0 \| 2 \| 1 \| 3 \| 4 |`Readonly` 取得影片的就緒狀態。<br><br><br>* `0`: HAVE_NOTHING，表示沒有媒體資源的相關資訊。<br><br>* `1`: HAVE_METADATA，表示已擷取足夠媒體資源，可初始化中繼資料，且快轉/倒轉不會引發例外。<br><br>* `2`: HAVE_CURRENT_DATA，表示目前播放位置的資料可用，但沒有足夠資料播放下一個影格。<br><br>* `3`: HAVE_FUTURE_DATA，表示目前播放位置及未來一小段時間（至少接下來兩個影格）有足夠資料。<br><br>* `4`: HAVE_ENOUGH_DATA，表示資料充足，且下載速率足以讓影片不間斷播放至結束。 |
|buffered |TimeRanges |`Readonly` 取得目前已緩衝的時間範圍。 |
|played |TimeRanges |`Readonly` 取得已播放音訊/影片的時間範圍。 |
|cumulateTime |number |`Readonly` 設定或取得影片目前播放位置，單位為秒。 |
|isFocused |boolean |`Readonly` 取得播放器是否取得焦點。播放器取得焦點時會顯示控制列。 |
|isFullscreen |boolean |`Readonly` 取得播放器是否處於全螢幕模式。在此模式下，播放器會覆蓋整個桌面。 |
|isCssFullscreen |boolean |`Readonly` 取得播放器是否處於全視窗模式。在此模式下，播放器會覆蓋整個瀏覽器視窗。 |
|networkState |0 \| 2 \| 1 \| 3 |`Readonly` 取得影片的網路狀況。<br><br><br>* `0`: NETWORK_EMPTY，表示尚無資料，且 `readyState` 為 `HAVE_NOTHING`。<br><br>* `1`: NETWORK_IDLE，表示 `HTMLMediaElement` 元素處於作用中且已選取資源，但未使用網路。<br><br>* `2`: NETWORK_LOADING，表示瀏覽器正在下載 `HTMLMediaElement` 元素的資料。<br><br>* `3`: NETWORK_NO_SOURCE，表示根據 `HTMLMediaElement` 元素的 `src` 屬性找不到媒體來源。 |
|paused |boolean |`Readonly` 取得目前影片是否暫停。 |
|ended |boolean |`Readonly` 取得目前影片是否已播放完畢。 |
|state |number |`Readonly` 取得播放器目前狀態。<br><br><br>* `0`: ERROR，表示發生播放錯誤<br><br>* `1`: INITIAL，表示初始化<br><br>* `2`: READY，表示設定/事件/外掛程式已初始化/繫結/實例化<br><br>* `3`: ATTACHING，表示正在掛載媒體物件。<br><br>* `4`: ATTACHED，表示媒體物件已掛載到 DOM<br><br>* `5`: NOTALLOW，表示播放遭封鎖<br><br>* `6`: RUNNING，表示播放已成功開始<br><br>* `7`: ENDED，表示播放已結束<br><br>* `8`: DESTROYED，表示播放器執行個體已銷毀 |
|url |string |`Readonly` 取得目前拉流位址。 |
|source |string |`Readonly` 取得目前播放來源 ID。 |
|playerVersion |string |`Readonly` 擷取播放器 SDK 版本號。 |
|definition |string |`Readonly` 取得目前解析度 ID。 |
|crossOrigin |string |取得播放器的跨網域設定。如需詳細資訊，請參閱 [crossorigin](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin)。 |
|volume |number |取得影片音量。值範圍為 [0,1]。 |
|muted |boolean |取得影片是否靜音。<br><br><br>* `true`: 已靜音。<br><br>* `false`: 未靜音。 |
|lang |string |取得目前語言。 |

### openLog()

啟用日誌上傳。

**類型**

```ts
() => void
```

### closeLog()

停用日誌上傳。

**類型**

```ts
() => void
```

### openInfoPanel()

開啟資訊面板。面板會顯示基本資訊，包括串流格式、影格率、位元率、GOP、影片解析度、編解碼器、緩衝時間和播放進度。如果使用軟體解碼，也會顯示軟體解碼效率和 CPU 使用量。

**類型**

```ts
() => void
```

### closeInfoPanel()

關閉資訊面板。

**類型**

```ts
() => void
```

### openAbr()

啟用自適應位元率串流 (ABR) 切換功能。

**類型**

```ts
() => void
```

### closeAbr()

停用自適應位元率串流 (ABR) 切換功能。

**類型**

```ts
() => void
```

### updateDrmConfig()

使用此方法更新 DRM 設定。

**類型**

```ts
(config: Drm) => Promise<void | undefined>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[Drm](https://docs.byteplus.com/en/docs/24/docs-1155423#drm) |Yes |None |A configuration object containing settings for Fairplay DRM. |

**傳回值**

`Promise<void | undefined>`

### switchAbr()

修改 ABR 設定，包括啟用或停用 ABR 功能，以及調整其他解析度。

**類型**

```ts
(options: { enable: boolean; bitrate: number;}) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |*  |Yes |*  |Configuration of ABR. |
|enable |boolean |Yes |`-` |Whether to enable the ABR function.<br><br><br>* `true`: Enabled ;<br><br>* `false`: Disabled |
|bitrate |number |Yes |None |Switch the bitrate corresponding to the Adaptive Bitrate (ABR) live stream. |

### getRTMNetWorkInfo()

取得 RTM 拉流的網路評估資訊。

**類型**

```ts
() => RTMNetWorkInfo
```

**傳回值**

[RTMNetWorkInfo](https://docs.byteplus.com/en/docs/24/docs-1155423#rtmnetworkinfo)

### getRTMStats()

取得 RTM 拉流的播放資訊。

**類型**

```ts
() => Promise<StatsSnapShoot>
```

**傳回值**

`Promise<`[StatsSnapShoot](https://docs.byteplus.com/en/docs/24/docs-1155423#statssnapshoot)`>`

### getFLVStats()

取得 FLV 拉流的播放資訊。

**類型**

```ts
() => FlvStats
```

**傳回值**

[FlvStats](https://docs.byteplus.com/en/docs/24/docs-1155423#flvstats)

### updatePlaylist()

此方法用於更新播放清單，支援更新來源、解析度及相關資訊。

**類型**

```ts
(playlist: Source[], target?: string | { definition?: string; source?: string;}, needUpdateProtocol?: boolean) => Promise<void>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|playlist |[Source](https://docs.byteplus.com/en/docs/24/docs-1155423#source)[] |Yes |None |The playlist, consisting of multiple `Source` type elements. |
|target |*  |No |*  |An optional target configuration, which can specify the resolution or source. Providing this information helps update the playback source for a specific resolution or stream. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback resource ID. |
|needUpdateProtocol |boolean |Yes |`true` |Whether the protocol needs to be updated.<br><br><br>* `true`: Forces the protocol update to ensure compatibility with the playback configuration or source.<br><br>* `false`: Does not update the protocol and continues to use the current configuration. |

**傳回值**

`Promise<void>`

### switch()

切換拉流位址、播放來源或解析度。

**類型**

```ts
(target: string | { definition?: string; source?: string;}, options?: { fallbackToFirstDefinition?: boolean; seamless?: boolean;}) => Promise<Definition>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|target |*  |Yes |*  |The target pull stream address, playback source, or resolution. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback source ID. |
|options |*  |No |*  |More configurations. |
|fallbackToFirstDefinition |boolean \| undefined |No |`false` |Whether to downgrade to the first resolution in the playlist when the player cannot play with the specified resolution. |
|seamless |boolean \| undefined |No |None |Whether seamless switching is enabled.<br><br><br>* `true`: Enables seamless switching, ensuring no interruption during playback.<br><br>* `false`: Disables seamless switching, which may cause interruptions during playback. |

**傳回值**

`Promise<`[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition)`>`

### once()

呼叫此方法以監聽指定事件。事件處理常式只會執行一次。

**類型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The name representing the event. |
|callback |(data?: any) =\> any |Yes |None |Callback functions representing events. |

### off()

停止監聽指定事件。

**類型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### emit()

觸發指定事件。

**類型**

```ts
(event: string, data?: any) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|data |any |Yes |None |The event information. |

### offAll()

停止監聽任何播放器事件。

**類型**

```ts
() => void
```

### on()

監聽指定事件。

**類型**

```ts
(event: string, callback: (data?: any) => any) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### play()

開始播放。

**類型**

```ts
() => any
```

**傳回值**

`any`

### pause()

暫停播放。

**類型**

```ts
() => void
```

### requestPIP()

開啟子母畫面 (PIP)。

**類型**

```ts
() => void
```

### exitPIP()

關閉子母畫面 (PIP)。

**類型**

```ts
() => void
```

### retry()

重試拉流。

**類型**

```ts
() => void
```

### focus()

播放器取得焦點。呼叫此方法時，`veplayer.isFocused` 會變成 `true`，並觸發 `PLAYER_FOCUS` 事件。

**類型**

```ts
(data?: { autoHide?: boolean; delay?: number;}) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |Related configurations. |
|autoHide |boolean \| undefined |No |`true` |Whether auto\-blur is enabled.<br><br><br>* `true`: Enables auto\-blur, meaning `blur()` will be automatically called after the specified delay time.<br><br>* `false`: Disables auto\-blur, meaning `blur()` will not be automatically called after the delay. |
|delay |number \| undefined |No |`3000` |Delay duration (in milliseconds) before auto\-blur is triggered. This takes effect only when `autoHide` is set to `true`. |

### blur()

播放器失去焦點。呼叫此方法時，`veplayer.isFocused` 會變成 `false`，並觸發 `PLAYER_BLUR` 事件。

**類型**

```ts
(data?: { ignorePaused?: boolean;}) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |The related configurations. |
|ignorePaused |boolean \| undefined |No |`false` |Whether the player retains focus when paused. The default is `true`, meaning the player will not automatically lose focus during pause. |

### canPlayType()

判斷瀏覽器是否支援播放格式。

**類型**

```ts
(type: string) => boolean
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|type |string |Yes |None |The playback format. |

**傳回值**

`boolean`

### requestFullscreen()

將播放器切換為全螢幕模式。在此模式下，播放器會覆蓋整個桌面。如果呼叫此方法時播放器處於全視窗模式，會自動結束全視窗模式，並觸發 `Events.FULLSCREEN_CHANGE` 事件。

**類型**

```ts
(el?: HTMLElement) => Promise<void>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-screen mode. |

**傳回值**

`Promise<void>`

### exitFullscreen()

結束全螢幕模式。呼叫此方法後，`veplayer.isFullscreen` 會變成 `false`，並觸發 `Events.FULLSCREEN_CHANGE` 事件。

**類型**

```ts
(el?: HTMLElement) => Promise<void>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node of the full screen effect. |

**傳回值**

`Promise<void>`

### requestCssFullscreen()

將播放器切換為全視窗模式。在此模式下，播放器會覆蓋整個瀏覽器視窗。如果呼叫此方法時播放器處於全螢幕模式，會自動結束全螢幕模式，並觸發 `Events.CSS_FULLSCREEN_CHANGE` 事件。

**類型**

```ts
(el?: HTMLElement) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-window mode. |

### exitCssFullscreen()

結束全視窗模式。呼叫此方法時，`veplayer.isFullscreen` 會變成 `false`，並觸發 `Events.CSS_FULLSCREEN_CHANGE` 事件。

**類型**

```ts
() => void
```

### registerPlugin()

將指定外掛程式註冊到目前播放器。

**類型**

```ts
(plugin: Function | { plugin: Function; options: object;}, config?: { [propName: string]: any; } | undefined) => any
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |*  |Yes |*  |The plugin constructor. |
|plugin |Function |Yes |None |The plugin constructor. |
|options |object |Yes |None |The plugin configurations. |
|config |{ [propName: string]: any; } \| undefined |No |None |The plugin configurations. |

**傳回值**

`any`

### unRegisterPlugin()

從播放器銷毀或取消註冊指定外掛程式。

**類型**

```ts
(plugin: any) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |any |Yes |None |The plugin instance or name. |

### showIcon()

顯示指定外掛程式的圖示。

**類型**

```ts
(pluginNames: string[]) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### hideIcon()

隱藏指定外掛程式的圖示。

**類型**

```ts
(pluginNames: string[]) => void
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### destroy()

銷毀播放器執行個體。

**類型**

```ts
() => void
```

## createLivePlayer()

建立直播播放器。

**類型**

```ts
(options?: LiveVePlayerOptions) => Promise<VePlayerLive>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[LiveVePlayerOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#liveveplayeroptions) \| undefined |No |None |The player settings. |

**傳回值**

`Promise<`[VePlayerLive](https://docs.byteplus.com/en/docs/24/107487#veplayerlive)`>` 播放器執行個體。

**範例**

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

**類型**

```ts
(options: PrepareOptions) => Promise<VeStrategyManager | undefined>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[PrepareOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#prepareoptions) |Yes |None |Configure strategy parameters. |

**傳回值**

`Promise<`[VeStrategyManager](https://docs.byteplus.com/en/docs/24/ref#vestrategymanager)` | undefined>`

**範例**

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

檢查目前瀏覽器是否支援播放 RTM 串流。

**類型**

```ts
() => Promise<boolean>
```

**傳回值**

`Promise<boolean>`

## isRTMSupportCodec()

目前瀏覽器是否支援播放以 H.264 編碼的 RTM 串流。

**類型**

```ts
(codec?: string) => Promise<boolean>
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string |Yes |`'h264'` |The stream codec. Supports `H264` currently. |

**傳回值**

`Promise<boolean>`

## isMseSupported()

檢查目前瀏覽器是否支援 MSE (MediaSource Extends) API，並檢查 MSE API 是否支援傳入的影片編碼資訊（MIME 格式）。

> **说明**

> 使用情境：檢查 PC 端瀏覽器和 Android 端瀏覽器是否支援傳入的編碼資訊。

**類型**

```ts
(codec?: string | undefined) => boolean
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MSE supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MSE supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**傳回值**

`boolean`

## isSoftDecodeSupported()

檢查目前瀏覽器是否支援軟體解碼。

**類型**

```ts
() => Promise<boolean>
```

**傳回值**

`Promise<boolean>`

## isMMSSupported()

檢查目前瀏覽器是否支援 MMS (ManagedMediaSource) API，並檢查 MMS API 是否支援傳入的影片編碼資訊（MIME 格式）。

> **说明**

* > 使用情境：檢查 iOS 端的 Safari 瀏覽器和 Chrome 瀏覽器是否支援傳入的編碼資訊。

* > iOS 17.1 或以上版本的瀏覽器開始支援 MMS。

**類型**

```ts
(codec?: string | undefined) => any
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MMS supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MMS supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**傳回值**

`any`

## isFLVSupported()

檢查目前瀏覽器是否支援 FLV 格式串流的編碼資訊。

> **说明**

* > 在 PC 或 Android 裝置的瀏覽器中呼叫此方法時，與使用預設編碼格式呼叫 isMseSupported 方法相同。

* > 在 iOS 裝置的瀏覽器中呼叫此方法時，與實作 isMMSSupported 方法相同。

**類型**

```ts
(codec?: string | undefined) => boolean
```

**參數**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if the H.264 encoding format is supported. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if the H.265 encoding format is supported. If supported, it can meet the playback requirements of most H.265 videos. |

**傳回值**

`boolean`

## isRTMSeiSupported()

檢查目前瀏覽器是否支援從 RTM 串流接收 SEI (Supplemental Enhancement Information) 訊息。

**類型**

```ts
() => Promise<boolean>
```

**傳回值**

`Promise<boolean>`

* `true`: 支援從 RTM 串流接收 SEI 訊息。

* `false`: 不支援從 RTM 串流接收 SEI 訊息。

## setLicenseConfig()

設定 SDK 授權。

**類型**

```ts
(params: LicenseConfig) => Promise<void>
```

**參數**

|參數名稱 |類型 |說明 |
|---|---|---|
|`params` |[LicenseConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#licenseconfig) |授權設定參數。 |

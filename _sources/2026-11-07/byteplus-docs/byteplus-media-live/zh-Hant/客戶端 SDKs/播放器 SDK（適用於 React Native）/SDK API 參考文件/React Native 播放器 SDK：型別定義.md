---
title: "React Native 播放器 SDK：型別定義"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition-zh-TW"
---

<span id="licenseconfig"></span>
## LicenseConfig

型別：`interface`

<span id="22268e4d"></span>
### AppID

型別：`string`

<span id="a1b8862f"></span>
### AppName

型別：`string`

<span id="8e59eca9"></span>
### AppVersion

型別：`string`

<span id="2a5c2766"></span>
### AppChannel

型別：`string`

<span id="fd1837d7"></span>
### LicenseUri

型別：`{ android: string; ios: string; }`

**成員**


|名稱 |型別 |說明 |
|---|---|---|
|android |`string` |Android App 的授權檔路徑。 |
|ios |`string` |iOS App 的授權檔路徑。 |


<span id="1e652764"></span>
### openLog

型別：`boolean | undefined`

<span id="b69a6b68"></span>
### UserUniqueID

型別：`string | undefined`

<span id="e0a44dd3"></span>
### PackageName

型別：`string | undefined`

<span id="59e43c39"></span>
### BundleID

型別：`string | undefined`

<span id="65235c62"></span>
## VeLivePlayerResolution

型別：`enum`

播放器解析度。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerResolutionOrigin |`0` |原始。 |
|VeLivePlayerResolutionUHD |`1` |超高畫質（UHD）。 |
|VeLivePlayerResolutionHD |`2` |高畫質（HD）。 |
|VeLivePlayerResolutionSD |`3` |標準畫質（SD）。 |
|VeLivePlayerResolutionLD |`4` |低畫質（LD）。 |


<span id="f6547cab"></span>
## VeLivePlayerConfiguration

型別：`class`

播放器初始化的配置。

<span id="fe0901c6"></span>
### enableSei

型別：`boolean`

是否啟用 SEI 訊息解析。預設值為 `false`。


* true：啟用；

* false：停用。


<span id="df72ece1"></span>
### enableHardwareDecode

型別：`boolean`

是否啟用硬體解碼。預設值為 `true`。啟用硬體解碼時，若播放器無法啟動硬體解碼或硬體解碼失敗，將自動切換為軟體解碼。


* true：啟用；

* false：停用。


<span id="290f3c15"></span>
### networkTimeoutMs

型別：`number`

網路逾時時間（毫秒）。預設值為 `5000`。若播放器發送網路請求並在此時間內未收到伺服器回應，則視為請求失敗。

<span id="3a98bfb1"></span>
### retryIntervalTimeMs

型別：`number`

重試時間間隔（毫秒）。預設值為 `5000`。此變數僅在無備用串流時生效。


* 若無備用串流且播放中斷，播放器會立即執行前三次重試。後續重試時，播放器會在每次嘗試間等待指定的時間間隔。

* 若有備用串流，則此時間間隔不適用，所有重試皆為即時。


<span id="408e6d5e"></span>
### retryMaxCount

型別：`number`

播放器在網路連線錯誤時自動重試的最大次數。預設值為 `5`。若值為 `0`，播放器將不會自動重試。


* 若無備用串流，每次重試皆計為一次嘗試。

* 有備用串流時，主串流與備用串流間的每次切換皆計為一次重試。


<span id="3dd01afc"></span>
### enableLiveDNS

型別：`boolean`

是否啟用本地 DNS 預取。預設值為 `false`。啟用本地 DNS 預取可減少啟動播放所需時間。若本地 DNS 預取異常，播放器可能無法正常運作。


* true：啟用；

* false：停用。


<span id="3722a3b3"></span>
### enableStatisticsCallback

型別：`boolean`

是否啟用播放資訊的定期回調。預設值為 `false`。如需回調統計資訊，請參考 [VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstatistics-VeLivePlayerStatistics)。若 `enableStatisticsCallback` 為 `true` 且 [statisticsCallbackInterval](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#statisticsCallbackInterval) 大於 `0`，播放器將以指定間隔定期回報播放器狀態資訊。


* true：啟用；

* false：停用。


<span id="42c645fb"></span>
### statisticsCallbackInterval

型別：`number`

提供播放資訊的定期回調時間間隔（秒）。預設值為 `5`。若 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) 為 `true` 且 `statisticsCallbackInterval` 大於 `0`，播放器將以指定間隔定期回報播放器狀態資訊。

<span id="d1a34194"></span>
## VeLivePlayerFormat

型別：`enum`

直播串流格式。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerFormatFLV |`0` |FLV。 |
|VeLivePlayerFormatHLS |`1` |HLS。 |
|VeLivePlayerFormatRTM |`2` |即時媒體（RTM）。 |


<span id="09205021"></span>
## VeLivePlayerProtocol

型別：`enum`

傳輸協議。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerProtocolTCP |`0` |TCP。 |
|VeLivePlayerProtocolQUIC |`1` |QUIC。 |
|VeLivePlayerProtocolTLS |`2` |TLS。 |


<span id="1697047e"></span>
## VeLivePlayerMirror

型別：`enum`

鏡像選項。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerMirrorNone |`0` |無鏡像。 |
|VeLivePlayerMirrorHorizontal |`1` |水平鏡像。 |
|VeLivePlayerMirrorVertical |`2` |垂直鏡像。 |


<span id="f920d758"></span>
## VeLivePlayerVideoBufferType

型別：`enum`

視訊資料封裝格式。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerVideoBufferTypeUnknown |`0` |未知格式。 |
|VeLivePlayerVideoBufferTypeByteBuffer |`1` |ByteBuffer。 |
|VeLivePlayerVideoBufferTypeByteArray |`2` |ByteArray。 |
|VeLivePlayerVideoBufferTypeTexture |`3` |Texture。 |
|VeLivePlayerVideoBufferTypePixelBuffer |`5` |CVPixelBufferRef。 |
|VeLivePlayerVideoBufferTypeSampleBuffer |`6` |CVSampleBufferRef。 |
|VeLivePlayerVideoBufferTypeNSData |`7` |NSData。 |


<span id="01afecd2"></span>
## VeLivePlayerStatus

型別：`enum`

直播播放器狀態。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerStatusStopped |`3` |播放已停止。 |
|VeLivePlayerStatusPaused |`2` |播放已暫停。 |
|VeLivePlayerStatusPrepared |`0` |播放器已完成準備，正在等待渲染影片。 |
|VeLivePlayerStatusPlaying |`1` |目前正在播放，表示已渲染首幀且播放器未發生錯誤。 |
|VeLivePlayerStatusError |`4` |播放器發生錯誤。 |


<span id="5c0fa055"></span>
## VeLivePlayerStreamData

型別：`class`

拉流地址的配置。

<span id="5504a465"></span>
### enableABR

型別：`boolean`

是否啟用自適應碼率（ABR）。預設值為 `false`。


* true：啟用；

* false：停用。


<span id="44dc7c26"></span>
### enableMainBackupSwitch

型別：`boolean`

是否啟用主備流切換。預設值為`false`。


* true：啟用；

* false：停用。


<span id="faaef3c9"></span>
### defaultResolution

型別：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution)

預設解析度。預設值為`VeLivePlayerResolutionOrigin`，表示原始解析度。詳情請參見[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution)。

<span id="e2f2349a"></span>
### defaultFormat

型別：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

預設視訊格式。預設值為`VeLivePlayerFormatFLV`。詳情請參見[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat)。

<span id="fbb7f54a"></span>
### defaultProtocol

型別：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol)

預設傳輸協定。預設值為`VeLivePlayerProtocolTCP`。詳情請參見[VeLivePlayerProtocol](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol-VeLivePlayerProtocol)。

<span id="ac4718ec"></span>
### mainStreamList

型別：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstream)`[]`

主流地址清單。詳情請參見[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream)。

<span id="2665c9ff"></span>
### backupStreamList

型別：[VeLivePlayerStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstream)`[]`

備流地址清單。詳情請參見[VeLivePlayerStream](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamdata-veliveplayerstream)。

<span id="a39ca559"></span>
## VeLivePlayerStream

型別：`class`

拉流地址的相關資訊。

<span id="9246292c"></span>
### url

型別：`string`

拉流地址。

<span id="891004c9"></span>
### resolution

型別：[VeLivePlayerResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution)

播放解析度。詳情請參見[VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerresolution-VeLivePlayerResolution)。

<span id="c51a333d"></span>
### bitrate

型別：`number`

播放碼率，單位為 Kbps。

<span id="f3412c31"></span>
### format

型別：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

直播流格式。詳情請參見[VeLivePlayerFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat-VeLivePlayerFormat)。

<span id="e555376b"></span>
### android_streamType

型別：`$p_a.VeLivePlayerStreamType`

該流為主流或備流。詳情請參見[VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerstreamtype-VeLivePlayerStreamType)。

<span id="cc5a63ce"></span>
## VeLivePlayerResolutionSwitchReason

型別：`enum`

視訊解析度變更的原因。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerResolutionSwitchByAuto |`0` |通過自適應碼率（ABR）功能自動切換解析度。 |
|VeLivePlayerResolutionSwitchByManual |`1` |呼叫[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#switchresolution)後變更解析度。 |


<span id="d4e1b91a"></span>
## VeLivePlayerFillMode

型別：`enum`

播放器畫面的填充模式。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerFillModeAspectFit |`0` |完整顯示影片。影片會等比例縮放，直到其中一個維度達到螢幕邊緣。螢幕上剩餘的空間將以黑色填充。 |
|VeLivePlayerFillModeFullFill |`1` |拉伸影片以填滿螢幕。影片的長寬比可能會改變。 |
|VeLivePlayerFillModeAspectFill |`2` |等比例縮放影片，直到螢幕被完全填滿。影片的部分區域可能會被裁切。 |


<span id="14681414"></span>
## VeLivePlayerPixelFormat

型別：`enum`

視訊畫格的像素格式。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerPixelFormatUnknown |`0` |未知格式。 |
|VeLivePlayerPixelFormatRGBA32 |`1` |RGBA8888。 |
|VeLivePlayerPixelFormatTexture |`2` |Texture。 |
|VeLivePlayerPixelFormatNV12 |`4` |NV12。 |
|VeLivePlayerPixelFormatI420 |`5` |YUVI420。 |
|VeLivePlayerPixelFormatBGRA32 |`6` |BGRA。 |


<span id="42dab9d5"></span>
## VeLivePlayerStatistics

型別：`class`

播放統計資訊。

<span id="61826fbb"></span>
### url

型別：`string`

`Readonly`，當前拉流地址。

<span id="b7665147"></span>
### isHardwareDecode

型別：`boolean`

`Readonly`，是否使用硬體解碼。


* true：使用硬體解碼；

* false：未使用硬體解碼。


<span id="b1a67af1"></span>
### videoCodec

型別：`string`

`Readonly`，視訊的編碼格式。

<span id="ff1c2c2b"></span>
### stallTimeMs

型別：`number`

唯讀。自播放開始以來的累計卡頓時長，單位為毫秒。

<span id="52ab55f5"></span>
### bandwidthEstimation

型別：`number`

`Readonly`。預估網路頻寬，單位為 Kbps。

<span id="91cbeb50"></span>
### delayMs

型別：`number`

`Readonly`。當前播放延遲，單位為毫秒。

<span id="5b2b1e4d"></span>
### width

型別：`number`

`Readonly`，視訊寬度，單位為像素。

<span id="82f859ce"></span>
### height

型別：`number`

`Readonly`，視訊高度，單位為像素。

<span id="c17e971b"></span>
### fps

型別：`number`

`Readonly`，視訊幀率，單位為 fps。

<span id="4b750f0d"></span>
### bitrate

型別：`number`

`Readonly`，下行碼率，單位為 Kbps。

<span id="81991728"></span>
### videoBufferMs

型別：`number`

`Readonly`，視訊緩衝，單位為毫秒。

<span id="49e1695c"></span>
### audioBufferMs

型別：`number`

`Readonly`，音訊緩衝，單位為毫秒。

<span id="0cdc5e51"></span>
### format

型別：[VeLivePlayerFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerformat)

`Readonly`，視訊格式。

<span id="3499bbac"></span>
### protocol

型別：[VeLivePlayerProtocol](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerprotocol)

`Readonly`，直播流的傳輸協定。

<span id="fece7704"></span>
## VeLivePlayerVideoFrame

型別：`class`

視訊畫格。

<span id="4dbce073"></span>
### bufferType

型別：[VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype)

封裝格式。詳情請參見[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)。

<span id="50fa9b75"></span>
### pixelFormat

型別：[VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat)

像素格式。詳情請參見[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)。

<span id="ce5a457e"></span>
### width

型別：`number`

視訊寬度，單位為像素。

<span id="b344efd5"></span>
### height

型別：`number`

視訊高度，單位為像素。

<span id="ce308637"></span>
### pts

型別：`number`

畫格渲染時的時間戳，單位為毫秒。

<span id="82d59e1c"></span>
### android_buffer

型別：`ArrayBuffer`

ByteBuffer 格式的視訊資料。若將[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)設為`VeLivePlayerPixelFormatRGBA32`，且[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)設為`VeLivePlayerVideoBufferTypeByteBuffer`，SDK 會回傳此類型的視訊資料。

<span id="38e94a83"></span>
### data

型別：`ArrayBuffer`

ByteArray 格式的視訊資料。若將[VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayerpixelformat-VeLivePlayerPixelFormat)設為`VeLivePlayerPixelFormatRGBA32`，且[VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayervideobuffertype-VeLivePlayerVideoBufferType)設為`VeLivePlayerVideoBufferTypeByteArray`，SDK 會回傳此類型的視訊資料。

<span id="9a3421e5"></span>
## VeLivePlayerStreamType

型別：`enum`

直播流型別。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerStreamTypeMain |`0` |主串流。 |
|VeLivePlayerStreamTypeBackup |`1` |備用串流。 |


<span id="ebd2a745"></span>
## VeLivePlayerLogLevel

型別：`enum`

播放器的日誌輸出等級。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerLogLevelVerbose |`0` |輸出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelDebug |`1` |輸出 DEBUG、INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelInfo |`2` |輸出 INFO、WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelWarn |`3` |輸出 WARNING 和 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelError |`4` |輸出 ERROR 等級的日誌。 |
|VeLivePlayerLogLevelNone |`5` |停用日誌列印。 |


<span id="e9e49d32"></span>
## VeLivePlayerAudioFrame

型別：`class`

音訊畫格。

<span id="036d4e51"></span>
### bufferType

型別：[VeLivePlayerAudioBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayeraudiobuffertype)

音訊資料的封裝格式。詳情請參見[VeLivePlayerAudioBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#veliveplayeraudiobuffertype-VeLivePlayerAudioBufferType)。

<span id="391ed2fc"></span>
### sampleRate

型別：`number`

音訊取樣率，單位為 Hz。

<span id="4edbca80"></span>
### channels

型別：`number`

音訊聲道數。


* 1：單聲道；

* 2：雙聲道。


<span id="72e1439e"></span>
### bitDepth

型別：`number`

音訊位元深度。

<span id="9193b964"></span>
### pts

型別：`number`

音訊渲染時的時間戳，單位為毫秒。

<span id="c89d0e21"></span>
### android_buffer

型別：`ArrayBuffer`

PCM 音訊資料。

<span id="e9a450c4"></span>
### 取樣數

型別：`number`

音訊取樣的數量。

<span id="a6083ccc"></span>
## VeLivePlayerAudioBufferType

型別：`enum`

音訊的封裝格式。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerAudioBufferTypeUnknown |`0` |未知格式。 |
|VeLivePlayerAudioBufferTypeByteArray |`1` |ByteArray。 |
|VeLivePlayerAudioBufferUnknown |`3` |未知格式。 |
|VeLivePlayerAudioBufferTypeSampleBuffer |`4` |CVSampleBufferRef。音訊資料將以 sample buffer 方式處理並渲染。 |
|VeLivePlayerAudioBufferTypeNSData |`5` |NSData。音訊資料將以 NSData 物件方式處理並渲染。 |


<span id="7877b1de"></span>
## VeLivePlayerRotation

型別：`enum`

順時針的影片旋轉角度。


|屬性 |值 |說明 |
|---|---|---|
|VeLivePlayerRotation0 |`0` |不旋轉。 |
|VeLivePlayerRotation90 |`1` |順時針旋轉 90 度。 |
|VeLivePlayerRotation180 |`2` |順時針旋轉 180 度。 |
|VeLivePlayerRotation270 |`3` |順時針旋轉 270 度。 |


<span id="8c318281"></span>
## InitOptions

型別：`interface`

播放器初始化的設定。

<span id="97db5320"></span>
### enableSei

型別：`boolean`

是否啟用 SEI 訊息的解析。預設值為 `false`。


* true：啟用；

* false：停用。


<span id="4028f347"></span>
### enableHardwareDecode

型別：`boolean`

是否啟用硬體解碼。預設值為 `true`。啟用硬體解碼時，若播放器無法啟動硬體解碼或硬體解碼失敗，則會自動切換為軟體解碼。


* true：啟用；

* false：停用。


<span id="ab9aff33"></span>
### networkTimeoutMs

型別：`number`

網路逾時時長（毫秒）。預設值為 `5000`。若播放器發送網路請求，在此時長內未收到伺服器回應，則認為請求失敗。

<span id="41b9ab3e"></span>
### retryIntervalTimeMs

型別：`number`

重試的時間間隔（毫秒）。預設值為 `5000`。僅當無備用串流時，此變數才生效。


* 若無備用串流且播放中斷，播放器會立即執行前三次重試。後續重試時，播放器會在每次重試之間等待指定的時間間隔。

* 若有備用串流，則此時間間隔不適用，所有重試皆為即時執行。


<span id="41b89fbd"></span>
### retryMaxCount

型別：`number`

當發生網路連線錯誤時，播放器自動重試的最大次數。預設值為 `5`。若設為 `0`，則播放器不會自動重試。


* 若無備用串流，每次重試皆計為一次。

* 若有備用串流，主串流與備用串流之間的每次切換皆計為一次重試。


<span id="ba175414"></span>
### enableLiveDNS

型別：`boolean`

是否啟用本地 DNS 預取。預設值為 `false`。啟用本地 DNS 預取可縮短啟動播放所需的時間。若本地 DNS 預取發生異常，播放器可能無法正常運作。


* true：啟用；

* false：停用。


<span id="bf2254dc"></span>
### enableStatisticsCallback

型別：`boolean`

是否啟用播放資訊的定期回調。預設值為 `false`。更多回調統計資訊請參考 VeLivePlayerStatistics。若 `enableStatisticsCallback` 為 `true` 且 statisticsCallbackInterval 大於 `0`，播放器會依指定間隔定期回報播放器狀態資訊。


* true：啟用；

* false：停用。


<span id="ac0baf49"></span>
### statisticsCallbackInterval

型別：`number`

提供播放資訊的定期回調時間間隔（秒）。預設值為 `5`。若 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-type-definition#enableStatisticsCallback) 為 `true` 且 `statisticsCallbackInterval` 大於 `0`，播放器會依指定間隔定期回報播放器狀態資訊。

<span id="dae2ea8d"></span>
### viewId

型別：`number`

播放器視圖的 ID

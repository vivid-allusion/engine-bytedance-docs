---
title: "React Native 播放器 SDK：API 參考"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW"
---

<span id="veliveplayer"></span>
## VeLivePlayer

類型：`class`

直播播放器。

<span id="f0fdefd0"></span>
### setConfig()

初始化播放器，並配置是否啟用 SEI 訊息、硬體解碼、本地 DNS 預取等其他設定。

**說明**

請於呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) 前，先呼叫此方法以初始化播放器。

**類型**

```TypeScript
(config: VeLivePlayerConfiguration) => void
```



* **參數**

   * **config**


類型：`VeLivePlayerConfiguration`

播放器設定。詳情請參閱 [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerConfiguration)。

<span id="76d86fb7"></span>
### setObserver()

設置播放器監聽器，用於監聽直播播放器的事件，例如播放錯誤或狀態更新、首幀音訊與視訊渲染，以及解析度切換等。

**說明**

請於呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#play) 前呼叫此方法。

**類型**

```TypeScript
(observer: VeLivePlayerObserver) => void
```



* **參數**

   * **observer**


類型：`VeLivePlayerObserver`

播放器監聽器。詳情請參閱 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerObserver)。

<span id="c1362d95"></span>
### setRenderFillMode()

設置播放器畫面的填充模式。

**說明**


* 請於呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-play) 前呼叫此方法，以設置播放器的初始填充模式。

* 可於播放過程中動態呼叫此方法以調整填充模式。


**類型**

```TypeScript
(fillMode: VeLivePlayerFillMode) => Promise<void>
```



* **參數**

   * **fillMode**


類型：`VeLivePlayerFillMode`

SurfaceView 的填充模式。預設值為 `VeLivePlayerFillModeAspectFill`。詳情請參閱 [VeLivePlayerFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerFillMode)。

**回傳值**

`Promise<void>`

<span id="4850159c"></span>
### setPlayUrl()

設置拉流地址。

**說明**

請於呼叫 play 前呼叫此方法。

**類型**

```TypeScript
(url: string) => void
```



* **參數**

   * **url**


類型：`string`

拉流地址。

<span id="08be74d7"></span>
### setPlayStreamData()

設置多路直播流。如需啟用多路直播流相關功能（如自適應碼率（ABR）、手動解析度切換、主備流等），請呼叫此方法。

**說明**

請於呼叫 play 前呼叫此方法。

**類型**

```TypeScript
(streamData: VeLivePlayerStreamData) => void
```



* **參數**

   * **streamData**


類型：`VeLivePlayerStreamData`

多路拉流地址設定。詳情請參閱 [VeLivePlayerStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerStreamData)。

<span id="c10943ab"></span>
### play()

開始或恢復播放。

**說明**

呼叫此方法後，當播放器完成拉流準備以及首幀渲染時，皆會觸發 `onPlayerStatusUpdate` 回呼。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="bfe7e8f4"></span>
### pause()

暫停播放。

**說明**

呼叫此方法後，當播放被暫停時，會觸發 `onPlayerStatusUpdate` 回呼。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="821b628f"></span>
### stop()

停止播放。此方法不會銷毀播放器。

**說明**

呼叫此方法後，當播放停止時，會觸發 `onPlayerStatusUpdate` 回呼。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="2ba0cb65"></span>
### destroy()

停止播放並銷毀播放器。

**類型**

```TypeScript
() => void
```


<span id="b875a31c"></span>
### switchResolution()

切換視訊解析度。

**說明**


* 請於呼叫此方法前，先透過 [setPlayStreamData](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#veliveplayer-setplaystreamdata) 設定多個解析度。

* 呼叫此方法後，當播放器切換至新解析度時，會觸發 [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback-zh-TW#onresolutionswitch) 回呼。


**類型**

```TypeScript
(resolution: VeLivePlayerResolution) => void
```



* **參數**

   * **resolution**


類型：`VeLivePlayerResolution`

視訊解析度。詳情請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerResolution)。

**回傳值**


* true：成功；

* false：失敗。


<span id="a1c9ecfc"></span>
### isPlaying()

檢查播放器是否正在播放。

**類型**

```TypeScript
() => boolean
```


**回傳值**

`boolean` 播放器是否正在播放。


* true：播放器正在播放；

* false：播放器未在播放。


<span id="8aae15c5"></span>
### setPlayerVolume()

設置播放器音量。

**類型**

```TypeScript
(volume: number) => void
```



* **參數**

   * **volume**


類型：`number`

音量。預設值為 `1.0`。取值範圍為 [0.0, 1.0]。

<span id="8031bd6b"></span>
### setMute()

設置是否靜音播放。

**類型**

```TypeScript
(mute: boolean) => void
```



* **參數**

   * **mute**


類型：`boolean`

是否靜音播放。預設值為 `false`。

```Plain Text
  * true：靜音；
  * false：不靜音。
```


<span id="abca2b64"></span>
### isMute()

檢查播放是否為靜音狀態。

**類型**

```TypeScript
() => boolean
```


**回傳值**

`boolean` 是否為靜音狀態。


* true：已靜音；

* false：未靜音。


<span id="2b9af50b"></span>
### setProperty()

配置播放器進階設定，包括離屏渲染、最大緩衝時長、自適應碼率（ABR）演算法等。如需進一步資訊，請聯繫 BytePlus 技術支援。

**類型**

```TypeScript
(key: string, value: Object) => void
```



* **參數**

   * **key**


類型：`string`

進階設定的參數名稱。


* **value**


類型：`Object`

進階設定的參數值。

<span id="7b8ee64b"></span>
### setRenderRotation()

設定影片的順時針旋轉角度。

**說明**


* 你可以在播放前或播放期間變更旋轉角度。

* 每次呼叫此方法時，播放器都會根據原始影片進行旋轉。

* 當同時對影片套用旋轉與鏡像時，播放器會先鏡像影片，再進行旋轉。


**類型**

```TypeScript
(rotation: VeLivePlayerRotation) => Promise<void>
```



* **參數**

   * **rotation**


類型：`VeLivePlayerRotation`

影片的順時針旋轉角度。預設不啟用旋轉。詳情請參閱 [VeLivePlayerRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerRotation)。

**回傳值**

`Promise<void>`

<span id="691650f7"></span>
### setRenderMirror()

設定鏡像參數。

**說明**


* 你可以在播放前或播放期間變更鏡像設定。

* 每次呼叫此方法時，播放器都會將鏡像設定套用至原始影片。

* 當同時對影片套用旋轉與鏡像時，播放器會先鏡像影片，再進行旋轉。


**類型**

```TypeScript
(mirror: VeLivePlayerMirror) => Promise<void>
```



* **參數**

   * **mirror**


類型：`VeLivePlayerMirror`

鏡像設定。預設不啟用鏡像。詳情請參閱 [VeLivePlayerMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerMirror)。

**回傳值**

`Promise<void>`

<span id="4859375d"></span>
### setEnableSuperResolution()

啟用或停用超解析度。使用前，必須先聯繫 BytePlus [technical support](https://www.byteplus.com/en/support) 開通此功能。

**說明**


* 請於收到 [onFirstVideoFrameRender](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback-zh-TW#onfirstvideoframerender) 回呼後或播放期間呼叫此方法。

* 若因裝置型號、影片解析度或幀率導致 SDK 無法啟用超解析度，將收到 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution) 回呼。


**類型**

```TypeScript
(enable: boolean) => void
```



* **參數**

   * **enable**


類型：`boolean`

是否啟用超解析度。

<span id="42746901"></span>
### startPictureInPicture()

啟用子母畫面（PiP）模式，並將播放器顯示於浮動視窗。

**類型**

```TypeScript
(aspectRatio?: number, x?: number, y?: number) => Promise<void>
```



* **參數**

   * **aspectRatio**


類型：`number`

PiP 視窗的寬高比（寬度 / 高度）。


* **x**


類型：`number`

距離螢幕左上角的水平偏移量（像素）。


* **y**


類型：`number`

距離螢幕左上角的垂直偏移量（像素）。

**回傳值**

`Promise<void>`

<span id="024a4f92"></span>
### stopPictureInPicture()

退出子母畫面（PiP）模式。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="26ed0a11"></span>
### isPictureInPictureSupported()

檢查目前環境是否支援子母畫面（PiP）模式。

**類型**

```TypeScript
() => boolean
```


**回傳值**

`boolean` 是否支援 PiP。


* true：支援。

* false：不支援。


<span id="c83adae8"></span>
### setPictureInPictureListener()

設定 PiP 相關事件的監聽器，例如 PiP 啟用、停用或錯誤。

**類型**

```TypeScript
(listener: PictureInPictureManagerListener) => void
```



* **參數**

   * **listener**


類型：`PictureInPictureManagerListener`

PiP 事件的監聽器。

<span id="09029475"></span>
### enablePictureInPicture()

 **(iOS only)**  當應用程式進入背景時，自動啟用 PiP 模式。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="5623783f"></span>
### disablePictureInPicture()

 **(iOS only)**  停用自動 PiP 模式。

**類型**

```TypeScript
() => Promise<void>
```


**回傳值**

`Promise<void>`

<span id="703db4e3"></span>
### `static` getVersion()

取得 Player SDK 的版本號。

**類型**

```TypeScript
() => string
```


**回傳值**

`string` Player SDK 的版本號。

<span id="a366ca4f"></span>
### `static` setLogLevel()

設定輸出日誌的等級。

**類型**

```TypeScript
(logLevel: VeLivePlayerLogLevel) => void
```



* **參數**

   * **logLevel**


類型：`VeLivePlayerLogLevel`

輸出日誌的等級。詳情請參閱 [VeLivePlayerLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api#VeLivePlayerLogLevel)。

---
title: "React Native 播放器 SDK：回調"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback-zh-TW"
---

<span id="veliveplayerobserver"></span>
## VeLivePlayerObserver

類型：`interface`

直播播放器觀察者。

<span id="c107d3ac"></span>
### onError

當播放器發生錯誤時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **error**


類型：`VeLivePlayerError`

錯誤訊息。詳情請參閱 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。

<span id="e161397d"></span>
### onFirstVideoFrameRender

當播放開始或重試後渲染出第一幀視訊畫面時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **isFirstFrame**


類型：`boolean`

該視訊畫面是否為播放開始時渲染的第一幀。

```Plain Text
  * true：該視訊畫面為播放開始時渲染的第一幀；
  * false：該視訊畫面為播放過程中重試後渲染的第一幀。
```


<span id="4454587f"></span>
### onFirstAudioFrameRender

當播放開始或重試後渲染出第一幀音訊畫面時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, isFirstFrame: boolean) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **isFirstFrame**


類型：`boolean`

該音訊畫面是否為播放開始時渲染的第一幀。

```Plain Text
  * true：該音訊畫面為播放開始時渲染的第一幀；
  * false：該音訊畫面為播放過程中重試後渲染的第一幀。
```


<span id="4d9fbfd7"></span>
### onStallStart

當播放卡頓開始時觸發。

**類型**

```TypeScript
((player: VeLivePlayer) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。

<span id="2976e8f1"></span>
### onStallEnd

當播放卡頓結束（即音訊緩衝足夠後恢復播放）時觸發。

**類型**

```TypeScript
((player: VeLivePlayer) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。

<span id="8c25e99c"></span>
### onVideoRenderStall

當視訊渲染卡頓時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **stallTime**


類型：`number`

卡頓持續時間（毫秒）。

<span id="6188cc0f"></span>
### onAudioRenderStall

當音訊渲染卡頓時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, stallTime: number) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **stallTime**


類型：`number`

卡頓持續時間（毫秒）。

<span id="f370517e"></span>
### onResolutionSwitch

當視訊解析度變更時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, resolution: VeLivePlayerResolution, error: VeLivePlayerError, reason: VeLivePlayerResolutionSwitchReason) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **resolution**


類型：`VeLivePlayerResolution`

更新後的解析度。詳情請參閱 [VeLivePlayerResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolution)。


* **error**


類型：`VeLivePlayerError`

解析度切換過程中是否發生錯誤。詳情請參閱 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。


* **reason**


類型：`VeLivePlayerResolutionSwitchReason`

解析度切換的原因。詳情請參閱 [VeLivePlayerResolutionSwitchReason](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerResolutionSwitchReason)。

<span id="c146e694"></span>
### onVideoSizeChanged

當視訊尺寸變更時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, width: number, height: number) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **width**


類型：`number`

更新後的視訊寬度（像素）。


* **height**


類型：`number`

更新後的視訊高度（像素）。

<span id="ab9560b3"></span>
### onReceiveSeiMessage

當 Player SDK 收到 SEI 訊息時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, message: string) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **message**


類型：`string`

SEI 訊息。

<span id="08f634f6"></span>
### onMainBackupSwitch

當播放器在主串流與備用串流間切換時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, streamType: VeLivePlayerStreamType, error: VeLivePlayerError) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **streamType**


類型：`VeLivePlayerStreamType`

更新後的串流類型。詳情請參閱 [VeLivePlayerStreamType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStreamType)。


* **error**


類型：`VeLivePlayerError`

切換原因。詳情請參閱 [VeLivePlayerError](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerError)。

<span id="330b176b"></span>
### onPlayerStatusUpdate

當播放狀態變更時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, status: VeLivePlayerStatus) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **status**


類型：`VeLivePlayerStatus`

播放器更新後的狀態。詳情請參閱 [VeLivePlayerStatus](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatus)。

<span id="a2085fca"></span>
### onStatistics

定期發生，用於回報當前拉流地址、碼率與幀率等資訊。

**類型**

```TypeScript
((player: VeLivePlayer, statistics: VeLivePlayerStatistics) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **statistics**


類型：`VeLivePlayerStatistics`

播放統計資訊。詳情請參見[VeLivePlayerStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerStatistics)。

<span id="6e424102"></span>
### onSnapshotComplete

呼叫截圖後觸發。

**類型**

```TypeScript
((player: VeLivePlayer, bitmap: any) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **bitmap**


類型：`any`

截圖對應的 Bitmap 物件。

<span id="fbfd4048"></span>
### onRenderVideoFrame

播放器解碼出一幀影像時觸發。

**說明**

若使用紋理格式進行外部渲染，建議於回調執行緒中渲染影像。

**類型**

```TypeScript
((player: VeLivePlayer, videoFrame: VeLivePlayerVideoFrame) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **videoFrame**


類型：`VeLivePlayerVideoFrame`

影像幀，包含像素格式、封裝格式、影像寬高等資訊。詳情請參見[VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerVideoFrame)。

<span id="a60df3d8"></span>
### onRenderAudioFrame

播放器解碼出一幀音訊時觸發。呼叫enableAudioFrameObserver以啟用音訊幀回調。

**說明**

回調返回的音訊資料型別為 Float32，且為大端位元組序。

**類型**

```TypeScript
((player: VeLivePlayer, audioFrame: VeLivePlayerAudioFrame) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **audioFrame**


類型：`VeLivePlayerAudioFrame`

音訊幀。詳情請參見[VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#VeLivePlayerAudioFrame)。

<span id="b65fb8f4"></span>
### onStreamFailedOpenSuperResolution

呼叫 setEnableSuperResolution 後，SDK 啟用超分辨率失敗時觸發。

**類型**

```TypeScript
((player: VeLivePlayer, error: VeLivePlayerError) => void) | undefined
```



* **參數**

   * **player**


類型：[VeLivePlayer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-zh-TW#veliveplayer)

觸發回調函式的播放器物件。


* **error**


類型：`VeLivePlayerError`

失敗原因。詳情請參見[VeLivePlayerErrorCode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api-error-code-zh-TW#veliveplayererrorcode)。

<span id="bd30cb5c"></span>
## PictureInPictureManagerListener

類型：`interface`

用於監聽子母畫面（PiP）相關事件的介面，例如狀態變化或使用者互動。

<span id="731525d9"></span>
### onStartPictureInPicture

啟動子母畫面模式時觸發。

可透過此回調更新 UI 狀態或新增分析追蹤。

**類型**

```TypeScript
(() => void) | undefined
```


<span id="1dfac6bc"></span>
### onStopPictureInPicture

結束子母畫面模式時觸發，可能由使用者操作或程式控制。

**類型**

```TypeScript
(() => void) | undefined
```


<span id="25914b59"></span>
### onClickPictureInPicture

 **（僅限 Android）**  點擊子母畫面視窗時觸發。可利用此回調響應使用者對 PiP 視窗的互動。

**類型**

```TypeScript
(() => void) | undefined
```


<span id="5922d709"></span>
### onError

發生與子母畫面模式相關的錯誤時觸發。可利用此回調進行錯誤回報或備援處理。

**類型**

```TypeScript
((code: number, extraData: any) => void) | undefined
```



* **參數**

   * **code**


類型：`number`

錯誤碼。


* 0：成功

* 1：不支援

* 2：參數無效

* 3：PiP 已啟用

   * **extraData**


類型：`any`

用於除錯或錯誤處理的額外資料。

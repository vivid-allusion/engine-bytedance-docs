---
title: "Web 端播放器 SDK：API 參考"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-api-reference-zh-TW"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文適用於 BytePlus MediaLive Web 端播放器 SDK 1.x 版本。強烈建議升級至最新版本，以獲得最佳播放體驗。</div>


本主題介紹 BytePlus MediaLive Web 端播放器 SDK（亦稱 VePlayer）的方法、回調及參數。

<span id="Parameters"></span>
## **參數**

您可以在建立 VePlayer 實例時，通過設置`options`來配置播放器：

```javascript
var player = new VePlayer(options);
```


以下列表包含播放器支援的部分配置：


* 拉流地址與協議

* 語言設置

* 軟硬體解碼

* 播放控制


<span id="options"></span>
### **options**

VePlayer 的配置項。


|**參數** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|isLive |Boolean |false |是否播放直播流。請務必設為`true`。 |
|id |String |無 |插入 VePlayer 的容器 ID。必須設置`id` 或 `root`。若同時設置兩個參數，VePlayer 將插入由`root`指定的容器。 |
|root |HTMLElement |無 |插入 VePlayer 的容器 ID。必須設置`id` 或 `root`。若同時設置兩個參數，VePlayer 將插入由`root`指定的容器。 |
|url |String |無 |拉流地址。您可以手動拼接地址，或使用[地址生成器](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)來生成地址。必須設置`url` 或 `playList`。 |
|playList |Array |無 |拉流地址列表。詳情請參見[playListItem](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#playListItem)。必須設置`url` 或 `playList`。 |
|plugins |Any |無 |自訂外掛。您可以傳入多個外掛，並以逗號分隔。 |
|languages |Object |無 |播放器在顯示使用者介面文字時所參考的字典。請搭配 `lang` 參數使用，此參數可設定播放器語言。你可以自定義字典，或使用 [default dictionary](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary)。請按照以下格式定義字典：`{[key: string]: object;}`。例如，`{ zh: { PIP: '畫中畫' }, en: { PIP: 'pip' }}`。 |
|useSoftDecoding |Boolean |false |是否啟用軟體解碼。<br><br><br>* `true`：啟用軟體解碼。<br><br>* `false`：不啟用軟體解碼。<br><br><br>播放器在某些 Android 瀏覽器中可能會被劫持，導致部分功能無法使用。你可以使用軟體解碼來解決此問題。<br><br>行動瀏覽器不支援播放 FLV 格式的串流。若需播放此格式，請使用軟體解碼。<br><br>[部分瀏覽器](https://caniuse.com/?search=HEVC)不支援 H.265 編碼格式。若需播放此編碼格式的影片，請使用軟體解碼。<br><br>軟體解碼依賴裝置的 CPU。播放高碼率與高解析度影片會導致 CPU 占用率偏高。 |
|enableH265Degrade |Boolean |false |是否啟用自動降級至 H.265 軟體解碼。啟用後，若瀏覽器不支援 H.265 硬體解碼，SDK 會自動切換至 H.265 軟體解碼。<br><br><br>* `true`：啟用自動降級。<br><br>* `false`：停用自動降級。 |
|codec |String |'h265' |影片串流的編碼格式。若設定 `enableH265Degrade` 為 `true` 以啟用自動降級至 H.265 軟體解碼，建議設定此參數。 |
|sdkErrorPlugin |[SdkErrorConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#SdkErrorConfig) |None |錯誤資訊。當播放器發生錯誤時，你可以配置文字、圖片及重新整理按鈕。 |
|rtm |[RtmConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#RtmConfig) |None |即時媒體（RTM）配置。僅當 `url` 設為 RTM 拉流地址時，此參數才會生效。 |
|width |String｜Number |100% |播放器的寬度。<br><br>若 `width` 設為包含百分比符號的字串，例如 `'30%'`，SDK 會將其視為播放器相對於容器的寬度。若字串不含百分比符號，例如 `'300'` 或 `'300px'`，SDK 會將其視為播放器的絕對寬度（單位：像素）。<br><br>若 `width` 設為數字，例如 `300`，SDK 會將其視為播放器的絕對寬度（單位：像素）。 |
|height |String｜Number |100% |播放器的高度。<br><br>若 `height` 設為包含百分比符號的字串，例如 `'30%'`，SDK 會將其視為播放器相對於容器的高度。若字串不含百分比符號，例如 `'300'` 或 `'300px'`，SDK 會將其視為播放器的絕對高度（單位：像素）。<br><br>若 `height` 設為數字，例如 `300`，SDK 會將其視為播放器的絕對高度（單位：像素）。 |
|volume |Number |0.6 |播放器的預設音量。有效範圍：[0, 1] |
|autoplay |Boolean |true |是否啟用自動播放。<br><br><br>* `true`：啟用自動播放。<br><br>* `false`：停用自動播放。僅當最終使用者點擊播放按鈕時才會開始播放。 |
|autoplayMuted |Boolean |true |是否在自動播放時靜音音訊。僅當你將`autoplay`設為`true`時，此參數才會生效。<br><br><br>* `true`：自動播放時靜音音訊。<br><br>* `false`：自動播放時不靜音音訊。 |
|poster |String |None |封面圖片的 URL。 |
|pip |Boolean |true |是否啟用子母畫面（PiP）。<br><br><br>* `true`：啟用子母畫面。<br><br>* `false`：停用子母畫面。 |
|fullscreen |[fullscreen](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#fullscreen) |None |與全螢幕模式相關的配置。 |
|lang |String |zh |播放器的顯示語言。預設語言包括：<br><br><br>* `zh`<br><br>* `en`<br><br>* `jp`<br><br>* `zh-hk` |
|liveInfoPanel |[LiveInfoPanel](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#LiveInfoPanel) |None |顯示串流資訊的面板。SDK 支援顯示 HLS 與 FLV 串流的資訊。在使用該面板前，必須先新增 LiveInfoPanel 外掛：`plugins: [window.VePlayer.LiveInfoPanel]`。 |
|timeShiftPlugin |[timeShiftPlugin](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#2f07a993) |None |時移功能相關配置。有關如何實現時移功能，請參考[Time shifting](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-features#cc924516)。 |
|liveLogger |[liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) |None |日誌配置。 |
|Subtitle |[Subtitle](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#subtitle) |None |字幕相關配置。僅當你指定此參數時，播放器才會顯示字幕。 |


<span id="fullscreen"></span>
### **fullscreen**

與全螢幕模式相關的配置。


|**名稱** |**資料型別** |**預設值** |**描述** |
|---|---|---|---|
|rotateFullscreen |Boolean |false |是否啟用自動旋轉至橫屏模式。啟用後，若使用者以直向持握手機並將播放器切換至全螢幕模式，SDK 會將播放器旋轉 90 度至橫屏模式。此功能常用於行動裝置。此參數會覆蓋`useCssFullscreen`的設定。<br><br><br>* `true`：啟用自動旋轉至橫屏模式。<br><br>* `false`：停用自動旋轉至橫屏模式。 |
|useCssFullscreen |Boolean |false |是否使用全視窗或全螢幕模式。<br><br><br>* `true`：全視窗模式，播放器覆蓋瀏覽器視窗。<br><br>* `false`：全螢幕模式，播放器覆蓋整個桌面。 |
|needBackIcon |Boolean |false |播放器進入全螢幕模式時，是否在右上角顯示返回按鈕。此功能常用於行動裝置。<br><br><br>* `true`：顯示按鈕。<br><br>* `false`：不顯示按鈕。 |


<span id="playListItem"></span>
### **playListItem**

拉流地址的詳細資訊。您可以配置多個不同解析度的地址。


|**名稱** |**資料型別** |**預設值** |**描述** |
|---|---|---|---|
|streamType |String |None |拉流協議。若你在`playList`中指定的拉流地址無副檔名，則必須設置`streamType`。支援的值包括：<br><br><br>* `rtm`<br><br>* `flv`<br><br>* `mp4`<br><br>* `hls` |
|url |String |None |拉流地址。你可以手動拼接地址，或使用[地址生成器](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)產生地址。此參數為必填。 |
|definition |String |None |串流的影片解析度，對應你在 BytePlus MediaLive 控制台配置的[轉碼模板](https://docs.byteplus.com/byteplus-media-live/docs/configuring-transcoding)。你可以傳入多個來源 ID（`lineId`）相同但解析度不同的拉流地址。建議值包括：<br><br><br>* `uhd`<br><br>* `hd`<br><br>* `sd`<br><br>* `ld`<br><br>* `ao` |
|definitionTextKey |String |`definition`的值 |串流影片解析度的語言鍵。預設情況下，播放器會顯示`definition`的值。需與`languages`搭配使用。例如，若你將`definitionTextKey`設為`HD_TEXT_KEY`，並將`languages`設為`{ en: { HD_TEXT_KEY: 'High definition' }}`，則播放器會顯示**High definition**作為串流的解析度。 |
|lineId |String |None |來源 ID。你可以傳入多個來源 ID 相同但解析度（`definition`）不同的拉流地址。 |
|lineTextKey |String |None |串流 ID 的語言鍵。例如，若將`lineTextKey`設為`LINE_ONE`，並將`languages`設為`{ en: { LINE_ONE: 'Line one' }}`，播放器會將**Line one**顯示為串流的 ID。 |
|backUrlList |陣列 |無 |備援拉流位址。若將`sdkErrorPlugin.isNeedDemoteBack`設為`true`，當主串流發生錯誤時，播放器會自動切換至備援串流。 |


<span id="SdkErrorConfig"></span>
### **SdkErrorConfig**

播放器的錯誤資訊。當播放器發生錯誤時，您可以配置顯示的文字、圖片及重新整理按鈕。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|errorImg |布林值 |true |發生錯誤時是否顯示圖片。<br><br><br>* `true`：顯示圖片。<br><br>* `false`：不顯示圖片。 |
|errorTips |布林值 |true |報錯時是否顯示錯誤訊息。預設錯誤訊息為「播放時發生錯誤，請點擊重新整理重試」，可透過在`languages`中設定`errorTips`來自訂。<br><br>例如，可將`languages`設為 { en: { errorTips: 'Player error' } }。 |
|isNeedRefreshButton |布林值 |true |發生錯誤時是否顯示重新整理按鈕。<br><br><br>* `true`：顯示按鈕。<br><br>* `false`：不顯示按鈕。 |
|retryLoopNum |數值 |1 |在播放器介面顯示錯誤前的重試次數。 |
|isNeedDemoteBack |布林值 |false |播放過程中發生錯誤時，是否降級切換至備援串流。<br><br><br>* `false`：不降級。播放器顯示錯誤訊息。<br><br>* `true`：發生錯誤時，切換至由`playListItem.backUrlList`定義的備援串流。 |


<span id="RtmConfig"></span>
### **RtmConfig**

拉取 RTM 流的配置。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|loadTimeout |數值 |5000 |拉流重試的最大等待時間（毫秒）。 |
|retryDelay |數值 |1000 |每次拉流重試的間隔時間（毫秒）。 |
|retryCount |數值 |0 |拉流重試的最大次數。 |
|backupURL |字串 |無 |當拉取 RTM 串流失敗時，播放器切換至的備援 FLV 或 HLS 串流。<br><br>若指定`backupURL`，播放器會啟用自動切換。<br><br>若未指定`backupURL`，當 RTM 串流播放失敗時，播放器會報錯且不會切換至備援串流。 |
|backupStreamType |字串 |無 |備援拉流位址的協定，需與`backupURL`搭配設定。支援的值包括：<br><br><br>* flv<br><br>* hls |
|delayHint |數值 |0 |音視頻的緩衝時間（秒）。 |


<span id="LiveInfoPanel"></span>
### **LiveInfoPanel**

用於顯示播放器內串流資訊面板的配置。串流資訊包括播放器中的串流格式、碼率與幀率。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|visible |布林值 |true |是否顯示面板。<br><br><br>* `true`：顯示面板。<br><br>* `false`：不顯示面板。 |
|showH265Info |布林值 |false |是否顯示 H.265 相關資訊，如解碼效率與 CPU 消耗。<br><br><br>* `true`：顯示資訊。<br><br>* `false`：不顯示資訊。<br><br><br>僅當`showH265Info`為`true`且瀏覽器使用軟體解碼時，播放器才會顯示 H.265 相關資訊。 |


<span id="2f07a993"></span>
### timeShiftPlugin

時移功能的配置。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|livingStartTime |數值 |目前時間 |直播會話開始的時間。Unix 時間戳（秒）。時間需依瀏覽器時區指定。 |
|maxMoveTime |數值 |604800 |播放過程中可時移的最長時間（秒）。例如，若將`maxMoveTime`設為`60`，表示超過 60 秒前的內容將無法再播放。有效範圍：[6,604800]。 |


<span id="liveLogger"></span>
### **liveLogger**

日誌上傳的配置。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|appId |String |None |應用程式 ID，為您的應用程式的唯一識別碼。請聯絡[BytePlus 技術支援](https://console.byteplus.com/workorder/create)以取得您的應用程式 ID。 |
|enable |Boolean |true |是否啟用將日誌上傳至 BytePlus MediaLive 伺服器。<br><br><br>* `true`：啟用日誌上傳。<br><br>* `false`：停用日誌上傳。 |
|userId |String |None |使用者 ID。我們強烈建議您設定能識別唯一使用者的值。技術支援可能需要此資訊以協助排查問題。若未定義`userId`及`deviceId`，SDK 會自動產生隨機的使用者 ID 與裝置 ID，並儲存於瀏覽器快取中。 |
|deviceId |String |None |裝置 ID。我們強烈建議您設定能識別唯一使用者裝置的值。技術支援可能需要此資訊以協助排查問題。若未定義`userId`及`deviceId`，SDK 會自動產生隨機的使用者 ID 與裝置 ID，並儲存於瀏覽器快取中。 |


<span id="200897d1"></span>
### **Subtitle**

影片字幕的配置。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|isDefaultOpen |Boolean |None |是否預設顯示字幕。<br><br><br>* `true`：預設顯示字幕。<br><br>* `false`：預設不顯示字幕。 |
|mode |"external" |"native" |None |
|updateMode |String |'live' |請務必設定為`'live'`。 |
|style |[style](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference-zh-TW#d1c656ee) |None |字幕樣式的配置。 |


<span id="d1c656ee"></span>
### **style**

字幕樣式的配置。


|**名稱** |**資料型別** |**預設值** |**說明** |
|---|---|---|---|
|follow |Boolean |true |是否根據播放器控制面板調整字幕位置。<br><br><br>* `true`：調整。<br><br>* `false`：不調整。 |
|mode |String |'stroke' |字體顯示模式。<br><br><br>* `'stroke'`：為文字添加描邊。<br><br>* `'bg'`：為文字添加陰影。 |
|followBottom |Boolean |true |是否根據播放器控制面板的垂直位置調整字幕位置。<br><br><br>* `true`：調整。<br><br>* `false`：不調整。 |
|fitVideo |Boolean |true |是否根據影片尺寸調整字體大小。<br><br><br>* `true`：調整。<br><br>* `false`：不調整。 |
|offsetBottom |Integer |4 |字幕與影片底部距離占影片高度的百分比。 |
|baseSizeX |Integer |49 |使用者橫向持手機時的預設字體大小。 |
|baseSizeY |Integer |28 |使用者直向持手機時的預設字體大小。 |
|minSize |Integer |16 |PC 裝置上的最小字體大小。 |
|minMobileSize |Integer |13 |行動裝置上的最小字體大小。 |
|line |'single' |'double' |'three' |
|fontColor |String |'#fff' |字體顏色。 |


<span id="Methods"></span>
## **方法**

本節將以`player.on()`為例，介紹 VePlayer 的方法，調用範例如下。

```javascript
var player = new VePlayer(options)

player.on('player_create_finish', () => {
    console.log('The player is created.')
})
```


方法列表如下。


|**名稱** |**說明** |
|---|---|
|[on()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#on()) |監聽事件。 |
|[once()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#once()) |僅監聽一次事件。 |
|[off()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#off()) |停止監聽事件。 |
|[destroy()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#destroy()) |銷毀播放器。 |
|[player.play()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#play()) |開始播放。 |
|[player.pause()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#pause()) |暫停播放。 |
|[player.retry()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#retry()) |重新整理播放器。 |
|[player.switchURL()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#switchURL()) |切換至其他拉流地址。 |


<span id="on()"></span>
### **on()** 

監聽事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**參數**


* `Action`：型別為`string`

* `Func`：型別為`(... args: any []) => void`


<span id="once()"></span>
### **once()** 

僅監聽一次事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**參數**


* `Action`：型別為`string`

* `Func`：型別為`(... args: any []) => void`


<span id="off()"></span>
### **off()** 

停止監聽事件。

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**參數**


* `Action`：型別為`string`

* `Func`：型別為`(... args: any []) => void`


<span id="destroy()"></span>
### **destroy()** 

銷毀當前播放器實例。

```typescript
() => Promise<void>
```


<span id="play()"></span>
### **play()** 

開始播放。

```typescript
() => Promise<void>
```


**範例程式碼**

範例 1

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play()
```


範例 2

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play().then(() => {
    // Actions to take if the playback starts successfully.
}).catch(() => {
    // Actions to take if the playback fails to start.通常發生於自動播放且無任何使用者互動時。
})
```


<span id="pause()"></span>
### **pause()** 

暫停播放。

```typescript
() => void
```


**範例程式碼**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.pause()
```


<span id="retry()"></span>
### **retry()** 

重新整理播放器。

```TypeScript
() => void
```


**範例程式碼**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.retry()
```


<span id="switchURL()"></span>
### **switchURL()** 

切換至其他拉流地址。

```TypeScript
(src: string) => void
```


**參數**


* `src`：型別為`string`


**範例程式碼**

```javascript
var veplayer = new VePlayer(options)
veplayer.switchURL('http://example.com');
```


<span id="Events"></span>
## **事件**

SDK 可監聽以下事件：


|**事件** |**事件值** |**說明** |
|---|---|---|
|PLAYER_CREATED_FINISH |'player_create_finish' |播放器已建立。 |
|PLAYER_REBUILD |'player_rebuild' |播放器銷毀後再次建立。 |
|CANCEL_UNMUTE |'cancel_unmute' |解除靜音。 |
|REFRESH_CLICK |'refresh_click' |使用者點擊重新整理按鈕。 |
|PLAY_BACKUP_CHANGE |'play_backup_change' |發生錯誤後觸發降級。 |
|PLAY_BACKUP_CHANGE_FINISH |'play_backup_change_finish' |發生錯誤後，降級已完成。 |
|PLAY_ERROR_BUTTON_CLICK |'play_error_button_click' |發生錯誤後會觸發重試。 |
|PlAY_URL_CHANGE |'play_url_change' |播放器切換至新的拉流地址。 |
|SHOW_PLAY_ERROR |'show_play_error' |播放器顯示錯誤。 |
|LONG_WAITING |'long_waiting' |超過最大等待時間，之後可能會發生降級。 |
|INNER_DEFINITION_CHANGE |'inner_definition_change' |播放器切換至其他解析度。 |
|LINE_CHANGE |'line_change' |播放器切換至其他來源。 |
|ENDED |'ended' |直播已結束。 |

---
title: "Web Viewer SDK：事件"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW"
---

<span id="8dc10ebf"></span>
## SDKEventsOn

類型：`interface`

<span id="9c9808ec"></span>
### player.play

當播放器開始播放影片時觸發。

```TypeScript
() => void
```


<span id="d5f99339"></span>
### player.playing

當播放器在暫停或緩衝後恢復播放時觸發。

```TypeScript
() => void
```


<span id="88ceb878"></span>
### player.pause

當影片被暫停時觸發。

```TypeScript
() => void
```


<span id="5a73f0eb"></span>
### player.ended

當影片播放結束時觸發。

```TypeScript
() => void
```


<span id="5a2cf424"></span>
### player.destroy

當播放器被銷毀時觸發。

```TypeScript
() => void
```


<span id="23e7aee8"></span>
### player.ratechange

當播放速度變更時觸發。

```TypeScript
(rate: number) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|rate |Number |播放速度。<br><br>有效值：<br><br><br>* `0.5`：半速。<br><br>* `0.75`：0.75 倍速。<br><br>* `1`：正常速度。<br><br>* `1.25`：1.25 倍速。<br><br>* `1.5`：1.5 倍速。<br><br>* `2`：雙倍速。 |


<span id="b703ce9a"></span>
### player.fullscreen_change

當全螢幕模式變更時觸發。

```TypeScript
(isFullScreen: boolean) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|isFullScreen |Boolean |表示播放器是否進入或退出全螢幕模式。<br><br><br>* `true`：進入全螢幕。<br><br>* `false`：退出全螢幕。 |


<span id="6c44f68d"></span>
### player.pip_change

當子母畫面（PiP）模式變更時觸發。

```TypeScript
(isPip: boolean) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|isPip |Boolean |表示觀眾是否在電腦端切換至或離開子母畫面（PiP）模式。<br><br>有效值：<br><br><br>* `true`：進入子母畫面（PiP）模式。<br><br>* `false`：退出子母畫面（PiP）模式。 |


<span id="33a46182"></span>
### player.waiting

當播放器等待資料載入時觸發。

```TypeScript
() => void
```


<span id="0cb32046"></span>
### player.status

當直播間狀態變更時觸發。

```TypeScript
(status: string) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|status |String |直播間狀態。<br><br>有效值：<br><br><br>* Live<br><br>* Preview<br><br>* Playback<br><br>* Over |


<span id="a87308eb"></span>
### player.vodConfigChange

用於從斷點恢復預覽或回放的事件。

當播放器正在播放預覽或回放時，於下列情況會觸發此事件：


* 觀眾在電腦端關閉觀看頁面。

* WebView 的 `pagehide` 事件被觸發，或觀眾於行動裝置上手動拖曳進度條。


```TypeScript
(VodInfo: { vid: string; currentTime: number; duration: number;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|VodInfo |\- |影片（預覽或回放）資訊。 |
|vid |String |影片 ID，即影片的唯一識別碼。 |
|currentTime |Number |目前播放時間（秒）。 |
|duration |Number |影片總長度。單位：秒。 |


<span id="64d88d3e"></span>
### comment.focus

當點擊或輕觸互動聊天選單下的留言文字框時觸發。

```TypeScript
() => void
```


<span id="1ee55848"></span>
### comment.send

當留言送出時觸發。

```TypeScript
(msg: string) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|msg |String |已發送的留言。 |


<span id="6e1a3846"></span>
### comment.nickNameClick

當於聊天區點擊或輕觸暱稱時觸發。

```TypeScript
(data: { Nickname: string; ExternalId: string; isTop: boolean; isPresenter: boolean;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|data |\- |被點擊或觸控的用戶暱稱資訊。 |
|Nickname |String |用戶暱稱。 |
|ExternalId |String |外部用戶 ID。 |
|isTop |Boolean |表示留言是否置頂於聊天室區域。<br><br><br>* `true`：已置頂。<br><br>* `false`：未置頂。 |
|isPresenter |Boolean |表示用戶是否為主持人。<br><br><br>* `true`：主持人。<br><br>* `false`：非主持人。 |


<span id="c91cc8cb"></span>
### permission.need

可利用此事件判斷是否需觸發自有帳號系統的登入流程。

若 `mode` 的值為 `1` 且 `disabledLogin` 的值為 `true`，則在需要用戶資訊的場景下會觸發此事件，例如觀眾點擊留言文字框或按讚留言時。

此事件觸發後，必須啟動自有帳號系統的登入流程。然後，請使用 `updateMode2Token` 方法，將 token 從 mode 1 token 更新為 mode 2 token。

```TypeScript
() => void
```


<span id="a92d7f8b"></span>
### lines.number

當行數變更時觸發。

```TypeScript
(lines: number) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|lines |Number |* 直播間狀態為 **Live** 時的直播來源數量。<br><br>* 直播間狀態為 **Playback** 時的回放數量。 |


<span id="59ec7864"></span>
### activity.status

當直播間狀態變更時觸發。

```TypeScript
(status: 1 | 2 | 3 | 4) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|status |1 |2<br><br><br>* `1`：直播。<br><br>* `2`：預覽。<br><br>* `3`：回放。<br><br>* `4`：結束。 |


<span id="44166c70"></span>
### reservation.click

當點擊或輕觸 **立即預約** 按鈕時觸發。

```TypeScript
() => void
```


<span id="799a1022"></span>
### reservation.attend

當直播被預約時觸發。

```TypeScript
(tel: string) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|tel |String |預約電話號碼。 |


<span id="2011f69b"></span>
### card.click

當點擊或輕觸商品卡片時觸發。

可將 `disableCardRedirect` 設為 `true`，並監聽此事件以實作自訂導向邏輯。

```TypeScript
(card: { text: string; url: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|card |\- |商品卡片資訊。 |
|text |String |商品名稱。 |
|url |String |商品網址。<br><br>該參數是否有值取決於在控制台設定或呼叫伺服器端 API（如支援）時的配置。 |


<span id="7f70dfa5"></span>
### card.configChange

當商品卡片資訊變更時觸發。

```TypeScript
(productInfo: ProductInfo) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-xing-bie-ding-yi-zh-TW#fe534689)[] |已更新的商品卡片資訊。 |


<span id="9c17df67"></span>
### popularity.configChange

當觀看頁面顯示的觀眾人數變更時觸發。

```TypeScript
(data: {Popularity?:number, PeopleCountEnable?:boolean}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|data |\- |人氣資訊。 |
|Popularity |Number |在觀看頁面顯示的觀眾人數。 |
|PeopleCountEnable |Boolean |是否啟用 **人氣顯示**功能。有效值：<br><br><br>* `true`：已啟用。<br><br>* `false`：未啟用。 |


<span id="163fd7d0"></span>
### floatingCard.update

當浮動商品卡片被更新時觸發。

```TypeScript
(productInfo: ProductInfo) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-xing-bie-ding-yi-zh-TW#fe534689)[] |已更新的商品卡片資訊。 |


<span id="d6026ee7"></span>
### floatingCard.click

當點擊或輕觸浮動商品卡片時觸發。

可將 `disableCardRedirect` 設為 `true`，並監聽此事件以自行實作導向功能。

```TypeScript
(card: { text: string; url: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|card |\- |商品卡片資訊。 |
|text |String |商品名稱。 |
|url |String |商品網址。<br><br>該參數是否有值取決於在控制台設定或呼叫伺服器端 API（如支援）時的配置。 |


<span id="9bff3721"></span>
### lottery.click

當點擊或輕觸抽獎圖示時觸發。

```TypeScript
(award: { awardId: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|awardId |String |抽獎 ID |


<span id="09d83b77"></span>
### lottery.attend

當觀眾參與抽獎時觸發。

```TypeScript
(award: { awardId: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|awardId |String |抽獎 ID |


<span id="4175a516"></span>
### lottery.result

當中獎者產生時觸發。僅當觀眾在直播間內且產生中獎者時才會觸發此事件。

```TypeScript
(award: { awardId: string; ifWin: boolean;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|awardId |String |抽獎 ID |
|ifWin |Boolean |表示觀眾是否中獎。<br><br><br>* `true`：中獎。<br><br>* `false`：未中獎。 |


<span id="95464d32"></span>
### lottery.winInfo

當觀眾中獎後提交個人資訊時觸發。

```TypeScript
(award: { awardId: string; awardTel: string; awardAddress?: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|awardId |String |抽獎 ID |
|awardTel |String |觀眾填寫的電話號碼。<br><br>該參數是否有值取決於主控台設定或是否呼叫伺服器端 API（如支援）。 |
|awardAddress |String |觀眾填寫的收貨地址。<br><br>該參數是否有值取決於主控台設定或是否呼叫伺服器端 API（如支援）。 |


<span id="e290813e"></span>
### lotteryTicket.click

當點擊或輕觸兌獎券獎品的領獎連結時觸發。

```TypeScript
(award: { url: string; ActivityId: string; TaskAwardId: string; TaskAwardItemId: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|url |String |領獎連結。 |
|ActivityId |String |直播間活動 ID。 |
|TaskAwardId |String |抽獎配置 ID。 |
|TaskAwardItemId |String |依觀看時長抽獎的獎品 ID。 |


<span id="5e56de30"></span>
### taskAwardPanel.pop

當顯示觀看時長抽獎的對話框時觸發。

```TypeScript
(award: { config: TaskAwardConfig | null; viewedTime: number; isLogin: boolean; winningRecordMap: Map<string, IRecordInfo>;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|config |TaskAwardConfig |null<br><br><br>* `TaskAwardId: string`：活動 ID。<br><br>* `TaskAwardRule: TaskAwardRuleItem[]`：抽獎規則，包括`index: number`（獎品序號，0 為一等獎，1 為二等獎，依此類推）、`TaskAwardItemId: string`（獎品 ID）、以及`WatchTime: number`（總觀看時長要求，單位：分鐘）。<br><br>* `TaskAwardStartTime: number`：抽獎活動開始時間（Unix 時間戳）。單位：秒。<br><br>* `TaskAwardEndTime: number`：抽獎活動結束時間（Unix 時間戳）。單位：秒。<br><br>* `TaskAwardStatus`：活動狀態。<br><br>   * `NULL(-1)`：無抽獎活動。預留未來擴充使用。<br><br>   * `INIT(0)`：初始化。活動尚未開始。<br><br>   * `START(1)`：活動進行中。<br><br>   * `END(2)`：活動已結束。<br><br>   * `CLOSE(3)`：活動已關閉。 |
|viewedTime |Number |觀眾累計的總觀看時長。單位：秒。 |
|isLogin |Boolean |表示觀眾是否已登入直播間。<br><br><br>* `true`：已登入。<br><br>* `false`：未登入。 |
|winningRecordMap |Map<string, IRecordInfo\> |觀眾的中獎紀錄。 |


<span id="1ba87761"></span>
### taskAwardBox.click

當點擊或觸碰觀看時長抽獎的中獎結果時觸發。

```TypeScript
(award: { index: number; WatchTime: number;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|award |\- |抽獎資訊。 |
|index |Number |寶箱的序號，從 0 開始。 |
|WatchTime |Number |觀眾累計的總觀看時長。單位：分鐘。 |


<span id="0062c289"></span>
### share.click

在 PC 上點擊**分享**，或在行動裝置上點擊**複製連結**或**儲存 QR Code**時觸發。

```TypeScript
() => void
```


<span id="b649c7cc"></span>
### poster.click

當點擊或觸碰邀請海報時觸發。

```TypeScript
() => void
```


<span id="d05864eb"></span>
### adFloating.click

當點擊或觸碰浮動廣告時觸發。僅當廣告配置了嵌入連結時才會觸發此事件。

你可以將`disableAdFloatingRedirect`的值設為`true`，並監聽此事件以自行實現跳轉功能。

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|ad |\- |廣告資訊。 |
|AdvertisementRedirectUrl |String |嵌入連結。 |


<span id="c1ff1133"></span>
### adMiddle.click

當點擊或觸碰頁內廣告時觸發。僅當廣告配置了嵌入連結時才會觸發此事件。

你可以將`disableAdMiddleRedirect`的值設為`true`，並監聽此事件以自行實現跳轉功能。

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|ad |\- |廣告資訊。 |
|AdvertisementRedirectUrl |String |嵌入連結。 |


<span id="3d0f7998"></span>
### adAccount.click

當點擊或觸碰主辦帳號時觸發。僅當主辦帳號配置了嵌入連結時才會觸發此事件。

你可以將`disableAdAccountRedirect`的值設為`true`，並監聽此事件以自行實現跳轉功能。

```TypeScript
(account: { AccountHeadRedirectUrl: string;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|account |\- |主播帳號資訊。 |
|AccountHeadRedirectUrl |String |嵌入連結。 |


<span id="1fc6e72e"></span>
### ready

當 Web Viewer SDK 初始化完成時觸發。觸發此事件並不代表影片播放已開始。

```TypeScript
() => void
```


<span id="93a24cfc"></span>
### menu.click

當點擊或觸碰選單時觸發。

```TypeScript
(tab: { terminal: 'pc' | 'mobile'; layout?: 'portrait'; tab: number;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|tab |\- |選單資訊。 |
|terminal |"pc" |"mobile"<br><br><br>* `"pc"`：電腦端。<br><br>* `"mobile"`：行動裝置。 |
|layout |"portrait" |undefined |
|tab |Number |選單類型。<br><br><br>* `3`：聊天互動選單。<br><br>* `31`：頂級評論選單。<br><br>* `5`：彙總直播流選單。<br><br>* `2`：商品卡片選單。<br><br>* `1`：圖形選單。<br><br>* `4`：互動工具選單。<br><br>* `6`：問答選單。<br><br>* `7`：嵌入連結選單。 |


<span id="750ccd04"></span>
### thumbs.click

當直播間被按讚時觸發。

```TypeScript
(thumb: { count: number;}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|thumb |\- |按讚資訊。 |
|count |數字 |按讚數量。 |


<span id="96c0ddb3"></span>
### lines.current

在下列情況下觸發：


* 當直播間狀態為**直播**時，觀眾點擊或觸碰直播源。

* 當直播間狀態為**回放**時，觀眾點擊或觸碰回放影片。


通常此事件會與`switchChannel` API 搭配使用。

```TypeScript
(lines: number) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|lines |數字 |被點擊或觸控的直播來源或回放影片的零起始索引。 |


<span id="75c92017"></span>
### activity.pcu

當觀眾進入觀看頁面時觸發。此事件用於檢查在訂閱直播並發觀眾數方案後，帳號下所有狀態為**直播**的直播間總峰值並發用戶數（PCU）是否超過並發上限。更多資訊請參見[Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/gong-neng-shi-xian-1-1-zh-TW#db59dce3)。

```TypeScript
(value: {isPCUFull: boolean}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|value |\- |PCU 資訊。 |
|isPCUFull |布林值 |您的帳戶下所有狀態為 **Live** 的直播間總 PCU 是否超過並發上限。有效值：<br><br><br>* `true`：超過上限。<br><br>* `false`：未超過上限。 |


<span id="7bd143bd"></span>
### shopCart.click

當在行動裝置的觀看頁面點擊購物車圖示時觸發。

將`disabledShopCartClick`的值設為`true`，然後監聽此事件以實現自定義邏輯。關於`disabledShopCartClick`的更多資訊，請參見[Web Viewer SDK：參數](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW)。

```TypeScript
() => void
```


<span id="d476ef36"></span>
### gift.click

無論`disableSendGift`設定如何，當觀眾點擊或觸碰禮物時觸發。

```TypeScript
(value:{data:{"GiftId": number; "GiftName": string; "GiftImage": string; "GiftPrice": string; "Index": number}}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|data |\- |禮物資訊。 |
|GiftId |數字 |此類禮物的唯一 ID。 |
|GiftName |字串 |禮物名稱。 |
|GiftImage |字串 |禮物圖片的 URL。 |
|GiftPrice |字串 |禮物單價。 |
|Index |數字 |禮物索引，表示禮物在觀看頁面的位置。 |


<span id="83e8b67c"></span>
### gift.sendError

無論`disableSendGift`設定如何，當觀眾送禮時因積分不足或請求異常發生錯誤時觸發。

將`disableSendGift`的值設為`true`，然後監聽此事件以實現自定義邏輯，例如當積分不足錯誤發生時顯示要求觀眾儲值積分的頁面。關於`disableSendGift`的更多資訊，請參見[Web Viewer SDK：參數](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW)。

```TypeScript
(value:{data:string|number}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|data |字串 |數字 |


<span id="e862732b"></span>
### gift.show

無論`disableSendGift`設定如何，當觀眾送禮時觸發。

將 `disableSendGift` 的值設為 `true`，然後監聽此事件以實現自定義邏輯，例如自訂禮物效果。如需瞭解 `disableSendGift` 的更多資訊，請參閱 [Web Viewer SDK：參數](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW)。

```TypeScript
(value: {data: GiftInfo[]}) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|data |[GiftInfo](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-xing-bie-ding-yi-zh-TW#e7c20786)[] |已送出禮物及送禮用戶的資訊。 |


<span id="4fa82edf"></span>
### giftPoint.result

觸發時機：


* 觀眾送出禮物後，禮物點數被更新

* 觀眾主動查詢禮物點數後，會呼叫 `webSDK.emit('gift.pointQuery')`


```TypeScript
(value: { point: number }) => void
```


**參數**


|名稱 |資料型別 |說明 |
|---|---|---|
|point |數字 |觀眾目前的禮物點數餘額。 |


**使用範例**

```TypeScript
// Step 1. Actively query the gift point
webSDK.emit('gift.pointQuery');

// Step 2. Listen for the result
webSDK.on('giftPoint.result', point => {
  console.log('Current gift point:', point);
  // You can update UI or trigger custom logic here
});
```


<span id="d83da9df"></span>
## SDKEventsEmit

類型：`enum`


|屬性 |值 |說明 |
|---|---|---|
|play |`'player.play'` |播放影片。 |
|pause |`'player.pause'` |暫停影片。 |
|pip |`'player.pip'` |在電腦上切換至小視窗模式或從小視窗模式切回原始畫面。<br><br><br>* `true`：切換至小視窗模式。<br><br>* `false`：從小視窗模式切回原始畫面。<br><br><br>範例程式碼：<br><br>```JavaScript```<br>```webSDK.emit('player.pip', {```<br>```    ifShow: true,```<br>```})```<br> |
|comment.send |`'comment.send'` |發送評論。<br><br>範例程式碼：<br><br>```JavaScript```<br>```webSDK.emit('comment.send', 'BytePlus Live');```<br> |
|comment.disabled |`'comment.disabled'` |禁用或啟用評論輸入框。<br><br><br>* 禁用：`webSDK.emit('comment.disabled', true)`<br><br>* 啟用：`webSDK.emit('comment.disabled', false)`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅在使用 <code>disabledCommentConfig</code> 參數配置評論框的禁用狀態及占位文字後，才能觸發此事件。更多資訊請參見 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#b6fb0c34">選項</a>。</div><br> |
|gift.send |`'gift.send'` |在 [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#d476ef36) 事件觸發後發送指定數量的禮物。`count` 的預設值為 `1`。您可以根據需求自定義 `count` 的值。<br><br>建議將 `disableSendGift` 的值設為 `true`，以禁用預設的 UI 相關送禮邏輯。<br><br>範例程式碼：<br><br>```JavaScript```<br>```webSDK.emit('gift.send', {```<br>```    ...value.data,```<br>```    count:10 // The number of gifts to send.```<br>```  });```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">有關 <code>disableSendGift</code> 的更多資訊，請參見 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW">Web Viewer SDK：參數</a>。</div><br> |
|gift.pointQuery |`'gift.pointQuery'` |查詢觀眾的禮物點數餘額。 |
|playbackListBtn.click |`'playbackListBtn.click'` |模擬點擊回放列表按鈕。 |

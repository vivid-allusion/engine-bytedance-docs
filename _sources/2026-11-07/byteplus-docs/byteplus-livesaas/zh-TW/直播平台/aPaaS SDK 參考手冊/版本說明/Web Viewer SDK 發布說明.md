---
title: "Web Viewer SDK 發布說明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/web-viewer-sdk-fa-bu-shuo-ming-zh-TW"
---

在此查閱 Web Viewer SDK 的所有變更。

<span id="d7e0d7a1"></span>
## 2026 年 8 月


|發布日期 |版本 |描述 |
|---|---|---|
|2026\-08\-12 |2.0.31 |**優化**<br><br>更新了 CSS 樣式。 |


<span id="july-2026"></span>
## 2026 年 7 月


|發布日期 |版本 |描述 |
|---|---|---|
|2026\-07\-23 |2.0.30 |**優化**<br><br><br>* 新增對商品卡片多環境直達連結功能的支援。<br><br>* 新增在直播範本中配置**按讚**和**人氣顯示**的支援。<br><br><br>**相容性變更**<br><br>自 v2.0.30 起，集成 SDK 時，域名已由 `https://res.bytepluscdn.com/obj/bp-console-fe-sg` 更改為 `https://res.gcloudcache.com/bp-fe`。詳情請參見 [整合方式](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-web-viewer-sdk-zh-TW#855885cc)。 |


<span id="0bc95836"></span>
## 2026 年 2 月


|發布日期 |版本 |描述 |
|---|---|---|
|2026\-02\-02 |2.0.27\-beta.4 |**問題修復**<br><br>修復了一些問題。 |


<span id="8e7d0d0f"></span>
## 2026 年 1 月


|發布日期 |版本 |描述 |
|---|---|---|
|2026\-01\-12 |2.0.27\-beta.2（僅播放器集成）及 2.0.27\-beta.3 |本次發佈包含內部優化。未涉及功能變更，現有用法不受影響。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">為確保服務穩定與持續支援，請更新至最新版本。詳情請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#7f20b494">Step 1: Import CSS and JS resources</a>。</div><br> |
|2026\-01\-06 |2.0.27 |**問題修復**<br><br>修復了一些問題。 |


<span id="67d0f65a"></span>
## 2025 年 12 月


|發布日期 |版本 |描述 |
|---|---|---|
|2025\-12\-10 |2.0.25 |**優化**<br><br><br>* 人氣顯示<br><br>   * 新增參數 `disablePopularityShow`，用於指定是否關閉觀看頁面的人數顯示。詳情請參見 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>   * 新增 `popularity.configChange` 事件，當觀看頁面顯示的人數變化時觸發。詳情請參見 [popularity.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#9c17df67)。<br><br>* 商品<br><br>   * 新增參數 `shopCartIcon`，用於指定購物車圖標配置。詳情請參見 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>   * 新增參數 `disabledShowExplainCard`，用於指定當商品被推薦時，是否關閉觀看頁面的浮動商品卡片。詳情請參見 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>   * 新增 `floatingCard.update` 事件，當浮動商品卡片更新時觸發。詳情請參見 [floatingCard.update](https://docs.byteplus.com/docs/byteplus-livesaas/events#163fd7d0)。 |


<span id="3cc7c0a1"></span>
## 2025 年 11 月


|發布日期 |版本 |描述 |
|---|---|---|
|2025\-11\-12 |2.0.24 |**優化**<br><br>為 `defaultLang` 參數新增更多語言支持。詳情請參見 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br><br>* 他加祿語<br><br>* 高棉語<br><br>* 老撾語<br><br>* 緬甸語<br><br>* 馬來語<br><br>* 印地語<br><br>* 法語<br><br>* 德語<br><br>* 義大利語 |


<span id="62f42b28"></span>
## 2025 年 10 月


|發布日期 |版本 |描述 |
|---|---|---|
|2025\-10\-16 |2.0.23 |**新功能**<br><br><br>* 商品<br><br>   * 新增 [ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689) 類型。<br><br>   * 新增 `card.configChange` 事件，當商品卡片配置變更時觸發。詳情請參見 [card.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#7f70dfa5)。<br><br>   * 新增以下 API。詳情請參見 [API](https://docs.byteplus.com/docs/byteplus-livesaas/api)。<br><br>      * `getProductList()`<br><br>      * `updateProductInfo()`<br><br>* 回放列表<br><br>   * 新增以下參數：<br><br>      * `vodSwitchMode`：指定自定義 VOD 播放模式。<br><br>      * `enablePlaybackSwitchBtn`：控制播放列表按鈕的顯示。<br><br>      * `enablePlaybackListPopup`：控制回放合集列表的顯示。<br><br>      * `playbackMode`：指定回放合集列表的播放模式。詳情請參見 [Options](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#b6fb0c34)。<br><br>   * 新增 `playbackListBtn.click` 事件，當點擊回放合集按鈕時觸發。詳情請參見 [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0)。<br><br>   * 針對觀看頁自定義回放合集列表，新增以下 API。詳情請參見 [API](https://docs.byteplus.com/docs/byteplus-livesaas/api)。<br><br>      * `showPlaybackListPopup()`<br><br>      * `hidePlaybackListPopup()`<br><br>      * `getPlayBackListInfo()`<br><br>      * `lockPlayBackVods()`<br><br>      * `unlockPlayBackVods()`<br><br>* 新增 `preloadActivity()` API，用於預加載並緩存直播間數據，以加速基於 feed 的房間切換。詳情請參見 [API](https://docs.byteplus.com/docs/byteplus-livesaas/api)。 |


<span id="46cb2a55"></span>
## 2025 年 9 月


|發布日期 |版本 |描述 |
|---|---|---|
|2025\-09\-18 |2.0.22 |**問題修復**<br><br>修復了一些問題。 |
|2025\-09\-05 |2.0.21 |**相容性變更**<br><br>自 v2.0.21 起，集成 SDK 時，域名已由 `https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm` 更改為 `https://res.bytepluscdn.com/obj/bp-console-fe-sg`。詳情請參見 [Integration method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#855885cc)。 |


<span id="0d3910db"></span>
## 2025 年 8 月


|發布日期 |版本 |描述 |
|---|---|---|
|2025\-08\-28 |2.0.20 |**新功能**<br><br><br>* 禮物<br><br>   * 新增 [giftPoint.result](https://docs.byteplus.com/docs/byteplus-livesaas/events#4fa82edf) 事件，當禮物積分更新或觀眾主動查詢禮物積分時觸發。<br><br>   * 新增 gift.pointQuery 事件，用於查詢觀眾的禮物積分。詳情請參見 [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0)。 |
|2025\-08\-12 |2.0.19 |新增參數 `shareUrl`，可為直播間設定自訂分享網址。如需更多資訊，請參閱 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。 |


<span id="7ab40088"></span>
## 2025 年 7 月


|發布日期 |版本 |說明 |
|---|---|---|
|2025\-07\-15 |2.0.17 |**新功能**<br><br><br>* 禮物<br><br>   * 新增參數 `disableSendGift`，可指定當觀眾點擊或觸控 **Send** 發送禮物時，是否停用 BytePlus Live 的禮物發送邏輯。如需更多資訊，請參閱 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>   * 新增 [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#d476ef36) 事件，當觀眾點擊或觸控禮物時觸發。<br><br>   * 新增 [gift.sendError](https://docs.byteplus.com/docs/byteplus-livesaas/events#83e8b67c) 事件，當觀眾發送禮物時因積分不足或請求異常導致錯誤時觸發。你可將 `disableSendGift` 的值設為 `true` 並監聽此事件，以實現自訂邏輯。<br><br>   * 新增 [gift.show](https://docs.byteplus.com/docs/byteplus-livesaas/events#e862732b) 事件，當觀眾發送禮物時觸發。<br><br>   * 新增 `gift.send` 事件，當你將 `disableSendGift` 設為 `true` 並觸發 [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#d476ef36) 事件後，可用於發送指定數量的禮物。如需更多資訊，請參閱 [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0)。<br><br>* 商品<br><br>   * 新增參數 `disabledShopCartClick`，可指定當觀眾在行動裝置觀看頁面點擊購物車圖示時，是否停用顯示商品列表功能。如需更多資訊，請參閱 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>   * 新增 [shopCart.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#7bd143bd) 事件，當行動裝置觀看頁面的購物車圖示被點擊時觸發。你可將 `disabledShopCartClick` 的值設為 `true` 並監聽此事件，以實現自訂邏輯。 |
|2025\-07\-01 |2.0.16 |**已修復問題**<br><br>已修復部分問題。 |


<span id="20ba9ed9"></span>
## 2025 年 5 月


|發布日期 |版本 |說明 |
|---|---|---|
|2025\-05\-15 |2.0.15 |**新功能**<br><br>新增 `pcuConfig` 參數及 [activity.pcu](https://docs.byteplus.com/docs/byteplus-livesaas/events#75c92017) 事件。可用於自訂當所有直播間的峰值同時在線人數（PCU）超過帳戶並發限制時顯示的錯誤頁面。如需更多資訊，請參閱 [Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#db59dce3)。 |


<span id="8a775a08"></span>
## 2025 年 3 月


|發布日期 |版本 |說明 |
|---|---|---|
|2025\-03\-19 |2.0.13 |**新功能**<br><br>留言文字框<br><br><br>* 新增 `disabledCommentConfig` 參數，可停用留言文字框並設定其預設提示文字。如需更多資訊，請參閱 [Options](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#b6fb0c34)。<br><br>* 新增 `comment.disabled` 事件。配置 `disabledCommentConfig` 參數的停用狀態及提示文字後，可觸發此事件以動態停用或啟用留言文字框。如需更多資訊，請參閱 [Events](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#sdkeventsemit)。<br><br>* 新增支援自訂停用狀態留言文字框的樣式。如需更多資訊，請參閱 [Customizing the style of the disabled comment text box](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#86db69f2)。 |


<span id="3d235239"></span>
## 2024 年 12 月


|發布日期 |版本 |說明 |
|---|---|---|
|2024\-12\-10 |2.0.11 |* **相容性變更**<br><br>   參數值變更<br><br>   用於指定觀看頁面預設語言的參數 `defaultLang`，其繁體中文值已從 `zh-Hant` 改為 `zh-hant`。如需更多資訊，請參閱 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>* **改進項目**<br><br>   提升表情符號顯示速度。 |


<span id="be911f23"></span>
## 2024 年 10 月


|發布日期 |版本 |說明 |
|---|---|---|
|2024\-10\-10 |2.0.6 |**新功能**<br><br>觀看頁面多語言<br><br><br>* 新增支援以下語言於觀看頁面：<br><br>   * 泰語<br><br>   * 越南語<br><br>   * 阿拉伯語<br><br>   * 土耳其語<br><br>   * 西班牙語<br><br>   * 印尼語<br><br>   * 葡萄牙語<br><br>   * 俄語<br><br>* 新增參數 `defaultLang`，可用於設定觀看頁面的預設語言。當觀眾進入直播間時，頁面將設定為所配置的預設語言，不論其 PC 瀏覽器預設語言或行動裝置系統語言為何。如需更多資訊，請參閱 [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>* 如果你在觀看頁面有自訂的語言切換按鈕，可以先呼叫[getPageLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#35db7c0e)以獲取觀看頁面支援的語言，然後呼叫[switchLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#a58b37a7)以切換至指定語言。 |


<span id="f2533834"></span>
## 2024 年 9 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-09\-12 |2.0.5 |優化簽到功能，包括將簽到時長的單位由分鐘改為秒，並將未及時簽到的觀眾踢出。 |
|2024\-09\-05 |2.0.4 |修復部分問題。 |


<span id="910cf611"></span>
## 2024 年 8 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-08\-23 |2.0.3 |新增支援在直式模式下自訂直播間圖示的樣式與背景色。如需更多資訊，請參閱[Customizing the style and background color of icons in live rooms in portrait mode](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#1b8b0536)。 |
|2024\-08\-15 |2.0.2 |新增支援在橫屏模式下於行動裝置顯示購物車圖示。 |


<span id="87c57f2d"></span>
## 2024 年 7 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-07\-23 |2.0.1 |優化預約直播的邏輯。 |
|2024\-07\-09 |2.0.0 |優化觀看頁面的 UI 風格。 |


<span id="cf28c503"></span>
## 2024 年 6 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-06\-24 |1.3.8 |* 在引入 CSS 和 JS 資源時，移除了 URL 中`mobile/`或`pc/`後的`byteplus`。如需更多資訊，請參閱[Integration method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#855885cc)。<br><br>* 修復部分問題。 |
|2024\-06\-07 |1.3.3 |新增支援超低延遲功能。 |
|2024\-06\-06 |1.3.2 |修復部分問題。 |


<span id="990338d3"></span>
## 2024 年 5 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-05\-10 |1.3.1 |* 新增參數`mobileGesture`、`showLikeInPlayer`、`disableLotteryTicketRedirect`、`extra`、`disableRotateFullscreen`、`disableLivePauseButton`及`loginInToThumbUp`。如需更多資訊，請參閱[Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>* 刪除參數`isBytePlus`、`playerCustomLoading`及`unloginIcon`。<br><br>* 新增事件[lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#e290813e)、[player.vodConfigChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#a87308eb)、[menu.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#93a24cfc)及[thumbs.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#750ccd04)。<br><br>* 新增 API [getVodPlayInfo()](https://docs.byteplus.com/docs/byteplus-livesaas/api#cb44cfa8)。 |


<span id="7234a4ad"></span>
## 2024 年 4 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-04\-29 |1.1.22 |優化禮物打賞功能，包括：<br><br><br>* 調整預設禮物。<br><br>* 優化禮物特效。<br><br>* 觀眾現在可於直播間處於「直播中」、「回放」或「已結束」狀態時送出禮物。此前僅於「直播中」狀態下可送禮。 |
|2024\-04\-09 |1.1.21 |* 新增參數`closePlayVideoFocus`，用於指定觀眾進入觀看頁面時，是否自動滾動至正在播放預覽、回放或直播影片的播放器。如需更多資訊，請參閱[Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters)。<br><br>* 新增[lines.current](https://docs.byteplus.com/docs/byteplus-livesaas/events#96c0ddb3)事件，當觀眾點擊「直播中」狀態的直播源或「回放」狀態的回放影片時觸發。<br><br>* 新增[switchChannel()](https://docs.byteplus.com/docs/byteplus-livesaas/api#88ab1ee1) API，可切換至指定的「直播中」直播源或「回放」狀態的回放影片。 |


<span id="f3d67bbd"></span>
## 2024 年 1 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2024\-01\-18 |1.1.14 |新增支援於行動裝置直式模式下顯示播放器 Logo。 |


<span id="87c920be"></span>
## 2023 年 12 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2023\-12\-14 |1.1.13 |新增支援於行動裝置橫屏模式下顯示播放器 Logo。 |


<span id="0c01bcd6"></span>
## 2023 年 11 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2023\-11\-30 |1.1.12 |新增支援於行動裝置橫屏與直式模式下顯示不同封面。 |
|2023\-11\-16 |1.1.11 |* 優化觀看頁面的投票樣式。<br><br>* 新增支援將 BytePlus Live 控制台的色彩配置同步至直式模式下的直播間。 |


<span id="9b0800a3"></span>
## 2023 年 10 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2023\-10\-16 |1.1.10 |修復部分問題。 |
|2023\-10\-10 |1.1.8 |修復部分問題。 |


<span id="e6d88c3f"></span>
## 2023 年 8 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2023\-08\-24 |1.1.7 |修復部分問題。 |


<span id="db2ebae4"></span>
## 2023 年 7 月


|發佈日期 |版本 |描述 |
|---|---|---|
|2023\-07\-31 |1.1.6 |修復部分問題。 |
|2023\-07\-20 |1.1.5 |修復部分問題。 |

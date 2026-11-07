---
title: "Web Viewer SDK：參數"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW"
---

<span id="2c9e46bc"></span>
## SDKconf

這些參數用於配置 SDK，以在觀看頁面顯示直播間。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SDK 配置優先於 BytePlus Live 控制台和伺服器端 OpenAPI 中的設定。</div>



|名稱 |類型 |是否必填 |預設值 |說明 |
|---|---|---|---|---|
|activityId |整數 |是 |不適用 |直播間的活動 ID。<br><br>一個直播間對應一個活動 ID。<br><br>取得活動 ID，可採用以下任一方法：<br><br><br>* 呼叫[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW)。<br><br>* 登入[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，在直播間左上角找到 ID。 |
|service |字串 |是 |不適用 |服務名稱，僅用於標記。<br><br>配置 BytePlus Live 的允許清單後，技術支持會將此參數值同步給你。 |
|mode |整數 |是 |不適用 |驗證模式。<br><br><br>* `1`：公開模式。觀眾以訪客模式進入直播間，當需要用戶資訊（如點擊評論文字框、參與抽獎）時，必須輸入暱稱或以手機號登入直播間以完成訪客註冊。<br><br>* `2`：自訂模式。觀眾以你的 Web 應用中的用戶資訊進入直播間，因此可直接進行發送評論、參與抽獎等操作。 |
|token |字串 |是 |不適用 |用戶 token。<br><br><br>* 若`mode`值為`1`，可透過呼叫[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)或前往**Producer** \> **Page embedding** \> **Web SDK embedding**，於[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播間頁面取得用戶 token。<br><br>* 若`mode`值為`2`，可透過呼叫[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)取得用戶 token。 |
|modules |[模組](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#b56510d0)[] |是 |不適用 |模組配置。 |
|options |Partial<[選項](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#b6fb0c34)\> |否 |不適用 |可選參數。 |


<span id="b56510d0"></span>
## 模組


|名稱 |類型 |是否必填 |預設值 |說明 |
|---|---|---|---|---|
|id |字串 |是 |不適用 |頁面元素 ID，用於指定要渲染模組的位置與大小。 |
|mode |字串 |是 |不適用 |模組名稱。<br><br><br>* `player`：播放器模組。建議 PC 端最小寬度為 640 px。<br><br>* `menu`：選單模組。SDK 支援渲染多種選單類型：聊天互動、圖文、商品卡片、互動工具、問答及嵌入連結。建議 PC 端最小寬度為 320 px。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">僅當在<strong>Display menu</strong> 開關於<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live console</a>中開啟時，互動工具選單才會顯示於觀看頁面上。   </div><br>   <br><br>* `lines`：多線路模組，用於直播源和回放列表。無需指定高度，模組會自動適應高度。<br><br>* `mobile`：手機橫屏全頁模組，包含播放器、多線路及選單模組。此模組僅支援行動裝置，且不可與其他模組同時使用。更多效果資訊，請參見[demo](https://live.byteplus.com/demo/sdk/index.mobile.all.html)。<br><br>* `mobile-portrait`：手機直屏全頁模組，包含播放器、多線路及選單模組。此模組僅支援行動裝置，且不可與其他模組同時使用。更多效果資訊，請參見[demo](https://live.byteplus.com/demo/sdk/index.mobile.all-portrait.html)。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當參數值設為<code>player</code>、<code>menu</code>或<code>lines</code>時，只能整合這些模組專屬的功能。若要在行動裝置上整合非特定模組的功能，例如預約、主播帳號與標頭圖片，可以將參數值設為<code>mobile</code>或<code>mobile-portrait</code>，以整合全頁模組。</div><br> |
|menu |字串[] |否 |無 |此參數僅在`modules.mode`的值為`menu`時生效。<br><br>使用此參數以配置要顯示的選單類型。例如，可以將其設為`["comment", "imagetext"]`。若未指定，則會顯示所有選單類型。<br><br><br>* `comment`：聊天互動選單。<br><br>* `imagetext`：互動工具選單。<br><br>* `cardlist`：商品卡片選單。<br><br>* `bandcontent`：圖形選單。<br><br>* `session`：問答選單。<br><br>* `embeddedurl`：嵌入連結選單。 |


<span id="b6fb0c34"></span>
## 選項


|名稱 |類型 |是否必填 |預設值 |描述 |
|---|---|---|---|---|
|origin |字串 |否 |`"https://live.byteplus.com"` |業務請求的網域名稱。若無特殊需求，無需配置此參數。 |
|saveUserInfo |布林值 |否 |`true` |指定當`mode`的值為`1`時，是否快取用戶資訊。<br><br><br>* `true`：快取。<br><br>* `false`：不快取。 |
|mobileBackgroundTransparent |布林值 |否 |`false` |指定行動裝置上模組背景是否透明。<br><br><br>* `true`：透明。在觀看頁面顯示您的背景圖片或顏色。<br><br>* `false`：不透明。 |
|mobileGetUserId |布林值 |否 |`true` |指定是否允許觀眾於行動裝置上，快速點擊觀看頁面左上角五次以獲取其用戶 ID。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|basicPolling |布林值 |否 |`true` |指定是否啟用輪詢 API 以即時更新直播間資訊。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|pcPlayerHeader |布林值 |否 |`false` |指定是否在 PC 端播放器頂部顯示直播間名稱、描述等資訊。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |
|playerRetryTimes |整數 |否 |`1` |播放器因網路異常無法播放影片時的重試次數。若切換主備流或降級至低畫質後問題仍存在，則視為重試失敗。若需無限次重試，請將參數值設為 0。 |
|disabledLogin |布林值 |否 |`false` |指定是否停用 BytePlus Live 內建登入系統。一般與 事件搭配使用。若系統被停用，您必須自行實作用戶登入邏輯。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|disableCardRedirect |布林值 |否 |`false` |指定是否停用觀眾於點擊或觸控商品卡片後，跳轉至其他頁面或觀看頁面浮層的功能。一般與 或 事件搭配使用。若此功能被停用，您必須自行實作跳轉邏輯。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|disableAdFloatingRedirect |布林值 |否 |`false` |指定是否停用觀眾於點擊或觸控浮動廣告後，跳轉至其他頁面或觀看頁面浮層的功能。一般與[adFloating.click](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#d05864eb) 事件搭配使用。若此功能被停用，您必須自行實作跳轉功能。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|disableAdMiddleRedirect |布林值 |否 |`false` |指定是否停用觀眾於點擊或觸控頁面內廣告後，跳轉至其他頁面或觀看頁面浮層的功能。一般與 事件搭配使用。若此功能被停用，您必須自行實作跳轉邏輯。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|disableAdAccountRedirect |Boolean |否 |`false` |指定是否停用當觀眾點擊或輕觸主帳號後，將其重定向至其他頁面的功能。通常，此參數與事件一起使用。若停用此功能，您必須自行實現重定向邏輯。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|purePlayer |Boolean |否 |`false` |指定是否顯示純播放器。純播放器指的是不含互動按鈕（如進度條）的播放器。<br><br><br>* `true`：顯示純播放器，播放器中不含任何互動按鈕。<br><br>* `false`：顯示一般播放器，播放器中包含互動按鈕。 |
|videoFillMode |String |否 |`'auto'` |指定播放器中影片的填充模式。<br><br><br>* `cover`：縮放影片以維持其長寬比，同時填滿播放器的整個內容區域。若影片的長寬比與播放器不符，影片將會被裁切以適應。<br><br>* auto：縮放影片以維持其長寬比，同時適應播放器的內容區域。影片將完整顯示，若長寬比不符則會出現信箱格式（黑邊）。<br><br>* `fill`：調整影片大小以填滿播放器。影片的長寬比可能會改變。<br><br>* `fillWidth`：拉伸影片寬度以填滿播放器寬度，高度不變。<br><br>* `fillHeight`：拉伸影片高度以填滿播放器高度，寬度不變。<br><br><br>此參數僅於行動裝置橫向模式及電腦端生效。<br><br>行動裝置直向模式下影片的填充模式會根據來源串流的長寬比而有所不同。 |
|softSolution |Boolean |否 |無 |指定是否強制啟用或停用行動裝置播放器的軟體解碼。此設定可防止部分行動瀏覽器或應用程式使用其內建播放器，確保影片於 SDK 播放器中播放。<br><br><br>* `true`：強制啟用。<br><br>* `false`：強制停用。 |
|disableReservationCell |Boolean |否 |`false` |指定是否停用顯示直播預約對話框的功能。通常，此參數與[reservation.click](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#44166c70)事件一起使用。若停用此功能，您必須自行實現直播預約功能。換言之，您必須使用`isReserved`參數指定當前觀眾是否已預約您的直播，並手動呼叫`updateModulesConf` API 以更新預約狀態。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|isReserved |Boolean |否 |無 |指定當前觀眾是否已預約直播。<br><br><br>* `true`：已預約。<br><br>* `false`：未預約。 |
|lotteryIcon |[lotteryIcon](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#3f23b8e9) |否 |無 |幸運抽獎圖示。支援的圖片格式與`img`標籤支援的格式相同。 |
|emojiIcon |String |否 |無 |觀眾於電腦端點擊或輕觸以發送表情符號的圖示。請將參數值設為圖示的 URL。支援的圖片格式與 img 標籤支援的格式相同。 |
|moreActionExpandPc |Boolean |否 |`false` |指定是否將電腦端聊天室互動選單中的省略號圖示選項以圖示方式展開顯示於選單下方。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |
|playerBackgroundTransparent |布林值 |否 |`false` |指定播放器中未被影片填滿的區域是否為透明。<br><br><br>* `true`：透明。會顯示封面圖片。<br><br>* `false`：不透明。該區域會以黑色顯示。 |
|disablePlayerCover |布林值 |否 |`false` |指定是否停用封面圖片。<br><br><br>* `true`：在播放器中顯示背景圖片或顏色。<br><br>* `false`：在播放器中顯示封面圖片。 |
|mobilePlayerIconIgnoreList |字串陣列 |否 |無 |指定要在行動裝置播放器中隱藏哪些圖示。<br><br><br>* `editNickname`：更改觀眾暱稱的圖示。<br><br>* `notification`：啟用或停用系統通知的圖示。<br><br>* `language`：切換其他語言的圖示。<br><br>* `share`：分享直播間海報、QR Code 或連結的圖示。 |
|riskWarning |布林值 |否 |`true` |指定是否啟用提醒彈窗。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|portraitMenuExtends |[PortraitMenuConf](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#0eef80a1)[] |否 |無 |指定行動裝置直式模式下直播間的圖示或按鈕。 |
|mobileGesture |[mobileGesture](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#85e1fb94) |否 |無 |行動裝置播放器手勢的設定。 |
|showLikeInPlayer |布林值 |否 |`false` |指定是否在播放器中顯示直播間的按讚圖示。<br><br><br>* `true`：在播放器中顯示。預設位於播放器右下角。你可以覆寫 `class` 屬性 `bytelive-player-like-button` 的樣式來調整圖示位置。<br><br>* `false`：顯示於留言文字框右側。 |
|disableLotteryTicketRedirect |布林值 |否 |`false` |指定是否停用觀眾點擊或觸碰兌獎券獎品領取連結後跳轉至其他頁面的功能。通常此參數會與 [lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#e290813e) 事件搭配使用。若停用此功能，需自行實作跳轉功能。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|extra |字串 |否 |不適用 |同步至 BytePlus Live 的額外參數，可用於與觀眾建立關聯。例如，你可以將參數值設為 `Marketing department`，以將觀眾的部門從自有帳號系統同步至 BytePlus Live。 |
|disableRotateFullscreen |布林值 |否 |`false` |指定是否停用行動裝置觀眾旋轉為橫式時自動全螢幕模式。<br><br><br>* `true`：停用。觀眾旋轉為橫式時，不會自動觸發全螢幕模式且不會顯示提示。<br><br>* `false`：啟用。 |
|disableLivePauseButton |布林值 |否 |`false` |指定是否在直播期間隱藏播放器中的暫停按鈕。<br><br><br>* `true`：隱藏。<br><br>* `false`：不隱藏。 |
|loginInToThumbUp |布林值 |否 |`false` |指定觀眾是否必須登入才能按讚直播。<br><br><br>* `true`：觀眾必須登入。若未登入，點擊或觸碰按讚圖示時會觸發 [permission.need](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#c91cc8cb) 事件。<br><br>* `false`：不需登入。 |
|closePlayVideoFocus |布林值 |否 |無 |指定觀眾進入觀看頁面時，是否自動捲動至正在播放預覽、回放或直播影片的播放器。<br><br><br>* `true`：自動捲動。<br><br>* `false`：不自動捲動。 |
|defaultLang |字串 |否 |不適用 |觀看頁面的預設語言。當觀眾進入直播間時，頁面將設為已配置的預設語言，無論其在 PC 上的瀏覽器預設語言或在行動裝置上的系統語言為何。<br><br>若未指定，預設語言將與其在 PC 上的瀏覽器預設語言或在行動裝置上的系統語言相同。<br><br>有效值：<br><br><br>* `zh`：簡體中文。<br><br>* `en`：英文。<br><br>* `ja`：日文。<br><br>* `zh-hant`：繁體中文。<br><br>* `ko`：韓文。<br><br>* `th`：泰文。<br><br>* `vi`：越南文。<br><br>* `ar`：阿拉伯文。<br><br>* `tr`：土耳其文。<br><br>* `es`：西班牙文。<br><br>* `id`：印尼文。<br><br>* `pt`：葡萄牙文。<br><br>* `ru`：俄文。<br><br>* `tl`：塔加洛語。<br><br>* `km`：高棉文。<br><br>* `lo`：寮語。<br><br>* `my-MM`：緬甸文。<br><br>* `ms`：馬來文。<br><br>* `hi`：印地語。<br><br>* `fr`：法文。<br><br>* `de`：德文。<br><br>* `it`：義大利文。 |
|disabledCommentConfig | |否 |無 |指定是否停用留言文字框，以及停用留言文字框時的預設提示文字。<br><br><br>* `disabled`：是否停用留言文字框。有效值：<br><br>   * `true`：停用。若停用，觀眾點擊留言文字框時將無法輸入內容。<br><br>   * `false`：啟用。<br><br>* `placeholder`：停用留言文字框時的預設提示文字。 |
|pcuConfig | |否 |無 |若您訂閱了直播並發觀看人數方案，當觀眾嘗試進入且所有直播間的總並發峰值用戶數（PCU）超過您的帳戶上限時，將顯示錯誤頁面。<br><br>可使用此參數自訂錯誤頁面的文字與圖片。更多資訊，請參見[Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/gong-neng-shi-xian-1-1-zh-TW#db59dce3)。 |
|disableSendGift |Boolean |否 |false |指定當觀眾點擊或輕觸**送出**以送禮時，是否停用 BytePlus Live 與 UI 相關的送禮邏輯。<br><br><br>* `true`：停用。您需自行實作與 UI 相關的送禮邏輯，例如設定送禮數量及自訂禮物效果。<br><br>* `false`：啟用。 |
|shopCartIcon |String |否 |無 |指定購物車圖示的配置。您可上傳 GIF 或 PNG 圖片來自訂購物車圖示。 |
|disabledShopCartClick |Boolean |否 |false |指定當觀眾於行動裝置觀看頁面點擊購物車圖示時，是否停用顯示商品清單的功能。<br><br>一般會與[shopCart.click](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW#7bd143bd)事件搭配使用此參數。若將參數值設為`true`，您需自行實作相關邏輯。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|disabledShowExplainCard |Boolean |否 |false |指定當商品被推薦時，是否停用觀看頁面的浮動商品卡片。<br><br><br>* `true`：停用。停用後，商品被推薦時將不會釘選於觀看頁面。<br><br>* `false`：啟用。 |
|disablePopularityShow |Boolean |否 |false |指定是否停用人氣顯示，即觀看頁面上顯示的觀眾人數。<br><br><br>* `true`：停用。<br><br>* `false`：啟用。 |
|shareUrl |String |否 |無 |自訂直播間分享網址。網址必須包含協定（例如：https://）。若未設定或留空，將使用主控台中的分享地址。適用於連結、邀請海報及資訊流。 |
|vodSwitchMode |Boolean |否 |false |指定是否啟用 VOD（隨選視訊）資訊流播放模式。<br><br><br>* `true`：啟用 VOD 資訊流模式。影片以動態資訊流樣式顯示，便於互動式瀏覽。<br><br>* `false`：停用 VOD 資訊流模式。影片以傳統清單樣式顯示。 |
|enablePlaybackSwitchBtn |boolean |否 |true |指定是否在播放器中顯示**回放合集**按鈕。<br><br><br>* `true`：顯示回放合集按鈕。觀眾可透過此入口進入回放清單。<br><br>* `false`：隱藏回放合集按鈕。 |
|enablePlaybackListPopup |boolean |否 |true |指定是否顯示回放合集清單視窗。<br><br><br>* `true`：顯示回放合集清單視窗。觀眾可從清單中檢視並選擇回放影片。<br><br>* `false`：隱藏回放合集清單視窗。即使點擊**回放合集**按鈕，也不會顯示回放清單。 |
|playbackMode |Number |否 |1 |指定回放合集清單的播放模式。<br><br><br>* `1`：依清單順序播放影片。<br><br>* `2`：循環播放清單中的所有影片。<br><br>* `3`：僅循環播放當前影片。 |


<span id="3f23b8e9"></span>
### lotteryIcon


|名稱 |類型 |是否必填 |預設值 |說明 |
|---|---|---|---|---|
|attendIcon |String |否 |無 |未選出中獎者時顯示的抽獎圖示。將參數值設為`1: '圖示圖片的 URL'`。<br><br>如需分別配置日文、簡體中文及繁體中文觀看頁面的圖示，請將`1`分別替換為`2`、`0`及`3`，並將 URL 換成對應語言的圖片網址。 |
|openIcon |String |否 |無 |選出中獎者時顯示的抽獎圖示。將參數值設為`1: '圖示圖片的 URL'`。<br><br>如需分別配置日文、簡體中文及繁體中文觀看頁面的圖示，請將`1`分別替換為`2`、`0`及`3`，並將 URL 換成對應語言的圖片網址。 |


<span id="0eef80a1"></span>
### PortraitMenuConf


|名稱 |類型 |是否必填 |預設值 |說明 |
|---|---|---|---|---|
|icon |String |否 |無 |行動裝置直式直播間的圖示。<br><br>有效值：<br><br><br>* `shoppingCart`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9adb88ab716e4de29b64b30da2d172c4~tplv-goo7wpa0wc-image.image) </span><br><br>* `share`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afdd86ef695443b39100c134f6769ea9~tplv-goo7wpa0wc-image.image) </span><br><br>* `info`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ddc0bd06c2e4637908514ae37de4355~tplv-goo7wpa0wc-image.image) </span><br><br>* `images`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09bdfb69f4e34879963e4dfc4c7c690b~tplv-goo7wpa0wc-image.image) </span><br><br>* `notification`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eda4fc851cea4601ae4bd55055915038~tplv-goo7wpa0wc-image.image) </span> |
|render |String |否 |無 |行動裝置直式直播間的圖示或按鈕。範例：`<div style="color: #fff">Go</div>`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">其優先順序低於<code>icon</code>參數，因此若要透過<code>render</code>參數自訂圖示或按鈕，請勿為<code>icon</code>參數設定值。</div><br> |
|name |String |否 |無 |圖示或按鈕的名稱，當觀眾點擊省略號圖示時，會顯示於對應圖示或按鈕下方。 |
|key |String |是 |無 |圖示或按鈕的唯一識別碼。 |
|onClick |Function |否 |無 |點擊圖示或按鈕時觸發的點擊事件回調。回傳值為`key`參數的值。 |
|index |Number |否 |`0` |圖示或按鈕的顯示順序。參數值越大，圖示或按鈕越靠左顯示。若參數值大於 70，觀眾僅能於點擊省略號圖示後查看該圖示或按鈕。最多可直接顯示 4 個圖示與按鈕（含預設項）。更多圖示可透過省略號（...）選單存取。 |


<span id="85e1fb94"></span>
### mobileGesture


|名稱 |類型 |是否必填 |預設值 |說明 |
|---|---|---|---|---|
|disableGesture |Boolean |否 |`false` |指定是否在行動裝置上停用手勢操作。<br><br><br>* `true`：停用。觀眾無法於預覽或回放時，透過左右滑動拖曳進度條。<br><br>* `false`：啟用。 |

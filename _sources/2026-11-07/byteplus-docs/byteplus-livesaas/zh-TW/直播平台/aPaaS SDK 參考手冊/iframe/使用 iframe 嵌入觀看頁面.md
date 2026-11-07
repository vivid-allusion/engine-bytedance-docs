---
title: "使用 iframe 嵌入觀看頁面"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/shi-yong-iframe-qian-ru-guan-kan-ye-mian-zh-TW"
---

要將 BytePlus Live 串流整合到您的網站中，您可以使用 iframe 嵌入觀看頁面。此方法可降低開發成本，並讓觀眾直接在您的頁面上觀看，有助於吸引新用戶並留住現有用戶。本指南提供成功實現的步驟、程式碼範例及重要注意事項。

<span id="542f23c9"></span>
## 注意事項


* 請勿執行任何讀取或寫入 cookie 的操作，因為部分瀏覽器會停用第三方 cookie。這表示以下功能不受支援：發佈問卷（發送時間為觀眾進入直播間時），以及要求觀眾在進入直播間前先登入（即將觀看限制設為密碼、手機號碼等）。若要使用這些功能，您可以透過新增 CNAME 記錄來自訂嵌入頁面的網域名稱（即觀看頁面），使您的頁面與嵌入頁面共用相同網域名稱。此時嵌入頁面的 cookie 將以第一方 cookie 寫入，避免第三方 cookie 限制。如需新增 CNAME 記錄，請聯絡 BytePlus Live 技術支援。

* 我們建議您將觀看限制設為**自訂**，並選擇觀眾登入您的帳號系統後可直接進入直播間、無需再次登入的方案。如需更多資訊，請參閱[方案 B](https://docs.byteplus.com/docs/byteplus-livesaas/zi-ding-yan-zheng-deng-ru-zh-TW#29214805)。

* 請勿在 HTTPS 頁面嵌入 HTTP 頁面，否則頁面可能無法正確顯示。

* 嵌入聊天互動選單時，PC 端的最小寬度為 320 px。


<span id="b1c0e113"></span>
## 嵌入方式


1. 將可嵌入的連結設為`iframe`標籤的 src 屬性。

   * 若需全頁嵌入，例如在 PC 端嵌入整個觀看頁面，請參考以下範例。

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?platform=pc"></iframe>
      ```
      

   * 若需嵌入特定模組，例如播放器，請參考以下範例。

      ```Plain
      <iframe src="https://live.byteplus.com/1323/6****21?mode=player"></iframe>
      ```
      

   請將`https://live.byteplus.com/1323/6****21`替換為您的直播間觀看頁面的網址。有關嵌入連結支援的參數，請參閱[參數](https://docs.byteplus.com/docs/byteplus-livesaas/can-shu-zh-TW)。如需監聽嵌入頁面的事件，請參閱[事件](https://docs.byteplus.com/docs/byteplus-livesaas/shi-jian-zh-TW)。

2. 設定`iframe`元素的屬性。以下為範例。

   ```Plain
   <iframe src="https://live.byteplus.com/1323/6****21?platform=pc" width="1000" height="600" allowfullscreen="true" autoplay="true" allow=“fullscreen; screen-wake-lock; autoplay; picture-in-picture; camera; microphone” frameborder="0" border="0"></iframe>
   ```
   

   * `width`：`iframe`元素的寬度。當值為數字時，單位為 px。當值為百分比時，表示相對於父容器寬度的百分比。

   * `height`：`iframe`元素的高度。當值為數字時，單位為 px。當值為百分比時，表示相對於父容器高度的百分比。

   * `allowfullscreen="true"`：允許嵌入頁面進入全螢幕模式。若嵌入頁面包含播放器，建議新增此屬性。

   * `autoplay="true"`：允許媒體自動播放。

   * `allow`：嵌入頁面支援的功能。多個參數值請以分號（;）分隔。有效值：

      * `fullscreen`：允許內容進入全螢幕模式。適用於嵌入頁面包含播放器的情境。

      * `screen-wake-lock`：保持螢幕常亮。

      * `autoplay`：允許媒體自動播放。

      * `picture-in-picture`：畫中畫（PiP）模式。僅適用於 PC 端。

   * `frameborder`：`iframe` 元素是否有邊框。有效值：

      * `0`：無邊框。

      * `1`：有邊框。

   * `border`：`iframe` 元素的邊框寬度。單位為 px。

3. 將 `iframe` 標籤插入到你的頁面中。

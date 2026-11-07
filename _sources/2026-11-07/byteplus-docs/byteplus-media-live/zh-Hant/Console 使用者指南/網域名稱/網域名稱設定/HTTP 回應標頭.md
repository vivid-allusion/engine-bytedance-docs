---
title: "HTTP 回應標頭"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-response-headers-zh-TW"
---

您可以為邊緣伺服器回傳給用戶端的回應新增自訂 HTTP 標頭。完成設定後，這些標頭將套用於所有發送至此網域名稱的請求回應。

HTTP 回應標頭是一組欄位，伺服器會在主要回應內容之前傳送這些欄位。這些欄位提供關於回應的中繼資料，例如狀態碼、內容類型、快取控制規則、Content\-Encoding 和 Content\-Disposition。透過設定適當的 HTTP 回應標頭，您可以提升安全性、優化效能、改善用戶體驗，並符合合規或瀏覽器互動需求。

預設情況下，我們的快取節點在處理用戶的拉流請求時，會直接傳遞來源伺服器的回應標頭。此功能允許您設定、新增或修改這些回應標頭參數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">回應標頭欄位比對不區分大小寫。若原始回應標頭中已存在某欄位，則新欄位值會覆蓋原欄位值。</div>


<span id="ba3aed7d"></span>
## 適用對象

拉流網域名稱。

<span id="437cee91"></span>
## 前置條件

您已新增拉流網域名稱。如需更多資訊，請參閱 [新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-TW)。

<span id="d55ece96"></span>
## 操作流程


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊 **網域**。

3. 找到您要查看的網域名稱，並在 **操作**欄點擊 **設定**。

4. 點擊 **存取控制**標籤。

5. 在 **HTTP 回應標頭**開關右側，點擊 **編輯**。

6. 在出現的 **HTTP 回應標頭設定**對話框中，按需求新增回應標頭。

   * **參數**：從下拉清單選擇常用標頭或輸入自訂標頭。最多可新增 20 個標頭。標頭名稱不得超過 1024 個字元。

      您可以從下拉清單選擇以下參數：

      
      |**參數** |**說明** |**範例** |
      |---|---|---|
      |Content\-Type |回傳給用戶端的內容類型。 |`text/plain` |
      |Cache\-Control |控制快取行為的指令。 |`max-age=3600` |
      |Content\-Disposition |回傳給用戶端的下載檔案名稱。 |`attachment;filename=Demo.xlsx` |
      |Content\-Language |回傳給用戶端的內容語言。 |`zh-CN` |
      |Expires |回應物件的到期時間。 |`Wed, 21 Oct 2015 07:28:00 GMT` |
      |Access\-Control\-Allow\-Origin |可供跨域請求存取的來源。 |`https://www.another-site.com` |
      |Access\-Control\-Allow\-Headers |跨域請求可包含的請求標頭。 |`X-Custom-Header` |
      |Access\-Control\-Allow\-Methods |可用於跨域請求的請求方法。 |`GET` |
      |Access\-Control\-Max\-Age |預檢請求結果可快取的時長。 |`3600` |
      |Access\-Control\-Expose\-Headers |跨域請求中用戶端可存取的回應標頭。 |`Content-Encoding`。若需讓用戶端存取更多回應標頭，可在此欄位指定。多個回應標頭以逗號（,）分隔。 |
      

   * **值**：指定常數或變數作為標頭值。

      * 常數不得超過 1024 個字元。

      * 對於變數，您可以從下拉清單選擇常用變數或手動輸入變數。

         您可以從下拉清單選擇以下變數：

         
         |**變數** |**說明** |**範例值** |
         |---|---|---|
         |$ |代表用戶端請求中的網域名稱。 |example.com |
         |$ |代表用戶端請求的路徑（不含查詢參數）。若客戶端請求被重寫，此變數表示重寫後的路徑。 |`/dir/sample.php` |
         |$ |表示客戶端請求中的查詢參數。若客戶端請求被重寫，此變數表示重寫後的參數。 |`color=red&n=10` |
         |$ |表示發送請求的客戶端 IP 位址。 |`192.0.2.1` |
         |$ |表示回應客戶端請求的邊緣伺服器 IP 位址。 |`192.0.2.1` |
         

7. 點擊 **確認**。

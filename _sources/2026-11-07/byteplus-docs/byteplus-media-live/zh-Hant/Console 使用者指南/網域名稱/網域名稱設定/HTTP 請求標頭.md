---
title: "HTTP 請求標頭"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-request-headers-zh-TW"
---

若要將特定資訊（例如用戶端類型或驗證詳細資料）傳遞給您的源站伺服器，您可以在回源任務中新增自訂 HTTP 請求標頭。本主題說明如何為拉流網域名稱設定這些標頭。設定完成後，該網域名稱的所有回源請求都會自動包含指定的標頭，讓您與源站伺服器之間的通訊更加靈活且安全。如需有關回源的更多資訊，請參閱[設定回源任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings)。

HTTP 請求標頭會在用戶端（如瀏覽器）發送 HTTP 請求時自動加入，以向伺服器提供額外資訊，例如用戶端類型、語言及偏好設定。例如，您可以設定`Accept` 欄位，以指定用戶端可接受的回應類型。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">請求標頭欄位比對不區分大小寫。若原始請求標頭中已存在該欄位，則新欄位值會覆寫原有欄位值。</div>


<span id="37a45946"></span>
## 適用範圍

拉流網域名稱。

<span id="7372d48b"></span>
## 先決條件

您已新增拉流網域名稱。如需更多資訊，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-TW)。

<span id="c7be96cf"></span>
## 操作步驟


1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊**網域名稱**。

3. 找到您要檢視的網域名稱，並在**操作**欄點擊**設定**。

4. 點擊**回源**分頁。

5. 在**HTTP 請求標頭**開關右側，點擊**編輯**。

6. 於**HTTP 請求標頭設定**對話方塊中，新增所需的請求標頭。

   * **參數**：最多可新增 20 個標頭。標頭名稱不得超過 1024 個字元。

   * **值**：可指定常數或變數作為標頭值。

      * 常數不得超過 1024 個字元。

      * 對於變數，您可以從下拉清單選擇預設變數，或手動輸入變數。

         支援的變數包括：

      
      |**變數** |**說明** |**範例值** |
      |---|---|---|
      |$ |表示回源請求的源站伺服器主機名稱。 |example.com |
      |$ |表示回源請求的路徑（不含查詢參數）。若請求被重寫，則此變數表示重寫後的路徑。 |`/dir/sample.php` |
      |$ |表示回源請求中的查詢參數。若請求被重寫，則此變數表示重寫後的參數。 |`color=red&n=10` |
      |$ |表示發送請求的用戶端 IP 位址。 |`192.0.2.1` |
      

7. 點擊**確認**。

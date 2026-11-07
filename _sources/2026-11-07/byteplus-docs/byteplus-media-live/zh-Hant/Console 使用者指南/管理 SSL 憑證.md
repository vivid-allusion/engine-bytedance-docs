---
title: "管理 SSL 憑證"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-certificates-zh-TW"
---

為了讓您的 MediaLive 網域名稱在推流與拉流時能夠透過 HTTPS 進行安全加密串流，您可以使用憑證託管功能。本主題提供逐步操作說明，指導您如何將 SSL 憑證上傳至 MediaLive 控制台、有效管理憑證，並準備將其綁定至您的網域名稱。

<span id="67b2ec91"></span>
## 限制

MediaLive 支援上傳 Nginx 伺服器類型的憑證與私鑰檔案。

<span id="8c573f7b"></span>
## 新增 SSL 憑證


1. 從您的憑證供應商下載 PEM 格式的 SSL 憑證檔案至您的電腦。

2. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

3. 在左側導覽窗格中，選擇 **設定** \> **憑證**，進入憑證列表頁面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba70f2ac8c4476688aa2ea51562caa5~tplv-goo7wpa0wc-image.image) </span>

4. 點擊 **新增憑證**，開啟 **新增 HTTPS 憑證**對話框，並依提示新增憑證。

   下表說明各參數：

   
   |**參數** |**說明** |
   |---|---|
   |憑證名稱 |自訂憑證名稱，不限字元類型，最大長度為 40 個字元。 |
   |選擇專案 |選擇憑證所屬專案，配置專案後，具有專案權限的子帳號可管理該憑證。 |
   |上傳方式 |選擇一種上傳方式。<br><br><br>* 手動輸入<br><br>* 檔案上傳 |
   |憑證內容 |憑證檔案內容：<br><br><br>* 若選擇手動上傳，請使用文字編輯器開啟憑證檔案，並將內容複製到此欄位。<br><br>* 若選擇檔案上傳，請選擇本地憑證檔案。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">支援自動補全憑證鏈。只需上傳為網域名稱簽發的憑證，憑證鏈將自動補全。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若選擇上傳憑證鏈，請確保憑證鏈包含伺服器憑證、中間憑證及根憑證。它們需按正確順序排列（伺服器憑證在前，中間憑證及根憑證依序排列）。順序錯誤將導致憑證鏈無效。</div><br> |
   |私鑰 |憑證私鑰檔案內容：<br><br><br>* 選擇手動上傳時，請使用文字編輯器軟體開啟本地憑證私鑰檔案，並將憑證私鑰內容複製到此處。<br><br>* 選擇檔案上傳時，請選擇本地憑證私鑰檔案進行上傳。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請確保憑證的私鑰未設置密碼保護。</div><br> |
   

5. 點擊 **確認**以儲存憑證。


<span id="82892b1b"></span>
## 管理 SSL 憑證

在 **憑證**頁面，您可以對已新增的憑證執行以下操作。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6939111c604049e19097063bce2601c5~tplv-goo7wpa0wc-image.image) </span>


|操作 |描述 |
|---|---|
|搜尋特定憑證 |可依下列條件篩選憑證：<br><br><br>* 憑證狀態：點擊不同的標籤頁可依狀態檢視憑證。為確保網域的 HTTPS 加密不中斷，必須及時更新已過期、即將過期或有變更的憑證。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02b6f7ae51b7482a9b75de171b3b4b85~tplv-goo7wpa0wc-image.image) </span><br><br>* 憑證名稱：支援模糊搜尋，英文不區分大小寫。<br><br>* 鏈 ID：點擊 **Chain ID** 輸入框，在彈出對話框中輸入所需的憑證鏈 ID。一次最多可輸入 50 個憑證鏈 ID，每行一個 ID。英文不區分大小寫。<br><br>* 可綁定網域名稱：可綁定至目前憑證的網域。一次最多可輸入 1 個網域。支援模糊搜尋，英文區分大小寫。<br><br>* 已綁定網域名稱：目前已綁定至憑證的網域。點擊 **Associated domain name** 輸入框，在彈出對話框中輸入所需的已綁定網域。一次最多可輸入 50 個網域，每行一個網域。英文區分大小寫。<br><br>* 已綁定網域狀態：可從下拉清單選擇一個或多個目前憑證綁定網域的狀態。當網域狀態為 **Online**、**Configuring**、**Offline** 或 **ICP Filing missing** 時，可為該網域更新憑證或綁定其他憑證。<br><br>* 搜尋專案：從 **query item** 下拉清單選擇憑證專案。<br><br>* 憑證到期時間：篩選在特定時間範圍內到期的憑證。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">可點擊相應標籤頁獲取特定狀態的憑證。其他條件需先配置，然後點擊 <strong>Search</strong> 以獲取符合條件的憑證。</div><br> |
|檢視憑證資訊 |檢視憑證資訊。<br><br>其中，<br><br><br>* 可點擊憑證的已綁定網域，跳轉至該網域的 HTTPS 設定頁面。<br><br>* 可依上傳時間與到期時間進行憑證排序，支援升序或降序。 |
|更新憑證資訊 |如需更新憑證資訊，請點擊該列的 **Update**。更新後的憑證僅對狀態為 **Online**、**Configuring**、**Offline** 或 **ICP Filing missing** 的已綁定網域生效。 |
|刪除憑證 |若憑證已無需使用，請點擊憑證右側的 **Delete**。 |


<span id="a976fb30"></span>
## 接下來

將 SSL 憑證綁定至網域名稱並啟用 HTTPS。如需啟用 HTTPS 的詳細資訊，請參閱 [HTTPS 設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-https-zh-TW)。

<span id="53a4af28"></span>
## 常見問題

<span id="43d0f559"></span>
### 憑證鏈順序錯誤

**錯誤**：上傳憑證時出現「憑證鏈順序錯誤，請檢查憑證並重新上傳」的錯誤。

**原因**：此問題可能是因為手動將憑證組合成鏈所造成。憑證鏈由多個憑證依一定順序組成，鏈中的每個憑證都由其後一個憑證簽發。若鏈中的某個憑證不是由下一個憑證簽發，則該鏈無效。

**解決方案**：MediaLive 憑證管理支援自動補全憑證鏈。您只需參考以下方法取得僅針對您的網域名稱簽發的憑證進行上傳，無需提交整個憑證鏈。

假設您的原始憑證鏈包含三個憑證，其結構如下：

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate B
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
Certificate C
-----END CERTIFICATE-----
```


您可以使用憑證解析工具分別解析憑證 A、憑證 B 和憑證 C，以找到針對您的網域名稱簽發的憑證。

假設您找到的憑證是憑證 A。那麼，在上傳憑證時，您只需輸入以下內容即可成功上傳憑證：

```Plain
-----BEGIN CERTIFICATE-----
Certificate A
-----END CERTIFICATE-----
```

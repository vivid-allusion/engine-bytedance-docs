---
title: "管理 DRM 授權"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-drm-licenses-zh-TW"
---

為了以加密方式保護您的影片串流，您需要將 DRM 金鑰和 FairPlay 憑證上傳至 BytePlus MediaLive。本主題提供這兩項操作的逐步指引。

<span id="8aa0da77"></span>
## 上傳 DRM 金鑰

<span id="24fcd147"></span>
### 前置作業

您必須先從[Intertrust](https://portal.expressplay.com/)取得 DRM 金鑰。如需取得金鑰的詳細說明，請參閱[取得 DRM 金鑰](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-drm-key)。

<span id="bf440097"></span>
### 操作步驟


1. 登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊**加密**。

3. 點擊**DRM**分頁。

4. 在**API 金鑰資訊**設定區域中點擊**編輯**。將會顯示對話方塊。

5. 輸入金鑰。

6. 點擊**確認**以儲存設定。


<span id="28aa3894"></span>
## 上傳 FairPlay 憑證

若要在 Apple 裝置上啟用加密，您也必須上傳 FairPlay 憑證。

<span id="c7f3874e"></span>
### 前置作業

您必須擁有 FairPlay 憑證。如需取得憑證及其他相關資訊的說明，請參閱[取得 FairPlay 憑證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate)。

<span id="ad2418f7"></span>
### 操作步驟


1. 登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左側導覽窗格中，點擊**加密**。

3. 點擊**DRM**分頁。

4. 在**憑證**設定區域中點擊**編輯**。將會顯示對話方塊。

5. 設定相關參數。

   
   |**參數** |**說明** |
   |---|---|
   |憑證名稱 |您的 FairPlay 憑證名稱。 |
   |憑證檔案 |上傳 .cer 檔案。 |
   |私鑰檔案 |上傳 .pem 檔案。 |
   |私鑰密碼 |用於解密私鑰檔案的密碼。 |
   |ASK |向 Apple 申請憑證時提供的 Application Secret Key (ASK) |
   

6. 點擊**確認**以儲存設定。


<span id="54d8c93d"></span>
## 後續操作

在 BytePlus MediaLive 控制台中，設定要加密的網域名稱及 AppName。您可參閱[管理加密設定](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task)以取得詳細說明。

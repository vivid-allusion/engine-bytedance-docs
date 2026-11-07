---
title: "取得 FairPlay 證書"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate-zh-TW"
---

若要在您的直播串流中實現 FairPlay 加密，您需先向 Apple 取得 FairPlay 串流證書。本主題提供取得證書及準備上傳至 BytePlus MediaLive 和 Intertrust 的逐步操作說明。

<span id="9aa7496a"></span>
## 先決條件

一個 [Apple Developer 帳戶](https://developer.apple.com/)。

<span id="cd56ff31"></span>
## 操作流程

<span id="79283f56"></span>
### 取得 PEM 檔案


1. 前往 Apple 的 [FairPlay Streaming](https://developer.apple.com/streaming/fps/) 概述頁面，並以您的 Apple Developer 帳戶登入。

2. 移至頁面底部並點擊 [Request FPS Deployment Package](https://developer.apple.com/contact/fps/)。

3. 依頁面指示下載 FPS 部署套件並解壓縮。

4. 根據套件內指示，建立 .pem 格式的私鑰檔案及 .csr 格式的憑證簽署請求檔案。記錄用於生成私鑰檔案的私鑰。


<span id="c164d382"></span>
### 取得 ASK 和證書檔案


1. 在 [Apple Developer Portal](https://developer.apple.com/) 左側導覽列中，點擊 **Certificates, ID & Profiles**。

2. 點擊 + 按鈕。

3. 選擇 **FairPlay Streaming Certificate**，然後點擊 **Continue**。

4. 上傳您於前一步取得的 CSR 檔案。成功上傳後，您將獲得 Application Secret Key (ASK)。

5. 依螢幕指示生成 FairPlay 證書。

6. 證書發出後，下載 FairPlay 串流證書。


<span id="1d180a9f"></span>
## 後續步驟

取得 FairPlay 串流證書後，您需將證書上傳至 BytePlus MediaLive 和 Intertrust。

如需詳細上傳操作說明，請參閱 [管理 DRM 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses) 和 [上傳 FairPlay 證書至 Intertrust](https://docs.byteplus.com/docs/byteplus-media-live/docs-uploading-a-fairplay-certificate-to-intertrust)。

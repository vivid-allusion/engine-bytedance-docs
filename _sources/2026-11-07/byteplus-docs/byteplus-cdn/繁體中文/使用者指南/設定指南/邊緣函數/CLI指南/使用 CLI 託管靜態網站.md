---
title: "使用 CLI 託管靜態網站"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/pages_host_webpage_zh-tw"
---

本文檔介紹如何使用邊緣函數 Pages 託管靜態頁面。

<span id="什麼是邊緣函數-pages"></span>
## 什麼是邊緣函數 Pages

邊緣函數 Pages 是 BytePlus 邊緣函數提供的靜態頁面託管服務，旨在幫助開發者快速、高效地將靜態網站部署到全球邊緣節點網路。透過邊緣函數 Pages，您可以輕鬆託管各類型的靜態內容，包括但不限於：


* 靜態網站（HTML/CSS/JavaScript）

* 單頁應用（SPA）

* 文件站點

* 部落格

* 靜態資源庫


邊緣函數 Pages 建構於全球分布的 BytePlus 邊緣節點之上，能將您的靜態資源快取到距使用者最近的節點，從而實現低延遲、高可用的內容傳遞。

<span id="基本概念"></span>
## 基本概念

<span id="pages-實例"></span>
### Pages 實例

Pages 實例是邊緣函數中用於託管與管理靜態頁面的基本單位。每個 Pages 實例都擁有唯一的 ID 作為識別。一個 Pages 實例可以包含多個資源（Asset），每個資源對應一個靜態網站版本，且各自擁有唯一的 ID。

透過 Pages 實例，您可以集中管理靜態頁面的生命週期，包括：


* 建立、設定與刪除實例

* 上傳、部署與管理資源版本


<span id="資源（asset）"></span>
### 資源（Asset）

資源是 Pages 實例中保存的靜態網站版本。每個資源包含完整的靜態站點檔案，並在上傳後生成唯一的資源 ID。

<span id="使用限制"></span>
## 使用限制

邊緣函數 Pages 的使用限制如下：


* 每個 BytePlus 帳戶最多可建立 10 個 Pages 實例

* 每個實例最多保留 100 個歷史資源，超出部分將自動清理

* 每個實例每月最多發布 100 次

* 每個資源的 gzip 壓縮後 tar 封裝大小不得超過 50 MB

* 每個資源中的檔案數量不得超過 500 個

* 每個資源中的單一檔案大小不得超過 25 MB


<span id="示例場景"></span>
## 示例場景

您有一個靜態網站專案，包含 .html、.css、.js 等檔案，希望透過邊緣函數 Pages 快速託管並發布該網站。

<span id="執行環境要求"></span>
## 執行環境要求

執行邊緣函數 CLI 的設備需符合以下要求：


* 作業系統：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 已安裝 [Node.js](https://nodejs.org/) 與 [npm](https://www.npmjs.com/)，版本要求：

   * Node.js：8.17.0+

   * npm：6.13.4+

* 已安裝 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步驟"></span>
## 操作步驟

<span id="步驟一：安裝邊緣函數-cli"></span>
### 步驟一：安裝邊緣函數 CLI

邊緣函數 Pages 無需本地函數專案，您可以選擇將 CLI 安裝到全域環境：

```shell
npm install -g @byteplus/nest
```


<span id="步驟二：設定您的-access-key-id-與-secret-access-key"></span>
### 步驟二：設定您的 Access Key ID 與 Secret Access Key

在任意目錄執行以下命令，於邊緣函數 CLI 中設定 BytePlus 帳戶的 Access Key ID 與 Secret Access Key。您可從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage) 取得對應憑證：

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="步驟三：建立並發布-pages-實例"></span>
### 步驟三：建立並發布 Pages 實例


1. 建立靜態資源目錄並放置站點檔案：

   ```shell
   mkdir -p site
   # 將您的靜態檔案（如 .html、.css、.js 等）放入 site 目錄
   ```
   

2. 執行以下命令，建立並立即發布 Pages 實例：

   ```shell
   npx nest pages create --name demo-site --assets ./site --deploy
   ```
   

   #### 參數說明    <span id="參數說明"></span>

   
   |參數 |類型 |是否必填 |描述 |
   |---|---|---|---|
   |\-\-name |string |是 |新建 Pages 實例的名稱 |
   |\-\-assets |string |是 |本地靜態資源目錄路徑（需包含 index.html 入口檔） |
   |\-\-deploy |flag |否 |建立完成後立即部署 Pages 實例 |
   

   命令執行成功後，您將看到類似以下的輸出訊息：

   ```shell
   ==> New Pages demo-site created!
   ==> [info]: Compressing given assets directory ./site...✓
   ==> [info]: Uploading assets...✓
   ==> [info]: Deploying pages...✓
   ==> Pages demo-site is publishing, you can visit it by open http://pywahntknjrhcufp.synthopages.bytepluses.com in browser a few minutes later
   ```
   

   發布操作通常需要 1–5 分鐘生效。生效後，您即可透過命令輸出提供的網域存取您的靜態站點。

   若您的 Pages 實例尚未綁定自訂網域，系統會自動分配一個用於預覽的臨時公開網域。該網域的後綴為 synthopages.bytepluses.com。請注意，此網域僅供預覽使用。您可以在瀏覽器中開啟該網域以預覽您的靜態網站。


<span id="步驟四：為靜態站點綁定自訂網域"></span>
### 步驟四：為靜態站點綁定自訂網域

為使靜態站點能透過自訂網域存取，可使用以下命令為 Pages 實例新增網域：

```shell
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


執行成功後，您將看到類似以下的輸出：

```Plain Text
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


新新增的網域需要驗證後才能正式上線使用。您需要為網域新增 CNAME 解析記錄，然後執行以下命令進行驗證：

```shell
nest pages domain verify -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


若需讓該網域支援 HTTPS，請為其上傳相應的 SSL/TLS 憑證：

```shell
# 為 Pages 實例的指定網域設定 SSL/TLS 憑證
nest pages domain update \
  -p p-2e9hpae39m2sqksy \
  --domain wow.test.example.com \
  --certificate ~/path/test.example.com.crt \
  --private-key ~/path/test.example.com.key
```

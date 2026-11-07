---
title: "使用 Pages 託管靜態頁面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/host_static_pages_console_zh-tw"
---

本文檔介紹如何在主控台使用 Pages 託管靜態頁面。

<span id="什麼是-pages"></span>
## 什麼是 Pages

Pages 是 BytePlus 邊緣函數提供的一項靜態頁面託管服務，旨在幫助您快速、高效地將靜態網站部署到全球邊緣節點網路。透過 BytePlus Pages，您可以輕鬆託管各種類型的靜態內容，包括但不限於：


* 靜態網站（HTML/CSS/JavaScript）

* 單頁應用（SPA）

* 文件網站

* 部落格

* 靜態資源庫


Pages 基於分佈在全球的 BytePlus 邊緣節點構建，將您的靜態資源快取到離使用者最近的邊緣節點，從而實現低延遲、高可用的內容交付。

<span id="使用限制"></span>
## 使用限制

Pages 的使用限制如下：


* 每個 BytePlus 帳號最多可以建立 10 個 Pages 實例

* 每個 Pages 專案最多保留 100 個歷史部署，多餘部署會自動清理

* 每個 Pages 實例每個月最多部署 100 次

* 每個 zip 套件的大小不超過 50 MB

* 每個 zip 套件內的檔案個數不超過 500 個

* 每個 zip 套件內的單一檔案大小不超過 25 MB


<span id="操作步驟"></span>
## 操作步驟

<span id="步驟一：建立-pages-專案"></span>
### 步驟一：建立 Pages 專案


1. 在 [Pages 頁面](https://console.byteplus.com/cdn/cdn-bp/synthopages/list)，按一下 **新專案**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b1218deb1b579bbed26535ce606e04fc.png) </span>

2. 在 **建立專案** 頁面，配置以下參數，然後按一下 **建立**。

   
   |分類 |參數 |說明 |
   |---|---|---|
   | |**建立方式** |選擇 **上傳檔案**。 |
   | |**上傳檔案** |上傳 .zip 格式的檔案套件，包含靜態網站的 .html，.js 或 .css 檔案。檔案套件中單一檔案壓縮前的大小不超過 25 MB。檔案套件中必須包含 index.html 入口檔案。 |
   |**通用設定** |**Pages 專案名稱** |輸入您的 Pages 專案名稱。 |
   ||**專案描述** （可選） |輸入 Pages 專案描述。 |
   ||**專案** |選擇所屬的 BytePlus 專案。 |
   ||**加速區域** |選擇加速區域。僅支援 **中國內地以外的區域**。 |
   |**加速設定** |**網域名稱**（可選） |您可以選擇關聯一個自訂網域名稱。如果您的 Pages 實例尚未關聯自訂網域名稱，系統會自動分配一個用於預覽的臨時公網網域名稱。 |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d977087c3b4466ee8c9ef57cba915a46.png) </span>

   建立成功後，靜態網站會自動部署。


<span id="步驟二：為-pages-專案配置網域名稱"></span>
### 步驟二：為 Pages 專案配置網域名稱


1. 在 **Pages** 頁面，找到步驟一建立的 Pages 專案，按一下專案名稱進入詳情頁。

   您可以透過 **預覽連結** 下的連結預覽您的部署。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e80b4557e1ff468802c63737f5b50145.png) </span>

2. 若您在建立專案時已新增自訂網域名稱，或需要綁定新的自訂網域名稱，請前往自訂網域名稱的 DNS 服務商主控台，新增一條 CNAME 記錄，將您的自訂網域名稱指向 BytePlus Pages 提供的 CNAME 地址。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">以 GoDaddy 為例，新增 CNAME 記錄的步驟如下：   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">登入 GoDaddy 的 <strong>Domain Portfolio</strong>。   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">選擇您要配置的網域名稱，進入 <strong>DNS Management</strong> 頁面。   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">按一下 <strong>Add New Record</strong>，選擇 <strong>Type</strong> 為 <strong>CNAME</strong>。   </div>
   

   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">填寫以下資訊：   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Name</strong>：填寫您的子網域名稱（例如 <code>www</code>）。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Value</strong>：填寫 Pages 專案提供的 CNAME 地址（例如 <code>your-project.synthopages.bytepluses.com</code>）。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>TTL</strong>：可以使用預設值或設定為您需要的時間（例如 <code>1 Hour</code>）。   </div>
   

   5. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">按一下 <strong>Save</strong> 儲存配置。   </div>
   

3. 配置完成後，按一下 **驗證**。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fa90f4a788d22b9d35d572673b95d2d9.png) </span>

   驗證完成後，即可透過您的自訂網域名稱存取靜態網站。


<span id="其他操作"></span>
## 其他操作

<span id="新增網域名稱"></span>
### 新增網域名稱

在 Pages 專案詳情頁的 **網域名稱管理** 區域，按一下 **新增**，可以為專案新增更多自訂網域名稱。

<span id="下載部署"></span>
### 下載部署

在 Pages 專案詳情頁的 **部署記錄** 區域，找到你需要下載的部署，在 **操作** 列按一下 **下載**。

<span id="更新部署"></span>
### 更新部署

在 Pages 專案詳情頁的 **部署記錄** 區域，按一下 **新部署**。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1edb091045f5d25156911d3989f36a69.png) </span>

在建立部署頁面重新上傳靜態網站的 zip 套件，即可更新部署。

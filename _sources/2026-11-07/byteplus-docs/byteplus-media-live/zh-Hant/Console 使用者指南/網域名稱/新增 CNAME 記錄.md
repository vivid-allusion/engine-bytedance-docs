---
title: "新增 CNAME 記錄"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adding-a-cname-record-zh-TW"
---

在 BytePlus MediaLive 控制台新增網域名稱後，系統會自動為您的網域名稱指派一個 BytePlus MediaLive 網域名稱，您可以在網域名稱清單的 **CNAME** 欄位中找到該名稱。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/921578252bd64ce5b8cdba2a4952cb4d~tplv-goo7wpa0wc-image.image) </span>

請將您的網域名稱指向由 BytePlus MediaLive 指派的 CNAME 位址。設定生效後，您的直播流將會加速。若要使用 BytePlus MediaLive 服務，您必須新增 CNAME 記錄。

<span id="78110c72"></span>
### 前置條件


* 已新增網域名稱。

* 網域名稱尚未設定 CNAME 記錄，這會在 **CNAME** 欄位中以黃色驚嘆號（!）標示。


<span id="a9099180"></span>
### 操作流程

本主題說明設定 CNAME 記錄的一般方法。此流程僅為一般指引。若您無法依照這些步驟設定 CNAME 記錄，請聯絡您的網域服務供應商以取得更多資訊。


1. 登入您的網域服務供應商控制台。

2. 選取您要管理的網域名稱。

3. 在出現的頁面上，設定以下參數以新增 CNAME 記錄。

   * 主機記錄：輸入子網域名稱的前綴。例如，若網域名稱為 example.live.com，請輸入 `example`。

   * 記錄類型：選擇 **CNAME**。

   * 線路類型：選擇預設線路類型。

   * 記錄值：輸入該網域名稱的 CNAME 位址。您可以在 BytePlus MediaLive 控制台的網域名稱清單中找到 CNAME 位址。

   * TTL：建議您輸入 600s。

4. 儲存設定並等待其生效。此時，網域名稱清單的 **CNAME** 欄位會顯示綠色勾號（✓）。

---
title: "禁用的 HTTP 方法"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/disallowed-http-method_zh-tw"
---

本文檔介紹了如何在 BytePlus CDN 中指定不支援的請求方法。

<span id="關於-http-請求方法"></span>
## 關於 HTTP 請求方法

HTTP 請求方法指定了資源請求的方式。不同的請求方法有特定的使用場景。預設情況下，CDN 允許使用者使用以下請求方法存取網域名稱。


* GET

* POST

* HEAD

* DELETE

* PUT

* PATCH

* CONNECT

* OPTIONS


您可以根據需求配置 CDN 所不支援的 HTTP 請求方法。 如果一個使用者請求使用了不支援的 HTTP 請求方法，CDN 會拒絕該請求並回傳 405 回應狀態碼。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">GET 和 POST 是使用者存取 CDN 時普遍使用的請求方法，我們不建議您禁用。</div>


* <div data-tips="true" data-tips-type="tip">在 CDN 向物件儲存來源伺服器發送回源請求時，回源請求使用的方法與使用者請求相同。預設情況下，CDN 支援使用者請求使用的請求方法有 DELETE、GET、HEAD、POST、PUT、PATCH、CONNECT、OPTIONS。如果您不希望使用特定請求方法的回源請求存取您的來源伺服器，例如您不希望使用 DELETE 方法的請求刪除來源伺服器上檔案，建議您執行以下所有操作：</div>


   * <div data-tips="true" data-tips-type="tip">對於您提供的 AK/SK 所對應的雲端供應商帳號，在雲端供應商處設定權限，禁止該帳號在您的物件儲存來源伺服器上執行特定的操作。</div>


   * <div data-tips="true" data-tips-type="tip">在 "禁用 HTTP 方法" 設定中，指定 CDN 不支援使用者請求使用的請求方法。</div>



<span id="操作步驟"></span>
## 操作步驟


1. 打開 **禁用的 HTTP 方法** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為 **開啟**。

3. 勾選那些不支援的 HTTP 請求方法，然後點擊 **儲存**。

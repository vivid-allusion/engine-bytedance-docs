---
title: "TLS 版本設定"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/tls-version_zh-tw"
---

本文件介紹如何在 BytePlus CDN 中對網域名稱配置 TLS 版本的支援。

使用者在使用瀏覽器訪問啟用了 HTTPS 加速的網域名稱時，CDN 會根據瀏覽器的 TLS 版本支援情況以及網域名稱支援的 TLS 版本，選擇匹配的最高的 TLS 版本進行資料傳輸。如果 CDN 找不到匹配的 TLS 版本，TLS 握手失敗，導致連接建立失敗。

<span id="tls-版本"></span>
## TLS 版本

越早版本的 TLS 相容性越好，但是安全性越差。最新版本的 TLS 提供了最好的安全性，但是相容性相對差一些。但是目前絕大部分瀏覽器都已支援 TLS 1.3。TLS 1.0 和 TLS 1.1 的版本較早，存在安全漏洞的風險。

CDN 支援所有 TLS 版本。但為了兼顧相容性和安全性，在您開啟 HTTPS 加密服務時，CDN 預設啟用對 TLS 1.1、TLS 1.2 和 TLS 1.3 的支援。您可以依需求手動啟用 CDN 對 TLS 1.0 的支援。

關於 CDN 支援的 TLS 加密套件，參見 [加密套件](https://docs.byteplus.com/en/docs/18/36330#cdn-%E6%94%AF%E6%8F%B4%E7%9A%84-tls-%E5%8A%A0%E5%AF%86%E5%A5%97%E4%BB%B6)。

<span id="瀏覽器支援的-tls-版本"></span>
## 瀏覽器支援的 TLS 版本

TLS 版本與瀏覽器支援情況如下表。


|**TLS 版本** |**支援的瀏覽器** |**備註** |
|---|---|---|
|TLS 1.0 |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |TLS 1.0 和 TLS 1.1 的支援在以下版本的瀏覽器中被移除了：<br><br><br>* Google Chrome 84+<br><br>* Microsoft Edge 84+<br><br>* Mozilla Firefox 78+<br><br>* Safari 14+ |
|TLS 1.1 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ ||
|TLS 1.2 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ | |
|TLS 1.3 |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ | |


<span id="前提條件"></span>
## 前提條件

要開啟該配置，網域名稱必須已經開啟了 HTTPS 加密服務。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **TLS 版本設定** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **TLS 版本設定** 下方，勾選需要啟用的 TLS 版本。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您至少需要勾選一個 TLS 版本。   </div>
   

3. 配置完成後，點擊 **儲存**。


<span id="更多資訊"></span>
## 更多資訊

<span id="cdn-支援的-tls-加密套件"></span>
### CDN 支援的 TLS 加密套件

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN 會根據伺服器上配置的套件優先級選擇最優的套件。</div>



|**TLS 版本** |**支援的加密套件** |
|---|---|
|TLS 1.1 |* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS1.2 |* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-RSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-ECDSA\-AES256\-CCM8<br><br>* ECDHE\-ECDSA\-AES256\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA256\-SHA384<br><br>* ECDHE\-ECDSA\-CAMELLIA256\-SHA384<br><br>* AES256\-GCM\-SHA384<br><br>* AES256\-CCM8<br><br>* AES256\-CCM<br><br>* AES256\-SHA256<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA256<br><br>* CAMELLIA256\-SHA<br><br>* ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-CCM8<br><br>* ECDHE\-ECDSA\-AES128\-CCM<br><br>* AES128\-CCM8<br><br>* AES128\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA128\-SHA256<br><br>* ECDHE\-ECDSA\-CAMELLIA128\-SHA256<br><br>* AES128\-GCM\-SHA256<br><br>* AES128\-SHA256<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA256<br><br>* CAMELLIA128\-SHA<br><br>* ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ARIA128\-GCM\-SHA256 |
|TLS1.3 |* TLS_AES_256_GCM_SHA384<br><br>* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_128_GCM_SHA256 |


<span id="如何查看瀏覽器請求所使用的-tls-版本"></span>
### 如何查看瀏覽器請求所使用的 TLS 版本


1. 在瀏覽器中打開某個網站。譬如使用最新版本的 Google Chrome 打開 [BytePlus 官網](https://www.byteplus.com/en)。

2. 按 F12 鍵打開開發者工具（DevTools）。

3. 點擊 **安全** 標籤頁。

4. 在 **安全** 標籤頁上，留意紅框中的內容。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23dd1e4fba6a4badb124a07bce3ce2b7~tplv-goo7wpa0wc-image.image) </span>

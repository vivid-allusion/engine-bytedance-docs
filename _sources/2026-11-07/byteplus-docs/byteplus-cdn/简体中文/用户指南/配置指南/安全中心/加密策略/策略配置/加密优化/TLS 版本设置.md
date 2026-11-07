---
title: "TLS 版本设置"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-allowed-tls-versions-cn"
---

本文档介绍如何在 BytePlus CDN 中对域名配置 TLS 版本的支持。

用户在使用浏览器访问启用了 HTTPS 加速的域名时，CDN 会根据浏览器的 TLS 版本支持情况以及域名支持的 TLS 版本，选择匹配的最高的 TLS 版本进行数据传输。如果 CDN 找不到匹配的 TLS 版本，TLS 握手失败，导致连接建立失败。

<span id="tls-版本"></span>
## TLS 版本

越早版本的 TLS 兼容性越好，但是安全性越差。最新版本的 TLS 提供了最好的安全性，但是兼容性相对差一些。但是目前绝大部分浏览器都已支持 TLS 1.3。TLS 1.0 和 TLS 1.1 的版本较早，存在安全漏洞的风险。

CDN 支持所有 TLS 版本。但为了兼顾兼容性和安全性，在您开启 HTTPS 加密服务时，CDN 默认启用对 TLS 1.1，TLS 1.2 和 TLS 1.3 的支持。您可以按需手动启用 CDN 对 TLS 1.0 的支持。

关于 CDN 支持的 TLS 加密套件，参见 [加密套件](https://docs.byteplus.com/en/docs/18/6976#cdn-%E6%94%AF%E6%8C%81%E7%9A%84-tls-%E5%8A%A0%E5%AF%86%E5%A5%97%E4%BB%B6)。

<span id="浏览器支持的-tls-版本"></span>
## 浏览器支持的 TLS 版本

TLS 版本与浏览器支持情况如下表。


|**TLS 版本** |**支持的浏览器** |**备注** |
|---|---|---|
|TLS 1.0 |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |TLS 1.0 和 TLS 1.1 的支持在以下版本的浏览器中被移除了：<br><br><br>* Google Chrome 84+<br><br>* Microsoft Edge 84+<br><br>* Mozilla Firefox 78+<br><br>* Safari 14+ |
|TLS 1.1 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ ||
|TLS 1.2 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ | |
|TLS 1.3 |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ | |


<span id="前提条件"></span>
## 前提条件

要开启该配置，域名必须已经开启了 HTTPS 加密服务。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **TLS 版本控制** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 勾选需要启用的 TLS 版本。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">您至少需要勾选一个 TLS 版本。   </div>
   

3. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58f261ed7551482589c52d09ac6625cf~tplv-goo7wpa0wc-image.image) </span>

<span id="更多信息"></span>
## 更多信息

<span id="cdn-支持的-tls-加密套件"></span>
### CDN 支持的 TLS 加密套件

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN 会根据服务器上配置的套件优先级选择最优的套件。</div>



|**TLS 版本** |**支持的加密套件** |
|---|---|
|TLS 1.1 |* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS1.2 |* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-RSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-ECDSA\-AES256\-CCM8<br><br>* ECDHE\-ECDSA\-AES256\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA256\-SHA384<br><br>* ECDHE\-ECDSA\-CAMELLIA256\-SHA384<br><br>* AES256\-GCM\-SHA384<br><br>* AES256\-CCM8<br><br>* AES256\-CCM<br><br>* AES256\-SHA256<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA256<br><br>* CAMELLIA256\-SHA<br><br>* ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-CCM8<br><br>* ECDHE\-ECDSA\-AES128\-CCM<br><br>* AES128\-CCM8<br><br>* AES128\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA128\-SHA256<br><br>* ECDHE\-ECDSA\-CAMELLIA128\-SHA256<br><br>* AES128\-GCM\-SHA256<br><br>* AES128\-SHA256<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA256<br><br>* CAMELLIA128\-SHA<br><br>* ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ARIA128\-GCM\-SHA256 |
|TLS1.3 |* TLS_AES_256_GCM_SHA384<br><br>* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_128_GCM_SHA256 |


<span id="如何查看浏览器请求所使用的-tls-版本"></span>
### 如何查看浏览器请求所使用的 TLS 版本


1. 在浏览器中打开某个站点。譬如使用最新版本的 Google Chrome 打开 [BytePlus 官网](https://www.byteplus.com/en)。

2. 按 F12 键打开开发者工具（DevTools）。

3. 点击 **安全** 标签页。

4. 在 **安全** 标签页上，留意红框中的内容。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23dd1e4fba6a4badb124a07bce3ce2b7~tplv-goo7wpa0wc-image.image) </span>

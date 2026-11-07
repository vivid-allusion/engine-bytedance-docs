---
title: "TLS Versions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-allowed-tls-versions"
---

To balance security and compatibility for your HTTPS\-enabled domains, you can configure the supported TLS versions in BytePlus CDN.

This document explains how TLS versions affect connections and provides instructions on how to modify the default TLS settings for your domain names to ensure successful handshakes.

<span id="tls-versions"></span>
## TLS Versions

Earlier versions of TLS offer better compatibility but lower security. The latest version of TLS provides the best security but relatively lower compatibility. However, most browsers now support TLS 1.3. TLS 1.0 and TLS 1.1 are older versions that pose security vulnerabilities.

CDN supports all TLS versions. However, to balance compatibility and security, when you enable HTTPS Encryption Service for your domain, CDN enables support for TLS 1.1, TLS 1.2, and TLS 1.3 by default. You can manually enable CDN support for TLS 1.0 as needed.

For information about the TLS cipher suites supported by CDN, see [Cipher Suites](https://docs.byteplus.com/en/docs/18/6604#cdn-supported-tls-cipher-suites).

<span id="browser-support-for-tls-versions"></span>
## Browser Support for TLS Versions

The following table shows the TLS versions and their browser support.


|**TLS Version** |**Supported Browsers** |**Notes** |
|---|---|---|
|TLS 1.0 |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |Support for TLS 1.0 and TLS 1.1 has been removed in the following browser versions:<br><br><br>* Google Chrome 84+<br><br>* Microsoft Edge 84+<br><br>* Mozilla Firefox 78+<br><br>* Safari 14+ |
|TLS 1.1 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ ||
|TLS 1.2 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ | |
|TLS 1.3 |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ | |


<span id="prerequisites"></span>
## Prerequisites


1. Open the **TLS Versions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Select the TLS versions you want to enable.

   You must select at least one TLS version.

3. After the configuration is complete, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b70499a7dcb8b09e26ddae69fc0c0daa.png) </span>

<span id="more-information"></span>
## More Information

<span id="cdn-supported-tls-cipher-suites"></span>
### CDN Supported TLS Cipher Suites

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN selects the highest\-priority suite based on the order configured on the server.</div>



|**TLS Version** |**Supported Cipher Suites** |
|---|---|
|TLS 1.1 |* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS1.2 |* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-RSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-ECDSA\-AES256\-CCM8<br><br>* ECDHE\-ECDSA\-AES256\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA256\-SHA384<br><br>* ECDHE\-ECDSA\-CAMELLIA256\-SHA384<br><br>* AES256\-GCM\-SHA384<br><br>* AES256\-CCM8<br><br>* AES256\-CCM<br><br>* AES256\-SHA256<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA256<br><br>* CAMELLIA256\-SHA<br><br>* ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-CCM8<br><br>* ECDHE\-ECDSA\-AES128\-CCM<br><br>* AES128\-CCM8<br><br>* AES128\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA128\-SHA256<br><br>* ECDHE\-ECDSA\-CAMELLIA128\-SHA256<br><br>* AES128\-GCM\-SHA256<br><br>* AES128\-SHA256<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA256<br><br>* CAMELLIA128\-SHA<br><br>* ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ARIA128\-GCM\-SHA256 |
|TLS1.3 |* TLS_AES_256_GCM_SHA384<br><br>* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_128_GCM_SHA256 |


<span id="checking-the-tls-version-used-in-a-browser"></span>
### Checking the TLS Version Used in a Browser


1. Open a site in a browser. For example, use the latest version of Google Chrome to open [BytePlus official website](https://www.byteplus.com/en).

2. Press the F12 key to open the Developer Tools (DevTools).

3. Click the **Security** tab.


On the **Security** tab, the TLS version is listed under the **Connection** section.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23dd1e4fba6a4badb124a07bce3ce2b7~tplv-goo7wpa0wc-image.image) </span>

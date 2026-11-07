---
title: "Supported TLS versions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-supported-tls-versions"
---

To balance security and browser compatibility for your HTTPS\-accelerated domain names, you can configure the supported TLS versions in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring TLS version support applies to <strong>Playback domain name</strong>, <strong>Image domain name</strong>, and <strong>Custom\-origin domain name</strong>.</div>


<span id="a8631035"></span>
## Introduction

When users access a domain name that has enabled HTTPS acceleration using a browser, the cache node selects the highest matching TLS version for data transmission based on the browser's TLS version support and the TLS version configured for the accelerated domain. If the cache node cannot find a matching TLS version, the TLS handshake fails, resulting in a connection establishment failure.

<span id="dd922fc3"></span>
### TLS version selection

Earlier versions of TLS have better compatibility but lower security. The latest version of TLS provides the best security but may have relatively lower compatibility. However, most browsers currently support TLS 1.3.

To ensure compatibility with earlier versions of browsers, when HTTPS is enabled, the CDN enables support for all TLS versions except TLS 1.0. Due to security vulnerabilities in TLS 1.0 and TLS 1.1, if you have higher security requirements, you can manually disable support for TLS 1.1. Note that after disabling support for TLS 1.1, if the user's browser does not support TLS 1.2 and TLS 1.3, the connection establishment will fail.

For the TLS encryption suites supported by the CDN, refer to the [Cipher Suites](https://docs.byteplus.com/docs/byteplus-vod/docs-supported-tls-versions#86d5e942) section.

<span id="baae2c44"></span>
### TLS versions supported by browsers

The following table shows the TLS versions and browser support:


|**TLS version** |**Supported browsers** |**Notes** |
|---|---|---|
|TLS 1.0 |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |Support for TLS 1.0 and TLS 1.1 has been removed in the following versions of browsers:<br><br><br>* Google Chrome 84+<br><br>* Microsoft Edge 84+<br><br>* Mozilla Firefox 78+<br><br>* Safari 14+ |
|TLS 1.1 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ ||
|TLS 1.2 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ |None |
|TLS 1.3 |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ |None |


<span id="4c94f5c7"></span>
## Prerequisites

To configure TLS version support, you must have already enabled HTTPS for the domain name.

<span id="657027a3"></span>
## Configuring TLS version support


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **HTTP configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Supported TLS versions**, enable the **Status** toggle and select the TLS versions. You need to select at least one TLS version.

8. Click **Save**.


<span id="e8fe711e"></span>
## More information

<span id="6959b65f"></span>
### Cipher suites supported by BytePlus VOD

When selecting the cipher suite to use, BytePlus VOD will choose the optimal suite based on the priority of the suites configured on the server.


|**TLS version** |**Supported cipher suites** |
|---|---|
|TLS 1.0 |* ECDHE\-RSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS 1.1 |* ECDHE\-RSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS 1.2 |* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* AES256\-GCM\-SHA384<br><br>* AES256\-SHA256<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* AES128\-GCM\-SHA256<br><br>* AES128\-SHA256<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS 1.3 |* TLS_AES_256_GCM_SHA384<br><br>* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_128_GCM_SHA256<br><br>* TLS_AES_128_CCM_8_SHA256<br><br>* TLS_AES_128_CCM_SHA256 |


<span id="40456586"></span>
### How to check the TLS version used by a browser request


1. Open a website in a browser; for example, open the [BytePlus official website](https://www.byteplus.com/) in the latest version of Google Chrome.

2. Press the F12 key to open the developer tools (DevTools).

3. Click the **Security** tab.

4. On the **Security** tab, pay attention to the content in the red box.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3505de959e594c0b84da658d4440ebf5~tplv-goo7wpa0wc-image.image) </span>

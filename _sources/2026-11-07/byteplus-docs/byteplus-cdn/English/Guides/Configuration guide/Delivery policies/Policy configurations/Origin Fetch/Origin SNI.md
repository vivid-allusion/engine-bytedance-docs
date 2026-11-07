---
title: "Origin SNI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-sni_1"
---

<span id="what-is-sni"></span>
## What is SNI

SNI stands for Server Name Indication. It is an extension to the TLS protocol. SNI addresses the following issue in scenarios where multiple sites are deployed on the same server:


* When a client establishes a connection using the HTTPS protocol, the server cannot determine which site's certificate to send to the client.


If the client communicates with the server using the insecure HTTP protocol, during data transmission, the server uses the Host header in the client's request to determine which site the client wants to access. However, if the client connects to the server using the HTTPS protocol, there is a TLS handshake process before the start of data transmission. During this process, the Host header has not yet been passed to the server. Therefore, the server cannot obtain Host field information to determine the site certificate to send to the client. In this case, the client can use the SNI header to specify the target site. This allows the server to send the appropriate certificate to the client during the TLS handshake phase.

<span id="origin-sni"></span>
## Origin SNI

When pulling content from an origin server that hosts multiple HTTPS sites, you must ensure the CDN presents the correct identity. The Origin Server Name Indication (SNI) feature allows you to specify the domain name the CDN uses during the TLS handshake with your origin. This guide explains the concept of Origin SNI and provides step\-by\-step instructions for configuring it in the console to ensure successful and secure connections. The SNI discussed in this article refers to the Origin SNI feature of BytePlus CDN. Origin SNI specifies the domain name of the origin site that the CDN needs to access when requesting content from the origin site using the HTTPS protocol. If HTTPS is enabled for your domain, the default Origin SNI is set as follows:


* If you have not specified an Origin Host, the Origin SNI is the same as your domain name.

* If you have specified an Origin Host, the Origin SNI is the same as the "Origin Host."


However, in some scenarios, Origin SNI and Origin Host are not the same. In such cases, you can configure the Origin SNI in the CDN console.

<span id="steps"></span>
## Steps


1. Open the **Origin SNI** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set the **Status** to **Enabled**.

3. Set the **SNI Domain Name** to the target site's domain name, ensuring the length does not exceed 1024 characters.

4. After the configuration is complete, click **Save**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecb5c058f6b049e4919667da9f8599d3~tplv-goo7wpa0wc-image.image) </span>

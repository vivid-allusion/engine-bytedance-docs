---
title: "Origin SNI"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-origin-sni"
---

To ensure your origin server presents the correct TLS certificate when BytePlus VOD pulls content via HTTPS, you can configure a custom Origin SNI. This guide provides step\-by\-step instructions for setting the Origin SNI for a custom\-origin domain name in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Origin SNI applies to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="0172a271"></span>
## Introduction

SNI stands for Server Name Indication. SNI is an extension of the TLS protocol. In scenarios where multiple sites are deployed on the same server, SNI solves this problem: When a client establishes a connection with the server using the HTTPS protocol, the server cannot determine which site's certificate to send to the client.

If the client communicates with the server using the insecure HTTP protocol, the server can determine the site the client wants to access based on the Host field in the client's request. However, if the client connects to the server using the HTTPS protocol, there is a TLS handshake process before data transmission begins. During this process, the client has not yet transmitted the Host field to the server. Therefore, the server cannot obtain the Host field information to determine which site's certificate to send to the client. In this case, the client can use the SNI field to inform the server of the desired target site. This allows the server to send the corresponding certificate to the client during the TLS handshake phase.

<span id="131865b9"></span>
### Origin SNI

Origin SNI specifies the origin domain name that BytePlus VOD needs to access when requesting content from the origin server using the HTTPS protocol. If your accelerated domain name is enabled with HTTPS, there is a default Origin SNI setting. The default Origin SNI setting is as follows:


* If you do not specify an origin host, the Origin SNI is the same as the accelerated domain name.

* If you specify an origin host, the Origin SNI is the same as the origin host.


However, in some scenarios, the Origin SNI may be different from the origin host. If you have such a scenario, you can specify the Origin SNI in the BytePlus CDN Console.

<span id="操作步骤"></span>
## Configuring Origin SNI


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Origin SNI**, turn on the **Status** toggle and set the **SNI Domain Name** to the domain name of the target site. The length of the **SNI Domain Name** cannot exceed 1024 characters.

8. Click **Save**.

---
title: "HTTP/2"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-http-2"
---

To improve your website's performance and loading speed, you can enable the HTTP/2 protocol in BytePlus CDN. This guide provides instructions on how to enable this feature for your domain.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please note that due to conflicting protocol mechanisms, HTTP/2 and WebSocket cannot be enabled simultaneously.</div>


<span id="prerequisites"></span>
### Prerequisites

To enable this configuration, your domain must have HTTPS Encryption Service enabled.

<span id="what-is-http-2"></span>
## What is HTTP/2

HTTP/2 extends the capabilities of HTTP/1.x. It is compatible with HTTP/1.x but adds a binary framing layer, header compression, multiplexing, server push, and other features.

HTTP/2 does not mandate the use of HTTPS for websites. However, mainstream browsers' support for HTTP/2 is implemented based on SSL/TLS. Currently, websites that use HTTP/2 have HTTPS enabled.

<span id="steps"></span>
## Steps


1. Open the **HTTP/2** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Click **Save** to apply your changes.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260806105112-1460259610500.png) </span>

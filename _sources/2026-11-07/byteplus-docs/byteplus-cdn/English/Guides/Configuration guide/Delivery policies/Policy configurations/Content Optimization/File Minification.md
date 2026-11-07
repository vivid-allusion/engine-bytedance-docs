---
title: "File Minification"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/qJ-Dp4"
---

File Minification is a BytePlus CDN feature that reduces file size and improves content delivery speed. It automatically removes comments and redundant whitespace from HTML pages, as well as embedded JavaScript and CSS code, before returning the content to the user.

<span id="feature-introduction"></span>
## Feature Introduction

Comments and redundant whitespace characters may exist in HTML pages, as well as in embedded JavaScript and CSS code. When "File Minification" is enabled, the CDN will remove these whitespace characters before returning the HTML page, thereby reducing the file size and improving content delivery speed.

This feature only takes effect for user requests that meet all of the following conditions:


* The response's Content\-Type header is `text/html`.

* The response contains the `Content-Length` header.

* The response status code is 200.

* The user request is not a Range request.

* "File Compression" is not enabled.


<span id="steps"></span>
## Steps


1. Open the **File Minification** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set the **Status** to **Enabled**.

3. After completing the configuration, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_96b3c030acc5c74b48a413a130025914.png) </span>

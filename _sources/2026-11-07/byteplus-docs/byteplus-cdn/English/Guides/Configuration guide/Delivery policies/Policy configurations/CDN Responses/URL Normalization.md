---
title: "URL Normalization"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-normalization_en-us"
---

URL Normalization is a feature provided by BytePlus CDN that automatically standardizes request URLs. This feature helps prevent request failures by correcting non\-standard content, such as backslashes or consecutive slashes, ensuring that both the CDN and your origin server can process requests correctly. This document explains how the feature works and guides you through the configuration steps.

<span id="how-it-works"></span>
## How it works

If a user's request URL contains non\-standard content, the origin server might fail to process the request because the CDN forwards the original, non\-standard URL. Similarly, if you submit a non\-standard URL when performing purge or prefetch operations, the operations might fail or not work as intended.

This feature normalizes the following non\-standard components of a request URL.


|**Non\-standard Content** |**Normalization Method** |**Example: Non\-standard URL** |**Example: Normalized URL** |
|---|---|---|---|
|Backslash () |Replaced with a single slash (/) |https://www.example.com/img\test |https://www.example.com/img/test |
|Consecutive slashes (//) |Replaced with a single slash (/) |https://www.example.com//img///test |https://www.example.com/img/test |
|/./ |Replaced with a single slash (/) |https://www.example.com/./img/test |https://www.example.com/img/test |
|/../ |* If there is a directory before `/../`, then `/../` and that directory are deleted.<br><br>* If there is no directory before `/../`, the original URL is retained. |https://www.example.com/all/img/../test |https://www.example.com/all/test |
|||https://www.example.com/../test |https://www.example.com/../test |



* URL normalization does not redirect the user's request URL to the normalized URL. Therefore, the URL in the client's browser address bar does not change.

* When a user request is received, the URL Normalization configuration takes precedence over other configurations. The "URL Authentication" feature operates based on the normalized URL.


<span id="steps"></span>
## **Steps**


1. Open the **URL Normalization** configuration page. For instructions, see [Domain Management](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to enabled.

3. In **Settings Object**, select the normalization options to enable.

4. After the configuration is complete, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_eaf71fde6d33a15a80544e2a2129079a.png) </span>

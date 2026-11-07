---
title: "Serve Stale"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/always-online_en-us"
---

The Serve Stale feature from BytePlus CDN enhances your website's availability. When your origin server fails or returns an error, this feature allows the CDN to continue serving cached content to users, even if the cache has expired.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


This document guides you through enabling and configuring Serve Stale to handle conditions like origin unresponsiveness or specific 5xx error codes.

After you enable Serve Stale, if the configured conditions are met and CDN has cached the requested file, CDN will send the cached file to the user.

<span id="steps"></span>
## Steps


1. Open the **Serve Stale** configuration page. For the steps, see [Domain Management](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to Enabled.

3. Refer to the following configuration instructions.

4. After the configuration is complete, click **Save**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e6cf9400be958274c72adbbc7136ee11.png) </span>

<span id="configuration-description"></span>
## Configuration Description


|**Configuration** |**Description** |
|---|---|
|Conditions |Specifies the conditions that trigger the CDN to serve stale content to users. You can select one or more of the following conditions:<br><br><br>* **Origin Unresponsive**: The CDN did not receive a response from the origin.<br><br>* **Origin 5xx Errors**: The origin server's response is a 5xx status code. If you select this condition, you need to specify the specific 5xx status code in **Error Status Code**. |
|Error Code |Specifies the 5xx response status codes that trigger this rule. The range is 500\-599. Multiple status codes are separated by semicolons (;). For example, `505;504`. You can also enter `5xx` to represent any status code starting with the number 5.<br><br>This configuration appears only when you select **Origin 5xx Errors** under **Conditions**. |


<span id="serve-stale-and-negative-caching"></span>
## Serve Stale and Negative Caching

If you configure a 5xx status code in both Serve Stale and [Negative Caching](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-negative-caching), when the origin response contains that 5xx status code:


* If the CDN has cached the 5xx status code, Negative Caching takes effect.

* If the 5xx status code has not been cached, the CDN caches the origin's 5xx response and forwards it to the user.

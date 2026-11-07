---
title: "Geographic Restrictions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-geographical-restrictions"
---

To control which geographic locations can access your content, you can use the Geographic Restrictions feature in BytePlus CDN. This guide provides step\-by\-step instructions on how to configure an allowlist to permit access only from specified regions, or a blocklist to deny access from specified regions.

<span id="steps"></span>
## Steps


1. Open the **Geographic Restrictions** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Configure the settings as described in the following table.

4. When you are finished, click **Save**.



|**Configuration** |**Description** |
|---|---|
|Filter |The configuration has the following options:<br><br><br>* **Allowlist**: Allows requests from the specified regions to access your domain.<br><br>* **Blocklist**: Blocks requests from the specified regions from accessing your domain.<br><br><br>If a request matches the blocklist or does not match the allowlist, the CDN will reject the request and return a 403 response status code. |
|Countries & Regions |Specify one or more regions. The **Others** option applies to client IP addresses from locations that the CDN cannot recognize. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d85763009a4a7f9fc5a57efc91435f~tplv-goo7wpa0wc-image.image) </span>

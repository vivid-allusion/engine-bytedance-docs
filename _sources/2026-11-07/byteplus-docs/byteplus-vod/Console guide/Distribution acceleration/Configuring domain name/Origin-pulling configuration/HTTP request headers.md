---
title: "HTTP request headers"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-http-request-headers"
---

To control the information passed from the CDN to your origin server, you can configure HTTP request headers for your custom\-origin domain names in the BytePlus VOD console. This guide provides instructions on how to add, overwrite, or delete specific header fields in back\-to\-origin requests.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring HTTP request headers applies to <strong>Custom\-origin domain</strong> <strong>names</strong>.</div>


<span id="41ac73ad"></span>
## Introduction

You can do the following with request headers:


* **Set request header**: If you need to add fields in the back\-to\-origin request header, you can configure it through this operation. If the field already exists in the request header when matching, the existing field value will be overwritten. Matches are case\-insensitive. For example, you added the field `X-Form:huoshan`, but the field `x-form:hs` already exists in the request header. At this point, the field in the request header will be updated to `x-form:huoshan`.

* **Delete Request Header**: If you do not need certain fields in the back\-to\-origin request header, you can use this operation to remove them. CDN removes these fields from the request headers of back\-to\-origin requests.


<span id="9b51eaa3"></span>
## Configuring HTTP request headers


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Origin\-pulling configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **HTTP request headers**, switch the **Status** toggle and click **Add rule**. You can add up to 50 rules. At this point, a rule to be configured will appear in the rule list.

   
   |**Configuration** |**Description** |
   |---|---|
   |Header operation |Specify the operation to perform on the header. You can set the following values:<br><br><br>* **Set**: Indicates adding a field or setting a specific value for an existing field.<br><br>* **Delete**: Indicates deleting a specific field. |
   |Header name |Enter a request header field. You can set any name, such as `X-Form`. Field names cannot exceed 1,024 characters and can contain printable ASCII characters except underscore (_), space, double quote ("), Delete (ASCII code 127). |
   |Value type |Specify how the header's value is determined. You can set the following values:<br><br><br>* **Constant**: Indicates that the value of the request header field is a fixed value. You need to set this value in **Header value**.<br><br>* **Variable**: Indicates that the header value is dynamically set from a system variable. You must select a variable from the **Header value** list. See [Variable fields](https://docs.byteplus.com/docs/byteplus-vod/docs-http-request-headers#db21d2e2). |
   |Header value |Set the value of the request header field. Field values cannot exceed 1,024 characters and may contain printable ASCII characters except: dollar sign ($), and Delete (ASCII code 127). |
   |Action |Indicates the action that can be taken on the rule. For example, delete the rule. |
   

8. Click **Save**.


<span id="db21d2e2"></span>
## Variable fields

The system provides the following variable fields.


|**Field name** |**Description** |**Example** |
|---|---|---|
|uri |Indicates the URI of the back\-to\-origin request. If the URI itself contains parameters, the question mark (?) and the parameters following the question mark are removed. |`/dir/image.php` |
|request_uri |Indicates the URI of the back\-to\-origin request. If the URI itself contains parameters, the question mark (?) and the parameters following the question mark are preserved. |`/dir/image.php?color=red&n=10` |
|http_host |Indicates the value of the host field in the back\-to\-origin request header. |`example.com:8080` |
|args |Indicates the parameter part of the back\-to\-origin request URI, but does not contain the question mark (?) before the parameter. |`color=red&n=10` |
|msec |Indicates the time when the CDN sends the request back to the origin. The format is a decimal Unix timestamp. |`1650558396` |
|scheme |Indicates the protocol used by the back\-to\-origin request. |`https` |


<span id="d8806c51"></span>
## Precautions

When defining header names, you cannot use names that start with `x-bdcdn-` or any of the following names; otherwise, an error will be reported. Field names are case\-insensitive.


* x\-forwarded\-for

* x\-bdcache\-trace\-id

* x\-real\-ip

* x\-client\-scheme

* x\-tos\-request\-id

* bd\-bdcdn\-oss\-switch

* x\-storagegw\-request\-id

* x\-sign


If you enter any of these field names, you will receive the `The header is invalid` error.

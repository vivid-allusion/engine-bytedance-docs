---
title: "Origin Request Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers"
---

The Origin Request Headers feature in BytePlus CDN allows you to add, modify, or delete HTTP headers in requests sent from CDN nodes to your origin server. You can use this capability for various purposes, such as identifying CDN traffic, distinguishing requests from different domains, or implementing access control at your origin. This document provides detailed instructions on how to configure these headers.

In requests sent to the origin, the CDN includes all request headers from the original user request. Additionally, the CDN will add some default request headers. Refer to [List of Default Headers Added by CDN](https://docs.byteplus.com/en/docs/18/6587#list-of-default-headers-added-by-cdn).

In addition to the default headers, you can configure custom headers to be included in origin requests.

<span id="applicable-scenarios"></span>
## Applicable Scenarios

**Identify Requests from the CDN**

Your origin server might receive requests from sources other than the CDN, or you might use multiple CDN providers for content delivery. In these cases, you can add a specific request header to the origin request. In the origin server's request logs, you can use this request header to collect the following data:


* The number of requests not from the CDN.

* The number of requests from BytePlus CDN versus other CDN providers.


**Distinguish Requests from Different Acceleration Domains**

If you have configured multiple domains with different usage scenarios to use the same origin server, you can add a custom header to distinguish requests from each domain. This allows you to collect domain\-specific data from your origin server's logs.

**Implement Access Control at the Origin Server**

To block requests that do not originate from the CDN, you can add a custom request header. You can then configure your origin server to reject any requests that lack this specific header.

<span id="steps"></span>
## Steps


1. Open the **Origin Request Headers** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add up to 50 rules.

3. Follow the configuration instructions below.

4. After configuring, click **Save**.


<span id="configuration-instructions"></span>
## Configuration Instructions


|**Configuration** |**Description** |
|---|---|
|Header Operation |Indicates an operation type. This configuration has the following options:<br><br><br>* **Set**: Indicates setting a header. The set operation includes adding and modifying. If the specified header already exists in the request, its value is overwritten. If it does not exist, the header is added.<br><br>* **Delete**: Indicates deleting a header. |
|Header Name |Indicates the header to be set or deleted. The header name is case\-insensitive. Except for the header names listed in [Notes](https://docs.byteplus.com/en/docs/18/6587#notes), you can enter any header name. The header name cannot exceed 1,024 characters and cannot contain the following characters:<br><br><br>* Chinese characters, underscores (_), spaces, double quotes ("), colons (:) |
|Value Type |The type of value for the header specified in **Header Name**, with the following options:<br><br><br>* **Literal Value**: Indicates the header value is a string.<br><br>* **HTTP Variable**: Indicates the header value comes from a variable.<br><br>* **Custom**: Indicates the header value is constructed by combining literal strings and variables. |
|Header Value |Indicates the value of the header specified in **Header Name**.<br><br><br>* If **Value Type** is **Literal Value**, you need to enter a string. The string length cannot exceed 1,024 characters and cannot contain the following characters:<br><br>   * Chinese characters, underscores (_), spaces, double quotes ("), colons (:)<br><br>* If **Value Type** is **HTTP Variable**, you need to select a variable from the list. Refer to [Variable List](https://docs.byteplus.com/en/docs/18/6587#variable-list).<br><br>* If **Value Type** is **Custom**, enter a combination of literal strings and variables. Wrap variables in curly braces {} and prefix them with a dollar sign $. For example, `bind${scheme}to${client\_ip}done`. |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a0a2983cb264fa3ab430eb649fc4ba5~tplv-goo7wpa0wc-image.image) </span>

<span id="variable-list"></span>
## Variable List

CDN provides the following variables.


|Variable Name |Description |Example Value |
|---|---|---|
|uri |Indicates the path in the origin request URL. |`/dir/sample.php` |
|request_uri |Indicates the path and query string in the origin request URL. |`/dir/sample.php?color=red&n=10` |
|http_host |Indicates the value of the Host header in the origin request. |`example.com:8080` |
|args |Indicates the query string in the origin request URL. |`color=red&n=10` |
|msec |Indicates the time when the CDN sets this origin request header, in Unix timestamp format, with millisecond precision. |`1704444754.917` |
|scheme |Indicates the protocol used in the origin request. |`https` |
|origin_srv_addr |Indicates the domain name or IP address of the origin server. |`www.example.com` |
|query_string |Has the same meaning as the `args` variable. |`size=small&color=red` |
|host |Indicates the value of the Host header in the origin request.<br><br>&nbsp;<br><br>Note that the CDN may modify this header value when processing the request. Therefore, it is recommended to use `http_host` instead. |`example.com:8080` |
|client_ip |Indicates the real IP address of the client that connected to the CDN and triggered this origin request. |`127.1.1.1` |


<span id="notes"></span>
## Notes

The request header names you set cannot start with `x-bdcdn-` or `X-Bytecdn-`, and cannot be any of the following headers.


* x\-tos\-request\-id

* bd\-bdcdn\-oss\-switch

* x\-storagegw\-request\-id

* x\-sign

* host

* X\-Trace\-Via


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the user request contains headers starting with <code>x-bdcdn-</code> or <code>X-Bytecdn-</code>, these headers will not be included in the origin request.</div>


<span id="default-headers-added-by-cdn"></span>
## Default Headers Added by CDN

By default, the CDN adds the following headers to origin requests.


|Request Header |Description |Example |
|---|---|---|
|X\-Forwarded\-For |Indicates the IP address of the CDN node that sent the origin request. |`xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxx`, `xx.xx.xxx.xxx` |
|X\-Forwarded\-Protocol |Indicates the protocol used in the origin request. |`http` |
|X\-Real\-IP |Indicates the IP address of the client that initiated the request to the CDN. |`xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxx` |
|X\-Forwarded\-Proto |Indicates the protocol used in the user request. |`http` |
|X\-Client\-Scheme |Indicates the protocol used in the user request. |`http` |
|X\-Trace\-Via |Indicates the identifier of the CDN node that sent the origin request. |`gycm` |
|Bd\-Raw\-Host |Indicates the domain name in the user's request URL. |`www.example.com` |
|X\-Bdcache\-Trace\-Id |Indicates the ID of the user request. |`f455f0415d901f8aee3b2c7336bfad16` |
|X\-Tt\-Trace\-Id |Indicates the ID of the origin request. |`202405301714110101720050051BB69184` |

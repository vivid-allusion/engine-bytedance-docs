---
title: "Origin Response Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-headers_en-us"
---

Origin Response Header Settings enables you to modify headers in responses returned by your origin before the CDN performs further processing.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use this feature, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


When the CDN receives a response from your origin, it first applies your Origin Response Header rules to the response headers. It then processes the response based on the modified headers.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814073607-1720749573894.png) </span>

<span id="steps"></span>
## Steps


1. Go to the **Origin Response Header** page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. In the **Origin Response Header** section, click **Add**. You can add up to 50 rules.

3. Configure the rule as described in [Configuration](https://docs.byteplus.com/en/docs/18/118297#configuration).

4. Click **Save**.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260814084155-781547460298.png) </span>

<span id="configuration"></span>
## Configuration


|Setting |Description |
|---|---|
|Action |Specifies the action to perform. Available options:<br><br><br>* **Set**: Sets the specified header. If the header is not present in the origin response, the CDN adds it. If the header already exists in the origin response, the CDN replaces its value with the specified value.<br><br>* **Delete**: Removes the specified header. |
|Header Name |Specifies the header to set or delete. Header names are case\-insensitive.<br><br>&nbsp;<br><br>You can select a commonly used header from the list. For more information, see [Common headers](https://docs.byteplus.com/en/docs/18/118297#common-headers). You can also enter a custom header name. A header name can contain up to 1,024 characters and cannot contain Chinese characters, spaces, double quotation marks (`"`), or colons (`:`). |
|Value Source |Specifies how the value is defined for the header specified in **Header Name**. Available options:<br><br><br>* **Literal**: Sets the header to a string value.<br><br>* **Variable**: Sets the header to a variable value.<br><br>* **Custom**: Sets the header to an expression that can contain strings and variables. |
|Header Value |Specifies the value of the header specified in **Header Name**.<br><br>&nbsp;<br><br>\- When **Value Source** is **Literal**, enter a string of up to 1,024 characters. The string cannot contain Chinese characters or dollar signs (`$`).<br><br>\- When **Value Source** is **Variable**, select a variable from the list. For more information, see [Variables](https://docs.byteplus.com/en/docs/18/118297#variables).<br><br>\- When **Value Source** is **Custom**, enter an expression composed of strings and variables. Enclose each variable name in braces (`{}`) and prefix it with a dollar sign (`$`). For example: `bind${remote_addr}to${host}done`.<br><br>&nbsp;<br><br>If **Header Name** is `Access-Control-Allow-Origin`, **Header Value** can contain multiple source IP addresses and source domain names, separated by commas (`,`), to tell browsers which origins' scripts can read cross\-origin responses. |
|Scope |Specifies the origin responses to which the rule applies. Available options:<br><br><br>* **Default Scope**: The rule applies only when the origin response has one of the following status codes: `200`, `201`, `204`, `206`, `301`, `302`, `303`, `304`, `307`, or `308`.<br><br>* **All Requests**: The rule applies to all origin responses, regardless of status code.<br><br><br>When **Action** is **Delete**, only **All Requests** is available. |


<span id="variables"></span>
## Variables

For a list of supported variables and their descriptions, see [Origin Request Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers#variable-list).

<span id="notes"></span>
## Notes

You cannot configure a response header whose name begins with `x-bdcdn-`, `x-byteinternal-`, or `X-Volc-`. You also cannot configure any of the following headers:


* `X-Kfc-Cachekey`

* `X-Bdcdn-Origin-Err`

* `access-check`

* `server-timing`

* `via`

* `x-request-ip`

* `x-tt-trace-tag`

* `x-bdcdn-logid`

* `byte-error-code`

* `x-bdcdn-cache-status`

* `host`

* `X-Exception-Info`


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If an origin response contains a header whose name begins with <code>x-bdcdn-</code>, <code>x-byteinternal-</code>, or <code>X-Volc-</code>, the CDN removes the header before returning the response to the client.</div>


<span id="common-headers"></span>
## Common Headers

For a list of commonly used headers and their descriptions, see [Client Response Header](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers#common-headers).

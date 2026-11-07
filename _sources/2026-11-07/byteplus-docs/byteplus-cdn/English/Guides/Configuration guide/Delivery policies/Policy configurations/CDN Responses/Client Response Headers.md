---
title: "Client Response Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers"
---

To control browser behavior or add custom metadata, you can configure the HTTP response headers that BytePlus CDN delivers to your users.

By default, in response to user requests, the CDN will include all headers from the origin server's response. You can configure the headers included in the CDN's response to user requests.

<span id="steps"></span>
## Steps


1. Open the **Client Response Headers** configuration page. For instructions, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Click **Add Rule**.

   You can add up to 50 rules.

3. Refer to the following configuration instructions.

4. After configuring, click **Save**.



|**Configuration** |**Description** |
|---|---|
|Header Operation |Specifies the operation to perform on the header. This configuration has the following options:<br><br><br>* **Set**: Indicates setting a header. The set operation includes adding and modifying. If the origin server's response already contains this header, its value will be overwritten. If the origin server's response does not contain this header, the header will be added.<br><br>* **Delete**: Indicates deleting a header. |
|Header Name |Indicates the header that needs to be set or deleted. Header names are case\-insensitive. You can select a common header from the dropdown list, see [Common Headers](https://docs.byteplus.com/en/docs/18/6574#common-headers). Except for the header names listed in the [Notes](https://docs.byteplus.com/en/docs/18/6574#notes), you can enter any header name. The header name cannot exceed 1,024 characters and cannot contain the following characters:<br><br><br>* Chinese characters, underscores (_), spaces, double quotes ("), colons (:) |
|Value Type |For the header specified in **Header Name**, this configuration indicates the type of the header value, with the following options:<br><br><br>* **Literal Value**: Indicates that the header value is a string.<br><br>* **HTTP Variable**: Indicates that the header value comes from a variable.<br><br>* **Custom**: Indicates that the header value is a string concatenated from variables and strings. |
|Header Value |Indicates the value of the header specified in **Header Name**.<br><br><br>* If the **Value Type** is **Literal Value**, you need to enter a string. The string length cannot exceed 1,024 characters and cannot contain the following characters:<br><br>   * Chinese characters, underscores (_), spaces, double quotes ("), colons (:)<br><br>* If the **Value Type** is **HTTP Variable**, you need to select a variable from the list. See [Variable List](https://docs.byteplus.com/en/docs/18/6574#variable-list).<br><br>* If the **Value Type** is **Custom**, you need to enter a string concatenated from variables and strings. Variables need to be enclosed in `{}`, starting with `$`. For example, `bind${remote_addr}to${host}done`.<br><br><br>If the **Header Name** is `Access-Control-Allow-Origin`, you can enter multiple source IPs and source domains separated by commas (,) in **Header Value**, indicating the source IPs and source domains allowed to access your domain. The domain can be a wildcard domain. |
|CORS Validation |This setting determines whether the CDN validates and sets the Access\-Control\-Allow\-Origin header based on the Origin field in the request header. This setting appears only when the following two conditions are met:<br><br><br>* **Header** **Name** is `Access-Control-Allow-Origin`.<br><br>* **Value Type** is **Literal Value**.<br><br><br>`Access-Control-Allow-Origin` values support the following formats:<br><br><br>* Any origin : Set to `*`.<br><br>* Specific origin : Set single or multiple IPs, domain names, or a combination of IPs and domain names. Multiple origins are separated by commas (,). The origin must include the protocol `http://` or `https://` and supports ports.<br><br>* Wildcard domain : Supports wildcard domain format, for example, `https://*.``example.com`.<br><br><br>When **CORS** **Validation** is enabled, the CDN processing logic is as follows:<br><br><br>* Any match : If header value is set to `*`, the CDN returns `Access-Control-Allow-Origin: *` in the response regardless of whether the request carries the `Origin` header or what the value of the `Origin` header is.<br><br>* Exact match : If header value is set to single or multiple specific origins, the CDN checks if the `Origin` value in the request header exactly matches any of the configured origins.<br><br>   * If the match is successful, the CDN returns the `Access-Control-Allow-Origin` header in the response, with the value being the `Origin` value from the request.<br><br>   * If the match fails, the CDN does not return the `Access-Control-Allow-Origin` header in the response.<br><br>* Wildcard domain match : If header value is set to a wildcard domain, the CDN checks if the `Origin` value in the request header matches the wildcard domain. The processing logic after matching is the same as exact match.<br><br><br>If **CORS** **Validation** is not enabled, the CDN does not check the `Origin` header and always adds your configured `Access-Control-Allow-Origin` header to the response.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the value of <code>Access-Control-Allow-Origin</code> contains multiple origins, it is strongly recommended that you enable <strong>CORS</strong> <strong>Validation</strong>. If not enabled, the CDN will return all origins as the header value, while browsers typically only allow <code>Access-Control-Allow-Origin</code> to contain a single value, causing browser errors.</div><br> |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f48c8ebafecaeccb0a07eec66ec42047.png) </span>

<span id="variable-list"></span>
## Variable List

The CDN provides the following variables.


|Variable Name |Description |Example |
|---|---|---|
|raw_uri |Indicates the path in the client's request URL. |`/dir/sample.php` |
|request_uri |Indicates the path and query string in the client's request URL. |`/dir/sample.php?color=red&n=10` |
|remote_addr |Indicates the IP address of the client that initiated this request. |`192.0.2.1` |
|remote_port |Indicates the port of the client that initiated this request. |`5936` |
|host |Indicates the value of the host header in the client's request.<br><br>&nbsp;<br><br>Note that the CDN may modify the value of this header when processing the request. Therefore, we recommend using `http_host` instead. |`www.example.com:8080` |
|http_host |Indicates the value of the host header in the client's request. This header value will not be modified by the CDN. | |
|args |Indicates the query string in the client's request URL. |`color=red&n=10` |
|msec |Indicates the time the CDN sets the response header, in Unix timestamp format, accurate to milliseconds. This timestamp is close to the response time of the first packet. |`1704444754.917` |
|scheme |Indicates the protocol used by the client. |`https` |
|cdn_cache_status |Indicates whether the request hit the cache.<br><br><br>* `edge_hit`: Indicates the request hit the edge node cache.<br><br>* `parent_hit`: Indicates the request hit the origin node cache.<br><br>* `miss`: Indicates the request did not hit the cache. |`edge_hit` |


<span id="common-headers"></span>
## Common Headers

The CDN provides the following common headers.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These headers are standard HTTP response headers. If the value of the response header is valid, the client's browser acts on the header accordingly. Depending on your use case, you can also set the values of these common headers to any string. For example, you can set the value of <code>Access-Control-Allow-Origin</code> to <code>helloworld</code>.</div>



|**Header Name** |**Description** |**Example** |
|---|---|---|
|Access\-Control\-Allow\-Origin |Specifies the origins allowed to access your site's resources.<br><br><br>* Multiple origins are separated by commas (,).<br><br>* You can specify `*`, indicating any origin.<br><br>* The host in the origin can be an IP address or a domain name. The domain name can be a wildcard domain.<br><br>* The origin can include a port.<br><br>* If the origin you specify is not `*` and **CORS Validation** is **Enable**, the origin must comply with URL specifications, which means the origin must include a scheme and a host. |Example 1<br><br>`*`<br><br>&nbsp;<br><br>Example 2<br><br>`https://www.another-site.com:448,http://192.0.2.1,https://*.example.com` |
|Access\-Control\-Allow\-Methods |Specifies the HTTP request methods allowed for cross\-origin requests. Multiple methods are separated by commas (,). |`GET` |
|Access\-Control\-Allow\-Headers |Specifies the HTTP request headers allowed to be included in cross\-origin requests. Multiple request headers are separated by commas (,). |`X-Custom-Header` |
|Access\-Control\-Expose\-Headers |Specifies the response headers that the scripts running on the client are allowed to access. Multiple response headers are separated by commas (,).<br><br>&nbsp;<br><br>By default, the response headers that client\-side scripts can access are `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`. If you need client\-side scripts to access more response headers, you can specify them in this header. |`Content-Encoding` |
|Access\-Control\-Allow\-Credentials |Specifies whether cross\-origin requests need to include authentication information. Authentication information includes cookies, authentication request headers, or client TLS certificates. |`true` |
|Access\-Control\-Max\-Age |Specifies the cache duration of the preflight request initiated by the client for cross\-origin requests. The unit is seconds. Before the cache expires, the client does not need to send the preflight request again. |`3600` |
|Cache\-Control |For content returned by the CDN, specifies how the content is cached on the client. |`max-age=3600` |
|Content\-Disposition |Indicates that the content returned by the CDN to the client is provided as a download and specifies the download file name. |`attachment;filename=Demo.xlsx` |
|Content\-Language |Indicates the language of the content returned by the CDN to the client. |`zh-CN` |
|Content\-Type |Indicates the MIME type of the response content. |`text/plain` |
|Pragma |For HTTP/1.0, this header indicates how the CDN response should be cached by the client. The header value can only be `no-cache`, indicating that the client should not cache the CDN response. |`no-cache` |


<span id="notes"></span>
## Notes

You cannot set response headers with any of the following names:


* access\-check

* server\-timing

* via

* x\-request\-ip

* x\-tt\-trace\-tag

* x\-bdcdn\-logid

* byte\-error\-code

* x\-bdcdn\-cache\-status

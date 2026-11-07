---
title: "HTTP response headers"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-http-response-headers"
---

To gain fine\-grained control over how browsers and clients handle your VOD content, you can customize the HTTP response headers delivered by the CDN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Configuring HTTP response headers applies to <strong>Playback domain name</strong>, <strong>Image domain name</strong>, and <strong>Custom\-origin domain name</strong>.</div>


<span id="fb0b01dd"></span>
## Introduction

By default, when an edge node responds to a user request, it will include all response headers from the origin server. In CDN, you can perform the following operations on response headers to achieve specific purposes.


* **Set response header**: If you need to add a field in the response header, you can configure it through this operation. If the field already exists in the response header when matching, the existing field value will be overwritten. Matches are case\-insensitive. For example, you added the field `X-Test:123`, but the field `x-test:456` already exists in the response header of the origin site. At this point, the field in the response header of the cache node will be updated to `x-test:123`.

* **Delete response header**: If you do not need some fields in the response header of the origin site, you can configure them through this operation. When an edge node responds to a user request, these fields are not included in the response header.


When you set up fields, you can enter any field or select a [Common fields](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers#5d3bdbdc) from the list. However, CDN does not support setting certain fields, see [Precautions](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers#aec6a4d5) for details.

<span id="ad2445c3"></span>
## Configuring HTTP response headers


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Advanced configuration** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **HTTP response header**, switch the **Status** toggle and click **Add rule**. You can add up to 50 rules. At this point, a rule to be configured will appear in the rule list.

   
   |**Configuration** |**Description** |
   |---|---|
   |Header operation |Set specific operations. You can set the following values:<br><br><br>* **Set**: Indicates adding a field or setting a specific value for an existing field.<br><br>* **Delete**: Indicates deleting a specific field. |
   |Header name |Enter a response header field. You can set any name, such as `X-Form`. Field names cannot exceed 1,024 characters and can contain printable ASCII characters except underscore (_), space, double quote ("), Delete (ASCII code 127). |
   |Value type |Set the value method of the request header field. You can set the following values:<br><br><br>* **Constant**: Indicates that the value of the request header field is a fixed value. You need to set this value in **Header value**.<br><br>* **Variable**: Indicates that the value of the request header field comes from a variable field. You need to select a variable field in the **Header value** list. The value of this variable field will be used as the value of the request header field. See [Variable fields](https://docs.byteplus.com/docs/byteplus-vod/docs-configuring-an-http-response-header#12ce5edf). |
   |Header value |Set the value of the request header field. Field values cannot exceed 1,024 characters and may contain printable ASCII characters except: dollar sign ($), and Delete (ASCII code 127). |
   |CORS |Indicates whether to verify the Origin field in the request header when CDN responds to user requests. You can enable or disable this configuration.<br><br><br>* Enabled: Indicates that the CDN will validate the Origin field. If the verification is successful, CDN includes the Access\-Control\-Allow\-Origin field in the response header. The field value is the same as the Origin field value. If the validation fails, the Access\-Control\-Allow\-Origin field will not be included in the response header.<br><br>* Disabled: Indicates that the CDN will not validate the Origin field. CDN will always include the Access\-Control\-Allow\-Origin header with the value you configure in the response headers.<br><br><br>This configuration can only be configured in the following cases:<br><br><br>* The **Header** in the rule is Access\-Control\-Allow\-Origin.<br><br>* The **Value type** in the rule is a **Constant**.<br><br><br>Note that:<br><br><br>* If you set Access\-Control\-Allow\-Origin to `*`. At this point, regardless of whether **Cross\-Origin Validation** is enabled or not, the value of the Access\-Control\-Allow\-Origin field in the response header is `*`.<br><br><br>**Example**: Your accelerated domain name is example.com. The Access\-Control\-Allow\-Origin you set in the rule is a constant value of `http://example.com,https://www.test.com`. At this point, a user requests to access your accelerated domain name.<br><br><br>* Suppose the value of the Origin field in the request header is `https://www.test.com`.<br><br>* If **CORS** is enabled, the value of the Access\-Control\-Allow\-Origin field in the response header is `https://www.test.com`.<br><br>* If **CORS** is disabled, the value of the Access\-Control\-Allow\-Origin field in the response header is `http://example.com,https://www.test.com`.<br><br><br>In this case, users can access your accelerated domain name.<br><br><br>* Suppose the value of the Origin field in the request header is `https://www.abc.com`.<br><br>* If **CORS** is enabled, the Access\-Control\-Allow\-Origin field will not be included in the response header. This occurs because the origin domain does not match the allowed list.<br><br>* If **CORS** is disabled, the response header will include the Access\-Control\-Allow\-Origin field. The value of this field is `http://example.com,https://www.test.com`.<br><br><br>In this case, users cannot access your accelerated domain name. The client will display an error message that cross\-domain access failed. |
   |Action |Indicates the action that can be taken on the rule. For example, delete the rule. |
   

8. Click **Save**.


<span id="56b8bf67"></span>
## Variable fields

The system provides the following variable fields. These variable fields are not included in CDN responses by default.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The variables in the following list are standard HTTP variables that are not included in CDN responses by default. You can use a variable from this list as a response header name (provided the name does not contain an underscore) and assign it a custom value. This action overwrites the variable's default behavior.</div>



|**Field name** |**Description** |**Example value** |
|---|---|---|
|uri |Indicates the URI requested by the client. If the URI itself contains query parameters, the question mark (?) is removed along with the query parameters.<br><br>It should be noted that CDN may modify the value of this field when processing the request. It is not recommended to use this field. Please use raw_uri instead. |`/dir/sample.php` |
|raw_uri |Indicates the URI of the original client request. The field value will not be modified. If the URI itself contains query parameters, the question mark (?) is removed along with the query parameters. |`/dir/sample.php` |
|request_uri |Indicates the URI requested by the client. The field value will not be modified. If the URI itself contains query parameters, keep the question mark (?) along with the query parameters. |`/dir/sample.php?color=red&n=10` |
|remote_addr |Indicates the IP address of the client sending the request. |`10.10.10.10` |
|remote_port |Indicates the port number used by the client request. |`443` |
|host |Indicates the value of the host field in the client request header.<br><br>It should be noted that CDN may modify the value of this field when processing the request. It is not recommended to use this field. Please use http_host instead. |`www.example.com:8080` |
|http_host |Indicates the value of the host field in the original client request header. The field value will not be modified. | |
|args |Indicates the parameters part of the client request URI, but does not contain the question mark (?) preceding the query parameters. |`color=red&n=10` |
|msec |Indicates the time at which the client request was sent. The format is a decimal Unix timestamp. |`1650558396` |
|scheme |Indicates the protocol used when the client request is sent. |`https` |


<span id="5d3bdbdc"></span>
## Common fields

You can select frequently used fields from the list to set. Descriptions of these commonly used fields follow:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">These fields are standard HTTP response headers. If the value of the response header is valid, the browser will handle it accordingly. You can also use these fields as custom fields, giving them arbitrary values. For example, you might want to set Access\-Control\-Allow\-Origin to <code>helloworld</code> for special purposes.</div>



|**Field name** |**Description** |**Example** |
|---|---|---|
|Access\-Control\-Allow\-Origin |Specifies the sites that can be accessed by cross\-domain requests, and supports wildcard domain names. Multiple sites are separated by commas (,). |`https://www.another-site.com` |
|Access\-Control\-Allow\-Methods |Specifies the HTTP request methods that can be used for cross\-origin requests. Multiple methods are separated by commas (,). |`GET` |
|Access\-Control\-Allow\-Headers |Specifies the HTTP request headers that cross\-origin requests can include. Multiple request headers are separated by commas (,). |`X-Custom-Header` |
|Access\-Control\-Expose\-Headers |Specifies which response headers are accessible to clients in CDN responses. By default, the response headers that the client can access are `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, and `Last-Modified`. |`Content-Encoding`. If you need the client to access more response headers, you can specify them in this field. Multiple response headers are separated by commas (,). |
|Access\-Control\-Allow\-Credentials |Specifies whether cross\-origin requests need to include authentication information. Authentication information includes cookies, authentication request headers or client TLS certificates. |`true` |
|Access\-Control\-Max\-Age |When specifying a cross\-domain request, the cache time of the preflight request initiated by the client for the request content. The unit is seconds. During the cache time, the client does not need to send the preflight request again. |`3600` |
|Cache\-Control |For content returned by CDN, specifies how the content is cached on the client side. |`max-age=3600` |
|Content\-Disposition |Indicates that the content returned by the CDN to the client is provided as a download and specifies the downloaded file name. |`attachment;filename=Demo.xlsx` |
|Content\-Language |Indicates the language of the content returned by the CDN to the client. |`zh-CN` |
|Content\-Type |Indicates the type of content returned by the CDN to the client. |`text/plain` |
|Pragma |For HTTP/1.0, indicates how the content returned by the CDN should be cached on the client side. The field value can only be `no-cache`, which means no cache. |`no-cache` |


<span id="aec6a4d5"></span>
## Precautions

When you set the fields, the following fields cannot be used, otherwise an error will be reported. Field names are not case sensitive.


* access\-check

* server\-timing

* via

* x\-request\-ip

* x\-tt\-trace\-tag

* x\-bdcdn\-logid

* byte\-error\-code

* x\-bdcdn\-cache\-status


If you enter any of these field names, you will receive the `The header is invalid` error.

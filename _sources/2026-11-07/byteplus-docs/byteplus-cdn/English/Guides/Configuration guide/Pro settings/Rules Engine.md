---
title: "Rules Engine"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/rules-engine_en"
---

<span id="472b54d3"></span>
## Rules Engine overview

The BytePlus CDN Rules Engine enables you to customize request processing. By configuring a set of Match Conditions and Actions, you can control how the CDN responds to user requests. For example, you can customize caching policies, rewrite request URLs, control access, and manipulate request and response headers. This topic describes the core concepts, processing workflow, configuration precedence, and specific configuration items of the Rules Engine, and provides examples to help you get started quickly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Not all CDN features can be configured in the Rules Engine. For example, <strong>Origin Request Parameters</strong> and <strong>Multi\-range</strong> can be configured only in <strong>Delivery Policy</strong>. For CDN features supported by the Rules Engine, see <a href="https://docs.byteplus.com/en/docs/18/40500#actions">Actions</a>.</div>


<span id="c1b4adaf"></span>
### Core concepts

The Rules Engine includes the following core concepts:


* **Rules Engine Policy**: In the Rules Engine, Rules are defined in Rules Engine Policies. Each policy contains one Rule. You can create up to 201 policies. By associating a policy with a domain name, the Rule in the policy is applied to that domain name. One policy can be associated with multiple domain names, while each domain name can be associated with only one Rules Engine Policy.

* **Rule**: A Rule is the basic unit of Rules Engine configuration and defines how CDN processes a particular type of request. Each Rule contains a conditional expression with an `IF...ELSE...` structure.

* **Subrule**: A Subrule is nested under the `IF` or `ELSE` branch of a parent Rule to implement more granular logic control. When a request meets the condition of a parent Rule, CDN continues to process the Subrules under that parent Rule after executing the Actions defined in the parent Rule. A Rule can contain a total of up to 10 Subrules across its `IF` and `ELSE` branches. Subrules cannot be nested further.

* **Conditional expression**: A conditional expression is the core of a Rule. It defines the logic for matching user requests and the Actions that CDN needs to execute. A conditional expression consists of `IF` and `ELSE` parts. If a request meets the condition defined in `IF`, CDN executes the Actions under `IF`; otherwise, it executes the Actions under `ELSE`.

* **Match Condition**: A Match Condition defines the matching logic of an `IF` statement. You can create one or more Match Conditions and define their logical relationship. The logical relationships are **And** and **Or**. Match Conditions include the following types:

   * **Single condition**: Consists of a match type, operator, and match value.

   * **Condition group**: Contains multiple single conditions and the logical relationship between them.

* **Action**: An Action is a specific operation that CDN performs after a request meets the Match Conditions, such as redirecting a URL or modifying an HTTP response header.


The following figure shows the relationships among these concepts:

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260910090449-467484752443.png) </span>

<span id="28411819"></span>
## Rule evaluation logic and precedence

<span id="rule-execution-logic"></span>
### Rule execution logic

CDN processes Rules and their Subrules using the following logic:


* **A single Subrule**: Follows `IF...ELSE...` logic. If the request meets the `IF` condition, CDN executes the Actions under `IF`; otherwise, it executes the Actions under `ELSE`.

* **A single Rule**:

   * **A Rule without Subrules**: Directly follows `IF...ELSE...` logic.

   * **A Rule with Subrules**:

      * If the request meets the outer `IF` condition, CDN first executes the Actions under the outer `IF`, then processes all Subrules under that outer `IF` in sequence.

      * If the request does not meet the outer `IF` condition, CDN first executes the Actions under the outer `ELSE`, then processes all Subrules under that outer `ELSE` in sequence.


<span id="82dff350"></span>
## Action execution stages

The Rules Engine processes requests across the following five stages (as shown in the figure). Each Action that you define in the Rules Engine is executed in one of these five stages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e57fac536284f3bba701414e119c5bb~tplv-goo7wpa0wc-image.image) </span>

The Rules Engine primarily matches requests at the following two stages:


* **User request received**

* **Origin response received**


Each Action has an execution stage. The following table summarizes the mappings among match types, Actions, and Action execution stages:


| |**Available match types** |**Available Actions** |**Action execution stage** |
|---|---|---|---|
|User request |* Request path<br><br>* URL (excluding protocol and host)<br><br>* Full URL<br><br>* Request parameter<br><br>* Referer request header<br><br>* Client IP<br><br>* Origin request header<br><br>* UA request header<br><br>* HTTP request header<br><br>* Client region<br><br>* Request method<br><br>* Request time<br><br>* Request protocol<br><br>* Client certificate information |* URL Redirect<br><br>* Allow access<br><br>* Protocol Redirect<br><br>* Data Rate Limiting<br><br>* Client request header settings<br><br>* Deny access<br><br>* Signed URL Authentication |Client request |
|||* Range GET<br><br>* Redirect Follow<br><br>* Origin TCP timeout<br><br>* Origin HTTP timeout<br><br>* Origin URL Rewrite<br><br>* Origin SNI<br><br>* Origin Protocol<br><br>* Origin Request Headers<br><br>* Origin Host |Origin request |
|||* Cache Key<br><br>* File Compression<br><br>* Video Seeking<br><br>* Caching Rules |CDN cache |
|||* Client Response Headers<br><br>* Browser Caching<br><br>* HTTP status code rewrite<br><br>* Custom Error Pages |Client response |
|Origin response |* HTTP response header<br><br>* HTTP response status code |* Client Response Headers<br><br>* Browser Caching<br><br>* HTTP status code rewrite<br><br>* Custom Error Pages |Client response |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To use the <strong>Client certificate information</strong> condition, Mutual TLS must be enabled for the domain name. See <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us">Mutual TLS</a>.</div>


* <div data-tips="true" data-tips-type="tip">When a Rule includes a <strong>Client certificate information</strong> condition, you cannot specify the following Actions:</div>


   * <div data-tips="true" data-tips-type="tip">Actions in the <strong>CDN cache</strong> stage.</div>


   * <div data-tips="true" data-tips-type="tip">Actions in the <strong>Origin request</strong> stage.</div>


   * <div data-tips="true" data-tips-type="tip">The <strong>Signed URL Authentication</strong> Action in the <strong>Client request</strong> stage.</div>


* <div data-tips="true" data-tips-type="tip">If any Match Condition uses the <strong>Is in Universal Catalog</strong> or <strong>Is not in Universal Catalog</strong> operator, you can specify only Actions in the <strong>Client request</strong> and <strong>Client response</strong> stages.</div>



<span id="42bb5353"></span>
## Configuration precedence

<span id="5831fbe8"></span>
### Precedence of identical Actions

CDN processes Rules and Subrules from top to bottom and from outer to inner. When the same Action is configured in multiple Rules or Subrules, **the configuration of the last Action executed takes effect**; that is, a configuration lower in the rule list or nested more deeply overrides a configuration higher in the list or in an outer rule.

**Example**:

Assume that your Rule configuration is as follows:


* **Parent Rule condition**: Request path \- Suffix match \- `php`, `asp`, `jsp`, `html` (Ignore case)

* **Parent Rule Action**: Client Response Headers \- Delete `param_a`; set `param_c` to `value_1`

* **Subrule condition**: Request path \- Prefix match \- `/docs/` (Ignore case)

* **Subrule Action**: Client Response Headers \- Delete `param_b`; set `param_c` to `value_2`


When CDN receives a request for `/docs/3.php` and the origin response includes the `param_a`, `param_b`, and `param_c` response headers, the response ultimately received by the client does not include `param_a` or `param_b`, but includes `param_c`, whose value is set to `value_2`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6317672bfe20434ab7ccf7575609a78a~tplv-goo7wpa0wc-topic.webp) </span>

<span id="b744bb7f"></span>
### Precedence between the Rules Engine and Delivery Policy

If you configure the same CDN feature in both the Rules Engine and **Delivery Policy**, **the Rules Engine has higher precedence**. When the two conflict, the system prioritizes the Action setting in the Rules Engine.

For the **Allow access** Action, you need to specify the effective scope. After you do so, access control rules within that scope no longer block requests that meet the Rules Engine conditions; other requests that do not meet the conditions are still processed according to the corresponding access control rules.

For example, in Delivery Policy, you configure a Referer denylist for `www.example.com`, and in the Rules Engine, you configure **Allow access** for request paths with the `.txt` suffix, with the effective scope set to **Referer rule**. In this case, if a user's request has the `Referer` header `https://www.example.com/page.html` and the request path is `/3.txt`, the request is allowed. If the user's request has the same `Referer` header but the request path is `/3.html`, the request is still blocked by the Referer denylist.

**Precedence example**:

Assume that you want to set the HTTP timeout for origin requests for `.php` files to 10 seconds and for other files to 5 seconds. You can configure the following:


* **Rules Engine configuration**:

   * **Condition**: Request path \- Suffix match \- `.php` (Ignore case)

   * **Action**: Origin HTTP timeout \- `10 seconds`

* **Delivery Policy (Origin configuration)** :

   * **HTTP timeout**: `5 seconds`


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc9650f84c792ec6ddf686b960f04837.png) </span>

<span id="conditions"></span>
## Conditions

In the Rules Engine, Match Conditions define the Rule logic for intercepting and processing client requests. This topic lists all match types supported by the Rules Engine and their configuration instructions.

<span id="fd6db647"></span>
### Conditions

The following table lists all available match types and their descriptions.


|Match type |Description |Available operators |Ignore case |
|---|---|---|---|
|**All (any request)**  |Takes effect for any user request. |N/A |N/A |
|**Request path** |The path in the user request URL, excluding the query string. |Equals, Does not equal, Prefix match, Prefix does not match, Suffix match, Suffix does not match, Regex match, Regex does not match, Is in Universal Catalog, Is not in Universal Catalog |Supported |
|**URL (excluding protocol and host)**  |The path and query string in the user request URL. |||
|**Full URL** |The full user request URL. |||
|**Request parameter** |The query parameters in the user request URL. |Equals, Does not equal, Exists, Does not exist, Regex match, Regex does not match, Is in Universal Catalog, Is not in Universal Catalog ||
|**Origin request header** |The `Origin` header in the user request. |||
|**Referer request header** |The `Referer` header in the user request. |||
|**UA request header** |The `User-Agent` header in the user request. |||
|**HTTP request header** |A specified header in the user request. |||
|**HTTP response header** |A specified header in the response that CDN returns for the user request. |||
|**Client IP** |The client IP address that sends the user request. |Matches, Does not match, Is in Universal Catalog, Is not in Universal Catalog |N/A |
|**Request time** |The time at which CDN receives the user request. The options are daily, weekly, or a specific time period. A specific time period is accurate to the second. |Matches, Does not match |N/A |
|**Client region** |The country or region of the client IP address. |||
|**HTTP response status code** |The HTTP status code with which CDN responds to the user request. |||
|**Request method** |The HTTP method used by the user request. |Equals, Does not equal ||
|**Request protocol** |The protocol used by the user request, which can be HTTP or HTTPS. |||
|**Client certificate information** |A specified field in the client certificate, used to match certificate content in Mutual TLS scenarios. The supported fields are:<br><br><br>* CN (Common Name)<br><br>* SN (Serial Number)<br><br>* C (Country)<br><br>* L (City/Locality)<br><br>* O (Organization/Company)<br><br>* OU (Department/Organizational Unit)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To use the <strong>Client certificate information</strong> condition, Mutual TLS must be enabled for the domain name. See <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/mtls_en-us">Mutual TLS</a>.</div><br> |Matches, Does not match |Supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Operators requiring additional explanation</strong>:</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Equals/Does not equal</strong>: Performs an exact string match.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Prefix/Suffix match</strong>: Determines whether a string starts with the specified prefix or ends with the specified suffix.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Regex match</strong>: Determines whether a string matches the specified regular expression. For example, for the string <code>abc123a45</code>, the regular expression <code>[0-9]{1,}a{1,3}</code> matches <code>123a</code>, and is therefore considered a successful match. To use <strong>Regex match</strong>, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Is in Universal Catalog</strong>: Determines whether a string belongs to the specified global configuration. See <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/global-catalog_en">Universal catalog</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Logic for multiple match values</strong>:</div>


   * <div data-tips="true" data-tips-type="tip">For <strong>Equals</strong>, <strong>Prefix match</strong>, <strong>Suffix match</strong>, and <strong>Regex match</strong>, the relationship between multiple match values is OR.</div>


   * <div data-tips="true" data-tips-type="tip">For <strong>Does not equal</strong>, <strong>Prefix does not match</strong>, <strong>Suffix does not match</strong>, and <strong>Regex does not match</strong>, the relationship between multiple match values is AND.</div>



<span id="698fbc21"></span>
### Appendix: match value input requirements


|Match type |Input requirements |
|---|---|
|**Request path** |* Starts with `/`<br><br>* No more than 300 characters in length<br><br>* Cannot contain `%` or spaces<br><br>* Up to 100 values, separated by line breaks |
|**URL (excluding protocol and host)**  |* Starts with `/`<br><br>* No more than 300 characters in length<br><br>* Cannot contain `%` or spaces<br><br>* Up to 100 values, separated by line breaks |
|**Full URL** |* Starts with `http://` or `https://`<br><br>* No more than 300 characters in length<br><br>* Cannot contain `%` or spaces<br><br>* Up to 100 values, separated by line breaks |
|**Request parameter** |* Name is no more than 30 characters<br><br>* Each value is no more than 100 characters and cannot contain `%` or spaces<br><br>* Up to 100 values, separated by line breaks |
|**Origin request header** |* Each header value is no more than 200 characters<br><br>* Up to 100 values, separated by line breaks |
|**Referer request header** |* Each header value is no more than 200 characters<br><br>* Up to 100 values, separated by line breaks |
|**UA request header** |* Each header value is no more than 200 characters<br><br>* Up to 100 values, separated by line breaks |
|**HTTP request header** |* Name is no more than 100 characters<br><br>* Each value is no more than 200 characters<br><br>* Up to 100 values, separated by line breaks |
|**HTTP response header** |* Name is no more than 100 characters<br><br>* Each value is no more than 200 characters<br><br>* Up to 100 values, separated by line breaks |
|**Client IP** |* Supports IPv4, IPv6, and CIDR formats<br><br>* Up to 100 values, separated by line breaks |
|**Client certificate information** |* Each match value is no more than 64 characters<br><br>* Up to 100 values, separated by line breaks<br><br>* Supports exact matching and wildcard matching with `*` as a prefix (for example, `*value`, which indicates a value ending in `value`) or suffix (for example, `value*`, which indicates a value beginning with `value`)<br><br>* Does not support using `*` at both the beginning and the end (for example, `*value*`) |


<span id="actions"></span>
## Actions

In the Rules Engine, CDN performs the corresponding action when a client request or origin response meets the Match Conditions that you specify. This topic describes all Action types supported by the Rules Engine, their execution stages, and how to configure them.

The following table lists all available Actions, their execution stages, and configuration instructions.


|**Action** |**Action execution stage** |**Configuration instructions** |
|---|---|---|
|URL Redirect |Client request |[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-url-redirect). In the Rules Engine, you can also set up to 10 query parameters and their values. Configure query parameters as `k=v` key\-value pairs. `k` cannot exceed 30 characters, and `v` cannot exceed 100 characters. `v` can include the variables listed in [Variables](https://docs.byteplus.com/en/docs/18/40500#variables) at the end of this topic. The query parameters that you set are retained in the rewritten path. |
|Allow access ||Allows requests that meet the conditions to access CDN. You need to specify the effective scope for this Action. After you do so, access control rules within that scope no longer block requests that meet the Rules Engine conditions. |
|Protocol Redirect ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-protocol-redirect_1) |
|Data Rate Limiting ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-data-rate-throttling) |
|Client request header settings ||Before CDN processes a client request, you can add, modify, or delete HTTP headers in the request. |
|Deny access ||Prevents requests that meet the conditions from accessing CDN. You also need to specify the CDN response status code when access is denied, in the range 100\-999. |
|Signed URL Authentication ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview). In the Rules Engine, you can configure **M3U8 rewrite** for each authentication type. |
|Cache Key |CDN cache |See [Cache Key](https://docs.byteplus.com/en/docs/18/40500#cache-key). |
|File Compression ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-file-compression) |
|Video Seeking ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-video-seeking) |
|Caching Rules ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules) |
|Client Response Headers |Client response |[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers) |
|Browser Caching ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-browser-caching) |
|HTTP status code rewrite ||Specifies the CDN response status code, in the range 100\-999. |
|Custom Error Pages ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-custom-error-pages_1) |
|Range GET |Origin request |[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-range-get) |
|Redirect Follow ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-redirect-follow) |
|Origin TCP timeout ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out) |
|Origin HTTP timeout ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-request-time-out) |
|Origin URL Rewrite ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1). |
|Origin SNI ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-sni_1). |
|Origin Protocol ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-protocol_en-us). |
|Origin Request Headers ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers). |
|Origin Host ||[See documentation](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-hostname_en-us). |


<span id="7f6052be"></span>
### Cache Key

In CDN, you can configure cache keys in either of the following ways:


* **Standard method**: On the domain configuration page, you can create a cache key rule and specify which query parameters are included in the cache key. For more information, see [Cache Key](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cache-keys).

* **Rules Engine**: You can also configure cache keys in the Rules Engine. The Rules Engine provides additional configuration options. In addition to query parameters, you can:

   * Set which request headers are included in the cache key.

   * Set which Cookies are included in the cache key.

   * Rewrite the file path in the cache key.

   * Specify whether the file path in the cache key is case\-sensitive.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, the cache key includes all query parameters, but does not include any cookies or request headers.</div>


The following describes cache key configuration in the Rules Engine.


|**Configuration** |**Description** |
|---|---|
|Query string |Specifies which query parameters in the request URL are included in the cache key. This setting has the following options:<br><br><br>* **Keep specified parameters**: Retains the specified parameters. Input requirements:<br><br>   * You can specify up to 30 parameters, separated by line breaks. Parameter names can contain letters, digits, underscores (_), hyphens (\-), and commas (,). Each query parameter cannot exceed 30 characters.<br><br>* **Remove specified parameters**: Retains all parameters except the specified parameters. The input requirements are the same as for **Keep specified parameters**.<br><br>* **Keep all parameters**: Retains all parameters.<br><br>* **Remove all parameters**: Does not retain any parameters.<br><br><br>You can also specify whether parameter names are case\-sensitive. For example, suppose that the parameter you choose to retain is `Header` and you do not select **Ignore case**. In this case, CDN treats `http://www.example.com/file?header=value` and `http://www.example.com/file?Header=value` as different files. |
|Request path |Rewrites the file path in the cache key. You need to specify the **Path before rewrite** and **Path after rewrite**. **Path before rewrite** is a regular expression.<br><br>&nbsp;<br><br>The path must start with `/` and cannot exceed 300 characters.<br><br>&nbsp;<br><br>See the path rewrite example below. |
|HTTP request header |Specifies which request headers are included in the cache key. Header names are case\-insensitive. You can specify up to 30 headers, separated by line breaks. Header names can contain letters, digits, underscores (_), and hyphens (\-). Each specified header name must be no more than 100 characters long.<br><br>&nbsp;<br><br>The order of the specified request headers affects cache matching. For example, if the cache key specifies the header list `header1, header2`, but CDN receives a request with the header list `header2, header1`, the request cannot match the cache.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, the cache key does not include any request headers.</div><br> |
|Cookie |Specifies the cookies included in the cache key. Specify the keys of the cookies to retain. This setting has the following options:<br><br><br>* **Keep specified key\-value pairs**: Retains the specified Cookies. Input requirements:<br><br>   * You can specify up to 30 Cookies, separated by line breaks. Key names can contain letters, digits, underscores (_), hyphens (\-), and commas (,). Each Cookie cannot exceed 30 characters.<br><br>* **Remove specified key\-value pairs**: Retains all Cookies except the specified Cookies. The input requirements are the same as for **Keep specified key\-value pairs**.<br><br>* **Keep all key\-value pairs**: Retains all Cookies.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, the cache key does not include any Cookies.</div><br> |
|Ignore case for cache path |Specifies whether the file path in the cache key is case\-sensitive. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6dc366885bddc5911d173b87f18e746.png) </span>

<span id="da7d1bd2"></span>
#### Path rewrite example in a cache key

**Configuration**


* Path before rewrite: ^/a{1,2}(.\*)g$

* Path after rewrite: /food$1g


**Rewrite examples**


* /a/bbb/image.png is rewritten to /food/bbb/image.png

* /c/a/bbb/image.png is not rewritten


<span id="8ecb5715"></span>
### Variables

In the following action configurations, you can use variables to retrieve values from specific request attributes. Reference a variable in a parameter value by using the `${variable}` format. For example, set the value of an HTTP response header to `my ${request_uri} is ${host}`.

&nbsp;

**Client Response Headers**

See [the list of variables supported by Client Response Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers).

&nbsp;

**Origin Request Headers**

See [the list of supported variables](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers).

&nbsp;

**Client request header settings**

The variables provided by CDN are listed below.


|Variable name |Description |Example |
|---|---|---|
|request_uri |The path and query string in the client request URL. |`/dir/shoppinglist.php?color=red&n=10` |
|raw_uri |The path in the client request URL. |`/dir/volcano.php` |
|host |The value of the host header in the client request. Note that CDN might modify the value of the `host` header when processing a request. Therefore, we recommend using the `http_host` variable instead of the `host` variable. |`www.example.com:8080` |
|http_host |The value of the host header in the client request. CDN does not modify this header value. |`www.example.com:8080` |
|args |The query string in the client request URL. |`color=red&n=10` |
|query_string |Has the same meaning as `args`. |`color=red&n=10` |
|scheme |The protocol used by the client. |`https` |
|remote_addr |The IP address of the client that initiated this request. |`203.0.113.4` |
|http_%s |The value of a specific header, where `%s` is the header name. For example, `http_hello` represents the value of the `hello` header. |`http_hello` |
|arg_%s |The value of a specific query parameter, where `%s` is the query parameter name. For example, `arg_size` represents the value of the `size` query parameter. |`arg_size` |


<span id="best-practices"></span>
## Best practices

The Rules Engine provides flexible configuration capabilities. The following are common application scenarios and configuration examples:

<span id="0efcd768"></span>
### Allow or deny specific client requests

Create allowlists and denylists based on the characteristics of client requests, such as request headers, client IP addresses, request URLs, and client regions, and specify the CDN response status code.

**Configuration example**:


* **Conditions** (Or):

   * Request path \- Equals \- `/test/` (Ignore case)

   * Request parameter \- `myParam` \- Exists

   * Referer request header \- Equals \- `http://www.example.com/` (Ignore case)

   * Client IP \- Matches \- `198.51.100.25`

   * UA request header \- Regex match \- `.*test.*` (Ignore case)

* **Action**: Deny access \- HTTP status code `403`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90cd5fc06e184b8a8db9d0f8d2259a32~tplv-goo7wpa0wc-topic.webp) </span>

<span id="75846eb7"></span>
### Set a caching policy

Set different cache durations based on the characteristics of client requests, such as request headers, request URLs, and client regions.

**Configuration example**:


* **Conditions** (And):

   * Request path \- Equals \- `/test/` (Ignore case)

   * Request parameter \- `myParam` \- Exists

   * Referer request header \- Equals \- `http://www.example.com/` (Ignore case)

   * Client IP \- Matches \- `198.51.100.25`

   * UA request header \- Regex match \- `.*test.*` (Ignore case)

* **Action**: Caching Rules \- Caching policy `CDN cache`, Force cache `false`, Cache duration `30 seconds`, Do not cache Set\-Cookie `false`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d27494bdb7a8442ea5abf68c5b2ba7e2~tplv-goo7wpa0wc-topic.webp) </span>

You can also address specific caching requirements. For example, you can configure CDN to respond directly to `OPTIONS` requests with status code `200`.

**Configuration example**:


* **Condition**: Request method \- Equals \- `OPTIONS`

* **Action**: Deny access \- HTTP status code `200`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/482cb39445ce47668ef33ec54eae8ce8~tplv-goo7wpa0wc-topic.webp) </span>

<span id="f78f1904"></span>
### Throttle specific client requests

Throttle requests based on client request characteristics, such as parameters in the request URL and the client region.

**Configuration example**:


* **Condition**: Request parameter \- `myParam` \- Exists

* **Action**: Data Rate Throttling \- Rate limit `300 B/s`, Unlimited portion `10 KB`


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260910071628-18072350399.png) </span>

<span id="d4eb2c61"></span>
### Configure validation rules for cross\-origin requests

You can implement complex cross\-origin resource sharing (CORS) policies. For example, in addition to standard HTTP/HTTPS requests, you can allow cross\-origin requests from WeChat Mini Programs and dynamically set the `Access-Control-Allow-Origin` response header based on the `Origin` header in the request.

**Configuration example**:


* **Parent Rule condition**: Entire site (using the wildcard `*`)

* **Parent Rule Action**: Client Response Headers \- Delete `Access-Control-Allow-Origin`

* **Subrule condition**: Origin request header \- Regex match \- `^weapp://www.example.com`, `^http://img.example.com.com` (Ignore case)

* **Subrule Action**: Client Response Headers \- Set response header name to `Access-Control-Allow-Origin`, and response header value to `${http_origin}`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a52a886da2f46b8b0ecbef3ec0fa15c~tplv-goo7wpa0wc-topic.webp) </span>

<span id="308d1e9f"></span>
### Modify the Content\-Disposition response header

You can customize the filename displayed when a browser downloads a file and prevent the file from being hijacked during download.

To do this, you can pass the file's actual name through a query parameter, request header, or Cookie named `filename`, and then set the `Content-Disposition` response header to `attachment;filename="${arg_filename}";filename*=utf-8''${arg_filename}`.

**Configuration example**:


* **Condition**: Request parameter \- `filename` \- Exists

* **Action**: Client Response Headers \- Set response header name to `Content-Disposition`, and response header value to `attachment;filename="${arg_filename}";filename*=utf-8''${arg_filename}`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In this example, the actual filename is passed through a query parameter.</div>


* <div data-tips="true" data-tips-type="tip">The <code>filename*=utf-8''${arg_filename}</code> format follows <a href="https://datatracker.ietf.org/doc/html/rfc5987">RFC 5987</a>.</div>


* <div data-tips="true" data-tips-type="tip"><code>filename="${arg_filename}";</code> is for compatibility with some legacy browsers that do not support RFC 5987. Note that the downloaded filename might display as garbled text in those legacy browsers.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0abba297cc054acb994e7c15535a8956~tplv-goo7wpa0wc-topic.webp) </span>

<span id="37a742ad"></span>
### Hide origin response headers based on cache hit status

To improve the security of the origin server and prevent attackers from discovering its internal architecture by probing response headers, you might need to filter specific headers returned by the origin on a cache miss.

Because the Rules Engine can identify the cache marker `X-Response-Cache`, which CDN generates by default, you can configure the Rules Engine to delete sensitive headers that expose the backend technology stack, such as `Server: nginx/1.18.0` or `X-Powered-By: PHP/7.4`, when it detects a cache miss (that is, `miss`).


* **Condition**: HTTP response header \- `X-Response-Cache` \- Equals \- `miss` (Ignore case)

* **Action 1**: Client Response Headers \- Delete response header `Server`

* **Action 2**: Client Response Headers \- Delete response header `X-Powered-By`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72d77b7176234b7cb23d8cbc19c42714~tplv-goo7wpa0wc-topic.webp) </span>

<span id="5c8d8313"></span>
### Customize response headers for cache hit status and response time

To standardize internal company logging and troubleshooting practices, you might want to hide the long default CDN header `X-Response-Cache`, define a response header dedicated to indicating cache hit status (such as `X-Cache: HIT`), and record the request's response time at a CDN edge point of presence so that clients or frontend monitoring SDKs can collect performance data.

You can implement this set of response header control logic by checking the value of `X-Response-Cache`.


* **Condition**: HTTP response header \- `X-Response-Cache` \- Equals \- `edge_hit` (Ignore case)

* **Action 1**: Client Response Headers \- Delete response header `X-Response-Cache`

* **Action 2**: Client Response Headers \- Set response header name to `X-Cache`, and response header value to `HIT`

* **Action 3**: Client Response Headers \- Set response header name to `X-Edge-Response-Time`, and response header value to `${response_time}ms`


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260910071353-183153001062.png) </span>

<span id="fa183c95"></span>
### Customize response pages and status codes for blocked requests

When a client request is blocked due to access control configuration, rate limiting, or other reasons, CDN adds the `X-Exception-Info` response header to the HTTP response by default to indicate the exception reason. For the specific response information corresponding to each exception type, see the **Common ** **`X-Exception-Info`** ** response information** list below.

By matching these response headers in the Rules Engine, you can use the **HTTP status code rewrite** or **Custom Error Pages** Action to handle blocked requests in a user\-friendly way. Common scenarios include:


* **Scenario 1: Redirect to a custom page when a request is rate\-limited.**  When a data rate throttling rule is triggered, you can identify the `X-Exception-Info: rate limit by download speed limit` response header and use the **Custom Error Pages** Action to redirect the request to a specified notification page (for example, `https://www.example.com/rate-limit.html`).

   **Configuration example**:

   * **Condition**: HTTP response header \- `X-Exception-Info` \- Equals \- `rate limit by download speed limit` (Ignore case)

   * **Action**: Custom Error Pages \- Page type `Custom redirect page`, status code `303`, Location `https://www.example.com/rate-limit.html`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b869ce4c0c3478eac719f7632414ed1~tplv-goo7wpa0wc-topic.webp) </span>

* **Scenario 2: Customize the status code when a request is blocked by the IP denylist.**  When a request matches an IP denylist rule and is blocked, CDN returns a specific status code by default. You can identify the `X-Exception-Info: deny by ip access rule` response header and use the **HTTP status code rewrite** Action to change it to the status code required by your business (for example, `404` or `450`).

   **Configuration example**:

   * **Condition**: HTTP response header \- `X-Exception-Info` \- Equals \- `deny by ip access rule` (Ignore case)

   * **Action**: HTTP status code rewrite \- Status code `450`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df11b765c2434e51a915002864baf7fe~tplv-goo7wpa0wc-topic.webp) </span>


**Reference: Common ** **`X-Exception-Info`** ** response information**


|**Exception type** |**`X-Exception-Info`** ** response information** |
|---|---|
|Geographic access control |deny by area access rule |
|Disabled HTTP Method |deny by method rule |
|IP allowlist/denylist |deny by ip access rule |
|Referer allowlist/denylist |deny by referer access rule |
|UA allowlist/denylist |deny by ua access rule |
|Origin allowlist/denylist |deny by origin access rule |
|Custom header allowlist/denylist |deny by customiza access rule |
|Custom blocking rule |deny by request block rule |
|Signed URL Authentication |deny by url auth |
|Remote authentication |deny by remote url auth |
|Data Rate Throttling |rate limit by download speed limit |
|Data Rate Throttling (Rules Engine) |rate limit by rule engine |
|Deny access (Rules Engine) |deny by rule engine |
|Flow detection \- rate limiting |rate limit by flow detection |
|Flow detection \- blocking |deny by flow detection |
|Flow detection (high\-risk IP intelligence database) |deny by flow detection (high risk IP) |

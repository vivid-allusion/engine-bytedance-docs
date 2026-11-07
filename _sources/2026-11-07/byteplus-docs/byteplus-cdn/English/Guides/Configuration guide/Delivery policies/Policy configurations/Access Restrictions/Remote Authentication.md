---
title: "Remote Authentication"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-remote-authentication_1"
---

If your site has a dedicated authentication server, you can integrate it with BytePlus CDN to manage user access. This feature forwards user requests to your server for validation before delivering content. This guide provides step\-by\-step instructions on how to configure authentication rules, server endpoints, and result handling to implement your custom access control logic.

<span id="overview-of-remote-authentication"></span>
## Overview of Remote Authentication

If your site has a dedicated authentication server for authenticating user requests, you can configure remote authentication in the CDN.

The remote authentication process is as follows:


1. Users send requests to your site, containing an authentication parameter.

2. Upon receiving user requests, the CDN forwards the requests to the authentication server.

3. The authentication server authenticates the user requests and returns the authentication results to the CDN.

4. The CDN, based on the authentication results, sends the requested content to the user or denies the request.


<span id="difference-between-remote-authentication-and-url-authentication"></span>
## Difference Between Remote Authentication and URL Authentication

URL Authentication: Authentication is performed by the CDN.

Remote Authentication: Authentication is performed by the authentication server. The CDN forwards the request to the authentication server to obtain the authentication result.

<span id="steps"></span>
## Steps


1. Open the **Remote Authentication** configuration page. For the operation steps, see [Domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en).

2. Set **Status** to **Enable**.

3. Configure the settings on the following tabs.

   * [Authentication Rules](https://docs.byteplus.com/en/docs/18/6563#authentication-rules)

   * [Authentication Server](https://docs.byteplus.com/en/docs/18/6563#authentication-server)

   * [Authentication Parameters](https://docs.byteplus.com/en/docs/18/6563#authentication-parameters)

   * [Authentication Headers](https://docs.byteplus.com/en/docs/18/6563#authentication-headers)

   * [Authentication Results](https://docs.byteplus.com/en/docs/18/6563#authentication-results)

4. After configuring, click **Save**.


<span id="authentication-rules"></span>
### Authentication Rules

On this tab, you can add one or more rules. You can add a maximum of 50 rules. When the CDN receives a user request, it matches the rules against the request in the order they appear. If a rule matches the request, the request is then sent for remote authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to authenticate all requests, you can add a rule with the following configuration:</div>



* <div data-tips="true" data-tips-type="tip">Set <strong>Condition</strong> to <strong>URL Path Directory</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Set <strong>Patterns</strong> to <strong>/</strong>.</div>



<span id="configuration-description"></span>
#### Configuration Description


|**Configuration** |**Description** |
|---|---|
|Condition |Represents the matching condition of the rule. CDN will send the matched requests to the authentication server for authentication. The configuration has the following options:<br><br><br>* **URL Path Extension**: Indicates that the rule is used to match requests for files ending with a specific suffix.<br><br>* **URL Path Directory**: Indicates that the rule is used to match requests for files under a specific directory path.<br><br>* **URL Path**: Indicates that the rule is used to match requests for specific files. |
|Match Type |Indicates the matching method of the rule. The configuration has the following options:<br><br><br>* **Match**: Indicates that requests matching the rule need to be authenticated.<br><br>* **Not Match**: Indicates that requests not matching the rule need to be authenticated.<br><br><br>Note that if you add multiple rules, they need to have the same matching type. |
|Patterns |Indicates the content of the rule. It cannot exceed 1,024 characters and must not include the following characters:<br><br><br>* Consecutive slashes (//), spaces, dollar signs ($), question marks (?), or Delete (ASCII code 127).<br><br><br>Additionally,<br><br><br>* If the rule type is **URL Path Extension**, the rule content must be one or more file extensions separated by semicolons (;). File extensions do not need to start with a dot (.). For example: `png;txt`.<br><br>* If the rule type is **URL Path Directory**, the rule content must be one or more directory paths separated by semicolons (;). Directory paths must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If the rule type is **URL Path**, the rule content must be one or more file paths separated by semicolons (;). File paths must start with a slash (/) and can include asterisks (\*) to represent one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_84f6210ee03aac504bdc0c8e574b419b.png) </span>

<span id="authentication-server"></span>
### Authentication Server

On this tab, you specify the configuration of the authentication servers.

<span id="configuration-description"></span>
#### Configuration Description


|**Configuration** |**Description** |**Example** |
|---|---|---|
|Server Endpoint (Primary) |Indicates the endpoint of the primary authentication server, the length cannot exceed 100 characters. The endpoint must be in one of the following formats:<br><br><br>* `<scheme>://<domain>`<br><br>* `<scheme>://<ip>`<br><br><br>The value of `<scheme>` is `http` or `https`. The value of `<domain>` must not be `localhost`. The value of `<ip>` shouldn't be `127.0.0.1`. |`https://example.com` |
|Server Endpoint (Secondary) |Indicates the endpoint of the secondary authentication server. The length cannot exceed 100 characters and must meet the same requirements as the primary server endpoint.<br><br>&nbsp;<br><br>**Primary\-secondary switching logic**<br><br>For a single request, if an authentication exception occurs, CDN **will not** send the request to the secondary authentication server. Instead, it will process the user request according to the configuration in the **Authentication Results** tab. For the definition of authentication exceptions, see the description of the **Authentication Exceptions Considered As** configuration at the end of the document.<br><br>&nbsp;<br><br>If authentication exceptions occur **consecutively** 25 times within the current minute, the current IP address of the primary server will be added to the blocklist. Then, for newly received requests:<br><br><br>* If the primary server's domain resolves to multiple IP addresses, CDN will send the request to another IP address. Similarly, if authentication exceptions occur consecutively 25 times within the current minute, that IP address will be added to the blocklist.<br><br>* If all IP addresses are on the blocklist, CDN will send the request to the secondary authentication server.<br><br><br>At the beginning of the next minute, the blocklist will be cleared. For newly received requests, CDN will send requests to the primary authentication server. | |
|Request Path |Indicates the authentication path. The address of the authentication server and this path make up the authentication URL. The CDN forwards user requests to this authentication URL. The configuration has the following options:<br><br><br>* **Match Request**: Indicates the authentication path is the same as the path in the user request URL.<br><br>* **Specified**: Indicates a specified path. You need to specify this path in **Specified Path**. | |
|Specified Path |This configuration appears only if **Authentication Path** is set to **Specified**. Here, you specify an authentication path. The path must start with a slash (/) and cannot exceed 100 characters in length. It can include printable ASCII characters except for the following:<br><br><br>* Consecutive slashes (//), percent signs (%), dollar signs ($), spaces, question marks (?), Delete (ASCII code 127). |`/sign` |
|Request Method |The request method used by the CDN to send the authentication request. The configuration has the following options:<br><br><br>* **Match Request**: The method for the authentication request is the same as the user request.<br><br>* **GET**: The authentication request uses the GET method.<br><br>* **POST**: The authentication request uses the POST method.<br><br>* **HEAD**: The authentication request uses the HEAD method. | |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8e30394ee428a48a2b4448988644270f.png) </span>

<span id="authentication-parameters"></span>
### Authentication Parameters

On this tab, you specify the query parameters to be included in the authentication request.

<span id="configuration-description"></span>
#### Configuration Description


|**Configuration** |**Description** |
|---|---|
|Query Parameters from User Request |Specifies which query parameters from the user request URL are included in the authentication request. The configuration has the following options:<br><br><br>* **Include All**: All query parameters from the user request URL are included in the authentication request.<br><br>* **Include None**: No query parameters from the user request URL are included in the authentication request.<br><br>* **Include Specified**: Only specified query parameters from the user request URL are included in the authentication request. |
|Specified Parameters |This configuration appears if **Query Parameters from User Request** is set to **Include Specified**. It specifies which query parameters from the user request URL need to be included in the authentication request. Multiple parameters are separated by semicolons (;), and the total length cannot exceed 1,024 characters. Parameter names are case\-sensitive and can include printable ASCII characters except for the following:<br><br><br>* Space, double quotes ("), and Delete (ASCII code 127) |
|Additional Parameters |Indicates the additional query parameters that you need to add to the authentication request. You can add up to 50 parameters. |
|Parameter Name |Indicates the name of a query parameter you need to add. The parameter name cannot exceed 1,024 characters in length and can include printable ASCII characters except for the following:<br><br><br>* Double quotes ("), space, and Delete (ASCII code 127) |
|Value Type |Specifies how the value of the query parameter is defined. The configuration has the following options:<br><br><br>* **Literal Value**: The parameter value is a fixed string value.<br><br>* **HTTP Variable**: The parameter value comes from a variable. See the variable description below. |
|Value |The value of the query parameter.<br><br><br>* If **Value Type** is **Literal Value**, you specify a fixed value as the parameter value, which cannot exceed 1,024 characters in length, cannot start with a dollar sign ($), and can include printable ASCII characters except for the following:<br><br>   * Double quotes ("), and Delete (ASCII code 127).<br><br>* If **Value Type** is **HTTP Variable**, you need to select a variable from the list. The value of the selected variable will be set as the parameter value. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_57f4513cdca9423315f182190014ef9f.png) </span>

<span id="variable-description"></span>
#### **Variable Description**

The CDN provides the following variables.


|**Variable** |**Description** |**Example** |
|---|---|---|
|host |The value of the Host header in the user request. |`example.com:8080` |
|ua |The value of the User\-Agent header in the user request. |`Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail` |
|referer |The value of the Referer header in the user request. |`https://www.example.com/file?name=123` |
|content_type |The value of the Content\-Type header in the user request. |`text/html` |
|X\-Forwarded\-For |The value of the X\-Forwarded\-For header in the user request. |`203.0.113.10` |
|client_ip |The IP address from which the user request is sent. |`198.51.100.10` |
|scheme |The scheme used in the user request. |`https` |
|server_protocol |The protocol version used in the user request. |`HTTP/2.0` |
|URI |The URL in the user request, excluding the query string. |`/dir/page.php` |
|req_args |All query parameters in the user request. |`color=red&n=10` |
|request_method |The request method used in the user request. |`GET` |
|request_uri |The URL in the user request, including the query string. |`/dir/page.php?color=red&n=10` |
|local_ip |The IP address of the CDN edge node that responds to the user request. |`192.0.2.45` |
|req_time |The time when the CDN received the user request. For the time format, please see the example. |`18/Apr/2022:16:48:48 +0800` |
|msec |The current time as a Unix timestamp in seconds. |`1650558396` |


<span id="authentication-headers"></span>
### Authentication Headers

On this tab, you specify the request headers that need to be included in the authentication request.

<span id="configuration-description"></span>
#### Configuration Description


|**Configuration** |**Description** |
|---|---|
|Host Header |Indicates the value of the Host header in the authentication request. This configuration has the following options:<br><br><br>* **Domain Name**: Indicates that the value of the Host header is the same as your domain name.<br><br>* **Specified**: Represents a specified value for the Host header. If you choose this option, the **Specified Host** configuration will appear. In this configuration, you need to enter a value for the Host header, which cannot exceed 1,024 characters. |
|Other Headers from User Request |Indicates which headers from the user's request are included in the authentication request. This configuration has the following options:<br><br><br>* **Include All**: Indicates that the authentication request includes all headers from the user's request.<br><br>* **Include None**: Indicates that the authentication request does not include any headers from the user's request.<br><br>* **Include Specified**: Indicates that the authentication request includes only specified headers from the user's request. |
|Specified Headers |This configuration only appears if **Other Headers from User Request** is set to **Include Specified**. It specifies the headers that need to be included in the authentication request. Multiple headers are separated by a semicolon (;). Headers are case\-insensitive. |
|Additional Headers |This configuration indicates the additional request headers that you need to add. You can add up to 50 request headers. |
|Header Name |Represents a request header that you need to add. Headers are case\-insensitive and cannot be `Host`, nor can they exceed 1,024 characters in length. The header can contain printable ASCII characters except for the following:<br><br><br>* Underscore (_), space, double quotes ("), Delete (ASCII code 127) |
|Value Type |Indicates how the value of the request header is defined. This configuration has the following options:<br><br><br>* **Literal Value**: Indicates that the value of the request header is a fixed value, which is a string.<br><br>* **HTTP Variable**: Indicates that the value of the request header comes from a variable. See the variable description above. |
|Value |Represents the value of the request header. The description of this configuration is as follows:<br><br><br>* If **Value Type** is **Literal Value**, you specify a fixed value as the value of the request header. The length of this value cannot exceed 1,024 characters, cannot start with a dollar sign ($), and can contain printable ASCII characters except for the following:<br><br>   * Double quotes ("), Delete (ASCII code 127).<br><br>* If **Value Type** is **HTTP Variable**, you need to select a variable from the list. The value of the variable you choose will be set as the value of the request header. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6a10f41ced5c634e9f53fe0405f587d6.png) </span>

<span id="authentication-results"></span>
### Authentication Results

On this tab, you specify how the CDN handles the authentication results returned from the authentication server.

<span id="configuration-description"></span>
#### Configuration Description


|**Configuration** |**Description** |
|---|---|
|Success Response Code |Indicates which status codes returned by the authentication server are considered successful authentication. The default value is 200.<br><br>You can enter one or more status codes within the range of 200\-299. Multiple status codes are separated by a semicolon (;). You can also enter 2xx to represent any status code within the 200\-299 range. |
|Failure Response Code |Indicates which status codes returned by the authentication server are considered authentication failures. The default value is 401.<br><br>&nbsp;<br><br>You can enter one or more status codes within the range of 400\-499. Multiple status codes are separated by a semicolon (;). You can also enter 4xx to represent any status code within the 400\-499 range. |
|Other Response Codes Considered As |This configuration indicates how the CDN handles user requests when the following conditions are met:<br><br><br>* The status code returned by the authentication server is not one of the specified codes that represent successful authentication.<br><br>* The status code returned by the authentication server is not one of the specified codes that represent authentication failure.<br><br><br>This configuration has the following options:<br><br><br>* **Authentication Success**: Indicates that the CDN considers that authentication is successful and returns the requested file to the user.<br><br>* **Authentication Failure**: Indicates that the CDN considers that authentication failed, denying the user's request. |
|Cache Response? |Specifies whether the CDN caches the authentication results. The authentication result is the authentication status code returned by the authentication server. The default is **No**.<br><br>&nbsp;<br><br>Once this configuration is enabled, for the received user requests, the CDN will check whether the authentication status code has been cached. If the authentication status code is cached, the CDN will use it to determine whether to send the requested file to the user.<br><br>This configuration can improve authentication efficiency. |
|TTL |Indicates the caching time for the authentication status code, in seconds. This configuration only appears when **Cache Response?**  is set to **Yes**. You can enter a value ranging from 1 to 86,400. 86,400 seconds represent 24 hours. |
|Cache Key |Represents the fields included for the cached authentication status code. Each cached authentication status code has a unique cache key. This configuration appears only when **Cache Response?**  is set to **Yes**.<br><br>When a request is received, the CDN attempts to match the request with the cache key of each authentication status code in the cache. If a match is found, the CDN will use the cached authentication status code.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The <strong>Cache Key</strong> must include the <code>URI</code> field, otherwise, the CDN cannot determine the request file corresponding to the cached authentication result.</div><br><br><br>**Example**<br><br>The fields you specify in the cache key are `URI` and `client_ip`. This configuration indicates that the CDN caches the authentication results based on the following objects in the user request:<br><br><br>* The IP address from which the request originated<br><br>* The URL of the request<br><br><br>In this way, for subsequent requests from the same IP address, if the request URL is the same, the CDN will use the cached authentication result. |
|CDN Response Code for Authentication Failure |Indicates the status code with which the CDN responds to the user's request when authentication fails. The default status code is 403.<br><br>You can enter any status code within the range of 400\-499. |
|Authentication Request Time\-out |Indicates the timeout period for the authentication request, in milliseconds, with the default value being 200. You can enter a timeout period ranging from 200 to 3,600. |
|Authentication Exceptions Considered As |This configuration indicates how CDN handles authentication when an authentication exception occurs.<br><br>&nbsp;<br><br>This configuration has the following options:<br><br><br>* **Authentication Success**: Indicates that the CDN considers the user's request authenticated successfully and returns the requested file to the user.<br><br>* **Authentication Failure**: Indicates that the CDN considers the user's request authentication failed, denying the user's request.<br><br><br>Authentication exceptions include, but are not limited to, the following situations:<br><br><br>* The authentication request timed out.<br><br>* The authentication server rejected the authentication request.<br><br>* The CDN could not establish a connection with the authentication server. |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0d1dd845bc891dea6c564fe896c91812.png) </span>

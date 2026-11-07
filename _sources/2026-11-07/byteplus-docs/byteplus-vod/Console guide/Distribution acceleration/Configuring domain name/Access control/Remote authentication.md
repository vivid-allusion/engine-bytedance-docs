---
title: "Remote authentication"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-remote-authentication"
---

This article describes how to configure remote authentication in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Remote authentication applies to <strong>Playback domain name</strong> and <strong>Custom\-origin domain name</strong>.</div>


<span id="9bac51b2"></span>
## What is remote authentication?

If your website has a dedicated authentication server to authenticate user requests, you can configure remote authentication.

The process of remote authentication is as follows:


1. A user sends a request to your website, including authentication parameters.

2. After receiving the user request, the CDN node forwards the request to the authentication server.

3. The authentication server authenticates the user request and returns the authentication result to the CDN node.

4. Based on the authentication result, the CDN node either sends the requested content to the user or rejects the user request.


<span id="10915a46"></span>
## Difference between remote authentication and URL authentication


* URL authentication: The CDN node directly authenticates the request.

* Remote authentication: The CDN node does not authenticate the request directly, but forwards the request and receives the authentication result from the authentication server.


<span id="a1aa02d2"></span>
## Configuring remote authentication


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name** or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Remote authentication**, switch the **Status** toggle and configure the following:

   * [Configuring authentication rules](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#3fbacb6c)

   * [Configuring authentication endpoints](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#d43858bc)

   * [Authentication parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#b5a1d27c)

   * [Authentication headers](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#1494ac99)

   * [Authentication responses](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#7ba1b233)

8. Click **Save**.


<span id="3fbacb6c"></span>
### Authentication rules

You can add up to 50 rules. If a request matches any of the rules, the request needs to be authenticated.


|**Configuration** |**Description** |
|---|---|
|Rule type |Select the type of rule. The available options are:<br><br><br>* **File suffix**: Authentication is required for requests to files with specific suffixes.<br><br>* **File directory**: Authentication is required for requests to files within specified directories.<br><br>* **File full path**: Authentication is required for requests to specific files. |
|Match type |Specify the matching method. The available options are:<br><br><br>* **Match**: Requests that match the rule content will require authentication.<br><br>* **Mismatch**: Requests that do not match the rule content will require authentication.<br><br><br>Note that if you add multiple rules, each rule must be set to the same matching method. |
|Rule |Enter one or more configuration items, separated by semicolons (;). The requirements for configuration items are as follows:<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file suffixes, with a total length of no more than 1,024 characters. File suffixes are case\-sensitive and can include letters and numbers. Multiple suffixes are separated by semicolons (;). For example, `xlsx` or `png;txt`.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths, with a total length of no more than 1,024 characters. Multiple directory paths are separated by semicolons. Directory paths are case\-sensitive. The requirements for directory paths are as follows:<br><br>   * Directory paths must start and end with a forward slash (/). For example, `/www/img/;/www/doc/`. To specify all directories, enter `/`.<br><br>   * Directory paths can include printable ASCII characters, except for the following characters:<br><br>      * Consecutive forward slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127)<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths, with a total length of no more than 1,024 characters. Multiple file paths are separated by semicolons (;). You can use wildcard (\*) in file paths to represent one or more consecutive characters. File paths are case\-sensitive, and the requirements are as follows:<br><br>   * File paths must start with a forward slash (/). For example, `/www/img/picture.png;/doc/study.docx`.<br><br>   * File paths can include printable ASCII characters, except for the following characters:<br><br>      * Consecutive forward slashes (//)<br><br>      * Percent signs (%)<br><br>      * Spaces<br><br>      * Dollar signs ($)<br><br>      * Question marks (?)<br><br>      * Delete (ASCII code 127) |


<span id="d43858bc"></span>
### Authentication endpoints

Specify the configuration of the authentication server.


|**Configuration** |**Description** |**Example** |
|---|---|---|
|Endpoint domain name (primary) |Represents the primary address of the authentication server, with a maximum length of 100 characters. The primary address must be in one of the following formats:<br><br><br>* ://<br><br>* ://<br><br><br>The value ofcan be `http` or `https`. The value ofcannot be `localhost`. The value ofcannot be `127.0.0.1`. |`https://example.com` |
|Endpoint domain name (backup) |Represents the backup address of the authentication server, with a maximum length of 100 characters. The format and input requirements are the same as the primary address. | |
|Authentication path |Represents the path in the authentication URL. The address of the authentication server and this path form the authentication URL. The CDN forwards user requests to this authentication URL. The options for this configuration are as follows:<br><br><br>* **Same as user request path**: The path in the authentication URL is the same as the path in the user request URL.<br><br>* **Specified path**: A specific path is specified. You need to specify this path in the **Specified path**. | |
|Specified path |This configuration appears only if the **Authentication path** is **Specified path**. In this configuration, you specify an authentication path. The authentication path must start with a slash (/) and have a maximum length of 100 characters. The authentication path can contain printable ASCII characters except for the following:<br><br><br>* Consecutive forward slashes (//)<br><br>* Percent signs (%)<br><br>* Spaces<br><br>* Dollar signs ($)<br><br>* Question marks (?)<br><br>* Delete (ASCII code 127) |`/sign` |
|Request method |Represents the request method used by the CDN when sending authentication requests. The options for this configuration are as follows:<br><br><br>* **Same as user request method**: The authentication request uses the same method as the user request.<br><br>* **GET**: The authentication request uses the GET method.<br><br>* **POST**: The authentication request uses the POST method.<br><br>* **HEAD**: The authentication request uses the HEAD method. | |


<span id="b5a1d27c"></span>
### Authentication parameters

Specify the parameters that need to be included in the authentication request.


|**Configuration** |**Description** |
|---|---|
|Request parameters |Represents which query parameters from the user request URL are included in the authentication request. This configuration has the following options:<br><br><br>* **Include all**: The authentication request includes all query parameters from the user request URL.<br><br>* **Include none**: The authentication request does not include any query parameters from the user request URL.<br><br>* **Include specified**: The authentication request includes specified query parameters from the user request URL. |
|Parameter list |This configuration only appears if the **Request Parameters** is **Include Specified**. This configuration represents which query parameters from the user request URL need to be included in the authentication request. Multiple parameters are separated by semicolons (;), and the total length cannot exceed 1,024 characters. The parameter names are case\-sensitive and can include printable ASCII characters, except for the following characters:<br><br><br>* Spaces<br><br>* Double quotes ("")<br><br>* Delete (ASCII code 127) |
|Additional parameters |This configuration represents additional query parameters that you need to add. You can add up to 50 parameters.<br><br><br>* **Name**: Represents the name of a query parameter that you need to add. The parameter name cannot exceed 1,024 characters and can include printable ASCII characters, except for the following characters:<br><br>   * Double quotes ("")<br><br>   * Spaces<br><br>   * Delete (ASCII code 127)<br><br>* **Value type**: Represents how the value of this query parameter is defined. This configuration has the following options:<br><br>   * **Constant**: The parameter value is a fixed value of type string.<br><br>   * **Variable**: The parameter value comes from a variable. See [Variables](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#ba172f40).<br><br>* **Value**: Represents the value of this query parameter. The description of this configuration is as follows:<br><br>   * If the **Value type** is **Constant**, you specify a fixed value as the value of this parameter, with a maximum length of 1,024 characters. The parameter value cannot start with a dollar sign ($) and can include printable ASCII characters, except for the following characters:<br><br>      * Double quotes ("")<br><br>      * Delete (ASCII code 127)<br><br>   * If the **Value type** is **Variable**, you need to select a variable from the list. The value of the selected variable will be used as the value of this parameter. |


<span id="7a287af7"></span>
### Authentication headers

Specify the headers that need to be included in the authentication request.


|**Configuration** |**Description** |
|---|---|
|HOST request header |Represents the value of the HOST header in the authentication request. This configuration has the following options:<br><br><br>* **Same as domain name**: The value of the HOST header is the same as the domain name.<br><br>* **Specified**: A specified value for the HOST header. If you choose this option, the **Specified HOST** configuration will appear on the page. In this configuration, you need to enter a value for the HOST header, which cannot exceed 1,024 characters. |
|Request headers except HOST |Represents which request headers from the user request are included in the authentication request. This configuration has the following options:<br><br><br>* **Include all**: The authentication request includes all request headers from the user request.<br><br>* **Include none**: The authentication request does not include any request headers from the user request.<br><br>* **Include specified**: The authentication request includes specified request headers from the user request. |
|Header list |This configuration only appears if the **Request headers except host** is **Include specified headers**. This configuration represents which request headers from the user request need to be included in the authentication request. Multiple headers are separated by semicolons (;). The headers are case\-insensitive. |
|Additional headers |This configuration represents additional request headers that you need to add. You can add up to 50 headers.<br><br><br>* **Name**: Represents the name of a request header that you need to add. The header name is case\-insensitive and cannot be `Host`. The length of the header name cannot exceed 1,024 characters. The header name can include printable ASCII characters, except for the following characters:<br><br>   * Underscore (_)<br><br>   * Spaces<br><br>   * Double quotes (")<br><br>   * Delete (ASCII code 127)<br><br>* **Value type**: Represents how the value of this request header is defined. This configuration has the following options:<br><br>   * **Constant**: The header value is a fixed value of type string.<br><br>   * **Variable**: The header value comes from a variable. See [Variables](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication#ba172f40).<br><br>* **Value**: Represents the value of this request header. The description of this configuration is as follows:<br><br>   * If the **Value type** is **Constant**, you specify a fixed value as the value of this header, with a maximum length of 1,024 characters. The value cannot start with a dollar sign ($) and can include printable ASCII characters, except for the following characters:<br><br>      * Double quotes (")<br><br>      * Delete (ASCII code 127)<br><br>   * If the **Value type** is **Variable**, you need to select a variable from the list. The value of the selected variable will be used as the value of this header. |


<span id="7ba1b233"></span>
### Authentication results

Specify how the CDN handles the authentication result returned by the authentication server.

In the configuration shown in the screenshot, the fields specified in the cache key are `URI` and `client_ip`. This configuration indicates that the CDN caches the authentication result based on the following attributes of the user request:


* IP address of the request

* URI of the request


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When setting the cache key, the URI field must be included, otherwise the CDN cannot determine the request file corresponding to the authentication result.</div>


In this way, for subsequent requests from the same IP address with the same URI, the CDN will use the cached authentication result.


|**Configuration** |**Description** |
|---|---|
|Status code for successful authentication |Represents which status codes returned from the authentication server are considered successful authentication. The default value is 200. You can enter one or more status codes in the range of 200\-299. Multiple status codes are separated by semicolons (;). You can also enter 2xx to represent any status code in the range of 200\-299. |
|Status code for failed authentication |Represents which status codes returned from the authentication server are considered failed authentication. The default value is 401. You can enter one or more status codes in the range of 400\-499. Multiple status codes are separated by semicolons (;). You can also enter 4xx to represent any status code in the range of 400\-499. |
|Action for other status codes |This configuration represents how the CDN handles the user request when the following conditions are met.<br><br><br>* The status code returned from the authentication server is not one of the specified successful authentication status codes.<br><br>* The status code returned from the authentication server is not one of the specified failed authentication status codes.<br><br><br>This configuration has the following options:<br><br><br>* **Allow**: The CDN considers the user request as a successful authentication and returns the requested file to the user.<br><br>* **Block**: The CDN considers the user request as a failed authentication and rejects the request. |
|Caching authentication results |Represents whether the CDN caches the authentication result, which is the authentication status code returned by the authentication server. You can set this configuration to **Enabled** or **Disabled**. The default is **Disabled**.<br><br>After enabling this configuration, the CDN will check if the authentication status code of the received user request has been cached. If the authentication status code has been cached, the CDN will use that status code to determine whether to send the requested file to the user.<br><br>This configuration can improve the efficiency of the CDN in responding to user requests. |
|Caching duration |Represents the cache time of the authentication status code, in seconds. This configuration only appears when **Caching authentication results** is **Enabled**. You can enter a value in the range of 1\-86400. 86,400 seconds represents 24 hours. |
|Cache key |Represents the fields included in the cached authentication status code. These fields are defined in this configuration. Each authentication status code has a unique cache key. This configuration only appears when **Cache authentication results** is **Enabled**.<br><br>Additionally, the CDN uses the cache key to determine if the user request matches the cache of the authentication status code. When a request is received, the CDN tries to match the cache key with the fields in the request. If a match is found, the CDN will use the cached authentication status code.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The URI field must be included in the cache key, otherwise the CDN cannot determine the request file corresponding to the authentication result.</div><br> |
|CDN status code for failed authentication |Represents the status code returned by the CDN when authentication fails. The default status code is 403.<br><br>You can enter any status code in the range of 400\-499. |
|Authentication timeout |Represents the timeout period for the authentication request, in milliseconds. The default value is 200. The range of timeout periods you can enter is 200\-3600. |
|Action for authentication exceptions |This configuration represents how the CDN handles user requests when authentication exceptions occur.<br><br>This configuration has the following options:<br><br><br>* **Allow**: The CDN considers the user request as a successful authentication and returns the requested file to the user.<br><br>* **Block**: The CDN considers the user request as a failed authentication and rejects the request.<br><br><br>Authentication exceptions include, but are not limited to, the following situations:<br><br><br>* Authentication request timeout.<br><br>* The authentication server rejected the authentication request.<br><br>* The CDN failed to establish a connection with the authentication server. |


<span id="47348a8d"></span>
## Reference

<span id="ba172f40"></span>
### Variables

The following table lists the variables supported by BytePlus VOD.


|**Variable** |**Description** |**Example** |
|---|---|---|
|host |Represents the value of the Host header in the user request. |`example.com:8080` |
|ua |Represents the value of the User\-Agent header in the user request. |`Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail` |
|referer |Represents the value of the Referer header in the user request. |`https://www.example.com/file?name=123` |
|content_type |Represents the value of the Content\-Type header in the user request. |`text/html` |
|X\-Forwarded\-For |Represents the value of the X\-Forwarded\-For header in the user request. |`20.5.118.10` |
|client_ip |Represents the IP address from which the user request is sent. |`15.15.15.10` |
|scheme |Represents the protocol used in the user request. |`https` |
|server_protocol |Represents the version of the protocol used in the user request. |`HTTP/2.0` |
|URI |Represents the URI in the user request, excluding the query string. |`/dir/page.php` |
|req_args |Represents all the query parameters in the user request. |`color=red&n=10` |
|request_method |Represents the request method used in the user request. |`GET` |
|request_uri |Represents the URI in the user request, including the query string. |`/dir/page.php?color=red&n=10` |
|local_ip |Represents the IP address of the edge node that serves the user request in the CDN. |`267.89.0.45` |
|req_time |Represents the time when the CDN receives the user request. For the time format, please refer to the example. |`18/Apr/2022:16:48:48 +0800` |
|msec |Represents the current time. The format is a decimal Unix timestamp. |`1650558396` |

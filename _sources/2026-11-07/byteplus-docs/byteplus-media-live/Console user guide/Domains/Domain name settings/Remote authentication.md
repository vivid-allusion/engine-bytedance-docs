---
title: "Remote authentication"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/remote-authentication"
---

BytePlus MediaLive supports sending user requests to a specified authentication server, which verifies the user requests. If the verification passes, access is allowed; if the verification fails, access is rejected or other restrictions are imposed, effectively preventing your resources from being accessed by unauthorized users.

<span id="69f56575"></span>
## Feature Introduction

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc144af45954405a37a5b083d9167dd~tplv-goo7wpa0wc-image.image) </span>


1. The user sends a pull\-stream request to MediaLive, which comes with authentication parameters.

2. After MediaLiva receives a user request, it processes the request according to the remote authentication configuration and forwards it to the authentication server.

3. The authentication server returns the authentication result to MediaLive based on the received authentication request.

4. MediaLive takes corresponding actions to release or reject requests based on the authentication result returned by the authentication server.


<span id="d3d00b55"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only remote authentication is supported for pull stream requests.</div>



1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live)。

2. In the left\-side navigation pane, select **Settings** \> **Domains** to enter the domain list page.

3. On the **Domains** page that appears, find the pull domain name that you are about to configure and click **Settings** in the **Actions** column.

4. On the page that opens, click the **Access control** tab.

5. In the **Remote authentication** module, open the remote authentication switch or click **Edit** to open the configuration dialog box.

6. On the **Request Settings** tab, configure the request\-related parameters.

   The parameters needed to be filled in are described in the table below:

   
   |**Parameters** |**Description** |
   |---|---|
   |Authentication domain |Remote authentication server address supports HTTP/HTTPS protocol addresses and server IP addresses. The default ports used by the remote authentication server are 80/443. If non\-default ports are used, it supports setting in the form of domain name:port or IP:port. |
   |Authentication server path |The access path of the authentication request is used to specify the specific resource or service to be accessed, and the following configuration methods are supported.<br><br><br>* Matching the request: Use the path information carried in the user's pull\-streaming request;<br><br>* Custom authentication server path: Customize the remote authentication request path, which must start with / and have a maximum length of 100 characters, such as /auth. |
   |Request method |SET the request method for authentication requests, supporting the following values.<br><br><br>* GET: The data requested is included in the URL;<br><br>* POST: The data is sent to the server as the requested body. |
   |Maximum authentication duration |The timeout duration of a single authentication request, the default is 0, in seconds, and the value range is [0, 600]. |
   |Authentication failure strategy |When a request exception occurs, whether it is treated as an authentication failure or an authentication success. The values and meanings are as follows.<br><br><br>* Authentication succeeded;<br><br>* Authentication failure.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An exception occurs when a request fails to reach the authentication server, such as when the request times out, the request port does not match the authentication server port, and so on.</div><br> |
   |Retries on failure |The number of retries after the authentication request timed out, the default is 3 times, and the value range is [0, 10]. |
   |Retry interval |The time interval between retries after the authentication request timed out, in seconds, the default is 10, and the value range is [1, 30]. |
   

7. On the **Query Parameters** tab, configure the query parameters for the authentication request.

   
   |**Parameters** |**Description** |
   |---|---|
   |Use the query parameters in the user's request |Do not process the query parameters, and use the user's pull\-streaming request query parameters as the authentication request query parameters. |
   |Custom query parameters |Customize query parameters of the authentication request, which can support up to 50 parameters and support the following methods.<br><br><br>* Constant Type: Custom parameters, using constants for parameter values, maximum length of both parameters and parameter values is 100 characters, and spaces are not supported.<br><br>* Variable Type：Custom parameters, using variables as parameter values, maximum length of parameters is 100 characters, and spaces are not supported.<br><br><br>The selectable variables and their meanings supported by the parameter value are as follows.<br><br><br>* vhost: The domain name space to which the domain name in the pull\-stream request belongs.<br><br>* domain: The domain name used in the pull\-stream request.<br><br>* app: The AppName used in the pull\-stream request.<br><br>* stream: The StreamName used in the pull\-stream request.<br><br>* client_ip: The IP address of the pull\-stream client.<br><br>* server_ip: The IP address of the CDN node that responds to the pull\-stream request;<br><br>* request_uri: The URI of the pull\-stream request address.<br><br>* Extract user request query parameters: Extract the query parameters from the user's pull\-stream request and map them as query parameters in the authentication request.<br><br>   * User request parameter: The query parameters in the user's pull\-stream request.<br><br>   * Auth request parameter: The new parameter name used when mapping the query parameters from the user's pull\-stream request to the query parameters in the authentication request.<br><br>* Extract user request header parameters: Extract the header parameters from the user's pull\-stream request and map them as header parameters in the authentication request.<br><br>   * User request parameter: The header parameters in the user's pull\-stream request.<br><br>   * Auth request parameter: The new parameter name used when mapping the header parameters from the user's pull\-stream request to the header parameters in the authentication request. |
   |None |When calling an authentication request to the authentication server, do not carry any URL parameters. |
   

8. On the **Headers** tab, configure the header parameters for the authentication request.

   
   |**Parameters** ||**Description** |
   |---|---|---|
   |Authentication request Host header field |Same as authentication domain |Do not process the Host parameter in the user's pull request header. |
   ||Custom Host |Customize the value of the Host parameter in the authentication request header, do not support entering spaces, and the maximum length is 1024 characters. |
   |Other authentication request header fields |Custom header |Customize the header parameters of the authentication request, which can support up to 50 parameters and support the following methods.<br><br><br>* Constant Type：Custom parameters, using constants for parameter values, maximum length of both parameters and parameter values is 100 characters, and spaces are not supported.<br><br>* Variable Type： Custom parameters, using variables as parameter values, maximum length of parameters is 100 characters, and spaces are not supported.<br><br><br>The selectable variables and their meanings supported by the parameter value are as follows.<br><br><br>* vhost: The domain name space to which the domain name in the pull\-stream request belongs.<br><br>* domain: The domain name used in the pull\-stream request.<br><br>* app: The AppName used in the pull\-stream request.<br><br>* stream: The StreamName used in the pull\-stream request.<br><br>* client_ip: The IP address of the pull\-stream client.<br><br>* server_ip: The IP address of the CDN node that responds to the pull\-stream request;<br><br>* request_uri :The URI of the pull\-stream request address.<br><br>* Extract user request query parameters: Extract the query parameters in the user's pull\-stream request as the header parameters of the authentication request.<br><br>   * User request parameter: The query parameters in the user's pull\-stream request.<br><br>   * Auth request parameter: The new parameter name used when mapping the query parameters in the user's pull\-stream request to the header parameters in the authentication request.<br><br>* Extract user request header parameters: Extract the header parameters in the user's pull\-stream request as the header parameters of the authentication request.<br><br>   * User request parameter: The header parameters in the user's pull\-stream request.<br><br>   * Auth request parameter: The new parameter name used when mapping the header parameters in the user's pull\-stream request to the header parameters in the authentication request. |
   ||None |When calling an authentication request to the authentication server, do not carry other authentication request header parameters. |
   

9. On the **Request body** tab, configure the body parameters for the authentication request.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the authentication request method is POST, it is supported to configure the body parameters of the authentication request.   </div>
   

   
   |**Parameters** |**Description** |
   |---|---|
   |Customize the authentication request body |Customize the body parameters of the authentication request, which can support up to 50 parameters and support the following methods.<br><br><br>* Constant Type: Custom parameters, using constants for parameter values, the maximum length of both parameters and parameter values is 100 characters, and spaces are not supported.<br><br>* Variable Type： Custom parameters, using variables as parameter values, the maximum length of parameters is 100 characters, and spaces are not supported.<br><br><br>The selectable variables and their meanings supported by the parameter value are as follows.<br><br><br>* vhost: The domain name space to which the domain name in the pull\-stream request belongs.<br><br>* domain: The domain name used in the pull\-stream request.<br><br>* app: The AppName used in the pull\-stream request.<br><br>* stream: The StreamName used in the pull\-stream request.<br><br>* client_ip: The IP address of the pull\-stream client.<br><br>* server_ip: The IP address of the CDN node that responds to the pull\-stream request;<br><br>* request_uri: The URI of the pull\-stream request address. |
   |Query parameters or headers from user request |* Customize the Authentication Request Body: Customize the authentication request body, allowing specific parameters to be added to the body of the authentication request as needed. This can be done by setting constant parameters or using variables for dynamic population.<br><br>* Query Parameters or Headers from User Request: Extract query parameters or request headers from the user's request to be used as parameters in the authentication request. |
   

10. On the **Result** tab, configure the processing policy to return the authentication result.



|**Parameters** |**Description** |
|---|---|
|HTTP status code(Success) |The status code returned by the authentication server when authentication is successful. All status codes should be in the range [200,499], and should not duplicate the failure status code. |
|HTTP status code(Error) |The status code returned by the authentication server when authentication fails. All status codes should be in the range [200,499], and should not duplicate the success status code. |
|Additional HTTP status codes |When the status code returned by the authentication server is not in the defined authentication success status code or authentication failure status code, it will be processed according to authentication success or authentication failure. |
|HTTP status code (Error) return to client |When authentication fails, MediaLive should return a status code to the client, which should be in the range of [400,699]. |
|Result cache |Using the authentication result cache, when an authentication request is made again, if the last authentication result cache has not expired, the cached authentication result is used as the result of this authentication request.<br><br><br>* Authentication success and failure cache configuration are the same: Select whether authentication success and authentication failure use the same cache configuration.<br><br>* Authentication success/failure cache time: The cache expiration time when authentication is successful or fails, and the cache will not be used when it expires.<br><br>* Parameters for Generating Authentication Successful/Failure Cache Key: Configuring the parameters used to generate the cache key, supporting the following specified values.<br><br>   * Header parameter: Cache Key generation using parameters in the user's request header, specify the parameter name.<br><br>   * URL parameter: Cache Key generation using parameters in the user's requested URL, specify the parameter name.<br><br>   * Variable vhost: Cache keys are generated using the domain namespace of the pull request domain as a parameter, and there is no need to specify the parameter name.<br><br>   * Variable domain: Cache keys are generated using the domain name specified in the pull request as a parameter, without the need to specify the parameter name.<br><br>   * Variable app: Cache keys are generated using the AppName in the pull\-streaming request address as a parameter, no need to specify the parameter name.<br><br>   * Variable stream: Cache keys are generated using the StreamName in the pull request address as a parameter, no need to specify the parameter name.<br><br>   * Variable client_ip: Cache keys are generated using the client IP address from the pull request as a parameter, no need to specify the parameter name.<br><br>   * Variable request_uri: Cache keys are generated using the URI of the pull request as a parameter, no need to specify the parameter name. |
|HLS\-TS file authentication |Configures whether to enable authentication for HLS protocol pull requests.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the switch is turned on,remote authentication for TS files is also activated.</div><br> |



11. Click ** Confirm**。

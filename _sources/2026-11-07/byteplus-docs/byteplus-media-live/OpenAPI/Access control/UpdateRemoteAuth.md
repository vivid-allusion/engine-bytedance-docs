---
title: "UpdateRemoteAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023"
---

Call the `UpdateRemoteAuth` API to create a remote authentication configuration for the pull\-stream domain name. After the creation is successful, the user's pull\-stream request will be sent to the specified authentication server, which will verify the user's pull\-stream request.

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateRemoteAuth&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRemoteAuth` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space to which the pull stream domain name that needs to be configured for remote authentication belongs. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space to be queried. |
|Domain |String |Yes |`pull.example.com` |The pull stream domain name that needs to be configured for remote authentication. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain to be queried. |
|Enable |Boolean |Yes |`true` |Whether to enable the current remote authentication configuration. The values and their meanings are as follows.<br><br><br>* `true`: Enable;<br><br>* `false`: Disable. |
|AuthURL |String |Yes |`http://domain.com` |Remote authentication server address, supports HTTP/HTTPS protocol addresses, and supports filling in the server IP address. The default ports used by the remote authentication server are 80/443. If non\-default ports are used, it supports setting in the form of `domain name:port` or `IP:port`. |
|AuthURLPath |String |No |`/auth` |Custom remote authentication request path, required when `UseUserRequest` is set to `false`. |
|UseUserRequest |Boolean |Yes |`false` |The remote authentication request path uses the user request path or the custom request path. The values and meanings are as follows.<br><br><br>* `true`: Use the user request path, and use the user request path to splice to the authentication request address.<br><br>* `false`: Customize the remote authentication request path. |
|Method |String |Yes |`POST` |The authentication request method, and its values and meanings are as follows.<br><br><br>* `POST`: The data of the request is sent to the server as the request body;<br><br>* `GET`: The data of the request is contained in the URL. |
|Timeout |Float |No |`10` |The timeout duration of a single authentication request, the default is 1, in seconds, and the value range is [0, 600]. |
|DenyOnFailed |Boolean |Yes |`true` |When a request exception occurs, whether it is treated as an authentication failure, the value and meaning are as follows.<br><br><br>* `true`: Authentication failed;<br><br>* `false`: The authentication was successful.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An exception occurs when a request fails to reach the authentication server, such as when the request times out, the request port does not match the authentication server port, and so on.</div><br> |
|RetryTimes |Float |No |`3` |The number of retries after the authentication request timed out, the default is 3 times, and the value range is [0, 10]. |
|RetryInterval |Float |No |`10` |The time interval between retries after the authentication request timed out, in seconds, the default is 10, and the value range is [1, 30]. |
|QueryParamConfig |Object of [ParamConfig](https://docs.byteplus.com/en/docs/24/36371#paramconfig) |Yes |`-` |Authentication request URL parameter configuration. |
|HeaderParamConfig |Object of [ParamConfig](https://docs.byteplus.com/en/docs/24/36371#paramconfig) |Yes |`-` |Authentication request Header parameter configuration. |
|HeaderHost |String |No |`remoteauth.com` |Customize the value of the Host parameter in the authentication request header, do not support entering spaces, and the maximum length is 1024 characters. It defaults to empty, indicating the use of the Host parameter requested by the user. |
|BodyParams |Array of [Params](https://docs.byteplus.com/en/docs/24/36371#params) |No |`-` |Authentication request Body parameter configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the authentication request method is POST, it is supported to configure the body parameters of the authentication request.</div><br> |
|AllowStatus |Array of Integer |Yes |`[200]` |The status code returned by the authentication server when the authentication is successful. All status codes should be in the range of [200, 499], and not repeat with DenyStatus. |
|DenyRule |Object of [DenyRule](https://docs.byteplus.com/en/docs/24/36371#denyrule) |Yes |`-` |The status code returned by the authentication server when the authentication fails. All status codes should be in the range of [200, 499], and not repeat with AllowStatus. |
|DenyReturnCode |Float |Yes |`403` |When the authentication fails, the status code returned by the MediaLive to the client should be in the range of [400, 699]. |
|DenyOtherStatus |Boolean |Yes |`true` |When the status code returned by the authentication server is not in the defined authentication success or authentication failure status codes, it is treated as authentication success or authentication failure, and the values and their meanings are as follows.<br><br><br>* `true`: Authentication failure;<br><br>* `false`: Authentication success. |
|CacheConfig |Object of [CacheConfig](https://docs.byteplus.com/en/docs/24/36371#cacheconfig) |No |`-` |Authentication cache configuration. When the configuration is empty, it means that the cache is not used to determine the authentication result. |
|EnableHLSAuth |Boolean |No |`true` |Whether to enable the authentication switch for HLS protocol pull\-stream requests, and the values and their meanings are as follows.<br><br><br>* `true`: Enable;<br><br>* `false`: (Default) Disable. |
|EnableHLSTSAuth |Boolean |No |`true` |Whether to enable remote authentication for TS fragments of HLS protocol streams, and the values and their meanings are as follows.<br><br><br>* `true`: Enable;<br><br>* `false`: (Default) Disable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When enabling the remote authentication for TS fragments, authentication switch for HLS protocol pull\-stream requests must be enabled.</div><br> |


<span id="paramconfig"></span>
### ParamConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UseUserParam |Boolean |Yes |`true` |Whether to use the user request parameters or custom parameters for the URL or Header parameters of the remote authentication request, and the values and their meanings are as follows.<br><br><br>* `true`: Use user request parameters;<br><br>* `false`: Custom parameters. |
|Params |Array of [Params](https://docs.byteplus.com/en/docs/24/36371#params) |No |`-` |Parameter configuration when customizing parameters, supporting a total of no more than 25 constant parameters and variable parameters, and extracting no more than 25 user request parameters. |


<span id="params"></span>
### Params


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`header` |Parameter type, and the values and their meanings are as follows.<br><br><br>* `const_string`: Constant;<br><br>* `header`: Header parameters of the user request;<br><br>* `query`: URL parameters of the user request;<br><br>* `vhost`: Parameter with the value of the variable vhost, indicating the domain name space to which the domain name in the pull\-stream request belongs;<br><br>* `domain`: Parameter with the value of the variable domain, indicating the domain name used in the pull\-stream request;<br><br>* `app`: Parameter with the value of the variable app, indicating the AppName used in the pull\-stream request;<br><br>* `stream`: Parameter with the value of the variable stream, indicating the StreamName used in the pull\-stream request;<br><br>* `client_ip`: Parameter with the value of the variable client_ip, indicating the IP address of the pull\-stream client;<br><br>* `server_ip`: Parameter with the value of the variable server_ip, indicating the IP address of the CDN node responding to the pull\-stream request;<br><br>* `request_uri`: Parameter with the value of the variable request_uri, indicating the URI of the pull\-stream request address. |
|ParamName |String |No |`name` |Parameter name, with a maximum length of 100 characters, and spaces are not supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a constant, it represents the parameter name of the constant parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a Header parameter or a URL parameter of the user request, it indicates to extract the corresponding parameter from the user request.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a variable, it is not effective.</div><br> |
|ToName |String |No |`Name` |New parameter name, with a maximum length of 100 characters, and the default is empty, indicating that no new parameter name is set, and spaces are not supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a constant, it is not effective;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a Header parameter or a URL parameter of the user request, it means that the ToName value is used instead of the corresponding parameter name in the user request during the authentication request;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the parameter type is a variable, it means that the value of ToName is used as the parameter name of this variable.</div><br> |
|Value |String |No |`website` |The parameter value when the parameter type is a constant, with a maximum length of 100 characters, and spaces are not supported. |


<span id="denyrule"></span>
### DenyRule


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DenyStatus |Array of Float |Yes |`[403,404]` |The status code returned by the authentication server when the authentication fails. All status codes should be in the range of [200, 499], and not repeat with AllowStatus. |


<span id="cacheconfig"></span>
### CacheConfig


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UseSameCache |Boolean |Yes |`false` |Whether to use the same configuration (including the cached key value and cache expiration time) for successful and failed authentications.<br><br><br>* `true`: Use the same configuration;<br><br>* `false`: Do not use the same configuration. |
|CacheExpireSecond |Float |No |`1800` |Cache expiration time, the default value of `0` means no caching, in seconds, and the value range is [0, 3600].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the same configuration is used for successful and failed authentications, it represents the authentication cache expiration time;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the same configuration is not used for successful and failed authentications, it represents the expiration time of the successful authentication cache.</div><br> |
|CacheKeys |Object of [Keys](https://docs.byteplus.com/en/docs/24/36371#keys) |Yes |`-` |Parameter configuration used to generate the cache key for the authentication result, with a maximum of 50 parameters supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the same configuration is used for successful and failed authentications, it represents the configuration of the cache key for the authentication result;</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the same configuration is not used for successful and failed authentications, it represents the expiration time of the successful authentication cache.</div><br> |
|DenyExpireSecond |Float |No |`1800` |The expiration time of authentication failure cache, when the default value is `0`, means no caching, in seconds, and the value range is [0, 3600].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It takes effect when the same configuration is not used for successful and failed authentications, that is, when the <code>UseSameCache</code> configuration is <code>false</code>.</div><br> |
|DenyKeys |Object of [Keys](https://docs.byteplus.com/en/docs/24/36371#keys) |No |`-` |Parameter configuration used to generate the cache key for the authentication failure result, with a maximum of 50 parameters supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It takes effect when the same configuration is not used for successful and failed authentications, that is, when the <code>UseSameCache</code> configuration is <code>false</code>.</div><br> |


<span id="keys"></span>
### Keys


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`header` |The type of parameters used to generate the cache key, and the values and meanings are as follows.<br><br><br>* `query`: URL parameters of the user's pull request;<br><br>* `header`: Header parameters of the user's pull request;<br><br>* `vhost`: Use the vhost value of the domain where the user pulls the stream as the parameter;<br><br>* `domain`: Use the domain value of the user's pull request as the parameter;<br><br>* `app`: Use the AppName value in the user's pull request as the parameter;<br><br>* `stream`: Use the StreamName value in the user's pull request as the parameter;<br><br>* `client_ip`: Use the IP address of the pull user's client as the parameter;<br><br>* `request_uri`: Use the URI of the pull request address as the parameter. |
|ParamName |String |No |`host` |Parameter name, which takes effect and is required when the parameter type is query or Header, indicating that the parameter value corresponding to the parameter name in the specified pull request is used as the parameter for generating the cache key. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateRemoteAuth&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Enable": true,
    "AuthURL": "http://remoteauth.com",
    "AuthURLPath": "/auth",
    "UseUserRequest": true,
    "Method": "POST",
    "Timeout": 10,
    "RetryTimes": 3,
    "RetryInterval": 10,
    "DenyRule": {
        "DenyStatus": [
            400
        ]
    },
    "DenyReturnCode": 403,
    "CacheConfig": {
        "CacheExpireSecond": 1800,
        "DenyExpireSecond": 1800,
        "CacheKeys": {
            "Type": "header",
            "ParamName": "host"
        },
        "DenyKeys": {
            "Type": "query",
            "ParamName": "lr"
        },
        "UseSameCache": true
    },
    "EnableHLSAuth": true,
    "EnableHLSTSAuth": true,
    "HeaderHost": "remoteauth.com",
    "QueryParamConfig": {
        "UseUserParam": true,
        "Params": [
            {
                "Type": "query",
                "ParamName": "lr",
                "ToName": "LR",
                "Value": "lang_en"
            }
        ]
    },
    "HeaderParamConfig": {
        "UseUserParam": true,
        "Params": [
            {
                "Type": "header",
                "ParamName": "Accept",
                "ToName": "Accept",
                "Value": "text/html"
            }
        ]
    },
    "BodyParams": [
        {
            "Type": "const_string",
            "ParamName": "name",
            "ToName": "Name",
            "Value": "website"
        }
    ],
    "AllowStatus": [
        200,
        202
    ],
    "DenyOnFailed": true,
    "DenyOtherStatus": true
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateRemoteAuth",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {}
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/36371#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |You cannot pass in Domain and App simultaneously. Please modify the input parameters. |
|400 |InvalidParam.Empty |%s is required |The parameter is missing. Please check if the parameter specified in the error message is passed in. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.DomainNotExist |domain not found |The domain name (Domain) was not found. Please check if the passed\-in domain name is consistent with the actual domain name in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |

---
title: "UpdateAuthKey"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023"
---

Call the `UpdateAuthKey` API to add or update the URL authentication configuration for push and pull streaming addresses. When using this API to update the configuration, all authentication parameters will be updated.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateAuthKey` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domain |String |Yes |`live.push.example.com` |The domain name. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domain Management](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain names. |
|SceneType |String |Yes |`push` |The type of authentication scenario, with values and meanings as follows.<br><br><br>* `push`: Authentication for push streaming.<br><br>* `pull`: Authentication for pull streaming. |
|AuthDetailList |Array of [AuthDetailList](https://docs.byteplus.com/en/docs/24/27203#authdetaillist) |Yes |`-` |The list of authentication information. You can add a maximum of 100 array elements. |
|ValidDuration |Integer |No |`60` |The valid period of the authentication information, in seconds. The default value is `0`. Valid range: [0,2592000]. |
|PushPullEnable |Boolean |No |`true` |Whether the current authentication configuration is enabled.<br><br><br>* `false`: (default) Not enabled.<br><br>* `true`: Enabled. |
|TimeStampBase |Integer |No |`10` |Time format of the timestamp. The default value is `10`. However, the default value is `16` when the value of `AuthType` is set to `TypeC`. Valid values:<br><br><br>* `2`: Binary.<br><br>* `8`: Octal.<br><br>* `10`: Decimal.<br><br>* `16`: Hexadecimal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the value of <code>SceneType</code> is set to <code>push</code>, the value of this parameter is fixed at <code>10</code>.</div><br> |


<span id="authdetaillist"></span>
### AuthDetailList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SecretKey |String |Yes |`1*****1` |The secret key for authentication. It can include uppercase letters (A\-Z), lowercase letters (a\-z), and numbers (0\-9), with a length ranging from 1 to 100 characters. |
|EncryptionAlgorithm |String |Yes |`md5` |Algorithm for generating encrypted strings. Valid values:<br><br><br>* `md5`: Standard MD5 algorithm. When the value of `AuthType` is set to `TypeA`, `TypeB`, or `TypeC`, the value of this parameter must be set to `md5`.<br><br>* `md5_custom`: Custom MD5 algorithm. When the value of `AuthType` is set to `TypeCustom`, the value of this parameter must be set to `md5_custom`. |
|AuthField |JSON Map |No |`{ "volcSecret":"signature","volcTime":"expireTime" }` |Name of the authentication parameter. You need to configure this parameter only when the value of `AuthType` is set to `TypeCustom`.<br><br>The value of this parameter is a Key\-Value pair. The default value is `{"volcSecret":"sign","volcTime":"expire"}`. You can customize the values corresponding to `volcSecret` and `volcTime`, such as `{"volcSecret":"signature","volcTime":"expireTime"}`, which means using `signature` as the name of the authentication parameter for the encrypted string and `expireTime` as the name of the authentication parameter for the timestamp, thereby enabling URL authentication. |
|EncryptField |Array of String |No |`["key","volcTime","Domain"]` |Fields required for generating the encrypted string. You need to configure this parameter only when the value of `AuthType` is set to `TypeCustom`.<br><br>The parameter value is empty by default, but we recommend that you include at least `SecretKey` (authentication key) and `volcTime` (timestamp). For example, if the parameter value is `["SecretKey","volcTime","Domain"]`, the encrypted string can be calculated using `md5({SecretKey}{volcTime}{Domain})`. |
|AuthType |String |Yes |`TypeB` |The URL authentication type. Valid values:<br><br><br>* `TypeA`: Type A.<br><br>* `TypeB`: Type B.<br><br>* `TypeC`: Type C.<br><br>* `TypeCustom`: Custom type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value of <code>SceneType</code> is set to <code>push</code>, the value of this parameter can only be <code>TypeB</code> or <code>TypeCustom</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information on type A, B, or C, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>.</div><br> |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateAuthKey&Version=2023-01-01
{
    "AuthDetailList": [
        {
            "SecretKey": "1*****1",
            "EncryptionAlgorithm": "md5",
            "AuthType": "TypeB"
        }
    ],
    "Domain": "live.push.example.com",
    "PushPullEnable": true,
    "SceneType": "push",
    "ValidDuration": 60,
    "TimeStampBase": 10
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateAuthKey",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27203#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Length |%s should not be longer than %d |The parameter length is incorrect. Please check if the length of the specified parameter in the error message exceeds the limit. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.VhostNotExist |vhost not found |The domain name space (Vhost) was not found. Please check if the passed\-in domain name space is consistent with the actual domain name space in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

---
title: "DescribeAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023"
---

Call the `DescribeAuth` API to query the URL authentication configuration that meets the query conditions.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeAuth` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`pull.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domain Management](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify either <code>Vhost</code> or <code>Domain</code>, not both.</div><br> |
|Domain |String |No |`pull.example.com` |The domain name. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domain Management](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify either <code>Vhost</code> or <code>Domain</code>, not both.</div><br> |
|SceneType |String |Yes |`push` |Authentication scenario type, with values and meanings as follows.<br><br><br>* `push`: Authentication for stream pushing.<br><br>* `pull`: Authentication for stream pulling. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AuthList |Array of [AuthList](https://docs.byteplus.com/en/docs/24/27217#authlist) |`-` |The list of query results. |


<span id="authlist"></span>
### AuthList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`pull.example.com` |The domain name space. |
|Domain |String |`pull.example.com` |The domain name. |
|App |String |`live` |The AppName field. |
|SceneType |String |`push` |Authentication scenario type, with values and meanings as follows.<br><br><br>* `push`: Authentication for stream pushing.<br><br>* `pull`: Authentication for stream pulling. |
|AuthDetailList |Array of [AuthDetailList](https://docs.byteplus.com/en/docs/24/27217#authdetaillist) |`-` |The list of authentication information. |
|ValidDuration |Integer |`604800` |Valid duration, in seconds. |
|AuthStatus |Boolean |`false` |Authentication status. Valid values include:<br><br><br>* `false`: The authentication setting is disabled.<br><br>* `true`: The authentication setting is enabled. |
|TimeStampBase |Integer |`10` |Time format of the timestamp. Valid values:<br><br><br>* `2`: Binary.<br><br>* `8`: Octal.<br><br>* `10`: Decimal.<br><br>* `16`: Hexadecimal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the value of <code>SceneType</code> is <code>push</code>, the value of this parameter is fixed at <code>10</code>.</div><br> |


<span id="authdetaillist"></span>
### AuthDetailList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SecretKey |String |`1asd111` |The secret key for authentication. |
|EncryptionAlgorithm |String |`md5` |Encryption algorithm. |
|AuthField |JSON Map |`{"volcSecret":"sign","volcTime":"expire"}` |Custom parameter names for the authentication information in the push/pull stream addresses. |
|EncryptField |Array of String |`["key","volcTime","Domain"]` |Information you use for authentication. |
|AuthType |String |`TypeB` |The URL authentication type. Valid values:<br><br><br>* `TypeA`: Type A.<br><br>* `TypeB`: Type B.<br><br>* `TypeC`: Type C.<br><br>* `TypeCustom`: Custom type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on type A, B, or C, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>.</div><br> |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023-01-01
{
    "Vhost": "pull.example.com",
    "SceneType": "push"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeAuth",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "AuthList": [
            {
                "App": "live",
                "AuthDetailList": [
                    {
                        "SecretKey": "1asd111",
                        "EncryptionAlgorithm": "md5",
                        "AuthField": {
                            "volcSecret": "sign",
                            "volcTime": "expire"
                        },
                        "EncryptField": [
                            "key",
                            "volcTime",
                            "Domain"
                        ],
                        "AuthType": "TypeB"
                    }
                ],
                "AuthStatus": false,
                "Domain": "pull.example.com",
                "SceneType": "push",
                "ValidDuration": 604800,
                "Vhost": "pull.example.com",
                "TimeStampBase": 10
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27217#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.VhostNotExist |vhost not found |The domain name space (Vhost) was not found. Please check if the passed\-in domain name space is consistent with the actual domain name space in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |

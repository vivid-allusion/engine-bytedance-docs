---
title: "DescribeCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023"
---

Call the `DescribeCallback` API to retrieve callback configurations for your applications.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeCallback` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify either <code>Vhost</code> or <code>Domain</code>, not both.</div><br> |
|Domain |String |No |`push.example.com` |The domain name for stream pushing. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify either <code>Vhost</code> or <code>Domain</code>, not both.</div><br> |
|App |String |No |`Live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify Vhost and leave App unspecified, all your applications of the specified domain name space will be queried.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify Domain, you cannot specify App.</div><br> |
|MessageType |String |No |`push` |The type of callback message to be received. Valid values include:<br><br><br>* `push`: The callback is triggered when stream pushing starts.<br><br>* `push_end`: The callback is triggered when stream pushing ends.<br><br>* `snapshot`: The callback is triggered when screenshot events occur.<br><br>* `record`: The callback is triggered when recording events occur. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CallbackList |Array of [CallbackList](https://docs.byteplus.com/en/docs/24/27478#callbacklist) |`-` |The list of callback information. |


<span id="callbacklist"></span>
### CallbackList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|MessageType |String |`push` |The type of callback message to be received. Valid values include:<br><br><br>* `push`: The callback is triggered when stream pushing starts.<br><br>* `push_end`: The callback is triggered when stream pushing ends.<br><br>* `snapshot`: The callback is triggered when screenshot events occur.<br><br>* `record`: The callback is triggered when recording events occur. |
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`push.example.com` |The application name. |
|TranscodeCallback |Integer |`0` |Defines whether to receive callbacks from transcoded streams.<br><br><br>* `0`: No.<br><br>* `1`: Yes. |
|CallbackDetailList |Array of [CallbackDetailList](https://docs.byteplus.com/en/docs/24/27478#callbackdetaillist) |`-` |The list of callback address information. |
|CreateTime |String |`2021-01-02 15:04:05` |The time the callback configuration was created. |
|CreateTimeUTC |String |`2021-01-02T15:04:05Z` |The time the callback configuration was created(UTC time in RFC 3339 format with second precision). |
|AuthKeyPrimary |String |`1622194197-0-0-5552*****e4e20387c6dc18afce****` |The callback key. |
|AuthEnable |Boolean |`false` |Whether authentication is enabled.<br><br><br>* `false`: Authentication is not enabled.<br><br>* `true`: Authentication is enabled. |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CallbackType |String |`http` |The type of callback address utilized. If `http` is returned, it means both HTTP and HTTPS are supported. |
|URL |String |`http://example.com/callback` |The callback address, which is 1 to 100 characters long. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202108291443190102121532040E197F15",
        "Action": "DescribeCallback",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackList": [
            {
                "App": "live",
                "AuthEnable": false,
                "AuthKeyPrimary": "",
                "CallbackDetailList": [
                    {
                        "CallbackType": "http",
                        "URL": "http://example.com/callback"
                    }
                ],
                "CreateTime": "2021-01-02 23:04:05",
                "CreateTimeUTC": "2021-01-02T15:04:05Z",
                "Domain": "",
                "MessageType": "push",
                "TranscodeCallback": 0,
                "Vhost": "push.live.example.com"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27478#request-parameters) description for inspection. |
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


&nbsp;

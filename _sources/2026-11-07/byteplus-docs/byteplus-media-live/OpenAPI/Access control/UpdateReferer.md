---
title: "UpdateReferer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023"
---

Call the `UpdateReferer` API to create a domain\-level Referer blocklist or allowlist configuration.

<span id="requirements"></span>
## Requirements


* Restrictions: By default, you can create up to 100 Referer rules for the same domain. If you need to create more rules, please contact [Technical Support](https://console.byteplus.com/workorder/create) for assistance.

* Rate limit: 1 query per second per account.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateReferer` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space to which the configuration applies. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space. |
|Domain |String |Yes |`pull.example.com` |The domain name for pull streaming. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|RefererInfoList |Array of [RefererInfoList](https://docs.byteplus.com/en/docs/24/27219#refererinfolist) |Yes |`-` |The list of Referer information.<br><br>Within the same `Domain`, you can configure up to 100 Referer rules, and a maximum of 100 Referer rules can be configured in a single request. |


<span id="refererinfolist"></span>
### RefererInfoList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Key |String |Yes |`referer` |The keyword of the Referer configuration. You can only set it as `referer`. |
|Type |String |Yes |`deny` |Referer restriction type. It can take the following values:<br><br><br>* `deny`: A blocklist configuration. The pull\-stream request is denied if it matches the Referer rule.<br><br>* `allow`: An allowlist configuration. The pull\-stream request is allowed if it matches the Referer rule.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the same API call, all rules in <code>RefererInfoList</code> must use the same <code>Type</code> value.</div><br> |
|Value |String |No |`live.example1.net` |Referer restriction rule, namely the Referer value of the pull\-stream request to be verified. Full domain names or wildcard domain names can be added. A maximum of 300 characters can be entered. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RefererInfoList": [
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example1.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example2.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example3.net"
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateReferer",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27219#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|400 |InvalidParam.Length |%s should not be longer than %d |The parameter length is incorrect. Please check if the length of the specified parameter in the error message exceeds the limit. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name space (Vhost) or domain name (Domain) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |

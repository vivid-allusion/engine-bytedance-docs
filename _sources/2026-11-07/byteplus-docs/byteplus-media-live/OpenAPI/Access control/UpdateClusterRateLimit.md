---
title: "UpdateClusterRateLimit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit"
---

Call the `UpdateClusterRateLimit` API to add or modify the frequency limit for pull\-stream requests.

<span id="usage-scenario"></span>
## Usage scenario

You can do one of the following with this operation:


* Limit the frequency of requests sent from an individual IP address.

* Limit the frequency of requests sent to the same URL from an individual IP address.

* Limit the frequency of requests sent to an individual URL.

* Limit the frequency of requests sent to URLs containing a specified query parameter.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The frequency limit is applied on a per\-edge cluster basis, rather than across the entire network. To illustrate, consider a scenario where the frequency limit for requests sent from a particular IP address is set at 50 per second. If both cluster A and cluster B receive 50 requests from an IP address within a second, no errors will occur. However, if cluster A receives 101 requests while cluster B still receives 50 requests within the same second, any subsequent requests sent from that IP address and received by cluster A will be blocked during the rejection period. Cluster B, on the other hand, will remain unaffected.</div>


<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateClusterRateLimit` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space. |
|Domain |String |Yes |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|Status |Integer |No |`0` |Whether to enable rate limiting.<br><br><br>* `0`: Enable rate limiting.<br><br>* `2`: Disable rate limiting. |
|Type |String |Yes |`ipToAll` |The type of rate limiting you want to configure:<br><br><br>* `ipToAll`: Limit the frequency of requests sent from an individual IP address.<br><br>* `url`: Limit the frequency of requests sent to an individual URL.<br><br>* `queryParam`: Limit the frequency of requests sent to URLs containing a specified query parameter.<br><br>* `ipToUrl`: Limit the frequency of requests sent to the same URL from an individual IP address. |
|Param |String |No |`param1` |The query parameter for which you want to apply the rate limit.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required and takes effect only when both conditions are met:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>Type</code> is set to <code>queryParam</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">Technical support</a> has enabled query\-parameter rate limiting for your account.</div><br> |
|RejectDuration |Integer |No |`1` |The rejection period during which all incoming requests are rejected when the rate limit is exceeded, in seconds. The value range is [1, 10080]. The default value is `1`. |
|RejectCode |Integer |No |`429` |The status code received by the client when a request is rejected. The default value is `429`. |
|AggregationPeriod |Integer |No |`1` |The statistical period, in seconds, during which the request frequency is calculated. For example, if you set `AggregationPeriod` to `10`, the request frequency will be calculated every 10 seconds. The value range is [1, 3600]. The default value is `1`. |
|Limit |Integer |Yes |`101` |The maximum number of requests allowed within `AggregationPeriod`. The value range is [0, 100,000]. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Type": "ipToAll",
    "Limit": 101
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateClusterRateLimit",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7658#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |

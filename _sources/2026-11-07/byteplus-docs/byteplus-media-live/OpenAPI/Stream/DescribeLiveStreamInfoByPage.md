---
title: "DescribeLiveStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023"
---

Call the `DescribeLiveStreamInfoByPage` API to retrieve information of ongoing live streams by page.

<span id="requirements"></span>
## Requirements

Rate limit：1 query per second per account

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveStreamInfoByPage` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |
|PageNum |Integer |Yes |`1` |Page number. BytePlus MediaLive divides the query results into pages and only returns the results on the specified page. Valid range: ≥ 1. |
|PageSize |Integer |Yes |`10` |The number of results on each page. Valid range: 1–1000. |
|Vhost |String |No |`push.example.com` |The domain name space. If unspecified, it means to query all ongoing live streams in all domain name spaces. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|Domain |String |No |`push.example.com` |The domain name. If unspecified, it means that the query result does not filter the domain name of the live stream. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|App |String |No |`live` |The AppName field in the live stream URL. If unspecified, it means that the query result does not filter the AppName field of the live stream. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |No |`example_stream` |The StreamName field in the live stream URL. If unspecified, it means that the query result does not filter the StreamName field of the live stream. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters. |
|StreamType |String |No |`origin` |The type of the stream you want to query. If unspecified, both stream types will be included in your query.<br><br><br>* `origin`: Source stream.<br><br>* `trans`: Transcoded stream. |
|SourceType |String |No |`push` |Source of the stream you want to query.<br><br><br>* `push`: Streams directly pushed to and pulled from BytePlus MediaLive.<br><br>* `relay`: Streams pulled from third\-party CDN. |
|QueryType |String |No |`fuzzy` |The way to query the stream.<br><br><br>* `fuzzy`: Fuzzy match<br><br>* `strict`: (Defatul) Exact match |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StreamInfoList |Array of [StreamInfoList](https://docs.byteplus.com/en/docs/24/20050#streaminfolist) |`-` |A list of stream information. |
|RoughCount |Integer |`1` |The total number of streams. |


<span id="streaminfolist"></span>
### StreamInfoList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ID |Long |`1005002` |The stream ID. |
|Vhost |String |`push.example.com` |The domain name space. |
|Domain |String |`push.example.com` |The domain name. |
|App |String |`live` |The AppNmae field. |
|Stream |String |`example_stream` |The StreamName field. |
|SessionStartTime |String |`2021-10-29T00:55:50.186Z` |The time the live\-stream session starts. |
|SourceType |String |`push` |Source of the stream queried.<br><br><br>* `push`: Streams directly pushed to and pulled from BytePlus MediaLive.<br><br>* `relay`: Streams pulled from third\-party CDN. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&StreamType=origin&SourceType=push&QueryType=fuzzy
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202110291811420102250842170013F8D2",
        "Action": "DescribeLiveStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "Domain": "push.example.com",
                "ID": 1005002,
                "SessionStartTime": "2021-10-29T08:55:50.186Z",
                "Stream": "example_stream\t",
                "SourceType": "push",
                "Vhost": "push.example.com"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/20050#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |The request is rejected. There is no requested resource (domain name space, domain name, application, configuration template, certificate) or interface permission under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.VhostNotExist |vhost not found |The domain name space (Vhost) was not found. Please check if the passed\-in domain name space is consistent with the actual domain name space in use. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name space (Vhost) or domain name (Domain) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

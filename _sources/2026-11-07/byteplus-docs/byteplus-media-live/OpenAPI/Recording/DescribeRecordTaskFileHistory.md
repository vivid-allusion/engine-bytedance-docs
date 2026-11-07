---
title: "DescribeRecordTaskFileHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023"
---

Queries information about previous recordings of a specified domain name space, such as their duration, file format, start time, and end time. Ongoing recordings will not be retrieved.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeRecordTaskFileHistory&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeRecordTaskFileHistory` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`push.example.com` |The domain name space. By default, it is empty, indicating that all domain name space under your BytePlus MediaLive will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |No |`live` |The AppName field in the live stream URL. By default, it is empty, indicating that all AppName under the domain name space will be queried. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |No |`stream-123` |The StreamName field in the live stream URL. By default, it is empty, indicating that the all StreamName under the AppName will be queried. . It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you specify <code>Stream</code>, you must also specify <code>App</code>.</div><br> |
|DateFrom |String |Yes |`2023-11-01T00:00:00Z` |The start time of your query's range (Local time in RFC 3339 format with second precision). When you query the details of a specified recording task, DateFrom should be set to any time before the start time of the recording task. |
|DateTo |String |Yes |`2023-11-07T23:59:59Z` |The end time of your query's range (Local time in RFC 3339 format with second precision). DateTo must be later than DateFrom, and the interval between DateTo and DateFrom should not exceed 7 days. |
|PageNum |Integer |Yes |`1` |Page number. BytePlus MediaLive divides the query results into pages and only returns the results on the specified page. |
|PageSize |Integer |Yes |`30` |The number of query results on each page. |
|Type |String |No |`tos` |Storage type.<br><br><br>* `tos`: BytePlus TOS;<br><br>* `vod`: BytePlus VOD. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [Data](https://docs.byteplus.com/en/docs/24/27432#data) |`-` |A list of recording records. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/27432#pagination) |`-` |Page information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|Stream |String |`stream-123` |The StreamName field. |
|Bucket |String |`live-record-test` |The bucket name or the BytePlus TOS. |
|Path |String |`est6/record/push.example.org/live/testStream413` |Storage path of the recording, in the format of `/record/{vhost}/{app}/{stream}`. |
|Duration |String |`01:34` |Length of the recording file. |
|Format |String |`m3u8` |Format of the recording file. |
|StartTime |String |`2023-11-01 00:49:17` |The start time of the recording. |
|EndTime |String |`2023-11-01 00:45:44` |The end time of the recording. |
|FileName |String |`1630331125_16303312***.m3u8` |Name of the recording file. |
|Vid |String |`v03713g100**********bob16pnh65g` |The ID of the recorded file in BytePlus VOD. |
|StartTimeUTC |String |`2023-10-31T16:49:17Z` |The start time of the recording (UTC time in RFC 3339 format with second precision). |
|EndTimeUTC |String |`2023-10-31T00:45:44Z` |The end time of the recording (UTC time in RFC 3339 format with second precision). |


<span id="pagination"></span>
### Pagination


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The current page number. |
|PageSize |Integer |`10` |The number of results on each page. |
|PageTotal |Integer |`1` |The total number of pages. |
|TotalCount |Integer |`1` |The total number of recording files retrieved. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2023-11-01T00:00:00Z",
    "DateTo": "2023-11-07T23:59:59Z",
    "PageNum": 1,
    "PageSize": 30,
    "Type": "tos"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "202108302155380102252431000500BC2E",
        "Action": "DescribeRecordTaskFileHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "Stream": "testStream413",
                "Bucket": "live-test6",
                "Path": "est6/record/push.example.com/live/testStream413",
                "Duration": "01:34",
                "StartTime": "2021-08-16 00:00:00",
                "EndTime": "2021-08-17 00:00:00",
                "StartTimeUTC": "2021-08-16T00:00:00Z",
                "EndTimeUTC": "2021-08-17T00:00:00Z",
                "Format": "",
                "FileName": "1630331125_16303312***.m3u8"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 1,
            "TotalCount": 1
        }
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27432#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

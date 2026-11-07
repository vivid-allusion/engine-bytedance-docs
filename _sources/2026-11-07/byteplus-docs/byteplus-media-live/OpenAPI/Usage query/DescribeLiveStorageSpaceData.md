---
title: "DescribeLiveStorageSpaceData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata"
---

Call the `DescribeLiveStorageSpaceData` API to query the storage space usage of the live time\-shift function on a daily basis within a specified time range.

<span id="requirements"></span>
## Requirements


* Rate limit: 100 queries per second per account

* Data latency: Data for the previous day can be queried after 8:00 AM daily.

* Data metric: The storage capacity data is measured in binary multiples of 1024, for example, 1 GB = 1024 MB.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveStorageSpaceData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Aggregation |Integer |No |`86400` |The time granularity parameter, measured in seconds, supports configuration as 86400, representing a time interval of one day. The time span for a single query is 93 days, and the historical query time range is 366 days. |
|StartTime |String |Yes |`2022-02-11T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |Yes |`2022-02-17T23:59:59Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Buckets |Array of String |No |`["example"]` |Bucket list, by default, this parameter indicates querying all storage buckets under your account if not specified. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Buckets |Array of String |`["example"]` |Bucket list. |
|StartTime |String |`2022-02-16T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2022-02-17T23:59:59Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Boolean |`86400` |Data granularity, measured in seconds. |
|StorageDataList |Array of [StorageDataList](https://docs.byteplus.com/en/docs/24/25107#storagedatalist) |`-` |Time\-shift storage data. |


<span id="storagedatalist"></span>
### StorageDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-02-16T00:00:00Z` |Time Stamp, defaulting to the end time of each day. For example, returning 2022\-02\-16T00:00:00Z indicates that the storage usage at that time is taken as the billing amount for February 16th. |
|Storage |Float |`4503380.1` |Usage of live time\-shift storage, measured in GB. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023-01-01
{
    "Aggregation": 86400,
    "EndTime": "2022-02-17T23:59:59Z",
    "StartTime": "2022-02-11T00:00:00Z",
    "Buckets": [
        "example"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20180604110420010010****",
        "Action": "DescribeLiveStorageSpaceData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Buckets": [
            "example"
        ],
        "StartTime": "2022-02-16T00:00:00Z",
        "EndTime": "2022-02-17T23:59:59Z",
        "TimeShiftDataList": [
            {
                "TimeStamp": "2022-02-16T00:00:00Z",
                "Storage": 4503380
            },
            {
                "TimeStamp": "2022-02-16T00:05:00Z",
                "Storage": 4503380
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/25107#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

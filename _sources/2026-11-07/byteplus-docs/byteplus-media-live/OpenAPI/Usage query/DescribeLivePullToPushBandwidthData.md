---
title: "DescribeLivePullToPushBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata"
---

Call the `DescribeLivePullToPushBandwidthData` API to query the bandwidth usage of relay tasks generated within a specified time range.

<span id="requirements"></span>
## Requirements


* Billing: For relay bandwidth pricing when pushing streams to third parties, please refer to [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1).

* Rate limit: 30 queries per second per account

* Data latency: 15 minutes

* Data metric: Bandwidth data is calculated in base 1000, for example, 1 Mbps = 1000 Kbps.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLivePullToPushBandwidthData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|GroupList |Array of String |No |`["group001","group002"]` |The list of relay task groups. The default value is empty, which indicates querying the bandwidth usage of all relay tasks. |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |No |`300` |The granularity of data aggregation, measured in seconds, with the following supported options:<br><br><br>* `300` (default): 5 minutes. When aggregated in 5\-minute intervals, the maximum time span for a single query is 31 days, and for historical queries, the maximum time range is 366 days.<br><br>* `3600`: 1 hour. When aggregated in 1\-hour intervals, the maximum time span for a single query is 93 days, and for historical queries, the maximum time range is 366 days.<br><br>* `86400`: 1 day. When aggregated in 1\-day intervals, the maximum time span for a single query is 93 days, and for historical queries, the maximum time range is 366 days. |
|DetailField |Array of String |No |`["Group"]` |The dimension for data segmentation is empty by default, indicating no data segmentation. Currently, only the `Group` dimension is supported for data segmentation.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data segmentation by the <code>Group</code> dimension will occur only if the <code>DetailField</code> parameter is set to <code>Group</code> and the <code>GroupList</code> parameter contains multiple values.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StartTime |String |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |`300` |Data granularity, measured in seconds. |
|DetailField |Array of String |`["Group"]` |The data breakdown dimension is currently limited to `Group`, representing group names. |
|PeakUpBandwidth |Float |`12` |The peak bandwidth for pull and push streams under the current query conditions, measured in Mbps. |
|BandwidthDataList |Array of [BandwidthDataList](https://docs.byteplus.com/en/docs/24/25096#bandwidthdatalist) |`-` |Data at all time granularity levels. |
|BandwidthDetailDataList |Array of [BandwidthDetailDataList](https://docs.byteplus.com/en/docs/24/25096#bandwidthdetaildatalist) |`-` |Data after being segmented by dimensions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data will only be returned segmented by the specified dimension when multiple values are entered for the corresponding dimension parameter.</div><br> |
|GroupList |Array of String |`["group001"]` |The list of group names. |


<span id="bandwidthdatalist"></span>
### BandwidthDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |The start time of each time granularity when data is aggregated by time granularity, formatted in RFC3339 UTC time with second precision. |
|UpBandwidth |Float |`12.0` |The peak bandwidth for pull and push streams within the current data aggregation time granularity, measured in Mbps. |


<span id="bandwidthdetaildatalist"></span>
### BandwidthDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Group |String |`group001` |Group information when data is segmented by the group dimension. |
|PeakUpBandwidth |Float |`12.0` |The peak bandwidth for pull and push streams within the specified time range for the dimension, measured in Mbps. |
|BandwidthDataList |Array of [BandwidthDataList](https://docs.byteplus.com/en/docs/24/25096#bandwidthdatalist) |`-` |All data at every granularity level under the current dimension after data segmentation. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023-01-01
{
    "GroupList": [
        "group001"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Group"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePullToPushBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "GroupList": [
            "group001"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Group"
        ],
        "PeakUpBandwidth": 12,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 12
            },
            {
                "TimeStamp": "2022-04-13T00:00:05Z",
                "UpBandwidth": 10
            }
        ],
        "BandwidthDetailDataList": [
            {
                "DstAddrType": "Live",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
            },
            {
                "DstAddrType": "Third",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/25096#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

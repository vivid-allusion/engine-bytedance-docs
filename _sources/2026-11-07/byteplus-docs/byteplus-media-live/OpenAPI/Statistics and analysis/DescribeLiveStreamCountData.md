---
title: "DescribeLiveStreamCountData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata"
---

Gets the peak count of specific pushed streams, origin\-pull streams, or transcoded streams within a specific time range.

<span id="requirements"></span>
## Requirements


* Rate limit: 30 requests per second per account

* Data latency: 5 minutes


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveStreamCountData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StartTime |String |Yes |`2021-08-16T00:00:00+08:00` |The start time of your query range (UTC time in RFC 3339 format with second precision).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum historical query range is 366 days. The maximum time span for a single query depends on the time granularity for data aggregation.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">With data aggregated every 60 seconds, indicating the value of <code>Aggregation</code> is set to <code>60</code>, the maximum time span for a single query is 24 hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With data aggregated every 300 seconds, indicating the value of <code>Aggregation</code> is set to <code>300</code>, the maximum time span for a single query is 31 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">With data aggregated every 3600 seconds, indicating the value of <code>Aggregation</code> is set to <code>3600</code>, the maximum time span for a single query is 31 days.</div><br> |
|EndTime |String |Yes |`2021-08-16T00:01:59+08:00` |The end time of your query range (UTC time in RFC 3339 format with second precision). |
|DomainList |Array of String |No |`["push.exmaple.com","push2.example.com"]` |List of domains used for live streaming. By default, this list is empty, indicating that the peak stream count from all domains will be returned. You can call [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) or visit the **Domains** page in the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list) to get the domains used for live streaming. |
|StreamType |Array of String |No |`["push"]` |Stream type. By default, the peak stream count for all stream types will be returned. Valid values:<br><br><br>* `push`: Pushed streams.<br><br>* `relay-source`: Origin\-pull streams.<br><br>* `transcode`: Transcoded streams. |
|ISPList |Array of String |No |`["telecom"]` |Internet Service Provider (ISP) identifiers. By default, the peak stream count from all ISPs will be returned. Valid values:<br><br><br>* `unicom`: China Unicom.<br><br>* `telecom`: China Telecom.<br><br>* `mobile`: China Mobile.<br><br>* `cernet`: China Education and Research Network (CERNET).<br><br>* `drpeng`: Dr. Peng Telecom & Media Group<br><br>* `btvn`: Broadcast Television Network (BTVN)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter takes effect only when the value of <code>StreamType</code> is set to <code>push</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can also call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata">DescribeLiveISPData</a> to get the ISP identifiers.</div><br> |
|UserRegionList |Array of [UserRegionList](https://docs.byteplus.com/en/docs/24/25090#userregionlist) |No |`-` |List of regions to which the client IP belongs. By default, the peak stream count from all regions will be returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when the value of <code>StreamType</code> is set to <code>push</code>.</div><br> |
|Aggregation |Integer |No |`60` |The time granularity for data aggregation, measured in seconds. Default value: `300`. Valid values:<br><br><br>* `60`: 1 minute.<br><br>* `300`: 5 minutes.<br><br>* `3600`: 1 hour. |
|DetailField |Array of String |No |`["Domain"]` |The dimension for data segmentation. By default, data is not segmented by dimension.<br><br>Currently, this parameter only has the value `Domain`, indicating data is segmented by domains.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when you set multiple values for the <code>DomainList</code> parameter.</div><br> |


<span id="userregionlist"></span>
### UserRegionList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |No |`AP1` |The area identifier. You can call [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) to get the area identifier. |
|Country |String |No |`CN` |The country identifier. You can call [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) to get the country identifier. To filter based on countries, pass both the `Area` and `Country` parameters. |
|Province |String |No |`HK` |The province identifier. You can call [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) to get the province identifier. To filter based on provinces, you must pass the `Area`, `Country`, and `Province` parameters. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com","push2.example.com"]` |List of domains. |
|StartTime |String |`2021-08-16T00:00:00+08:00` |The start time of your query range (UTC time in RFC 3339 format with second precision). |
|EndTime |String |`2021-08-16T00:01:59+08:00` |The end time of your query range (UTC time in RFC 3339 format with second precision). |
|Aggregation |Integer |`60` |The time granularity for data aggregation, measured in seconds. Valid values:<br><br><br>* `60`: 1 minute.<br><br>* `300`: 5 minutes.<br><br>* `3600`: 1 hour. |
|DetailField |Array of String |`["Domain"]` |The dimension for data segmentation. Currently, this parameter only has the value `Domain`, indicating data is segmented by domains. |
|StreamType |Array of String |`["push"]` |Stream type. Valid values:<br><br><br>* `push`: Pushed streams.<br><br>* `relay-source`: Origin\-pull streams.<br><br>* `transcode`: Transcoded streams. |
|PeakCount |Integer |`100` |The peak count of streams under the current query conditions, namely the maximum concurrency of pushed streams, origin\-pull streams, or transcoded streams within a specific time range. |
|TotalStreamDataList |Array of [TotalStreamDataList](https://docs.byteplus.com/en/docs/24/25090#totalstreamdatalist) |`-` |Data for all time granularities. |
|StreamDetailDataList |Array of [StreamDetailDataList](https://docs.byteplus.com/en/docs/24/25090#streamdetaildatalist) |`-` |Data segmented by domains. |
|ISPList |Array of String |`["telecom"]` |Internet Service Provider (ISP) identifiers. |
|UserRegionList |Array of [UserRegionList](https://docs.byteplus.com/en/docs/24/25090#userregionlist-response) |`-` |List of regions to which the client IP belongs. |


<span id="totalstreamdatalist"></span>
### TotalStreamDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2021-08-16T00:00:00+08:00` |The start time (UTC time in RFC 3339 format with second precision) of each granularity when data is aggregated by time granularity. |
|PeakCount |Integer |`100` |The maximum number of streams within the current time granularity for data aggregation. |


<span id="streamdetaildatalist"></span>
### StreamDetailDataList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |Domain information when data is segmented by domains. |
|TotalStreamDataList |Array of [TotalStreamDataList](https://docs.byteplus.com/en/docs/24/25090#totalstreamdatalist) |`-` |Data for all time granularities under the current domain after data is segmented by domains. |


<span id="userregionlist-response"></span>
### UserRegionList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Area |String |`AP1` |The area identifier. |
|Country |String |`CN` |The country identifier. |
|Province |String |`HK` |The province identifier. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023-01-01
{
    "DomainList": [
        "example1.com",
        "example2.com"
    ],
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 60,
    "DetailField": [
        "Domain"
    ],
    "StreamType": [
        "pull",
        "relay-source"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveSourceStreamCountData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example1.com",
            "example2.com"
        ],
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 60,
        "DetailField": [
            "Domain"
        ],
        "StreamType": [
            "pull",
            "relay-source"
        ],
        "PeakCount": 100,
        "TotalStreamDataList": [
            {
                "TimeStamp": "2021-08-16T00:00:00Z",
                "PeakCount": 100
            }
        ],
        "StreamDetailDataList": [
            {
                "Domain": "example1.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
                    }
                ]
            },
            {
                "Domain": "example2.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Refer to the [request parameters](https://docs.byteplus.com/en/docs/24/25090#request-parameters) description for verification. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain namespace, domain name, app, configuration template, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

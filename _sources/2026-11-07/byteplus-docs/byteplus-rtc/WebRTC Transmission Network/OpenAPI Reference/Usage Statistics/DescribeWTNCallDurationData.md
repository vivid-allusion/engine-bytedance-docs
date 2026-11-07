---
title: "DescribeWTNCallDurationData"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/DescribeWTNCallDurationData"
---

Queries the real\-time call duration data (in minutes) of a specified WTN application within a specific time period. Supports aggregation statistics by business ID, resolution, and region.

<span id="3963b4cd"></span>
## Notes


* QPS limit: A tenant can submit up to 20 requests per second.

* Data latency: There is a data latency of approximately 6 hours.


<span id="7c08b414"></span>
## Request description


* Request method: `POST`

* Request address: `https://open.byteplusapi.com?Action=DescribeWTNCallDurationData&Version=2023-11-01`


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="default">For more information about the character encoding and signature mechanism of the API, see <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828">Call OpenAPI</a>.</div>


<span id="9867c15b"></span>
## Request parameters

<span id="de75afce"></span>
### Query


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeWTNCallDurationData` |API name. The name of the current API is `DescribeWTNCallDurationData`. |
|Version |String |Yes |`2023-11-01` |API version. The version of the current API is `2023-11-01`. |


<span id="2b749764"></span>
### Body


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|AppID |String |Yes |`68abcf6cb7da8a0f8457****` |Your App ID. Get it on the [RTC console](https://console.byteplus.com/rtc/listRTC). |
|StartTime |String |Yes |`2025-12-13T00:00:00+08:00` |The start of the time range to query.<br><br><br>* Use the RFC3339 format with second precision.<br><br>* You can query data for up to the past 366 days. |
|EndTime |String |Yes |`2025-12-13T00:00:00+08:00` |The end of the time range to query.<br><br><br>* Use the RFC3339 format with second precision.<br><br>* The value must not be earlier than `StartTime`. The maximum time span per query is 93 days. |
|BusinessIDList |Array of String |No |`["live-a.example.com", "live-b.example.com"]` |A list of business IDs. If omitted, the API returns the call duration for all business IDs under the specified `AppID`. You can provide up to 5 business IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">注意</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that you have created business IDs and passed them when creating publish/subscribe streams. Otherwise, usage statistics by business ID will not be available.</div><br> |
|Resolution |Array of String |No |`["audio", "360P", "720P", "1080P", "2K", "4K"]` |A list of video resolution levels. If omitted, the API returns data for all resolution levels. Supported values include:<br><br><br>* `audio`<br><br>* `360P`<br><br>* `720P`<br><br>* `1080P`<br><br>* `2K`<br><br>* `4K` |
|RegionList |Array of String |No |`["cn", "ap", "use"]` |A list of regions where WTN service nodes are located. If omitted, the API returns data for all regions.<br><br>Supported values include:<br><br><br>* `cn`: Chinese Mainland<br><br>* `ap`: Asia Pacific<br><br>* `use`: US East |
|Aggregation |Integer |No |`3600` |The time granularity for data aggregation, in seconds. Supported values include:<br><br><br>* `3600`: 1 hour.<br><br>* `86400`: 1 day.<br><br><br>&nbsp;<br><br>If omitted, the default rules apply:<br><br><br>* If the time span exceeds 1 day, the default is 1 day (`86400`).<br><br>* If the time span is 1 day or less, the default is 1 hour (`3600`). |
|DetailField |Array of String |No |`["business_id", "resolution"]` |The dimensions for data grouping. If omitted, the API returns only summary data without detailed grouping.<br><br>Supported values include:<br><br><br>* `business_id`: Group by business ID.<br><br>* `resolution`: Group by resolution.<br><br>* `region`: Group by region. |


<span id="ae7b0254"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|AppID |String |`68abcf6cb7da8a0f8457****` |Your App ID. |
|StartTime |String |`2025-12-13T00:00:00+08:00` |The start of the time range, in RFC3339 format with second precision. |
|EndTime |String |`2025-12-13T00:00:00+08:00` |The end of the time range, in RFC3339 format with second precision. |
|BusinessIDList |Array of String |`["live-a.example.com", "live-b.example.com"]` |A list of business IDs. |
|Resolution |Array of String |`["audio", "360P", "720P", "1080P", "2K", "4K"]` |A list of video resolution levels. |
|RegionList |Array of String |`["cn", "ap", "use"]` |A list of regions where WTN service nodes are located. |
|Aggregation |Integer |`3600` |The time granularity for data aggregation, in seconds.<br><br><br>* `3600`: 1 hour.<br><br>* `86400`: 1 day. |
|DetailField |Array of String |`["resolution"]` |The dimensions for data grouping:<br><br><br>* `business_id`: Group by business ID.<br><br>* `resolution`: Group by resolution.<br><br>* `region`: Group by region. |
|TotalDuration |Integer |`1000` |The total call duration within the query time range, in minutes. |
|DurationList |Array of [DurationList](https://docs.byteplus.com/docs/byteplus-rtc/DescribeWTNCallDurationData#27d102b0) |See response example |A list of call duration data aggregated by time granularity (`Aggregation`). |
|DurationDetailList |Array of [DurationDetailList](https://docs.byteplus.com/docs/byteplus-rtc/DescribeWTNCallDurationData#a4255673) |See response example |A list of detailed data grouped by dimension (`DetailField`). |


<span id="27d102b0"></span>
### DurationList


|Parameter |Type |Example value |Description |
|---|---|---|---|
|TimeStamp |String |`2025-12-13T00:00:00+08:00` |The start time of each aggregation interval, in RFC3339 format with second precision. |
|Duration |Integer |`10` |The total call duration (rounded up) within the current aggregation interval, in minutes. |


<span id="a4255673"></span>
### DurationDetailList


|Parameter |Type |Example value |Description |
|---|---|---|---|
|BusinessID |String |`live-a.example.com` |The business ID. |
|Resolution |String |`720P` |The resolution level. |
|TotalDuration |Integer |`1` |The total call duration for the current dimension, in minutes. |
|DurationList |Array of [DurationList](https://docs.byteplus.com/docs/byteplus-rtc/DescribeWTNCallDurationData#27d102b0) |See response example |The time\-aggregated data for the current dimension. |


<span id="2796e1d7"></span>
## Request example

Query the call duration of resources with Business ID `live-a.example.com` and resolution `720P` under AppID `68abcf6cb7da8a0f8457****` within a specified time range. The query results are aggregated by a time granularity of 1 hour (`3600` seconds) and grouped by `business_id` and `resolution` dimensions.

```JSON
POST https://open.byteplusapi.com?Action=DescribeWTNCallDurationData&Version=2023-11-01
{
    "AppID": "68abcf6cb7da8a0f8457****",
    "StartTime": "2025-12-13T00:00:00+08:00",
    "EndTime": "2025-12-13T02:00:00+08:00",
    "BusinessIDList": [
        "live-a.example.com"
    ],
    "Resolution": [
        "720P"
    ],
    "Aggregation": 3600,
    "DetailField": [
        "business_id",
        "resolution"
    ]
}
```


<span id="37eee7fd"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeWTNCallDurationData",
        "Version": "2023-11-01",
        "Service": "wtn",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AppID": "68abcf6cb7da8a0f8457****",
        "StartTime": "2025-12-13T00:00:00+08:00",
        "EndTime": "2025-12-13T02:00:00+08:00",
        "BusinessIDList": [
            "live-a.example.com"
        ],
        "Resolution": [
            "720P"
        ],
        "Aggregation": 3600,
        "DetailField": [
            "business_id",
            "resolution"
        ],
        "TotalDuration": 120,
        "DurationList": [
            {
                "TimeStamp": "2025-12-13T00:00:00+08:00",
                "Duration": 60
            },
            {
                "TimeStamp": "2025-12-13T01:00:00+08:00",
                "Duration": 60
            }
        ],
        "DurationDetailList": [
            {
                "BusinessID": "live-a.example.com",
                "Resolution": "720P",
                "TotalDuration": 120,
                "DurationList": [
                    {
                        "TimeStamp": "2025-12-13T00:00:00+08:00",
                        "Duration": 60
                    },
                    {
                        "TimeStamp": "2025-12-13T01:00:00+08:00",
                        "Duration": 60
                    }
                ]
            }
        ]
    }
}
```

---
title: "DescribeVodImageEnhancementData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodimageenhancementdata"
---

Queries image enhancement request counts for batch processing. You can aggregate the usage by hour or day and obtain details by space.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodImageEnhancementData&Version=2023\-07\-01

HTTP method: POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodImageEnhancementData` |The API action. Set this value to `DescribeVodImageEnhancementData`. |
|Version |String |Yes |`2023-07-01` |The API version. Set this value to `2023-07-01`. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|SpaceList |Array of String |No |`[]` |The spaces to query. If omitted, all spaces are queried. |
|StartTime |String |Yes |`2026-09-16T00:00:00+08:00` |The start time, in RFC 3339 format with second precision. Must be earlier than `EndTime` and within the last 366 days. |
|EndTime |String |Yes |`2026-09-18T23:59:59+08:00` |The end time, in RFC 3339 format with second precision. The query period cannot exceed 93 days. |
|Aggregation |Integer |No |`86400` |The aggregation interval, in seconds. Valid values: `3600` (hourly) and `86400` (daily). Default: `3600`. |
|TimeZone |String |No |`Asia/Shanghai` |The query time zone. If omitted, the server default time zone is used. |
|DetailFieldList |Array of String |No |`["SpaceName"]` |The dimension for detailed usage data. Set `SpaceName` to return usage by space. |

## Response parameters

For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceList |Array of String |`[]` |The spaces queried. |
|StartTime |String |`2026-09-16T00:00:00+08:00` |The query start time. |
|EndTime |String |`2026-09-18T23:59:59+08:00` |The query end time. |
|Aggregation |Integer |`86400` |The aggregation interval, in seconds. |
|TimeZone |String |`Asia/Shanghai` |The time zone used for the query. |
|DetailFieldList |Array of String |`["SpaceName"]` |The dimensions used for detailed usage data. |
|TotalImageEnhancementData |Integer |`1` |The total number of image enhancement requests during the query period. |
|ImageEnhancementDataList |Array of [ImageEnhancementVTUnit](https://docs.byteplus.com/en/docs/25/124101#imageenhancementvtunit) |`-` |The usage data aggregated by time interval. |
|ImageEnhancementDetailDataList |Array of [ImageEnhancementDetail](https://docs.byteplus.com/en/docs/25/124101#imageenhancementdetail) |`-` |The detailed usage data grouped by the dimensions in `DetailFieldList`. |

### ImageEnhancementDetail

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test-image-resize` |The space name. Returned when `DetailFieldList` contains `SpaceName`. |
|Total |Integer |`1` |The total number of requests for the space. |
|ImageEnhancementDataList |Array of [ImageEnhancementVTUnit](https://docs.byteplus.com/en/docs/25/124101#imageenhancementvtunit) |`-` |The usage data for the space, aggregated by time interval. |

### ImageEnhancementVTUnit

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2026-09-16T16:00:00Z` |The start of the aggregation interval, in RFC 3339 format with second precision. |
|Usage |Integer |`1` |The number of requests during the aggregation interval. |

## Samples

### Sample request

```http
POST /?Action=DescribeVodImageEnhancementData&Version=2023-07-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "SpaceList": [],
    "StartTime": "2026-09-16T00:00:00+08:00",
    "EndTime": "2026-09-18T23:59:59+08:00",
    "Aggregation": 86400,
    "DetailFieldList": [
        "SpaceName"
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20261012183726C780C8EF66067BEAC039",
        "Action": "DescribeVodImageEnhancementData",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "SpaceList": [
            "test-space-111",
            "test-tos",
            "media",
            "media1",
            "test-image-resize",
            "test-ll-image-compression",
            "media3",
            "mya-bps-test4",
            "test-space-11"
        ],
        "StartTime": "2026-09-16T00:00:00+08:00",
        "EndTime": "2026-09-18T23:59:59+08:00",
        "Aggregation": 86400,
        "DetailFieldList": [
            "SpaceName"
        ],
        "TimeZone": "Asia/Shanghai",
        "TotalImageEnhancementData": 1,
        "ImageEnhancementDataList": [
            {
                "TimeStamp": "2026-09-15T16:00:00Z",
                "Usage": 0
            },
            {
                "TimeStamp": "2026-09-16T16:00:00Z",
                "Usage": 1
            },
            {
                "TimeStamp": "2026-09-17T16:00:00Z",
                "Usage": 0
            }
        ],
        "ImageEnhancementDetailDataList": [
            {
                "SpaceName": "test-image-resize",
                "Total": 1,
                "ImageEnhancementDataList": [
                    {
                        "TimeStamp": "2026-09-15T16:00:00Z",
                        "Usage": 0
                    },
                    {
                        "TimeStamp": "2026-09-16T16:00:00Z",
                        "Usage": 1
                    },
                    {
                        "TimeStamp": "2026-09-17T16:00:00Z",
                        "Usage": 0
                    }
                ]
            }
        ]
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

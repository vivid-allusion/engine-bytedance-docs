---
title: "DescribeVodImageCompressionData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describevodimagecompressiondata"
---

Queries image compression usage for batch or real\-time image processing. You can query basic processing and advanced compression separately and aggregate usage by hour or day.

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeVodImageCompressionData&Version=2023\-01\-01

HTTP method: POST

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeVodImageCompressionData` |The API action. Set this value to `DescribeVodImageCompressionData`. |
|Version |String |Yes |`2023-01-01` |The API version. Set this value to `2023-01-01`. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StartTime |String |Yes |`2026-10-10T00:00:00+08:00` |The start time, in RFC 3339 format with second precision. Must be earlier than `EndTime` and within the last 366 days. |
|EndTime |String |Yes |`2026-10-12T23:59:59+08:00` |The end time, in RFC 3339 format with second precision. The query period cannot exceed 93 days. |
|Aggregation |Integer |No |`3600` |The aggregation interval, in seconds. Valid values: `3600` (hourly) and `86400` (daily). Default: `3600`. |
|ProcessMode |String |No |`Batch` |The processing mode. Valid values: `Realtime` (real\-time image processing) and `Batch` (batch image processing). Default: `Realtime`. |
|SpaceList |Array of String |No |`["media1","test-image-resize"]` |The spaces to query. Applies only when `ProcessMode` is `Batch`. An empty array queries all spaces. |
|DomainList |Array of String |No |`[]` |The domains to query. Applies only when `ProcessMode` is `Realtime`. |
|CompressionType |String |No |`Standard` |The usage type: `Standard` for basic processing or `Complex` for advanced compression. An empty string queries both types. |
|RegionList |Array of String |No |`[]` |The region filter. Use an empty array to query without filtering by region. |
|DetailFieldList |Array of String |No |`[]` |The dimensions for detailed usage data. Applies only when `ProcessMode` is `Realtime`; `Domain` requests details by domain. For `Batch`, leave this array empty. |

> **Note**

> For batch processing, use `SpaceList` to filter spaces and leave `DomainList` and `DetailFieldList` empty. Specifying a detail dimension with `ProcessMode=Batch` returns an `InvalidParameter` error.

## Response parameters

For common response parameters, see [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response).

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`[]` |The domains queried. |
|SpaceList |Array of String |`["media1","test-image-resize"]` |The spaces queried. |
|StartTime |String |`2026-10-10T00:00:00+08:00` |The query start time. |
|EndTime |String |`2026-10-12T23:59:59+08:00` |The query end time. |
|Aggregation |Integer |`3600` |The aggregation interval, in seconds. |
|RegionList |Array of String |`[]` |The region filter used for the query. |
|DetailFieldList |Array of String |`[]` |The dimensions used for detailed usage data. |
|TimeZone |String |`Asia/Shanghai` |The time zone used for the query. |
|CompressionType |String |`Standard` |The usage type queried. An empty string represents both basic processing and advanced compression. |
|ProcessMode |String |`Batch` |The processing mode queried. |
|TotalImageCompressionData |Integer |`26399445` |The total usage during the query period, in bytes. |
|ImageCompressionDataList |Array of [ImageCompressionData](https://docs.byteplus.com/en/docs/25/124102#imagecompressiondata) |`-` |The usage data aggregated by time interval. Can be `null` when no usage data is returned. |
|ImageCompressionDetailDataList |Array |`null` |Detailed usage data for real\-time processing. Returns `null` for batch processing. |

### ImageCompressionData

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Time |String |`2026-10-10T12:00:00Z` |The start of the aggregation interval, in RFC 3339 format with second precision. |
|Usage |Integer |`26399445` |The usage during the aggregation interval, in bytes. |

## Samples

### Sample request

```http
POST /?Action=DescribeVodImageCompressionData&Version=2023-01-01 HTTP/1.1
Host: vod.byteplusapi.com
Content-Type: application/json
```

```json
{
    "DomainList": [],
    "SpaceList": [
        "media1",
        "test-image-resize"
    ],
    "CompressionType": "",
    "ProcessMode": "Batch",
    "StartTime": "2026-10-10T00:00:00+08:00",
    "EndTime": "2026-10-12T23:59:59+08:00",
    "Aggregation": 3600,
    "RegionList": [],
    "DetailFieldList": []
}
```

### Sample response

The following excerpt shows the response `Result`. Other time intervals are omitted for brevity.

```json
{
    "Result": {
        "DomainList": [],
        "SpaceList": [
            "media1",
            "test-image-resize"
        ],
        "StartTime": "2026-10-10T00:00:00+08:00",
        "EndTime": "2026-10-12T23:59:59+08:00",
        "Aggregation": 3600,
        "RegionList": [],
        "DetailFieldList": [],
        "TimeZone": "Asia/Shanghai",
        "CompressionType": "",
        "ProcessMode": "Batch",
        "TotalImageCompressionData": 26399445,
        "ImageCompressionDataList": [
            {
                "Time": "2026-10-10T11:00:00Z",
                "Usage": 0
            },
            {
                "Time": "2026-10-10T12:00:00Z",
                "Usage": 26399445
            },
            {
                "Time": "2026-10-10T13:00:00Z",
                "Usage": 0
            }
        ],
        "ImageCompressionDetailDataList": null
    }
}
```

## Error codes

For common error codes, see [Common error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

---
title: "DescribeLivePushStreamInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata"
---

Call the `DescribeLivePushStreamInfoData` API to query the information about the push streaming and the cause of stream disconnection

## Requirements

* Rate limit: 100 queries per second per account

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLivePushStreamInfoData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com","push2.example.com"]` |A list of the domain names you want to query. |
|App |String |No |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |No |`example_stream` |The StreamName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters. |
|StartTime |String |Yes |`2023-05-29T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. You can query the data starting within the past 93 days. |
|EndTime |String |Yes |`2023-05-29T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|PageSize |Integer |No |`20` |The number of query results per page. Valid values: [1,1000]. Default value: `20`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |Domain name for stream pushing. |
|App |String |`example_app` |The AppName field in the live stream URL. |
|Stream |String |`exampel_stream` |The StreamName field in the live stream URL. |
|StartTime |String |`2024-03-16T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2024-03-16T00:01:59Z` |The end time of your query's range in RFC 3339 format with second precision. |
|PushStreamInfoDataList |Array of [PushStreamInfoDataList](https://docs.byteplus.com/en/docs/24/14000#pushstreaminfodatalist) |`-` |Details of the push streams. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/14000#pagination) |`-` |Paginated information. |

### PushStreamInfoDataList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|App |String |`example_app` |The AppName field in the live stream URL. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL. |
|StartTime |String |`2024-03-16T00:00:00Z` |The start time of each interval. UTC time in RFC 3339 format. |
|EndTime |String |`2024-03-16T00:00:30Z` |The end time of each interval. UTC time in RFC 3339 format. |
|Duration |Integer |`122345` |The duration of the streaming. |
|IP |String |`xx.xx.xx.xx` |The IP address of the push stream. |
|StreamBreakReason |String |`Duplicate stream push with the same stream ID` |The reason for ending the streaming. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The current page number. |
|PageSize |Integer |`20` |Size of the log file, in byte. |
|TotalCount |Integer |`2` |Total number of results. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023-01-01
{
    "Domain": "example.com",
    "App": "example_app",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePushStreamInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "App": "example_app",
        "Stream": "exampel_stream",
        "StartTime": "2024-03-16T00:00:00Z",
        "EndTime": "2024-03-16T00:01:59Z",
        "PushStreamInfoDataList": [
            {
                "App": "example_app",
                "Stream": "example_stream",
                "StartTime": "2024-03-16T00:00:00Z",
                "EndTime": "2024-03-16T00:00:30Z",
                "Duration": 122345,
                "IP": "xx.xx.xx.xx",
                "StreamBreakReason": "Duplicate stream push with the same stream ID"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 2
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata#request-parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |

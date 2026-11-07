---
title: "DescribeLiveTranscodeInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023"
---

Call the `DescribeLiveTranscodeInfoData` API to query detailed data, such as the transcode task ID, stream name, transcode suffix, and the start and end times of transcode for a specific live domain or live stream within a specified time range.

## Requirements

* Rate limit: 100 queries per second per account

* Data latency: 20 minutes

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveTranscodeInfoData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com","push.example2.com"]` |List of domains. By default, it is empty, indicating that the transcode data for all domains under your BytePlus MediaLive will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domains to be queried. |
|App |String |No |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length of 1 to 30 characters.<br><br>> **说明**<br><br><br>> When querying stream granularity data, both the `App` and `Stream` parameters are required.<br> |
|Stream |String |No |`example_stream` |The StreamName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters.<br><br>> **说明**<br><br><br>> When querying stream granularity data, both the `App` and `Stream` parameters are required.<br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision.<br><br>> **说明**<br><br><br>> The maximum time range for historical queries is 366 days.<br> |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|TranscodeType |Array of String |No |`["Normal_H264","ByteHD_H265"]` |The video codec. The default value is empty, indicating that the video codec is not specified. It can take the following values:<br><br><br>* `Normal_H264`: H.264 standard transcoding;<br><br>* `Normal_H265`: H.265 standard transcoding;<br><br>* `ByteHD_H264`: H.264 low\-bitrate HD;<br><br>* `ByteHD_H265`: H.265 low\-bitrate HD;<br><br>* `ByteQE`: Video enhancement;<br><br>* `Audio`: Audio stream. |
|Resolution |Array of String |No |`["720P","1080P"]` |The resolution of the transcoded video. For example, a 720P resolution means that the total area of the transcoded video is greater than 480P (640 × 480) and less than or equal to 720P (1280 × 720).<br><br><br>* `480P`: 640 × 480;<br><br>* `720P`: 1280 × 720;<br><br>* `1080P`: 1920 × 1088;<br><br>* `2K`: 2560 × 1440;<br><br>* `4K`: 4096 × 2160;<br><br>* `8K`: \> 4096 x 2160;<br><br>* `0P`: Audio stream transcoding. |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|PageSize |Integer |No |`20` |The number of query results per page. Valid values: [1,100000]. Default value: `20`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com","push.example2.com"]` |The list of domain names. |
|App |String |`live` |The AppName field in the live stream URL by which the streaming granularity is queried. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL by which the streaming granularity is queried. |
|StartTime |String |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-04-14T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|TranscodeType |Array of String |`["Normal_H264","ByteHD_H265"]` |The video codec. The default value is empty, indicating that the video codec is not specified. It can take the following values:<br><br><br>* `Normal_H264`: H.264 standard transcoding;<br><br>* `Normal_H265`: H.265 standard transcoding;<br><br>* `ByteHD_H264`: H.264 low\-bitrate HD;<br><br>* `ByteHD_H265`: H.265 low\-bitrate HD;<br><br>* `ByteQE`: Video enhancement;<br><br>* `Audio`: Audio stream. |
|Resolution |Array of String |`["720P","1080P"]` |The resolution of the transcoded video. For example, a 720P resolution means that the total area of the transcoded video is greater than 480P (640 × 480) and less than or equal to 720P (1280 × 720).<br><br><br>* `480P`: 640 × 480;<br><br>* `720P`: 1280 × 720;<br><br>* `1080P`: 1920 × 1088;<br><br>* `2K`: 2560 × 1440;<br><br>* `4K`: 4096 × 2160;<br><br>* `8K`: \> 4096 x 2160;<br><br>* `0P`: Audio stream transcoding. |
|TranscodeInfoDataList |Array of [TranscodeInfoDataList](https://docs.byteplus.com/en/docs/24/35862#transcodeinfodatalist) |`-` |Data for all time granularities. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/35862#pagination) |`-` |The pagination information. |

### TranscodeInfoDataList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskID |String |`yvnytvvnigm3456` |The transcoding task ID. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL. |
|TranscodeSuffix |String |`hd` |The transcoding suffix. |
|TranscodeType |String |`Normal_H264` |The transcoding format. It can take the following values:<br><br><br>* `Normal_H264`: H.264 standard transcoding;<br><br>* `Normal_H265`: H.265 standard transcoding;<br><br>* `ByteHD_H264`: H.264 low\-bitrate HD;<br><br>* `ByteHD_H265`: H.265 low\-bitrate HD;<br><br>* `ByteQE`: Video enhancement;<br><br>* `Audio`: Audio stream. |
|Resolution |String |`720P` |The resolution of the transcoded video. For example, a 720P resolution means that the total area of the transcoded video is greater than 480P (640 × 480) and less than or equal to 720P (1280 × 720).<br><br><br>* `480P`: 640 × 480;<br><br>* `720P`: 1280 × 720;<br><br>* `1080P`: 1920 × 1088;<br><br>* `2K`: 2560 × 1440;<br><br>* `4K`: 4096 × 2160;<br><br>* `8K`: \> 4096 x 2160;<br><br>* `0P`: Audio stream transcoding. |
|StartTime |String |`2022-03-07T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2022-03-08T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Duration |Float |`1.4475713543666666` |The transcoding duration of the current transcoding task within the query time range, in minutes. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The current page number. |
|PageSize |Integer |`20` |The number of results per page. |
|TotalCount |Integer |`1000` |The total number of results. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTranscodeInfoData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "App": "live",
    "Stream": "example_stream",
    "Resolution": [
        "720P",
        "1080P"
    ],
    "PageNum": 1,
    "PageSize": 20,
    "TranscodeType": [
        "Normal_H264",
        "ByteHD_H265"
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveTranscodeInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "push.example2.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "App": "live",
        "Stream": "example_stream",
        "Resolution": [
            "720P",
            "1080P"
        ],
        "TranscodeInfoDataList": [
            {
                "Duration": 1.4475713543666666,
                "Resolution": "720P",
                "TranscodeType": "Normal_H264",
                "Stream": "example_stream",
                "TranscodeSuffix": "hd",
                "StartTime": "2022-03-07T00:00:00Z",
                "EndTime": "2022-03-08T00:00:00Z",
                "TaskID": "yvnytvvnigm3456"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 1000
        },
        "TranscodeType": [
            "Normal_H264",
            "ByteHD_H265"
        ]
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/35862#request-parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |

---
title: "DescribeLiveBatchStreamTranscodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023"
---

Call the `DescribeLiveBatchStreamTranscodeData` API to query transcoding data such as transcoding duration, resolution level, and encoding method of all transcoding streams under the domain name within the specified time range.

## Requirements

* Limitations: Support querying traffic data under a specified domain name, including deleted domain names.

* Rate limit: 30 queries per second per account.

* Data latency: the data latency is 15 minutes.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveBatchStreamTranscodeData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com", "push2.example.com"]` |List of pull stream domains. By default, it is empty, indicating all domains will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the pull stream domains to be queried. |
|StartTime |String |Yes |`2022-11-10T00:00:00Z` |The start time of your query's range (UTC time in RFC 3339 format with second precision).<br><br>> **说明**<br><br><br>> The maximum time span for the historical query time range is 366 days.<br> |
|EndTime |String |Yes |`2022-11-11T00:00:00Z` |The end time of your query's range (UTC time in RFC 3339 format with second precision). |
|PageSize |Integer |No |`1000` |The number of query results per page. Valid values: [100,1000]. Default value: `1000`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com", "push2.example.com"]` |List of domains. |
|StartTime |String |`2022-11-10T00:00:00Z` |The start time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|EndTime |String |`2022-11-11T00:00:00Z` |The end time of the query in UTC time, formatted according to RFC3339, with precision to the second. |
|TotalDuration |Float |`40.1` |The total transcoding duration of all streams under the current query conditions, with the unit of minutes. |
|StreamInfoList |Array of [StreamInfoList](https://docs.byteplus.com/en/docs/24/36094#streaminfolist) |`-` |Data segmented by stream. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/36094#pagination) |`-` |Page information. |

### StreamInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |Domain name. |
|App |String |`live` |The AppName field of a stream address. |
|Stream |String |`example_stream` |The StreamName field of a stream address. |
|Resolution |String |`720P` |Transcoding resolution tier is optional and defaults to no specific resolution tier applied. For instance, selecting `720P` indicates that the transcoding configuration will target videos with an area, calculated by multiplying the longer side by the shorter side, that is greater than the `480P` resolution (640x480) and up to and including the `720P` resolution (1280x720). The supported values and their meanings are as follows:<br><br><br>* `480P`: 640 × 480;<br><br>* `720P`: 1280 × 720;<br><br>* `1080P`: 1920 × 1080;<br><br>* `2K`: 2560 × 1440;<br><br>* `4K`: 4096 × 2160;<br><br>* `8K`: Greater than 4096 x 2160;<br><br>* `0P`: Pure audio transcoding, indicating no video content. |
|Duration |Float |`20.1` |The total transcoding duration of the current stream within the query time, in minutes. |
|VCodec |String |`Normal_H264` |Video Encoding Format: The default value, if left empty, indicates no specified encoding format. Supported values and their meanings are as follows:<br><br><br>* `Normal_H264`: H.264.<br><br>* `Normal_H265`: H.265.<br><br>* `Normal_H266`: H.266.<br><br>* `ByteHD_H264`: H.264 in low\-bitrate HD mode.<br><br>* `ByteHD_H265`: H.265 in low\-bitrate HD mode.<br><br>* `ByteHD_H266`: H.266 in low\-bitrate HD mode.<br><br>* `ByteQE`：video quality enhancement.<br><br>* `Audio`: Pure audio stream. |
|Coderate |Integer |`2000` |The transcoding bitrate of the current stream. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |The current page number. |
|PageSize |Integer |`1000` |The number of results on each page. |
|TotalCount |Integer |`2` |The total number of results. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTranscodeData&Version=2023-01-01
{
  "StartTime": "2022-11-10T00:00:00Z",
  "EndTime": "2022-11-11T00:00:00Z"
}
```

### Sample response

```json
{
  "ResponseMetadata":{
    "RequestId": "201806041104200100100232280022D30",
    "Action": "DescribeLiveBatchStreamTranscodeData",
    "Version": "2023-01-01",
    "Service": "live",
    "Region": "ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z",
    "TotalDuration": 40,
    "StreamInfoList": [
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream001",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      },
      {
        "Domain": "pull.example.com"
        "Stream": "example_stream002",
        "App": "live",
        "Resolution": "720P",
        "Duration": 20,
        "VCodec": "Normal_H264"
      }
    ],
    "Pagination": {
        "PageNum":    1,
        "PageSize":   1000,
        "TotalCount": 2,
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/36094#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |

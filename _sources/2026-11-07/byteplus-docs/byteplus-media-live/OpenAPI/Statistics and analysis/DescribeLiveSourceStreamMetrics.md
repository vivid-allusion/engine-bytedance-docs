---
title: "DescribeLiveSourceStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics"
---

Call the `DescribeLiveSourceStreamMetrics` API to query the monitoring data, such as audio\-video frame rate and bitrate, of a single origin stream within the specified time range, to assess the health of the origin stream.

<span id="requirements"></span>
## Requirements


* Limitations: Supports querying historical monitoring data of origin streams under specified domains (including deleted domains).

* Rate limit: 30 queries per second per account

* Data latency: 30 seconds


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveSourceStreamMetrics` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domain |String |Yes |`pull.example.com` |Pull stream domains. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to view the pull stream domains used for live streaming. |
|App |String |Yes |`live` |The value of the `AppName` field in the live stream address. It can consist of uppercase and lowercase letters (A\-Z, a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length of 1 to 30 characters. |
|Stream |String |Yes |`example_stream` |The `StreamName` field in the live stream address. It can consist of uppercase and lowercase letters (A\-Z, a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length of 1 to 100 characters. |
|StartTime |String |Yes |`2021-08-16T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum time span for a single query is 1 day, and the maximum historical query time range is 366 days.</div><br> |
|EndTime |String |Yes |`2021-08-16T00:01:59Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |No |`30` |The granularity of the data aggregation is measured in seconds, and the current interface only supports data aggregation intervals of `30` seconds. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`pull.example.com` |Pull streaming domain. |
|App |String |`live` |The AppName field in the live stream URL. |
|Stream |String |`example_stream` |The StreamName field in the live stream URL. |
|StartTime |String |`2021-08-16T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-08-16T00:01:59Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |`30` |Data granularity, measured in seconds. |
|MetricList |Array of [MetricList](https://docs.byteplus.com/en/docs/24/25103#metriclist) |`-` |All data at every granularity level. |


<span id="metriclist"></span>
### MetricList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |The start time of each time granularity when data is aggregated by time granularity, formatted in RFC3339 UTC time with second precision. |
|Bitrate |Float |`20` |The maximum video bitrate within the current data aggregation time granularity, in kbps. |
|Framerate |Float |`20` |The maximum video frame rate within the current data aggregation time granularity, in fps. |
|AudioFramerate |Float |`20` |The maximum audio frame rate within the current data aggregation time granularity, in fps. |
|AudioBitrate |Float |`20` |The maximum audio bitrate within the current data aggregation time granularity, in kbps. |
|AudioPts |Double |`1651831909` |The Presentation Time Stamp (PTS) of the last audio frame within the current data aggregation time granularity, in milliseconds. |
|VideoPts |Double |`1651831910` |The Presentation Time Stamp (PTS) of the last video frame within the current data aggregation time granularity, in milliseconds. |
|PtsDelta |Float |`1` |The maximum difference in display timestamps between all audio and video frames within the current data aggregation time granularity, i.e., the maximum difference between all Audio PTS and Video PTS values, in milliseconds. |
|AudioFrameGap |Float |`20` |The maximum difference between the display timestamps of adjacent audio frames within the current data aggregation time granularity, in milliseconds. |
|VideoFrameGap |Float |`20` |The maximum difference between the display timestamps of adjacent video frames within the current data aggregation time granularity, in milliseconds. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 30
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 30,
        "MetricList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bitrate": 20,
                "Framerate": 20,
                "AudioFramerate": 20,
                "AudioBitrate": 20,
                "AudioPts": 1651831909,
                "VideoPts": 1651831910,
                "PtsDelta": 1,
                "AudioFrameGap": 20,
                "VideoFrameGap": 20
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/25103#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;

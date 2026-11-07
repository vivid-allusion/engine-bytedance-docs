---
title: "ListRealTimePublicStreamInfo"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1391228"
---

In real\-time audio and video calling, you can use this interface to query public streams' subscription data of an application over a period of time.

<span id="usage-scenario"></span>
## Usage scenario

The aggregation time for metrics is 30 seconds. If the query interval includes the 0th second or the 30th second, data for the corresponding timestamp will be returned, otherwise the result will be empty.

<span id="requirements"></span>
## Requirements


* Maximum request rate: 10 requests per second

* Furthest queryable time: 30 days

* Maximum time span of single query: 120 minutes

* Data latency: 60 seconds


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListRealTimePublicStreamInfo&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListRealTimePublicStreamInfo` |Interface name. The value of this interface: `ListRealTimePublicStreamInfo` |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|StreamId |String |No |`stream1` |The public stream ID to be queried; separate multiple StreamIds with commas.<br><br>If left blank, it queries all public streams under AppId. |
|StartTime |String |Yes |`2024-11-07T00:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2024-11-08T00:00:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|Indicator |Array of String |Yes |`["pull_num"]` |The name of the metric to query, only supports `pull_num` (subscription count). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/12/36153#indicator) |`-` |Metrics Details |


<span id="indicator"></span>
### Indicator


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [Data](https://docs.byteplus.com/en/docs/12/36153#data) |`-` |Detailed Metrics Information |
|Name |String |`pull_num` |Metric Name |
|Unit |String |`-` |Metric Units |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Value |Double |`99.99` |Metric value, floating point, two decimal places retained. |
|TimeStamp |String |`2021-07-24T00:00:00+08:00` |The start time of the period corresponding to the metric values. |
|StreamId |String |`stream1` |Public Stream ID |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListRealTimePublicStreamInfo&Version=2023-11-01
{
    "AppId": "661e****543cf",
    "StreamId": "stream1",
    "StartTime": "2024-11-07T00:00:00+08:00",
    "EndTime": "2024-11-08T00:00:00+08:00",
    "Indicator": [
        "pull_num"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListRealTimePublicStreamInfo",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Indicators": [
            {
                "Data": [
                    {
                        "Value": 99.99,
                        "StreamId": "stream1",
                        "TimeStamp": "2021-07-24T00:00:00+08:00"
                    }
                ],
                "Name": "pull_num",
                "Unit": ""
            }
        ]
    }
}
```


&nbsp;

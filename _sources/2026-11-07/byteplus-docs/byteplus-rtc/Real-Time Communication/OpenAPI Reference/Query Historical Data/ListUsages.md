---
title: "ListUsages"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-71234"
---

You can call this interface to query the call duration of an application over a period of time.

<span id="usage-scenario"></span>
## Usage scenario

Specify the time period and AppId to obtain the call duration data (granularity is days).

> Note: Due to the different granularity in different statistics, the data obtained here is different from data in the billing call . The final data is subject to the billing data.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListUsages&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListUsages` |Interface name. The value of this interface: `ListUsages` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |No |`You****pId` |The only identifier for your audio & video app |
|StartTime |String |No |`2021-07-24T00:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |No |`2021-07-25T00:00:00+08:00` |End timestamp for querying in the format of RFC3339 in second. The span between starting and ending time is up to 30 days. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Usages |Array of [Usage](https://docs.byteplus.com/en/docs/12/14233#usage) |`-` |Call duration |


<span id="usage"></span>
### Usage


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2021-07-24T00:00:00+08:00` |The time of the aggregation indicator in the format of the RFC 3339 specification. The value of this parameter refers to the start time of the time period corresponding to the call duration. Taking the example value as an example, it means that the corresponding time period is 1 day from 0:00 on July 24, 2021 Beijing time. |
|Audio |Long |`123456` |call duration for audio\-only in minutes |
|VideoSDM |Long |`123456` |Call duration for 360P video in minutes |
|VideoSD |Long |`123456` |Call duration for 720P video in minutes |
|VideoHD |Long |`123456` |Call duration for 1080P video in minutes |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListUsages&Version=2020-12-01
{
    "AppId": "You****pId",
    "StartTime": "2021-07-24T00:00:00+08:00",
    "EndTime": "2021-07-25T00:00:00+08:00"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ListUsages",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Usages": [
            {
                "TimeStamp": "2021-07-24T00:00:00+08:00",
                "Audio": 12345,
                "VideoSDM": 123456,
                "VideoSD": 11111,
                "VideoHD": 12321
            },
            {
                "TimeStamp": "2021-07-25T00:00:00+08:00",
                "Audio": 12345,
                "VideoSDM": 123456,
                "VideoSD": 11111,
                "VideoHD": 12321
            }
        ]
    }
}
```


&nbsp;

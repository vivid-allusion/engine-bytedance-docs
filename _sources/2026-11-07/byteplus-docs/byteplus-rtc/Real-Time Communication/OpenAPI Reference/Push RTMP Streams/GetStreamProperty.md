---
title: "GetStreamProperty"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-139261"
---

Queries properties (such as stream URL, start time, and audio/video parameters) for a specific RTMP stream pushed to WTN or an RTC room.

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=GetStreamProperty&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

The following table only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetStreamProperty` |API name. The value of this interface: `GetStreamProperty`。 |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01`。 |
|AppId |String |Yes |`661****543cf` |The only identifier for your audio & video ap |
|StreamId |String |Yes |`stream1` |WTN stream ID to be queried. |


<span id="response-parameters"></span>
## Response parameters

The following table only lists the return parameters specific to this interface. For the common return parameters, please refer to [Return Structure](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#response).


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|StreamId |String |`stream1` |WTN stream ID to be queried. |
|URL |String |`rtmp://111.62.241.38:8080/app/stream123?app_id=661543cf&vhost=rtmp_streaming` |Push stream address. |
|StartPushTime |Long |`1611736812853` |The start time of the push stream, in UTC format, with the unit of milliseconds. |
|Audio |Object of [Audio](https://docs.byteplus.com/en/docs/12/54363#audio) |`-` |Audio related information. |
|Video |Object of [Video](https://docs.byteplus.com/en/docs/12/54363#video) |`-` |Video related information. |


<span id="audio"></span>
### Audio


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Channels |Integer |`2` |Number of channels. |
|SampleRate |Integer |`44100` |Sampling rate, with the unit of `Hz`. |
|Bitrate |Integer |`10` |Bit rate, in units of `kbps`. |


<span id="video"></span>
### Video


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Width |Integer |`1920` |Video width, in pixels. |
|Height |Integer |`1080` |Video height, in pixels. |
|FPS |Integer |`30` |Frame rate. |
|Bitrate |Integer |`10` |Bit rate, in units of `kbps`. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetStreamProperty&Version=2023-11-01&AppId=&StreamId=
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetStreamProperty",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "cn-north-1"
    },
    "Result": {
        "StreamId": "stream1",
        "URL": "rtmp://111.62.241.38:8080/app/stream123?app_id=661543cf&vhost=rtmp_streaming",
        "StartPushTime": 1611736812853,
        "Audio": {
            "Channels": 2,
            "SampleRate": 44100,
            "Bitrate": 10
        },
        "Video": {
            "Width": 1920,
            "Height": 1080,
            "FPS": 30,
            "Bitrate": 10
        }
    }
}
```


&nbsp;

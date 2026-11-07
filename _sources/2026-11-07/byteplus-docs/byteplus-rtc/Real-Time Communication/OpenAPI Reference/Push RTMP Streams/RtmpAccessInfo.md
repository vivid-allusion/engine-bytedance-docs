---
title: "RtmpAccessInfo"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1392589"
---

You can use this interface to obtain RTMP push stream address, so that you can push RTMP streams such as local media files and audio and video captured by audio and video devices to WTN and play them in the RTC room.

<span id="requirements"></span>
## Requirements

RTMP Stream Format: The video codec protocol is `H.264`, the audio codec format is `AAC`, and B frames must not be included.

Active Number Limit of RTMP Stream: The number of RTMP streams in the push state under a single AppID must not exceed `5000`.

Request Frequency: The QPS must not exceed 60.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=RtmpAccessInfo&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

The following table only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`RtmpAccessInfo` |API name. The value of this interface: `RtmpAccessInfo`。 |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01`。 |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ClientIP |String |No |`111.62.241.38` |RTMP push stream device IP (IPV4 or IPV6).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to fill in. The WTN server will allocate the best server node according to the IP.</div><br> |
|AppID |String |Yes |`661****543cf` |Application ID. Obtained on the [Console](https://console.byteplus.com/rtc/workplaceRTC). |
|StreamID |String |Yes |`stream1` |Stream ID.<br><br>After the RTMP stream is pushed to WTN, you need to use the value of this parameter to call [startPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startpushmixedstream) (Natvie)/[startPlayWTN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104478#wtnstream-startplaywtn) (Web) to play this RTMP stream in the RTC room. |
|ExpectedIPType |String |No |`ipv4` |IP type of RTMP push stream device. The possible values and their meanings are as follows:<br><br><br>* `ipv4`: ipv4.<br><br>* `both`: ipv4 + ipv6.<br><br>   The default value is `ipv4` when not filled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to fill in for obtaining the best node.</div><br> |


<span id="response-parameters"></span>
## Response parameters

The following table only lists the return parameters specific to this interface. For the common return parameters, please refer to [Return Structure](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828).

Fold all


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RtmpUrls |Array of String |`["rtmp://111.62.241.38:8080/app/stream123?app_id=661543cf&vhost=rtmp_streaming"]` |RTMP Push Stream Address List.<br><br>The address format is: `rtmp://{ip}:{port}/app/{streamID}?app_id={AppId}&vhost=rtmp_streaming`.<br><br>Each query returns up to 500 push stream addresses at most. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=RtmpAccessInfo&Version=2023-11-01
{
    "ClientIP": "123.112.69.85",
    "AppID": "661****543cf",
    "StreamID": "stream1",
    "ExpectedIPType": "ipv4"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "RtmpAccessInfo",
        "Version": "2023-11-01",
        "Service": "wtn",
        "Region": "cn-north-1"
    },
    "Result": {
        "RtmpUrls": [
            "rtmp://111.62.241.38:8080/app/stream123?app_id=661543cf&vhost=rtmp_streaming",
            "rtmp://218.12.80.229:8080/app/stream123?app_id=661543cf&vhost=rtmp_streaming"
        ]
    }
}
```


&nbsp;

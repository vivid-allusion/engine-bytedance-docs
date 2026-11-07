---
title: "StopRelayStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105190"
---

> After realying an online media stream, you can use `StopRelayStream` to stop relaying this media stream.


<span id="usage-scenario"></span>
## Usage scenario

You can call the'StopRelayStream 'interface to stop relaying an online media stream.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StopRelayStream&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopRelayStream` |Interface name. The value of this interface: `StopRelayStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The AppId for your application.<br><br>Must be the same AppId that was used to start the task. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of the relayed online media stream. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StopRelayStream&Version=2020-12-01
{
    "AppId": "You****pId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StopRelayStream",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```

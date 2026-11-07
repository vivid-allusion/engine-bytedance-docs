---
title: "StopPushStreamToCDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153582"
---

After you start a single\-stream or mixed\-stream task of pushing to CDN, you can stop it by calling this interface.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `StopPushStreamToCDN` interface to stop specified task.

If you have enabled the message notification of Push to CDN, you can receive the relevant callback notification when the task stops. For message notification service, see [TranscodeStopped](https://docs.byteplus.com/en/docs/12/docs-75125#transcodestopped).

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StopPushStreamToCDN&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopPushStreamToCDN` |Interface name. The value of this interface: `StopPushStreamToCDN` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StopPushStreamToCDN&Version=2020-12-01
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
        "Action": "StopPushStreamToCDN",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;

---
title: "StopSegment"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-155131"
---

After starting a segmenting task, you can use `StopSegment` to stop the task.

<span id="description"></span>
## Description

You can call the `StopSegment`interface to stop a started task.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

POST

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopSegment` |Interface name. The value of this interface:`StopSegment`. |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface:`2022-06-01`. |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_BusinessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |string |Yes |`Your_TaskId` |ID of the task you need to stop. |


<span id="request-sample-code"></span>
### Request sample code

<span id="query"></span>
#### Query

```json
https://open.byteplusapi.com?Action=StopSegment&Version=2022-06-01
```


<span id="body"></span>
#### Body

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "MaxIdleTime": 200,
    "TargetStreams": {
        "StreamList": [
            {
                "UserId": "user1"
            },
            {
                "UserId": "user1"
            }
        ]
    },
    "Duration": 20,
    "Identifier":"Your_Identifier",
    "Handle":true
}
```


<span id="response"></span>
## Response

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_RequestId",
        "Action": "StopSegment",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
        }
}
```

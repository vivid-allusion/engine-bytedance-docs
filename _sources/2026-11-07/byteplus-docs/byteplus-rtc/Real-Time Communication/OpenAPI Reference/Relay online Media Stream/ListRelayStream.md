---
title: "ListRelayStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-121958"
---

Qquery all tasks of relaying media streams in a room under an `AppId`.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `ListRelayStream` interface and specify the `AppId` and `RoomId` to query all tasks of relaying media streams in the room.

> A maximum of 10,000 tasks of relaying media streams can be found in a single query.


<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=ListRelayStream&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListRelayStream` |Interface name. The value of this interface: `ListRelayStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|Offset |Integer |No |`0` |The starting position of querying. The default value is `0`. |
|Limit |Integer |No |`10` |Page size. The value range is [1,100], the default value is `10` |
|Order |Integer |No |`0` |Time order of querying.<br><br><br>* `0`: Ascending. By default.<br><br>* `1`: Descending |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Task |Array of [Task](https://docs.byteplus.com/en/docs/12/14269#task) |`-` |List of task |
|Total |Integer |`1` |Toal number of pages querid |
|Offset |Integer |`0` |Index of next page |
|Limit |Integer |`10` |page size |


<span id="task"></span>
### Task


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AppId |String |`You****pId` |The only identifier for your audio & video app |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |ID of relayed online media stream |
|TaskId |String |`Your_TaskId` |Task ID of the relayed online media stream. |
|Status |Integer |`1` |The current status of the task.<br><br><br>* `1`: The task is starting.<br><br>* `2`: The task is running.<br><br>* `3`: The task is over |
|CreateTime |Integer |`1656332552` |Start time of a task, unix time, in seconds |
|StreamUrl |String |`rtmp://xxx` |Address of oline media stream |
|StreamMode |Integer |`0` |Mode of processing stream.<br><br><br>* 0: transcoding<br><br>* 1: transcapsulation |
|MediaType |Integer |`0` |Media type.<br><br><br>* 0: audio and video<br><br>* 1: audio<br><br>* 2: video |
|VideoWidth |Integer |`640` |Video width in px, and the range is [16, 1920]. |
|VideoHeight |Integer |`480` |Video height in px, and the range is [16, 1920]. |
|FrameRate |Integer |`15` |Sent frame rate. The value's range is [1, 60] and the default value is `15`. This value takes effect when transcoding. |
|Bitrate |Integer |`6000` |The Maximum of bit rate sent, in Kbps. If not filled, there is no limit. It takes effect when transcoding. |
|Loop |Boolean |`false` |Whether to loop. This parameter only takes effect when the source stream is an on\-demand one. |
|Volume |Integer |`100` |The volume of the online media stream playback, in percentage. The range is `[0, 400]`.<br><br><br>* `0`: Mute<br><br>* `100` (default): Original volume<br><br>* `400`: 4 times the original volume. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=ListRelayStream&Version=2020-12-01&AppId=You****pId&RoomId=Your_RoomId&Offset=0&Limit=10&Order=0
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "Task": [
            {
                "AppId": "You****pId",
                "RoomId": "Your_RoomId",
                "TaskId": "Your_TaskId",
                "StreamUrl": "rtmp://xxx",
                "MediaType": 0,
                "StreamMode": 0,
                "VideoWidth": 1920,
                "VideoHeight": 1080,
                "FrameRate": 30,
                "Bitrate": 6000,
                "Loop": true,
                "UserId": "Your_UserId",
                "Status": 2,
                "CreateTime": 1656332552
            }
        ],
        "Offset": 0,
        "Limit": 10,
        "Total": 1
    },
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ListRelayStream",
        "Version": "2020-12-01"
    }
}
```

---
title: "GetPushSingleStreamToCDNTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-3w06olaa6w"
---

After you start a single\-stream task to push to CDN, you can call `GetPushSingleStreamToCDNTask` to specify the `AppId`, `RoomId` and `TaskId` to get the relevant information of the specified single\-stream task.

> A single\-stream task initiated by the server or client side can be queried, but the structure of return parameters is the one set on the server.

> The interface can query the task started within 72 hours.


<span id="Requirements"></span>
## Requirements

Before you call this interface, you must enable push to CDN on the [console](https://console.byteplus.com/rtc).

<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://open.byteplusapi.com?Action=GetPushSingleStreamToCDNTask&Version=2020\-12\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`GetPushSingleStreamToCDNTask` |Interface name. The value of this interface: `GetPushSingleStreamToCDNTask` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |Room Id. It's the identifier of a room. |
|TaskId |String |No |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|UserId |String |No |`Your_UserId` |The user ID of the client that initiates the live streaming relay task.<br><br>If you start more than two tasks, when calling this interface to query:<br><br><br>* The first task. `UserId` can be passed in by Id of user initiating the task, `TaskId` can be passed in by `Null` or Id of user initiating the task.<br><br>* Other tasks. `UserId` can be passed in by Id of user initiating the task, `TaskId` can be passed in by Id of mixing\-stream task. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|PushSingleStreamToCDNTask |Object of [PushSingleStreamToCDNTask](https://docs.byteplus.com/en/docs/12/14227#pushsinglestreamtocdntask) |`-` |Information about the single\-stream task |


<span id="pushsinglestreamtocdntask"></span>
### PushSingleStreamToCDNTask


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|StartTime |Long |`1677205841000` |Unix timestamp when the task starts, in ms. |
|EndTime |Long |`1677205914000` |Unix timestamp when the task stops, in ms.`0` means that the task is running. |
|Status |Long |`3` |Status of the task.<br><br><br>* `0`: Unknown exception<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String |`StopByAPI` |Reason why task stops:<br><br><br>* `Null`: the task is not finished<br><br>* `UnknownStopReason`: There is a unknown reason for stopping<br><br>* `StopByAPI`: The user stops the task by calling the API<br><br>* `StartTaskFailed`: The task failed to start<br><br>* `IdleTimeOut`: the idle time has exceeded the set value.<br><br>* `UserDisconnect`: User on the client server leaves room or call the interface to stop the single\-stream task. |
|PushStreamState |Integer |`6` |Status of pushing the stream<br><br><br>* `0`: . Failed to get the status of task. It's recommended to make a query again later.<br><br>* `1`: Not started<br><br>* `2`: First time to connect CDN service<br><br>* `3`: Reconnecting to CDN service<br><br>* `4`: Succeeded to connect CDN service, and trying to pushing the stream.<br><br>* `5`: Succeeded to connect CDN service and push the stream<br><br>* `6`: Stopped to push the stream.<br><br><br>Only when `Status`=`2`，`PushStreamState` is meaningful；When`Status`=`3`，`PushStreamState`=`6`; when `status` returns other values，`PushStreamState` =`0`. |
|Stream |Object of [SingleStream](https://docs.byteplus.com/en/docs/12/14227#singlestream) |`-` |Stream to be pushed to CDN |
|PushURL |String |`rtmp://xxxxx` |Push stream address. Only rtmp and rtmps protocols are supported. The rtmps protocol only supports internal business. |
|Control |Object of [SingleControl](https://docs.byteplus.com/en/docs/12/14227#singlecontrol) |`-` |Configuration options |


<span id="singlestream"></span>
### SingleStream


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|UserId |String |`Your_UserId` |UserId, indicating the user who publishes this stream |
|StreamType |Integer |`0` |The type of stream, the value can take `0` or `1`, and the default value is `0`.<br><br><br>* `0`: audio and video stream<br><br>* `1`: screen stream. |


<span id="singlecontrol"></span>
### SingleControl


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|MediaType |Integer |`0` |The type of stream, used to globally control the type of subscribed stream. The default value is `0`, and it can take `0` or `1`.<br><br><br>* `0`: Audio and video.<br><br>* `1`: Audio.<br><br><br>Pure video is not supported yet. When the value is invalid, it is automatically adjusted to the default value. |
|MaxIdleTime |Integer |`180` |The idle timeout time of the task. After this time, the task will be terminated automatically. It's unit is second. The value ranges from `[10, 86400]`, and the default value is `180`. |


<span id="QaWfPQOv"></span>
## Samples

<span id="b2hfiG3F"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetPushSingleStreamToCDNTask&Version=2020-12-01&AppId=You****pId&RoomId=Your_RoomId&TaskId=Your_TaskId&UserId=Your_UserId
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "PushSingleStreamToCDNTask": {
            "StartTime": 1677205841000,
            "EndTime": 1677205914000,
            "Status": 3,
            "StopReason": "StopByAPI",
            "PushStreamState": "6",
            "PushURL": "rtmp://xxxxx",
            "Stream": {
                "Index": 0,
                "UserId": "user1",
                "StreamType": 1
            },
            "Control": {
                "MediaType": 1,
                "MaxIdleTime": 180
            }
        }
    },
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "GetPushSingleStreamToCDNTask",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "cn-north-1"
    }
}
```

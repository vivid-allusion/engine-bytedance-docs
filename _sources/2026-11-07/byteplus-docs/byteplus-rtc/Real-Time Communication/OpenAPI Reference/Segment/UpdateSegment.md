---
title: "UpdateSegment"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-155130"
---

If you have started a segmenting task, you can call `UpdateSegment` to update the task，such as prefix of customized filename (`Identifier`), duration of every segment file (`Duration`).

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdateSegment&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSegment` |Interface name. The value of this interface: `UpdateSegment` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app. |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|Identifier |String |No |`Your_Identifier` |Prefix of customized filename. The filename consists of Identifier + UserId + timestamp+ sequence number. By default, the Identifier is a randomly generated UUID. |
|Handle |Boolean |No |`true` |Whether to start segmenting immediately when this function is turned on. `True` means to start segmenting immediately when this function is turned on; `False` means to hot start the task but not segmenting immediately when this function is turned on. The default value is `true`. |
|Duration |Integer |No |`30` |The duration of every segment file in seconds. The range is `[1,600]`, and the default value is `20`. If the value is not valid, it is automatically adjusted to the default value.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After this field is updated, the timer will restart and the current segmenting task will stop immediately and generate a file.</div><br> |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=UpdateSegment&Version=2022-06-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
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
    "Identifier": "Your_Identifier",
    "Handle": true
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "UpdateSegment",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;

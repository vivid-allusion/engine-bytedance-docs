---
title: "StartWebCast"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-119513"
---

In an online classrooms, video conference, and other scenarios, you may need to relay the content of a specified webpage to the RTC room for users to watch. You can use this interface to do this.

After relaying the content of a specified webpage to the RTC room, you can use cloud recording, snapshoting and other advanced features later.

<span id="description"></span>
## Description

You can call the `StartWebCast` interface to relay the content of the specified webpage to the RTC room.

When the first frame is sent or the task ends, the callback address you set on [console](https://console.byteplus.com/rtc) will receive the relevant callback. See [Webcast](https://docs.byteplus.com/en/docs/12/docs-75125#Webcast) for details on callback results.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
## Request method

POST

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters ](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartWebCast` |Interface name. The value of this interface: `StartWebCast` |
|Version |String |Yes |`2020-12-01` |Interface version. The value of this interface: `2020-12-01` |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_BusinessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |ID of the target RTC room. It's the identifier of a room. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of relaying. You must set the TaskId for each task.<br><br>About TaskId, see [TaskId](https://docs.byteplus.com/en/docs/12/14271#taskid) For naming rules for TaskId and other fields above, see [ID](https://docs.byteplus.com/en/docs/12/docs-69835#id). |
|UserId |String |Yes |`Your_UserId` |Each userId is unique in the same room. When a user with an existing userId joined the room, the one who has joined previously would be removed from the room. We recommend having a prefix for userId to distinguish users who joined the room from a client or by calling OpenAPI. For example, `webcast_`. |
|SourceURL |String |Yes |`https://xxx.xxx.xxx` |The address of the web page that needs to be relayed. This URL can carry custom queryParams for authentication and other needs, and the overall length does not exceed 1024. |
|VideoSolutions |[[]VideoSolution](https://docs.byteplus.com/en/docs/12/docs-69835#videosolution) |No | |The video parameters of the output stream. The resolution of the rendered web is determined by the larger resolution of input video streams. If the value is empty, a stream will be sent by the default value.<br><br><br>* When one stream is set, parameters of the output stream will be the same as the set value.<br><br>* When two streams are set, RTC will enable [Simulcasting](https://docs.byteplus.com/en/docs/12/docs-70139) function, and the resolutions of set streams will be the upper limits of the high stream and medium stream in the resolution level division. |
|MaxRunningTime |Int |No |3600 |Maximum running time. After this time, the task will be terminated automatically. The unit is seconds. The value's range is [10,86400], and the default value is `86400`. It is automatically adjusted to the default value when not filled. |
|Monitor |[MonitorConfig](https://docs.byteplus.com/en/docs/12/docs-69835#monitorconfig) |No |/ |Configuration on page Availability Monitor |
|EventNotify |[EventNotifyConfig](https://docs.byteplus.com/en/docs/12/docs-69835#eventnotifyconfig) |No |/ |Configuration of page event notification . This configuration can be enabled if it is necessary to prevent incomplete pages from being collected when the loading is not complete. |


<span id="taskid"></span>
#### TaskId

As the identifier of a task, `TaskId` in a room under an `AppId` is unique. `TaskId` in different rooms or `AppIds` can be repeated, so `AppId` + `RoomId` + `TaskId` is the unique identifier of a task. You can use `AppId` + `RoomId` + `TaskId` to flag a task running in a room under an `AppId`, so that it can be updated or stopped during running with this combination.

<span id="request-example"></span>
### Request example

<span id="query"></span>
#### Query

```postscript
https://open.byteplusapi.com?Action=StartWebCast&Version=2020-12-01
```


<span id="body"></span>
#### Body

```json
{
     "AppId": "Your_AppId",
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "UserId": "Your_UserId",
     "SourceURL": "https://xxx.xxx.xxx",
     "VideoSolutions": [
         {
             "Width": 1280,
             "Height": 720,
             "FrameRate": 30
         }
     ],
     "MonitorConfig":{
         "FreezeCheckInterval" : 3,
         "BlankCheckInterval" : 5,
         "CrashCheckInterval" : 5
     },
     "EventNotifyConfig":{
         "EnableEventNotify" : false,
         "StartTimeout" : 0
     },
     "MaxRunningTime": 60
}
```


<span id="response"></span>
## Response

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```json
{
     "ResponseMetadata": {
         "RequestId": "Your_RequestId",
         "Action": "Start Webcast",
         "Version": "2020-12-01",
         "Service": "rtc",
         "Region": "ap-singapore-1"
     },
     "Result": "ok"
}
```

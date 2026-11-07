---
title: "StopRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-116407"
---

After you start cloud recording by calling `StartRecord`, you can use `StopRecord`to stop it.

<span id="description"></span>
## Description

You can call the `StopRecord`interface to stop specified cloud recording task.

If you have enabled the message notification of stopping cloud recording, you can receive the relevant callback notification at the end of recording in the cloud. For message notification service, see [Enable Message Notification](https://docs.byteplus.com/en/docs/12/docs-75110).

<span id="prerequisites"></span>
## Prerequisites

You have started cloud recording.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

POST

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopRecord` |Interface name. The value of this interface: `StopRecord` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_BusinessId` |Business identity |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. You must set the TaskId for each cloud recording task. About TaskId, see [TaskId](https://docs.byteplus.com/en/docs/12/14219#taskid) |


<span id="taskid"></span>
#### TaskId

As the identifier of a task, `TaskId` in a room under an `AppId` is unique. `TaskId` in different rooms or `AppIds` can be repeated, so `AppId` + `RoomId` + `TaskId` is the unique identifier of a task. You can use `AppId` + `RoomId` + `TaskId` to flag a task running in a room under an `AppId`, so that it can be updated or stopped during running with this combination.

<span id="request-sample-code"></span>
### Request sample code

<span id="query"></span>
#### Query

```postscript
https://open.byteplusapi.com?Action=StopRecord&Version=2022-06-01
```


<span id="body"></span>
#### Body

```json
{
     "AppId": "Your_AppId",
     "RoomId": "Your_RoomId,"
     "TaskId": "Your_TaskId"
}
```


<span id="response"></span>
## Response

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```Plain Text
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_RequestId",
        "Action": "StopRecord",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
        }
}
```

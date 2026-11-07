---
title: "GetRecordTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/getrecordtask-wtn"
---

You can call this API to query information about a recording task.

<span id="description"></span>
## Description

If there are multiple tasks, you will get the information about the most recently created task .

The API can query the task started within 72 hours.

<span id="prerequisites"></span>
## Prerequisites

You must have started a task.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the API, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

<span id="request-method"></span>
### Request method

GET

<span id="request-parameters"></span>
### Request parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/12/docs-69828#request-parameters).

<span id="query"></span>
#### Query


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |`RecordTask` |API name |
|Version |String |Yes |`2022-06-01` |OpenAPI version |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|TargetType |Uint32 |Yes |`1` |`1` for WTN streams. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. |


<span id="request-sample-code"></span>
### Request sample code

<span id="query"></span>
#### Query

```json
https://open.byteplusapi.com?Action=GetRecordTask&Version=2022-06-01&AppId=Your_AppId&RoomId=Your_RoomId&TaskId=Your_TaskId
```


<span id="response"></span>
## Response

See [BaseResponse](https://docs.byteplus.com/en/docs/12/docs-69835#baseresponse) for the structure of return results. The structure of `BaseResponse.Result` is as follows:

The structure of the `Result` is as follows:


|Parameter |Type |Description |
|---|---|---|
|RecordTask |[RecordTask](https://docs.byteplus.com/en/docs/12/24855#recordtask) |Information of record task |


<span id="recordtask"></span>
#### RecordTask


|Parameter |Type |Description |
|---|---|---|
|StartTime |Uint64 |Start time of a task, Unix timestamp, in milliseconds |
|EndTime |Uint64 |End time of a task, Unix timestamp, in milliseconds. `0` means the task is not finished |
|Status |Uint64 |Task status:<br><br>`0`: Unknown exception status<br><br>`1`: Not started<br><br>`2`: Running<br><br>`3`: Ended<br><br>`4`: Task failed |
|StopReason |String |Reason why task stops:<br><br>`Null`: the task is not finished<br><br>`UnknownStopReason`: There is a unknown reason for stopping<br><br>`StopByAPI`: the user stops the task by calling the API<br><br>`StartTaskFailed`: the task failed to start<br><br>`IdleTimeOut`: the idle time has exceeded the set value. |
|RecordFileList |Array of [RecordFile](https://docs.byteplus.com/en/docs/12/docs-115995#recordfile) |the list of recorded files |


<span id="sample-response"></span>
### Sample response

```json
{
    "Result":
    {
        "RecordTask":
        {
            "StartTime":1716437308000,
            "EndTime":1716437321000,
            "Status":3,
            "StopReason":"StopByAPI",
            "TargetType":1,
            "RecordFileList":
            [
                {
                    "ObjectKey":"tkid_lf_psid_9999_1716437309034_000012_c1a90ca3.mp4",
                    "Duration":12245,
                    "Size":445247,
                    "StartTime":1716437309034,
                    "WTNStreamList":
                    [
                        {
                            "Index":0,
                            "StreamId":"lf_psid_9999"
                        }
                    ],
                    "videoCodec":"h264",
                    "audioCodec":"aac",
                    "videoWidth":640,
                    "videoHeight":480
                },
                {
                    "ObjectKey":"tkid_lf_psid_8888_1716437309092_000012_c1a90ca3.mp4",
                    "Duration":12115,
                    "Size":442218,
                    "StartTime":1716437309092,
                    "WTNStreamList":
                    [
                        {
                            "Index":0,
                            "StreamId":"lf_psid_8888"
                        }
                    ],
                    "videoCodec":"h264",
                    "audioCodec":"aac",
                    "videoWidth":640,
                    "videoHeight":480
                }
            ]
        }
    },
    "ResponseMetadata":
    {
        "RequestId":"4b035f6c-19d4-4855-86b2-27af3c31f024",
        "Action":"GetRecordTask",
        "Version":"2022-06-01"
    }
}
```

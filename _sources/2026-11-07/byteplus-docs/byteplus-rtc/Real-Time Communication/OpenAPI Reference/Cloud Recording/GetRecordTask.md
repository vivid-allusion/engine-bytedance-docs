---
title: "GetRecordTask"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-116408"
---

You can call this interface to query information about a recording task.

<span id="Usage scenario"></span>
## Usage scenario

If there are multiple tasks, you will get the information about the most recently created task.

The interface can query the task started within 72 hours.

<span id="Requirements"></span>
## Requirements

You must have started a task.

<span id="HTTP request"></span>
## HTTP request


* Method：GET

* Endpoint：https://open.byteplusapi.com?Action=GetRecordTask&Version=2022\-06\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`GetRecordTask` |Interface name. The value of this interface: `GetRecordTask` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |
|AppId |String |Yes |`Your_AppId` |The only identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. You must set the TaskId for each cloud recording task. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|RecordTask |Object of [RecordTask](https://docs.byteplus.com/en/docs/12/14220#recordtask) |`-` |Information of record task |


<span id="recordtask"></span>
### RecordTask


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|StartTime |Long |`1624873773000` |Start time of a task, Unix timestamp, in milliseconds |
|EndTime |Long |`1624874235000` |End time of a task, Unix timestamp, in milliseconds. `0` means the task is not finished |
|Status |Integer |`3` |Task status:<br><br><br>* `0`: Unknown exception status<br><br>* `1`: Not started<br><br>* `2`: Running<br><br>* `3`: Ended<br><br>* `4`: Task failed |
|StopReason |String |`StopByAPI` |Reason why task stops:<br><br><br>* `Null`: the task is not finished<br><br>* `UnknownStopReason`: There is a unknown reason for stopping<br><br>* `StopByAPI`: the user stops the task by calling the API<br><br>* `StartTaskFailed`: the task failed to start<br><br>* `IdleTimeOut`: the idle time has exceeded the set value. |
|RecordFileList |Array of [RecordFileList](https://docs.byteplus.com/en/docs/12/14220#recordfilelist) |`-` |the list of recorded files.<br><br>When Status equals 2, RecordFileList will return HLS recording file information only if `EnableSyncUpload` is set to true and `FileFormatConfig.FileFormat` includes HLS; in all other cases, it will be empty. |


<span id="recordfilelist"></span>
### RecordFileList


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Vid |String |`v02e96g10000c3cppu139mhmps58of80` |The unique identifier of the file on the Vod platform. You can find the corresponding file on the Vod platform according to the Vid. This parameter is only valid if you choose to store the configuration to the Vod platform. |
|ObjectKey |String |`-` |The full path of the file in the object storage platform, such as `abcefg123.mp4`. This parameter is only valid if you choose to configure storage to the object storage platform. |
|Duration |Long |`100` |Duration of file in ms. |
|Size |Long |`1000` |File size in bytes. |
|StartTime |Long |`1624873773000` |The UTC time when the recording starts in ms. |
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14220#stream) |`-` |List of streams contained in the recording file. For WTN, it's the info of `TargetWTNStreams`. |
|VideoCodec |String |`-` |Video Recording Encoding Protocol |
|AudioCodec |String |`-` |Audio Recording Encoder |
|VideoWidth |Integer |`-` |width of recorded video in px |
|VideoHeight |Integer |`-` |Height of recorded video in px |


<span id="stream"></span>
### Stream


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|Index |Integer |`0` |In custom layout, use `Index` to flag the stream. Later in the `Layout.regions.StreamIndex`, you need to use `Index` to specify the layout settings for the corresponding stream. |
|UserId |String |`Your_UserId` |UserId which represents the user a stream belongs to.<br><br>> Required when pushing RTC audio and video streams and is mutually exclusive with `WTNStreamId`. |
|StreamType |Integer |`0` |The type of RTC stream:<br><br><br>* `0` (default): Normal audio & video stream.<br><br>* `1`: Screen stream.<br><br><br>> It only takes effect when pushing an RTC stream. |
|WTNStreamId |String |`wtn_live_stream_01` |The ID of the WTN stream to be pushed.<br><br>> Required when pushing WTN streams, and mutually exclusive with `UserId`. |


<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetRecordTask&Version=2022-06-01&AppId=You****pId&RoomId=Your_RoomId&TaskId=Your_TaskId
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "RecordTask": {
            "StartTime": 1624873773000,
            "EndTime": 1624874235000,
            "Status": 3,
            "StopReason": "StopByAPI",
            "RecordFileList": [
                {
                    "Vid": "Your_Vid",
                    "Duration": 457280,
                    "Size": 30388433,
                    "StartTime": 1624873773354,
                    "StreamList": [
                        {
                            "UserId": "Your_UserId",
                            "StreamType": 0
                        }
                    ]
                }
            ]
        }
    },
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "GetRecordTask",
        "Version": "2022-06-01"
    }
}
```

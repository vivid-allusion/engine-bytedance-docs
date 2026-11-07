---
title: "EventType Reference"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-75125"
---

The events supported by the message notification service are as follows:


|Function |EventType |Description |
|---|---|---|
|Audio Stream |[UserAudioStreamStart](https://docs.byteplus.com/en/docs/12/14210#useraudiostreamstart) |Audio stream started to push |
||[UserAudioStreamStop](https://docs.byteplus.com/en/docs/12/14210#useraudiostreamstop) |Audio stream stopped pushing |
|Video stream |[UserVideoStreamStart](https://docs.byteplus.com/en/docs/12/14210#uservideostreamstart) |Video stream started to push |
||[UserVideoStreamStop](https://docs.byteplus.com/en/docs/12/14210#uservideostreamstop) |The video stream stopped pushing |
|Screen audio stream |[UserScreenAudioStreamStart](https://docs.byteplus.com/en/docs/12/14210#userscreenaudiostreamstart) |Screen audio stream started to push |
||[UserScreenAudioStreamStop](https://docs.byteplus.com/en/docs/12/14210#userscreenaudiostreamstop) |Screen audio stream stopped pushing |
|Screen video stream |[UserScreenVideoStreamStart](https://docs.byteplus.com/en/docs/12/14210#userscreenvideostreamstart) |Screen video stream started to push |
||[UserScreenVideoStreamStop](https://docs.byteplus.com/en/docs/12/14210#userscreenvideostreamstop) |Screen video stream stopped pushing |
|Cloud recording |[RecordStarted](https://docs.byteplus.com/en/docs/12/14210#recordstarted) |Recording started |
||[RecordStopped](https://docs.byteplus.com/en/docs/12/14210#recordstopped) |Recording stopped |
||[RecordUploadStarted](https://docs.byteplus.com/en/docs/12/14210#recorduploadstarted) |Uploading record started |
||[RecordUploadProcessing](https://docs.byteplus.com/en/docs/12/14210#recorduploadprocessing) |The process of uploading record |
||[RecordUploadDone](https://docs.byteplus.com/en/docs/12/14210#recorduploaddone) |Uploading record has been done |
||[RecordUploadBackuped](https://docs.byteplus.com/en/docs/12/14210#recorduploadbackuped) |Upload recording file failed and backed up |
||[RecordAudioStreamStateChanged](https://docs.byteplus.com/en/docs/12/14210#recordaudiostreamstatechanged) |The state of recording audio stream changed |
||[RecordVideoStreamStateChanged](https://docs.byteplus.com/en/docs/12/14210#recordvideostreamstatechanged) |The state of recording video stream changed |
||[RecordSyncUploadStarted(for RTC recording)](https://docs.byteplus.com/en/docs/12/14210#recordsyncuploadstarted-for-rtc-recording) |m3u8 file is generated and uploaded successfully. |
||[RecordSyncUploadFailed(for RTC recording)](https://docs.byteplus.com/en/docs/12/14210#recordsyncuploadfailed-for-rtc-recording) |m3u8 file is generated, but failed to be uploaded. |
||[RecordSyncUploadStarted(for WTN recording)](https://docs.byteplus.com/en/docs/12/14210#recordsyncuploadstarted-for-wtn-recording) |m3u8 file is generated and uploaded successfully. |
||[RecordSyncUploadFailed(for WTN recording)](https://docs.byteplus.com/en/docs/12/14210#recordsyncuploadfailed-for-wtn-recording) |m3u8 file is generated, but failed to be uploaded. |
|Room management |[UserJoinRoom](https://docs.byteplus.com/en/docs/12/14210#userjoinroom) |Visible user joined the room |
||[UserLeaveRoom](https://docs.byteplus.com/en/docs/12/14210#userleaveroom) |Visible user left the room |
||[InvisibleUserJoinRoom](https://docs.byteplus.com/en/docs/12/14210#invisibleuserjoinroom) |Invisible user joined the room |
||[InvisibleUserLeaveRoom](https://docs.byteplus.com/en/docs/12/14210#invisibleuserleaveroom) |Invisible user left the room |
||[RoleChangeInvisible2Visible](https://docs.byteplus.com/en/docs/12/14210#rolechangeinvisible2visible) |The role of user switched from the invisible to the visible) |
||[RoleChangeVisible2Invisible](https://docs.byteplus.com/en/docs/12/14210#rolechangevisible2invisible) |The role of user switched from the visible to the invisible) |
||[RoomCreate](https://docs.byteplus.com/en/docs/12/14210#roomcreate) |Room was created |
||[RoomDestroy](https://docs.byteplus.com/en/docs/12/14210#roomdestroy) |Room was destroyed |
|Push to CDN |[TranscodeStarted](https://docs.byteplus.com/en/docs/12/14210#transcodestarted) |Pushing stream to CDN started |
||[TranscodeStopped](https://docs.byteplus.com/en/docs/12/14210#transcodestopped) |Pushing stream to CDN stopped |
||[TranscodeUpdated](https://docs.byteplus.com/en/docs/12/14210#transcodeupdated) |Parameters of pushing stream to CDN updated |
||[TranscodeStateChanged](https://docs.byteplus.com/en/docs/12/14210#transcodestatechanged) |The state of pushing stream to CDN changed |
|Public stream |[PushPublicStream](https://docs.byteplus.com/en/docs/12/14210#pushpublicstream) |The state of public stream changed |
|Segment |[SegmentRealTimeData](https://docs.byteplus.com/en/docs/12/14210#segmentrealtimedata) |The result of a segment task |
|Snapshot |[SnapshotRealTimeData](https://docs.byteplus.com/en/docs/12/14210#snapshotrealtimedata) |The result of a snapshot task |
|Relay online media stream |[RelayStreamStateChanged](https://docs.byteplus.com/en/docs/12/14210#relaystreamstatechanged) |The state of relaying online media stream changed |
|Webrecord |[Webcast](https://docs.byteplus.com/en/docs/12/14210#webcast) |The state of relaying webpage content changed |
|WTN Stream |[WTNStreamStart](https://docs.byteplus.com/en/docs/12/14210#wtnstreamstart) |Pushing stream to WTN started |
|\-\-\- |[WTNStreamStop](https://docs.byteplus.com/en/docs/12/14210#wtnstreamstop) |Pushing the stream to WTN stopped |


<span id="useraudiostreamstart"></span>
## UserAudioStreamStart

<span id="eventtype"></span>
### EventType

`UserAudioStreamStart`

<span id="description"></span>
### Description

Audio stream started to push.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Timestamp": 1611736812853
}
```


<span id="useraudiostreamstop"></span>
## UserAudioStreamStop

<span id="eventtype"></span>
### EventType

`UserAudioStreamStop`

<span id="description"></span>
### Description

Audio stream stopped pushing.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Reason |String | |The reason for audio stream stopping pushing, see [Reason](https://docs.byteplus.com/en/docs/12/14210#reasonaudio). |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


 Reason


|Value |Description |
|---|---|
|StreamStop |Pushing stream terminated normally. |
|LeaveRoom |Pushing stream stopped because the user left the room. |
|BannedByAdmin |Pushing stream stopped because the user left the room because this stream is banned by the server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Reason": "StreamStop",
     "Timestamp": 1611736812853
}
```


<span id="uservideostreamstart"></span>
## UserVideoStreamStart

<span id="eventtype"></span>
### EventType

`UserVideoStreamStart`

<span id="description"></span>
### Description

Video stream started to push.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Timestamp": 1611736812853
}
```


<span id="uservideostreamstop"></span>
## UserVideoStreamStop

<span id="eventtype"></span>
### EventType

`UserVideoStreamStop`

<span id="description"></span>
### Description

Video stream stopped pushing.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Reason |String | |The reason for video stream stopping pushing, see [Reason](https://docs.byteplus.com/en/docs/12/14210#reasonvideo). |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


  Reason


|Value |Description |
|---|---|
|StreamStop |Pushing stream terminated normally. |
|LeaveRoom |Pushing stream stopped because the user left the room. |
|BannedByAdmin |Pushing stream stopped because the user left the room because this stream is banned by the server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Reason": "StreamStop",
     "Timestamp": 1611736812853
}
```


<span id="userscreenaudiostreamstart"></span>
## UserScreenAudioStreamStart

<span id="eventtype"></span>
### EventType

`UserScreenAudioStreamStart`

<span id="description"></span>
### Description

Screen audio stream started to push.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Timestamp": 1611736812853
}
```


<span id="userscreenaudiostreamstop"></span>
## UserScreenAudioStreamStop

<span id="eventtype"></span>
### EventType

`UserScreenAudioStreamStop`

<span id="description"></span>
### Description

Screen audio stream stopped pushing.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Reason |String | |The reason for screen audio streaming stopping pushing, see [Reason](https://docs.byteplus.com/en/docs/12/14210#reasonscreenaudio). |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


  Reason


|Value |Description |
|---|---|
|StreamStop |Pushing stream terminated normally. |
|LeaveRoom |Pushing stream stopped because the user left the room. |
|BannedByAdmin |Pushing stream stopped because the user left the room because this stream is banned by the server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Reason": "StreamStop",
     "Timestamp": 1611736812853
}
```


<span id="userscreenvideostreamstart"></span>
## UserScreenVideoStreamStart

<span id="eventtype"></span>
### EventType

`UserScreenVideoStreamStart`

<span id="description"></span>
### Description

Screen video stream started to push.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Timestamp": 1611736812853
}
```


<span id="userscreenvideostreamstop"></span>
## UserScreenVideoStreamStop

<span id="eventtype"></span>
### EventType

`UserScreenVideoStreamStop`

<span id="description"></span>
### Description

Screen video stream stopped pushing.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|UserId |String |`Your_UserId` |User ID. |
|DeviceType |String |`android`, `ios`, `web`, `mac`, `windows` |Device type. |
|Reason |String | |The reason for screen video stream stopping pushing, see [Reason](https://docs.byteplus.com/en/docs/12/14210#reasonscreenvideo). |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


 Reason


|Value |Description |
|---|---|
|StreamStop |Pushing stream terminated normally. |
|LeaveRoom |Pushing stream stopped because the user left the room. |
|BannedByAdmin |Pushing stream stopped because the user left the room because this stream is banned by the server. |


<span id="example"></span>
### Example

```json
{
     "RoomId": "Your_RoomId",
     "UserId": "Your_UserId",
     "DeviceType": "android",
     "Reason": "StreamStop",
     "Timestamp": 1611736812853
}
```


<span id="recordstarted"></span>
## RecordStarted

<span id="eventtype"></span>
### EventType

`RecordStarted`

<span id="description"></span>
### Description

Recording started.

No matter the task is started by calling OpenAPI or configuring automatic recording on the console, you will receive a notification that recording started, when a task begins.

<span id="eventdata"></span>
### EventData


|Parameter name |Type |Description |
|---|---|---|
|AppId |**String** |The only identifier for your audio & video app. |
|BusinessId |**String** |The Business identifier for your audio & video app. |
|TargetType |**Int** |`0` for RTC; `1` for WTN. |
|RoomId |**String** |The ID of the room. It's the only identifier of a room. `Null` for WTN. |
|TaskId |**String** |Task ID of recording. You must set the TaskId for each task. |
|Code |**Int32** |The status of task. Its values takes `0` or `1`. `0` means success, and `1` means failure. |
|ErrorMessage |**String** |Specific error message. When `Code`is not `0`, error message will be shown in `ErrorMessage`. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",    
    "TargetType": 0,
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Code": 0,
    "ErrorMessage": ""
}
```


<span id="recordstopped"></span>
## RecordStopped

<span id="eventtype"></span>
### EventType

`RecordStopped`

<span id="description"></span>
### Description

Recording stopped.

No matter the task is started by calling OpenAPI or configuring automatic recording on the console, you will receive a notification that recording started, when a task stopped.

<span id="eventdata"></span>
### EventData


|Parameter name |Type |Description |
|---|---|---|
|AppId |**String** |The only identifier for your audio & video app. |
|BusinessId |**String** |The Business identifier for your audio & video app. |
|TargetType |**Int** |`0` for RTC; `1` for WTN. |
|RoomId |**String** |The ID of the room. It's the only identifier of a room. `Null` for WTN. |
|TaskId |**String** |Task ID of recording. You must set the TaskId for each task. |
|Code |**Int32** |Task Status.<br><br><br>* `0`: Task completed. The recorded file has been successfully uploaded to the target storage platform.<br><br>* `1`: Task completed. The recorded file failed to be uploaded to the target storage platform and backed up.<br><br>* `2`: Task completed. The recorded file failed to be uploaded to the target storage platform, but succeeded to be backed up. |
|ErrorMessage |**String** |Specific error message. When `Code` is not `0`, error message will be shown in `ErrorMessage`. |
|RecordFileList |**Array of ** [RecordFile](https://docs.byteplus.com/en/docs/12/docs-115995#recordfile) |List of recorded audio & video files. |


> Note: If `Code = 0`, but the `RecordFileList`is empty and no recording file is generated, when recording ends, please contact technical support.


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "TargetType": 0,
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Code": 0,
    "ErrorMessage": "",
    "RecordFileList": [
        {
            "Vid": "Your_Vid",
            "ObjectKey": "TestObjectKey",
            "Duration": 57472,
            "Size": 5018305,
            "StartTime": 1611736812853,
            "StreamList": [
                {
                    "UserId": "TestUserId",
                    "StreamType": 0
                }
            ],
            "VideoCodec": "h264",
            "AudioCodec": "aac",
            "VideoWidth": 640,
            "VideoHeight": 360
        }
    ]
}
```


<span id="recorduploadstarted"></span>
## RecordUploadStarted

<span id="eventtype"></span>
### EventType

`RecordUploadStarted`

<span id="event-details"></span>
### Event Details

Uploading record started.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|TargetType |Int |`0` for RTC; `1` for WTN. | |
|RoomId |String |The ID of the room. It's the only identifier of a room. `Null` for WTN. | |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |The status of task. Its values takes `0` or `1`.<br><br><br>* `0`: Success.<br><br>* `1`: Failure. |
|ErrorMessage |String | |Specific error message. When Code is not `0`, ErrorMessage will display the specific error. |


<span id="example"></span>
### Example

```json
{
     "AppId": "Your_AppId",
     "BusinessId": "Your_BusinessId",
     "TargetType": 0,
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "Code": 1,
     "ErrorMessage": ""
}
```


<span id="recorduploadprocessing"></span>
## RecordUploadProcessing

<span id="eventtype"></span>
### EventType

`RecordUploadProcessing`

<span id="event-details"></span>
### Event Details

The progress of uploading record

> This callback will only occur when the upload process lasts for one minute or more. Upload is made every minute.


<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|TargetType |Int |`0` |`0` for RTC; `1` for WTN. |
|RoomId |String |`Your_roomID` |The ID of the room. It's the only identifier of a room. `Null` for WTN. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String | |Specific error message. When Code is not `0`, ErrorMessage will display the specific error. |
|progress |Int |`100` |A number between `0` and `10000`, the ratio of currently uploaded files to recorded files multiplied by `10000`. This number is constantly changing. After the recording is completed, the number reaches `10000`, indicating that uploading is done. |


<span id="example"></span>
### Example

```json
{
     "AppId": "Your_AppId",
     "BusinessId": "Your_BusinessId",
     "TargetType": 0,
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "Code": 1,
     "ErrorMessage": "",
     "progress": 100
}
```


<span id="recorduploaddone"></span>
## RecordUploadDone

<span id="eventtype"></span>
### EventType

`RecordUploadDone`

<span id="event-details"></span>
### Event Details

The recording file has been uploaded to the storage platform.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|TargetType |Int |`0` |`0` for RTC; `1` for WTN. |
|RoomId |String |`Your_roomID` |The ID of the room. It's the only identifier of a room. `Null` for WTN. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String | |Specific error message. When Code is not 0, ErrorMessage will display the specific error. |


<span id="example"></span>
### Example

```json
{
     "AppId": "Your_AppId",
     "BusinessId": "Your_BusinessId",
     "TargetType": 0,
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "Code": 1,
     "ErrorMessage": ""
}
```


<span id="recorduploadbackuped"></span>
## RecordUploadBackuped

<span id="eventtype"></span>
### EventType

`RecordUploadBackuped`

<span id="event-details"></span>
### Event Details

Upload recording file failed and backup

> TOS Bucket used for backup needs to enable version control to prevent files from being overwritten due to duplicate file names.


<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|TargetType |Int |`0` |`0` for RTC; `1` for WTN. |
|RoomId |String |`Your_roomID` |The ID of the room. It's the only identifier of a room. `Null` for WTN. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, its value can take `0` or `1`.<br><br>`0`: Success.<br><br>`1`: Failure. |
|ErrorMessage |String | |Specific error message. When Code is not `0`, ErrorMessage will display the specific error. |


<span id="example"></span>
### Example

```json
{
     "AppId": "Your_AppId",
     "BusinessId": "Your_BusinessId",
     "TargetType": 0,
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "Code": 1,
     "ErrorMessage": ""
}
```


<span id="recordaudiostreamstatechanged"></span>
## RecordAudioStreamStateChanged

<span id="eventtype"></span>
### EventType

`RecordAudioStreamStateChanged`

<span id="description"></span>
### Description

The state of recording audio stream changed.

The event does not apply to recording WTn streams.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|UserId |String |`Your_UserId` |ID of user. |
|StreamType |Int |`0` |Type of audio stream.<br><br><br>* `0`: Audio stream captured from microphone.<br><br>* `1`: Screen stream. |
|State |Int |`0` |Status of task.<br><br><br>* `0`: The stream stops publishing.<br><br>* `1`: The stream is publishing. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",    
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "UserId": "Your_UserId,
    "StreamType": 0,
    "State": 0,  
    "Timestamp": 1611736812853     
}
```


<span id="recordvideostreamstatechanged"></span>
## RecordVideoStreamStateChanged

<span id="eventtype"></span>
### EventType

`RecordVideoStreamStateChanged`

<span id="description"></span>
### Description

The state of recording video stream changed.

The event does not apply to recording WTn streams.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|UserId |String |`Your_UserId` |ID of user. |
|StreamType |Int |`0` |Type of video stream.<br><br><br>* `0`: Video stream captured from microphone.<br><br>* `1`: Screen stream. |
|State |Int |`0` |Status of task.<br><br><br>* `0`: The stream stops publishing.<br><br>* `1`: The stream is publishing. |
|Timestamp |Int64 |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",    
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "UserId": "Your_UserId",
    "StreamType": 0,
    "State": 0,  
    "Timestamp": 1611736812853     
}
```


<span id="recordsyncuploadstarted-for-rtc-recording"></span>
## RecordSyncUploadStarted(for RTC recording)

<span id="eventtype"></span>
### EventType

`RecordSyncUploadStarted`

<span id="event-details"></span>
### Event Details

An `m3u8` file was generated and uploaded to the specified storage platform.

This event is only triggered after the first successful upload.

<span id="eventdata"></span>
### EventData


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String |\- |The specific error message. When Code is not `0`, ErrorMessage will display the specific error |
|RecordFileList |Object |\- |List of recorded audio & video files. |


RecordFile


|Parameter Name |Type |Description |
|---|---|---|
|Vid |String |The unique identifier of the file on the Vod platform. You can find the corresponding file on the Vod platform according to the Vid. This parameter is only valid if you choose to store the configuration to the Vod platform. |
|ObjectKey |String |The full path of the file in the object storage platform, such as `abcefg123.mp4`. This parameter is only valid if you choose to configure storage to the object storage platform. |
|StartTime |uint64 |The UTC time when the recording starts in ms . |
|StreamList |Array of [Stream](https://docs.byteplus.com/en/docs/12/14210#stream1) |List of streams contained in the recording file. For WTN, it's the info of `TargetWTNStreams`. |
|VideoCodec |String |Video Recording Encoding Protocol |
|AudioCodec |String |Audio Recording Encoder |
|VideoWidth |Int |width of recorded video in px |
|VideoHeight |Int |Height of recorded video in px |


**Stream**

 &nbsp;


|Parameter Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Index |Uint32 |No |`0` |In custom layouts, `Index` is used to mark streams. Later, you will use `Index` in `Layout.regions.StreamIndex` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |The user ID, indicating the user to whom this stream belongs. |
|StreamType |Uint32 |No |`0` |The type of the stream, which can take the values `0` or `1`, with a default value of `0`. `0` indicates audio and video stream, `1` indicates screen stream. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Code": 0,
    "ErrorMessage": "",
    "RecordFileList": [
        {
            "Vid": "Your_Vid",
            "ObjectKey": "TestObjectKey",
            "StartTime": 1611736812853,
            "StreamList": [
                {
                    "UserId": "TestUserId",
                    "StreamType": 0
                }
            ],
            "VideoCodec": "h264",
            "AudioCodec": "aac",
            "VideoWidth": 640,
            "VideoHeight": 360
        }
    ]
}
```


<span id="recordsyncuploadfailed-for-rtc-recording"></span>
## RecordSyncUploadFailed(for RTC recording)

<span id="eventtype"></span>
### EventType

`RecordSyncUploadFailed`

<span id="event-details"></span>
### Event Details

An `m3u8` file was generated and failed to be uploaded to the specified storage platform.

<span id="eventdata"></span>
### **EventData**


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String |\- |The specific error message. When Code is not `0`, ErrorMessage will display the specific error |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",    
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Code": 1,
    "ErrorMessage": "Failed to upload the m3u8 file."
}
```


<span id="recordsyncuploadstarted-for-wtn-recording"></span>
## RecordSyncUploadStarted(for WTN recording)

<span id="eventtype"></span>
### EventType

`RecordSyncUploadStarted`

<span id="event-details"></span>
### Event Details

An `m3u8` file was generated and uploaded to the specified storage platform.

This event is only triggered after the first successful upload.

<span id="eventdata"></span>
### EventData


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|StreamId |String |`Your_StreamId` |The ID of WTN stream. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String |\- |The specific error message. When Code is not `0`, ErrorMessage will display the specific error |
|RecordFileList |Obetct |\- |List of recorded audio & video files. |


<span id="recordfile"></span>
### RecordFile


|Parameter Name |Type |Description |
|---|---|---|
|Vid |String |The unique identifier of the file on the Vod platform. You can find the corresponding file on the Vod platform according to the Vid. This parameter is only valid if you choose to store the configuration to the Vod platform. |
|ObjectKey |String |The full path of the file in the object storage platform, such as `abcefg123.mp4`. This parameter is only valid if you choose to configure storage to the object storage platform. |
|StartTime |uint64 |The UTC time when the recording starts in ms . |
|StreamList |Obetct |List of streams contained in the recording file. For WTN, it's the info of `TargetWTNStreams`. |
|VideoCodec |String |Video Recording Encoding Protocol |
|AudioCodec |String |Audio Recording Encoder |
|VideoWidth |Int |width of recorded video in px |
|VideoHeight |Int |Height of recorded video in px |


**StreamList**


|Parameter Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Index |Uint32 |No |`0` |In custom layouts, `Index` is used to mark streams. Later, you will use `Index` in `Layout.regions.StreamIndex` to specify the layout settings for the corresponding stream. |
|UserId |String |Yes |`Your_UserId` |The user ID, indicating the user to whom this stream belongs. |
|StreamType |Uint32 |No |`0` |The type of the stream, which can take the values `0` or `1`, with a default value of `0`. `0` indicates audio and video stream, `1` indicates screen stream. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "StreamId": "Your_StreamId",
    "Code": 0,
    "ErrorMessage": "",
    "RecordFileList": [
        {
            "Vid": "Your_Vid",
            "ObjectKey": "TestObjectKey",
            "StartTime": 1611736812853,
            "StreamList": [
                {
                    "UserId": "TestUserId",
                    "StreamType": 0
                }
            ],
            "VideoCodec": "h264",
            "AudioCodec": "aac",
            "VideoWidth": 640,
            "VideoHeight": 360
        }
    ]
}
```


<span id="recordsyncuploadfailed-for-wtn-recording"></span>
## RecordSyncUploadFailed(for WTN recording)

<span id="eventtype"></span>
### EventType

`RecordSyncUploadFailed`

<span id="event-details"></span>
### Event Details

An `m3u8` file was generated and failed to be uploaded to the specified storage platform.

**EventData**


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|StreamId |String |`Your_StreamId` |The ID of WTN stream. |
|TaskId |String |`Your_TaskId` |Task ID of recording. You must set the TaskId for each task. |
|Code |Int32 |`0` |Task status, the set of values is {0, 1}. Among them, `0` means success, `1` means failure. |
|ErrorMessage |String |\- |The specific error message. When Code is not `0`, ErrorMessage will display the specific error |


<span id="parameter-example"></span>
### Parameter Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",    
    "StreamId": "Your_StreamId",
    "TaskId": "Your_TaskId",
    "Code": 1,
    "ErrorMessage": "Failed to upload the m3u8 file."
}
```


<span id="userjoinroom"></span>
## UserJoinRoom

<span id="eventtype"></span>
### EventType

`UserJoinRoom`

<span id="description"></span>
### Description

Visible user joined the room.

When Users with the same UserId enter the room repeatedly, this callback will be triggered each time. It is recommended to deduplicate this callback.

> Note: For visible and invisible users, see [setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#RTCRoom-setuservisibility).


<span id="eventdata"></span>
### EventData


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|DeviceType |String |`android`/`ios`/`web`/`mac`/`windows` |Terminal type. |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |
|ExtraInfo |String |`Your_ExtraInfo` |User's extra information passed into by `joinRoom` |


<span id="example"></span>
### Example

```json
{
    "RoomId": "Your_RoomId",
    "UserId": "Your_UserId",
    "DeviceType": "android",
    "Timestamp": 1611736812853,
    "ExtraInfo": "Your_ExtraInfo"
}
```


<span id="userleaveroom"></span>
## UserLeaveRoom

<span id="eventtype"></span>
### EventType

`UserLeaveRoom`

<span id="description"></span>
### Description

Visible user left the room.

If users with the same UserId repeatedly logs in, resulting in the previous user being kicked out, the kicked\-out user will not trigger this callback. This callback will only be triggered when users finally leave the room.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|DeviceType |String |`android`/`ios`/`web`/`mac`/`windows` |Terminal type. |
|Reason |String |See [Reason](https://docs.byteplus.com/en/docs/12/14210#reason). | |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |
|Duration |Int |`20` |Duration of the user in the room. |


  Reason


|Value |Description |
|---|---|
|userLeave |Leave the room by themselves. |
|connectionLost |Leave the room due to exceptions such as failed network and killed process. |
|kickedByAdmin |Kick a user out of a room by calling the OpenAPI interface. |
|roomDismissByAdmin |Call the OpenAPI interface to dismiss the room and kick all users out of the room. |
|other |Other reasons. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "UserId": "4398491447867063",
    "DeviceType": "android",
    "Reason": "userLeave",
    "Timestamp": 1611736812853,
    "Duration": 20
}
```


<span id="invisibleuserjoinroom"></span>
## InvisibleUserJoinRoom

<span id="eventtype"></span>
### EventType

`InvisibleUserJoinRoom`

<span id="description"></span>
### Description

Invisible user joined the room.

When Users with the same UserId enter the room repeatedly, this callback will be triggered each time. It is recommended to deduplicate this callback.

<span id="eventdata"></span>
### EventData


|Parameters |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|DeviceType |String |`android`/`ios`/`web`/`mac`/`windows` |Terminal type. |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |
|ExtraInfo |String |`Your_ExtraInfo` |User's extra information passed into by `joinRoom` |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "UserId": "4398491447867063",
    "DeviceType": "android",
    "Timestamp": 1611736812853,
    "UserExtraInfo":"Your_UserExtraInfo",
    "ExtraInfo": "Your_ExtraInfo"
}
```


<span id="invisibleuserleaveroom"></span>
## InvisibleUserLeaveRoom

<span id="eventtype"></span>
### EventType

`InvisibleUserLeaveRoom`

<span id="description"></span>
### Description

Invisible user left the room.

If users with the same UserId repeatedly logs in, resulting in the previous user being kicked out, the kicked\-out user will not trigger this callback. This callback will only be triggered when users finally leave the room.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|DeviceType |String |`android`/`ios`/`web`/`mac`/`windows` |Terminal type. |
|Reason |String |See [Reason](https://docs.byteplus.com/en/docs/12/14210#reason2). | |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) when this event occurred on the RTC server. |
|Duration |Int |`20` |Duration of the user in the room. |


  Reason


|Value |Description |
|---|---|
|userLeave |Leave the room by themselves. |
|connectionLost |Leave the room due to exceptions such as failed network and killed process. |
|kickedByAdmin |Kick a user out of a room by calling the OpenAPI interface. |
|roomDismissByAdmin |Call the OpenAPI interface to dismiss the room and kick all users out of the room. |
|other |Other reasons. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "UserId": "4398491447867063",
    "DeviceType": "android",
    "Reason": "userLeave",
    "Timestamp": 1611736812853,
    "Duration": 20
}
```


<span id="rolechangeinvisible2visible"></span>
## RoleChangeInvisible2Visible

<span id="eventtype"></span>
### EventType

`RoleChangeInvisible2Visible`

<span id="description"></span>
### Description

Invisible user called `setUserVisibility` to switch the role into a visible one.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) for this event on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "UserId": "4398491447867063",
    "Timestamp": 1611736812853
}
```


<span id="rolechangevisible2invisible"></span>
## RoleChangeVisible2Invisible

<span id="eventtype"></span>
### EventType

`RoleChangeVisible2Invisible`

<span id="description"></span>
### Description

Visible user called `setUserVisibility` to switch the role into an invisible one.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RoomId |String |`6992870232038591758` |The ID of the room. It`s the only identifier of a room. \| |
|UserId |String |`4398491447867063` |ID of user. |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) for this event on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "UserId": "4398491447867063",
    "Timestamp": 1611736812853
}
```


<span id="roomcreate"></span>
## RoomCreate

<span id="eventtype"></span>
### EventType

`RoomCreate`

<span id="description"></span>
### Description

The RTC room was created.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) for this event on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "Timestamp": 1611736812853
}
```


<span id="roomdestroy"></span>
## RoomDestroy

<span id="eventtype"></span>
### EventType

`RoomDestroy`

<span id="description"></span>
### Description

The RTC room was destroyed, and all users left the room.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|Timestamp |Int |`1611736812853` |Unix timestamp (ms) for this event on the RTC server. |


<span id="example"></span>
### Example

```json
{
    "RoomId": "6992870232038591758",
    "Timestamp": 1611736812853
}
```


<span id="transcodestarted"></span>
## TranscodeStarted

<span id="eventtype"></span>
### EventType

`TranscodeStarted`

<span id="description"></span>
### Description

The task of pushing stream to CDN triggered either by calling server\-side OpenAPI or client\-side SDK API, has started.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|TaskId |String |`Your_TaskId` |Task ID of pushing stream to CDN. When initiating from the server side, this value is the TaskId passed in when calling the OpenAPI. When initiating from the client\-side SDK, the TaskId is formed by concatenating `userId` and `taskId` in the format of `userId`@@`taskId`. If the provided `taskId` is empty, the TaskId here will be the `userId`. |
|Timestamp |Int64 |`1661150097044` |Timestamp when the event occurred on the RTC server(ms). |
|PushURL |String |`rtmp://xxxx` |CDN address of the pushed stream. This parameter only takes effect for pushing mixed\-stream to CDN. |
|Code |Int |`0` |The result of operation.<br><br><br>* `0`: Successfully created the task.<br><br>* `1`: Failed to create the task. |
|ErrorMessage |String | |Specific error message. When `Code` takes `1`, ErrorMessage will show specific error message. |


<span id="example"></span>
### Example

```json
{
     "AppId":"Your_AppID",
     "BusinessId":"Your_BusinessId",   
    "RoomId":"Your_RoomID",
    "TaskId":"Your_TaskID",
    "Timestamp":1661150097044,
    "PushURL": "rtmp://xxxx", 
    "Code":0,
    "ErrorMessage":""
}
```


<span id="transcodestopped"></span>
## TranscodeStopped

<span id="eventtype"></span>
### EventType

`TranscodeStopped`

<span id="description"></span>
### Description

The task of pushing stream to CDN triggered either by calling server\-side OpenAPI or client\-side SDK API, has stopped.

> The task triggered by calling RTC Client SDK does not cause the event.


<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|TaskId |String |`Your_TaskId` |Task ID of pushing stream to CDN. When initiating from the server side, this value is the TaskId passed in when calling the OpenAPI. When initiating from the client\-side SDK, the TaskId is formed by concatenating `userId` and `taskId` in the format of `userId`@@`taskId`. If the provided `taskId` is empty, the TaskId here will be the `userId`. |
|Timestamp |Int64 |`1661150097044` |Timestamp when the event occurred on the RTC server(ms). |
|PushURL |String |`rtmp://xxxx` |CDN address of the pushed stream. This parameter only takes effect for pushing mixed\-stream to CDN. |
|Code |Int |`0` |The result of operation.<br><br><br>* `0`: Successfully stopped the task.<br><br>* `1`: Failed to stop the task. |
|ErrorMessage |String | |Specific error message. When `Code` takes `1`, ErrorMessage will show specific error message. |


<span id="example"></span>
### Example

```json
{
     "AppId":"Your_AppID",
     "BusinessId":"Your_BusinessId",   
    "RoomId":"Your_RoomID",
    "TaskId":"Your_TaskID",
    "Timestamp":1661150097044,
    "PushURL": "rtmp://xxxx", 
    "Code":0,
    "ErrorMessage":""
}
```


<span id="transcodeupdated"></span>
## TranscodeUpdated

<span id="eventtype"></span>
### EventType

`TranscodeUpdated`

<span id="description"></span>
### Description

The task of pushing stream to CDN has updated either by calling server\-side OpenAPI or client\-side SDK API.

> This callback only takes effect for pushing mixed stream to CDN.

> The task triggered by calling RTC Client SDK does not cause the event.


<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|TaskId |String |`Your_TaskId` |Task ID of pushing stream to CDN. When initiating from the server side, this value is the TaskId passed in when calling the OpenAPI. When initiating from the client\-side SDK, the TaskId is formed by concatenating `userId` and `taskId` in the format of `userId`@@`taskId`. If the provided `taskId` is empty, the TaskId here will be the `userId`. |
|Timestamp |Int64 |`1661150097044` |Timestamp when the event occurred on the RTC server(ms). |
|PushURL |String |`rtmp://xxxx` |CDN address of the pushed stream. |
|Code |Int |`0` |`0` |
|ErrorMessage |String | |Specific error message. When `Code` takes `1`, ErrorMessage will show specific error message. |


<span id="example"></span>
### Example

```json
{
    "AppId":"Your_AppID",
    "BusinessId":"Your_BusinessId", 
    "RoomId":"Your_RoomID", 
    "TaskId":"Your_TaskID",  
    "Timestamp":1661150055041,   
    "PushURL": "rtmp://xxxx", 
    "Code":0,
    "ErrorMessage":""
}
```


<span id="transcodestatechanged"></span>
## TranscodeStateChanged

<span id="eventtype"></span>
### EventType

`TranscodeStateChanged`

<span id="description"></span>
### Description

The state of pushing stream to CDN has changed either by actively calling server\-side OpenAPI or client\-side SDK API, or by transitions that occur during task executing.

<span id="eventdata"></span>
### EventData


|Parameter name |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|TaskId |String |`Your_TaskId` |Task ID of pushing stream to CDN. When initiating from the server side, this value is the TaskId passed in when calling the OpenAPI. When initiating from the client\-side SDK, the TaskId is formed by concatenating `userId` and `taskId` in the format of `userId`@@`taskId`. If the provided `taskId` is empty, the TaskId here will be the `userId`. |
|Timestamp |Int64 |`1661150097044` |Timestamp when the event occurred on the RTC server(ms). |
|StartTime |Int64 |`1661150054990` |Timestamp when the task is created on the RTC server(ms). |
|FinishTime |Int64 |`0` |Timestamp when the task is stopped on the RTC server(ms). |
|PushURL |String |`rtmp://xxxx` |CDN address of the pushed stream. This parameter only takes effect for pushing mixed\-stream to CDN. |
|TaskState |Int |`2` |Task status. The value takes `1`, `2`, `3` and `4`.<br><br><br>* `1`: Pushing streams has not started or has stopped.<br><br>* `2`: Task is reconnecting to the CDN service.<br><br>* `3`: Pushing streams is performing.<br><br>* `4`: The current address of pushed stream has changed. `ErrorMessage` will display previous and current address of pushed stream. |
|Code |Int |`0` |Error code. The value takes `0`, `1`, `2`, `3`, `4`, `5` or `9999`.<br><br><br>* `0`: Request succeeds.<br><br>* `1`: An error occurred in request parameter validation.<br><br>* `2`: An error occurred while subscribing to the audio and video stream published by the RTC user.<br><br>* `3`: An error occurred during task running.<br><br>* `4`: An error occurred while pushing to CDN<br><br>* `5`: There is no audio or video stream in the RTC room that needs to be subscribed to for a mixing\-stream task.<br><br>* `9999`: Other system exceptions. |
|ErrorMessage |String |\- |Specific error message. |
|OnStatusCode |String |\- |Error code returned by CDN when failed to pushing stream. |
|OnStatusDescription |String |\- |Error description returned by CDN when failed to pushing stream. |


<span id="example"></span>
### Example

```json
{
    "AppId":"Your_AppID",
    "BusinessId":"Your_BusinessId", 
    "RoomId":"Your_RoomID", 
    "TaskId":"Your_TaskID",  
    "Timestamp":1661150097044, 
    "StartTime":1661150054990,
    "FinishTime":0,   
    "PushURL": "rtmp://xxxx", 
    "TaskState":3,    
    "Code":0,
    "ErrorMessage":"",
    "OnStatusCode":"",
    "OnStatusDescription":""
}
```


<span id="pushpublicstream"></span>
## PushPublicStream

<span id="eventtype"></span>
### EventType

`PushPublicStream`

<span id="description"></span>
### Description

Exception or ending of public stream pushing

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|BusinessId |String |`Your_BusinessId` |The business identifier for your audio & video app. |
|PublicStreamId |String |`Your_PublicStreamId` |The Stream Id of the public stream |
|Timestamp |Int64 |`1661150097044` |Unix timestamp (ms) of the event occurring on the RTC server |
|Status |Int |`2` |The task status of public streams. Enumerated values are `{1,2,3}`.<br><br>`1`: Public stream pushed successfully<br><br>`2`: Public stream pushing ends<br><br>`3`: Public stream pushing is wrong |
|Msg |String |/ |Specific error message |
|Code |Int |`2` |Error code. Enumerated values are `{1，2，3}`.<br><br>`1`: Ends due to idle timeout.<br><br>`2`: Ends due to the call of OpenAPI.<br><br>`3`: Ends due to an internal error. |


<span id="sample-response"></span>
### Sample Response

```json
{
    "AppId":"Your_AppID", 
    "BusinessId":"Your_BusinessId",    
    "PublicStreamId":"Your_PublicStreamId", 
    "Timestamp":1661150097044, 
    "Status":2, 
    "Msg":"call api stop",     
    "Code":2
}
```


<span id="segmentrealtimedata"></span>
## SegmentRealTimeData

<span id="eventtype"></span>
### EventType

`SegmentRealTimeData`

<span id="description"></span>
### Description

The result of a segment task

<span id="eventdata"></span>
### EventData


|Parameter |Type |Description |
|---|---|---|
|AppId |String |The only identifier for your audio & video app. |
|BusinessId |String |The Business identifier for your audio & video app. |
|RoomId |String |The ID of the room. It‘s the only identifier of a room. |
|TaskId |String |ID of segment task. |
|Bucket |String |Bucket for storing segments. |
|Data |Array of [AudioData](https://docs.byteplus.com/en/docs/12/14210#audiodata) |Relevant parameters of audio segment. |
|Identifier |String |Flag of a task. If you don't customize a file's name, its name is UUID. |


  AudioData

Relevant parameters of audio segment.


|Parameter |Type |Description |
|---|---|---|
|Stream |[Stream](https://docs.byteplus.com/en/docs/12/14210#stream1) |Information of the stream corresponding to audio segment. |
|ObjectKey |String |TOS key corresponding to audio segment. |
|SampleRate |Int |`44100` |
|BitsPerSample |Int |`16` |
|Channels |Int |`2` |
|Size |Uint64 |The size of audio segment, in bytes. |
|TimeStamp |Uint64 |UNIX timestamp when audio segment is generated. |
|Duration |Uint32 |The duration of audio segment, in milliseconds. |


<span id="example"></span>
### Example

```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Bucket": "Your_Bucket",
    "Data": [
        {
            "Stream": {
                "UserId": "Your_UserId",
                "StreamType": 0
            },
            "ObjectKey": "Your_ObjectKey",
            "SampleRate": "44100",
            "BitsPerSample": "16",
            "Channels": "2",
            "Size": 256044,
            "TimeStamp": 1647317680214,
            "Duration": 8000
        }
    ], 
    "Identifier": "Your_Identifier" }
```


<span id="snapshotrealtimedata"></span>
## SnapshotRealTimeData

<span id="eventtype"></span>
### EventType

`SnapshotRealTimeData`

<span id="description"></span>
### Description

The result of a snapshot task

<span id="eventdata"></span>
### EventData


|Parameter |Type |Description |
|---|---|---|
|AppId |String |The only identifier for your audio & video app. |
|BusinessId |String |The Business identifier for your audio & video app. |
|RoomId |String |The ID of the room. It's the only identifier of a room. |
|TaskId |String |ID of snapshot task. |
|Bucket |String |Bucket to storing snapshots. |
|Data |Array of [ImageData](https://docs.byteplus.com/en/docs/12/14210#imagedata). |/ |


 ImageData


|Parameter |Type |Description |
|---|---|---|
|Stream |[Stream](https://docs.byteplus.com/en/docs/12/docs-115995#stream) |The snap shot stream. |
|ObjectKey |String |The ObjectKey for snapshot. |
|Format |Uint32 |The format of the snapshot: `JPEG`or `PNG`. |
|Width |Uint32 |Width of snapshot in px. |
|Height |Uint32 |Height of snapshot in px. |
|Size |Uint64 |Size of snapshot in byte. |
|TimeStamp |Uint64 |UNIX timestamp when a snapshot is generated. |


```json
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "Bucket": "Your_Bucket",
    "Data": [
        {
            "Stream": {
                "UserId": "Your_UserId",
                "StreamType": 0
            },
            "ObjectKey": "Your_ObjectKey",
            "Format": 0,
            "Width": 640,
            "Height": 360,
            "Size": 28802,
            "TimeStamp": 1647316896085
        }
    ]
}
```


<span id="webcast"></span>
## Webcast

<span id="eventtype"></span>
### EventType

`Webcast`

<span id="description"></span>
### Description

The state of relaying webpage content changed.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app. |
|RoomId |String |`Your_RoomId` |The ID of the room. It's the only identifier of a room, is the only sign of the room. |
|BusinessId |String |`Your_BusinessId` |The Business identifier for your audio & video app. |
|TaskId |String |`Your_TaskId` |Task ID. |
|Status |Int |`1` |Task status:<br><br><br>* `1`: start relaying<br><br>* `2`: terminate normally<br><br>* `3`: terminate abnormally<br><br>* `4`: refresh page<br><br>* `5`: reschedule the task (User pushing stream re\-enters the room). |
|Reason |String |/ |Description of terminating abnormally, only available when Status = {3,4,5}. THe value can take: `AudioCaptureModuleError`, `WebRstoperModuleError`, `SourceURLInaccessible`, `StartEventTimeout`, `PageBlank`, `PageCrash`, `PageFreeze`. |


<span id="example"></span>
### Example

```json
{
     "AppId": "Your_AppId",
     "BusinessId": "Your_BusinessId",
     "RoomId": "Your_RoomId",
     "TaskId": "Your_TaskId",
     "Status": 1
}
```


<span id="relaystreamstatechanged"></span>
## RelayStreamStateChanged

<span id="eventtype"></span>
### EventType

`RelayStreamStateChanged`

<span id="description"></span>
### Description

The status of relayed online media stream changed.

<span id="eventdata"></span>
### EventData


|Parameter |Type |Example |Description |
|---|---|---|---|
|RoomId |String |`Your_RoomId` |The ID of the room. It`s the only identifier of a room. \| |
|TaskId |String |`Your_TaskId` |Task ID. |
|UserId |String |`Your_UserId` |ID of relayed online media stream. |
|StreamUrl |String |`rtmp://xxx` |Url of online media stream. |
|Status |Int |`1` |Task Status:<br><br><br>* `1`: Standby.<br><br>* `2`: Connecting.<br><br>* `3`: Running.<br><br>* `4`: Stopped. |
|StartTimeStamp |Int |`0` |Start timestamp of task (Unix time), in seconds. This value is used for timing playback. Its default value is `0`, which means starting immediately. |
|Msg |String |/ |The message. |
|Reason |Int |`1` |`Reason` has a value only if `status`=`4`. The reason for task stopping:<br><br><br>* `1`: Idle timeout.<br><br>* `2`: `StopRelayStream` called.<br><br>* `3`: Stream playback stopped.<br><br>* `4`: Internal Error.<br><br>* `5`: Exception url address.<br><br>* `6`: Unsupported encoding format.<br><br>* `7`: `token` Error.<br><br>* `8`: No permission of publishing.<br><br>* `9`: Removed from the room. |


<span id="example"></span>
### Example

```json
    {
         "AppId": "Your_AppId",
         "EventId": "Your_eventId",
         "EventTime": "2021-08-17T19:22:02+08:00",
         "EventType": "RelayStreamStateChanged",
         "EventData": {
                 "RoomId": "Your_RoomId",
                 "TaskId": "Your_TaskId",
                 "UserId": "Your_UserId",
                 "StreamUrl": "rtmp://xxx",
                 "Status": 1,
                 "StartTimeStamp": 0,
                 "Msg": "",
                 "Vid": "xxxxvvv",
                 "Reason": 4
         },
}
```


<span id="wtn-stream"></span>
## WTN Stream

<span id="wtnstreamstart"></span>
### WTNStreamStart

**EventType**

`WTNStreamStart`

**Event Details**

Pushing stream to WTN started.

**EventData**


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|streamId |String |`stream1` |Stream ID |
|sourceProtocol |String |`RTMP` |Stream protocol. Valid values are: `RTMP` or `WHIP`. |
|startPushTime |Int64 |`1611736812853` |Stream pushing start time in UTC format, in milliseconds. |


**Parameter Example**

```json
{
    "streamId": "stream1",
    "sourceProtocol": "RTMP",
    "startPushTime": 1611736812853
}
```


<span id="wtnstreamstop"></span>
### WTNStreamStop

**EventType**

`WTNStreamStop`

**Event Details**

Pushing stream to WTN stopped.

**EventData**


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|streamId |String |`stream1` |Stream ID |
|sourceProtocol |String |`RTMP` |Stream protocol. Valid values are: `RTMP` or `WHIP`. |
|startPushTime |Int64 |`1611736812853` |Stream pushing start time in UTC format, in milliseconds. |
|stopPushTime |Int64 |`1611736815431` |Stream pushing stop time in UTC format, in milliseconds. |
|reason |Int |`430` |Stream pushing stop status code. See [reason](https://docs.byteplus.com/en/docs/12/14210#reasonwtn) for details. |


<span id="reason"></span>
### reason

 &nbsp;


|Status Code |Description |
|---|---|
|`430` |Streams with the same stream ID kick each other out. |
|`445` |The underlying connection is disconnected. |
|`446` |FFmpeg exits due to an error. |
|`447` |No transcoded data is received after timeout. |
|`448` |The stream format is H.265. |
|`449` |B \- frames are detected. |
|`450` |Process exception. |
|`0` |Other reasons. |


**Parameter Example**

```json
{
    "streamId": "stream1",
    "sourceProtocol": "RTMP",
    "startPushTime": 1611736812853,
    "stopPushTime": 1611736815431,
    "reason": 430
}
```

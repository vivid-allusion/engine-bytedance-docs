---
title: "StartRecord"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/startrecord-wtn"
---

In a WTN application, you can use cloud recording to record the published media streams.

<span id="description"></span>
## Description

You can call the `StartRecord` interface to record according to your configuration, including setting single\-stream or mixing\-stream recording mode, layout, and parameters of audio or video files.

You can choose either single\-stream or mixing\-stream recording as the recording mode.


* Single\-stream recording: You can record each stream separately as an audio or video file. In this mode, you cannot set the layout, and the resolution of the recorded file is determined by the original video and can't be modified. The height of the recorded file is the ever\-biggest height resolution of the original video, and so is the width. For example, if resolution of the original video changes from `1920*1080` to `1080*1920` during recording, the resolution of the recorded file is `1920*1920`.

* Mixing\-stream recording: You can mix the specified streams and record in an audio or video file. In this mode, you can set the video layout, resolution, frame rate, bit rate, etc.


You need to set the storage space to store the recording results on a storage platform. Now BytePlus VOD, Amazon S3, Alibaba Cloud, HUAWEI CLOUD OBS, Tencent Cloud COS and Qiniu Cloud Kodo are supported. You can also configure storage space and file format on the [Console](https://console.byteplus.com/rtc/workplaceRTC)

If you have enabled the message notification for starting recording, you can receive callback notifications when cloud recording starts. For message notification service, see [Enable Message Notification](https://docs.byteplus.com/en/docs/12/docs-75110).

<span id="prerequisites"></span>
## Prerequisites

Before starting recording, you must enable this function on [RTC console](https://console.byteplus.com/rtc/cloudRTC).

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the API, see [Call OpenAPI](https://docs.byteplus.com/en/docs/12/docs-69828).

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
|Action |String |Yes |`StartRecord` |API name. The value of this API: `StartRecord` |
|Version |String |Yes |`2022-06-01` |API version. The value of this API: `2022-06-01` |


<span id="body"></span>
#### Body


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|AppId |String |Yes |`Your_AppId` |The only identifier for your WTN app |
|BusinessId |String |No |`Your_BusinessId` |The Business identifier for WTN app |
|TargetType |Uint32 |Yes |`1` |`1` for WTN streams. |
|TargetWTNStreams |[WTNStreamList](https://docs.byteplus.com/en/docs/12/docs-115995#wtnstreamlist) |No |\- |You can use this parameter to set streams to be recorded. The maximum number of streams recorded is 5 in single\-stream recording. When you use an empty list, you are not recording any WTN stream. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of cloud recording. You must set a different `TaskId` for each task under the same `AppID`. |
|RecordMode |Uint32 |No |`1` |Use this parameter to set the recording mode: Single\-stream or mixing\-stream recording.<br><br>`0`: mixing\-stream recording,<br><br>`1`: single\-stream recording.<br><br>The default value is `0`. |
|Encode |[Encode](https://docs.byteplus.com/en/docs/12/docs-115995#wtnencode) |No |\- |Audio & video encoding parameters.<br><br>For single\-stream recording, you can set `VideoFps`, `VideoBitrate` and audio parameters.<br><br>For mixing stream recording, you can set `VideoWidth`, `VideoHeight`, `VideoFps`, `VideoBitrate` and audio parameters. |
|Layout |[Layout](https://docs.byteplus.com/en/docs/12/docs-115995#wtnlayout) |No |\- |Layout parameters. It's valid only in mixing\-stream mode. |
|Control |[Control](https://docs.byteplus.com/en/docs/12/docs-115995#control) |No |\- | |
|FileFormatConfig |[FileFormatConfig](https://docs.byteplus.com/en/docs/12/docs-115995#fileformatconfig) |No |\- |Configuration about the format of recording file |
|FileNameConfig |[FileNameConfig](https://docs.byteplus.com/en/docs/12/docs-115995#filenameconfig) |No |\- |Configuration about the name of recording file. See [the rule of file name](https://docs.byteplus.com/en/docs/12/24852#theruleoffilename) |
|StorageConfig |[StorageConfig](https://docs.byteplus.com/en/docs/12/docs-115995#storageconfig) |No |\- |Configuration about storage platform. Now BytePlus VOD, Amazon S3, Alibaba Cloud, HUAWEI CLOUD OBS, Tencent Cloud COS, Qiniu Cloud Kodo and Google Cloud Storage are supported. |


<span id="the-rule-of-file-name"></span>
#### The rule of file name

 &nbsp;

The name of the file name is jointly determined by [StorageConfig.Type](https://docs.byteplus.com/en/docs/12/docs-115995#storageconfig) and [FileNameConfig](https://docs.byteplus.com/en/docs/12/docs-115995#filenameconfig).


* When `StorageConfig.Type` is equal to `1`, the file will be stored in the Vod platform. The file name consists of `FilenameConfig.Pattern` + random number.

* When the `StorageConfig.Type` is equal to `2`, the file will be stored on a third\-party storage platform. The file name consists of `FilenameConfig.Prefix` + `FilenameConfig.Pattern` + random number.


To customize `FilenameConfig.Pattern`, see [Custom Recording Name](https://docs.byteplus.com/en/docs/12/docs-106873). If you set `Pattern`, you need to ensure the uniqueness of the output file's name, or files with the same name will be overwritten. You can also enable version control for your bucket to support Support duplicate file names.

For example, when `StorageConfig.Type` is equal to `1`, `FilenameConfig.Pattern` is set to `{TaskId}_{RoomId}_{StartTime}_{Duration}`,

`TaskId` = `Your_TaskId`, `Your_StreamId` = `Your_StreamId`, `StartTime` = `1645769481126`, `Duration` = `30s`, and the random number is `c4694fa1`, the file name is: `Your_TaskId_Your_StreamId_1645769481126_000030_c4694fa1.mp4`.

When `StorageConfig.Type` is equal to `2`, `FilenameConfig.Prefix` is set to `directory1/directory2/`, `FilenameConfig.Pattern` is set to `{TaskId}_{RoomId}_{StartTime}_{Duration}`,

`TaskId` = `Your_TaskId`, `Your_StreamId` = `Your_StreamId`, `StartTime` = `1645769481126`, `Duration` = `30s`, and the random number is `c4694fa1`, the file name is: `directory1/directory2/Your_TaskId_Your_StreamId_1645769481126_000030_c4694fa1.mp4`.

<span id="request-sample-code"></span>
### Request sample code

<span id="query"></span>
#### Query

```json
https://open.byteplusapi.com?Action=StartRecord&Version=2022-06-01
```


<span id="body"></span>
#### Body

```json
{
    "AppId": "663e",
    "BusinessId": "",
    "TaskId": "test_id",
    // WTN stream
    "TargetType": 1,
    // Single-stream recording
    "RecordMode": 1,
    "TargetWTNStreams": {
        "WTNStreamList": [
            // 5 streams
            { "Index": 0, "StreamId": "lf_psid_9877" },
            { "Index": 1, "StreamId": "lf_psid_9878" },
            { "Index": 2, "StreamId": "lf_psid_9879" },
            { "Index": 3, "StreamId": "lf_psid_9880" },
            { "Index": 4, "StreamId": "lf_psid_9881" }
        ]
    },
    "Control": {
        "MaxIdleTime": 120,
        "MediaType": 0,
        "FrameInterpolationMode": 1
    },
    "Encode": {
        "VideoFps": 30,
        "VideoBitrate": 1200
    },
    "FileFormatConfig": {
        "FileFormat": [
            "mp4"
        ]
    },
    "StorageConfig": {
        // VoD
        "Type": 1,
        "VodConfig": {
            "AccountId": "Your_AccountId",
            "Space": "Your_Space"
        }
    }
}
```


<span id="response"></span>
## Response

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="sample-response"></span>
### Sample response

```json
{
    "Result":"ok",
    "ResponseMetadata":
    {
        "RequestId":"427876ef-f965",
        "Action":"StartRecord",
        "Version":"2022-06-01"
    }
}
```

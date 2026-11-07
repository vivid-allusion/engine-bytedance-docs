---
title: "StartRelayStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105188"
---

Relay online media streams into the RTC room for remote users to enjoy.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `StartRelayStream` interface and specify the `AppId`to relay online media streams into a room.

If the state of an online media stream changes, the url address you specified on the RTC [console](https://console.byteplus.com/rtc) will receive a message callback from the RTC server. Information about related events will be contained in the callback field. For details about the callback result, see [RelayStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-75125#relaystreamstatechanged).

<span id="requirements"></span>
## Requirements


* Prerequisites：You have enabled the media streaming on the [RTC console](https://console.byteplus.com/rtc/cloudRTC?tab=onlineStream).

* Limitations: Each task expires in 72 hours after it starts. You will get notification via the callback when the task is stopped.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartRelayStream&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartRelayStream` |Interface name. The value of this interface: `StartRelayStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The only identifier for your audio & video app. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|BusinessId |String |No |`busin****12345` |The unique identifier for your business within the audio & video application. This field helps in distinguishing different business units or services under the same app. |
|RoomId |String |Yes |`room_12345` |The unique identifier of the RTC room where the online media stream will be relayed. |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|UserId |String |Yes |`Your_UserId` |ID of relayed online media stream. |
|MaxIdleTime |Integer |No |`300` |The max idle time for the task. The task will automatically stop after the idle time exceeds the set value. The range of values is [5,600], in seconds. The default value is `300`. |
|Token |String |Yes |`You****ken` |The `Token` value used for authentication when the client communicates with the server. |
|Control |Object of [StreamControl](https://docs.byteplus.com/en/docs/12/14266#streamcontrol) |Yes |`/` |Control Options. |


<span id="streamcontrol"></span>
### StreamControl


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|StreamUrl |String |Yes |`rtmp://xxx` |Url of online media stream. The format must be hls, rtmp, mp4, flv, dash, ts or mp3. |
|MediaType |Integer |No |`0` |Media type.<br><br><br>* 0: By default. Audio & Video<br><br>* 1: Audio. The audio must be encoded with AAC or Opus.<br><br>* 2: Video |
|StreamMode |Integer |No |`0` |Stream processing mode. The default value is `0`. Supported values are as follows.<br><br><br>* `0`: Transcode. The video must be encoded with H.264 or ByteVC1.<br><br>* `1`: Encapsulate. The video must be encoded with H.264. |
|StartTimeStamp |Integer |No |`0` |Unix timestamp of the beginning of a task, used for timed playback, in seconds. The default is `0`, which means that the task starts immediately. This parameter only takes effect for the `StartRelayStream` interface. |
|Loop |Boolean |No |`False` |Whether to loop. This parameter only takes effect when the source stream is an on\-demand one. |
|VideoWidth |Integer |No |`640` |Video width. It’s required when transcoding. The unit is px, and the range is [16, 1920]. It must be an even number, and it is automatically adjusted to an even number when the value is an odd number. |
|VideoHeight |Integer |No |`480` |Video height. It‘s required for transcoding. The unit is px, and the range is [16, 1920]. It must be an even number, and it is automatically adjusted to an even number when the value is an odd number. |
|FrameRate |Integer |No |`15` |Frame rate sent. The range is [1, 30], and the default value is`15`. It takes effect when transcoding. |
|Bitrate |Integer |No |`6000` |The Maximum of bit rate sent, in Kbps. If not filled, there is no limit. It takes effect when transcoding. |
|Volume |Integer |No |`100` |The volume of the online media stream playback, in percentage. The range is `[0, 400]`.<br><br><br>* `0`: Mute<br><br>* `100` (default): Original volume<br><br>* `400`: 4 times the original volume. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StartRelayStream&Version=2020-12-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "UserId": "Your_UserId",
    "Token": "You****ken",
    "MaxIdleTime": 300,
    "Control": {
        "StreamUrl": "rtmp://xxx",
        "MediaType": 0,
        "StreamMode": 0,
        "StartTimeStamp": 0,
        "Loop": false,
        "VideoWidth": 640,
        "VideoHeight": 480,
        "FrameRate": 15,
        "Bitrate": 6000
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartRelayStream",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": "ok"
}
```


&nbsp;

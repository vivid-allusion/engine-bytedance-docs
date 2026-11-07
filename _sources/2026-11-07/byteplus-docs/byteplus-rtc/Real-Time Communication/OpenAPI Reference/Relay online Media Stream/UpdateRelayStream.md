---
title: "UpdateRelayStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-105189"
---

After you relay an online media stream, you can update the url adress of this media stream to relay a new media stream.

<span id="usage-scenario"></span>
## Usage scenario

You can call the `UpdateRelayStream` interface to update the url address of the relayed media stream.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=UpdateRelayStream&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRelayStream` |Interface name. The value of this interface: `UpdateRelayStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`661e****543cf` |The AppId for your application.<br><br>Must be the same AppId that was used to start the task. See [get the AppId](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid). |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. |
|TaskId |String |Yes |`Your_TaskId` |Task ID of the relayed online media stream. |
|Control |Object of [StreamControl](https://docs.byteplus.com/en/docs/12/14267#streamcontrol) |Yes |`/` |Control Options |


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
POST https://open.byteplusapi.com?Action=UpdateRelayStream&Version=2020-12-01
{
    "AppId": "You****pId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
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
        "Action": "UpdateRelayStream",
        "Version": " 2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": "ok"
}
```

---
title: "StartPushSingleStreamToCDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153583"
---

In an audio and video application, you can push a stream to the specified CDN address through the RTMP protocol

You can use `StartPushSingleStreamToCDN` to do this.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A taskId can't start a mixed\-stream and single\-stream task at the same time.</div>


* <div data-tips="true" data-tips-type="tip">Calling this API <strong>will encode audio streams</strong>, the auido encoding protocol is fixed to <code>aac</code>, the audio channel is fixed to dual channel, and audio sample rate is fixed to <code>44100</code>.</div>


* <div data-tips="true" data-tips-type="tip">Calling this API <strong>will not encode video streams</strong>, video streams pushed to RTMP will change depending on the behavior of the stream publisher including resolution change, encoding method, and on/off status of the camera.</div>


* <div data-tips="true" data-tips-type="tip">When using the OpenAPI, it is recommended to set the orientation of the captured video frame to fixed on the mobile terminal. For more details, see API documentation:</div>


   * <div data-tips="true" data-tips-type="tip">Android: <a href="https://docs.byteplus.com/en/docs/12/docs-70080#setvideoorientation">setVideoOrientation</a></div>


   * <div data-tips="true" data-tips-type="tip">iOS: <a href="https://docs.byteplus.com/en/docs/12/docs-70086#setvideoorientation">setVideoOrientation:</a></div>



<span id="usage-scenario"></span>
## Usage scenario

You can call the `StartPushSingleStreamToCDN` interface to push the specified audio or video stream in the specified room to the specified address.

When the status of a single\-stream task changes, the url address you specified on the RTC [console](https://console.byteplus.com/rtc) will receive a message callback from the RTC server. Information about related events will be contained in the callback field. For details about the callback result, see [TranscodeStarted](https://docs.byteplus.com/en/docs/12/docs-75125#transcodestarted).

<span id="requirements"></span>
## Requirements

Before using the function, you need to go to [console](https://console.byteplus.com/rtc) to enable Push to CDN service.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartPushSingleStreamToCDN&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartPushSingleStreamToCDN` |Interface name. The value of this interface: `StartPushSingleStreamToCDN` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_****nessId` |The Business identifier for your audio & video app |
|RoomId |String |Yes |`Your_RoomId` |The ID of the room. It's the only identifier of a room |
|TaskId |String |Yes |`Your_TaskId` |Custom an ID for this task.<br><br>It is defined, generated and maintained by you, and supports combinations of uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.) and @, with a maximum length of 128 characters.<br><br>The `TaskId` is the identifier of the task. Under a RoomId of an AppId, the TaskId is unique. The TaskId can be repeated under different AppId or different RoomId. Therefore, AppId + RoomId + TaskId is the unique identifier of the task, which can be used to identify the running task in a certain room under the specified AppId, so that this task can be updated or stopped during the running of this task. |
|Stream |Object of [SingleStream](https://docs.byteplus.com/en/docs/12/14223#singlestream) |Yes |`/` |Streams to be pushed to CDN in the room |
|PushURL |String |Yes |`rtmp://xxx/xxx` |Push URL. Only rtmp protocol is supported. |
|Control |Object of [SingleControl](https://docs.byteplus.com/en/docs/12/14223#singlecontrol) |Yes |`/` |Configuration Options |


<span id="singlestream"></span>
### SingleStream


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|UserId |String |No |`Your_UserId` |UserId, indicating the user who publishes this stream |
|StreamType |Integer |No |`0` |The type of stream, the value can take `0` or `1`, and the default value is `0`.<br><br><br>* `0`: audio and video stream<br><br>* `1`: screen stream. |


<span id="singlecontrol"></span>
### SingleControl


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|MediaType |Integer |No |`0` |The type of stream, used to globally control the type of subscribed stream. The default value is `0`, and it can take `0` or `1`.<br><br><br>* `0`: Audio and video.<br><br>* `1`: Audio.<br><br>   Pure video is not supported yet. When the value is invalid, it is automatically adjusted to the default value. |
|MaxIdleTime |Integer |No |`180` |The idle timeout time of the task. After this time, the task will be terminated automatically. It's unit is second. The value ranges from `[10, 86400]`, and the default value is `180`. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StartPushSingleStreamToCDN&Version=2020-12-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "PushURL": "rtmp://xxx/xxx",
    "Stream": {
        "UserId": "Your_UserId",
        "StreamType": 0
    },
    "Control": {
        "MediaType": 0,
        "MaxIdleTime": 180
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartPushSingleStreamToCDN",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;

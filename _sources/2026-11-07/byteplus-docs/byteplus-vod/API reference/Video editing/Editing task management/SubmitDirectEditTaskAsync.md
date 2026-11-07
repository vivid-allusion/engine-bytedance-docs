---
title: "SubmitDirectEditTaskAsync"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitdirectedittaskasync"
---

Call `SubmitDirectEditTaskAsync` to submit the asynchronous video editing task.

<span id="usage-scenario"></span>
## Usage scenario

This API operates in direct editing mode, suitable for one\-time video editing scenarios with no need to save or reuse editing configurations. You can pass the `EditParam` parameter containing all editing information, including multiple tracks, materials, special effects, and transitions. The system performs asynchronous synthesis on the backend.

After submitting the task, you can monitor the task status and obtain result through the following methods:


* Call [GetDirectEditProgress](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditprogress) to check the task progress.

* Call [GetDirectEditResult](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditresult) to obtain the detailed result of the task.


<span id="requirements"></span>
## Requirements


* Pricing: The amount you are charged for video editing is calculated based on the resolution and duration of output files. For details, please refer to [Pay-as-you-go pricing](https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing#video-editing).

* To obtain the playback URL of the task, please complete the following steps before submitting the editing task:

   * [Adding and configuring domain name](https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring).

   * Enable [Auto-publishing after uploading](https://docs.byteplus.com/en/docs/byteplus-vod/docs-publishing-status#auto-publishing-after-uploading) within the space.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=SubmitDirectEditTaskAsync&Version=2025\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`SubmitDirectEditTaskAsync` |The API action. For the current API, the value is `SubmitDirectEditTaskAsync`. |
|Version |String |Yes |`2025-01-01` |The API version. For the current API, the value is `2025-01-01`. |


#{.custom\-md\-table\-5}#

<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Uploader |String |Yes |`edit_space` |The upload space for output video. |
|Application |String |Yes |`VideoTrackToB` |The editing task type. Only `VideoTrackToB` is supported. |
|EditParam |JSON Map |Yes |`-` |For details, see [Editing params](https://docs.byteplus.com/en/docs/byteplus-vod/editing_videos_via_openapi). |
|Priority |Integer |No |`0` |The editing task priority is set to 0 by default. The higher the priority, the faster the task will be executed. |
|CallbackArgs |String |No |`YourCallbackArgs` |A customizable field that will be returned in the event. The length limit is 64 KB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If your custom field exceeds 100 B, please <a href="https://console.byteplus.com/workorder/create">create a ticket</a> to contact technical support for configuration.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ReqId |String |`3b5fece1a47******443a6aeea5abc` |The asynchronous editing task ID |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="请求示例"></span>
## Sample request

```json
POST https://vod.byteplusapi.com?Action=SubmitDirectEditTaskAsync&Version=2025-01-01
{
    "Application": "VideoTrackToB",
    "CallbackArgs": "",
    "Uploader": "edit_space",
    "CreateAt": "2022-02-28T16:38:49+08:00",
    "EditParam": {
        "Canvas": {
            "Height": 2160,
            "Width": 3840
        },
        "Output": {
            "Alpha": false,
            "Codec": {
                "AudioBitrate": 128,
                "AudioCodec": "aac",
                "Crf": 23,
                "Preset": "slow",
                "VideoCodec": "h264"
            },
            "DisableAudio": false,
            "DisableVideo": false,
            "Fps": 30
        },
        "Track": [
            [
                {
                    "TargetTime": [
                        0,
                        195000
                    ],
                    "Type": "video"
                }
            ]
        ],
        "Upload": {
            "SpaceName": "edit_tob",
            "VideoName": "test",
            "FileName": "demo/.mp4"
        },
        "Uploader": "edit_tob"
    }
}
```


<span id="返回示例"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220228******09170404E144",
        "Action": "SubmitDirectEditTaskAsync",
        "Version": "2025-01-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ReqId": "3b5fece1a47******443a6aeea5abc"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|500 |1000 |\- |Internal error. |
|500 |1001 |\- |Database write error. |
|400 |1010 |\- |Parameter error. |
|500 |1014 |\- |The downstream service error. |


#{.custom\-md\-table\-4}#

&nbsp;

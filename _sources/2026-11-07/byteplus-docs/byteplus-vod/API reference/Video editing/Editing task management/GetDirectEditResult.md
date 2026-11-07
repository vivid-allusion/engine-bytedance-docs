---
title: "GetDirectEditResult"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getdirecteditresult"
---

Call `GetDirectEditResult` to obtain the result of an asynchronous video editing task through the `ReqId` (task ID).

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=GetDirectEditResult&Version=2025\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetDirectEditResult` |The API action. For the current API, the value is `GetDirectEditResult`. |
|Version |String |Yes |`2025-01-01` |The API version. For the current API, the value is `2025-01-01`. |


#{.custom\-md\-table\-5}#

<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ReqIds |Array of String |Yes |`["e0102ae2104a4953af14f83b3f8******"]` |The task ID list. You can obtain by calling the [SubmitDirectEditTaskAsync](https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitdirectedittaskasync).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The number of <code>ReqId</code>s must not exceed 30.</div><br> |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Result |Array of [Result](https://docs.byteplus.com/en/docs/25/77457#result) |`-` |The task ID of the asynchronous video editing task. |


#{.custom\-md\-table\-4}#

<span id="result"></span>
### Result


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Uploader |String |`tob-devide-5555` |The upload space for output video. |
|EditParam |Object of [EditParam](https://docs.byteplus.com/en/docs/25/77457#editparam) |`-` |For more details, see [Editing params](https://docs.byteplus.com/en/docs/byteplus-vod/editing_videos_via_openapi). |
|CallbackUri |String |`-` |The callback URI after the task is complete. |
|CallbackArgs |String |`-` |Custom field. It will be transparently returned in the callback. |
|Priority |Integer |`0` |The priority of the video editing tasks. |
|ReqId |String |`29276c7e3aa74dc4b281c64c****4a85` |The request ID of the task. |
|Status |String |`success` |The execution status of the task. Valid values are as follows:<br><br><br>* `pending`: The task is waiting to be processed.<br><br>* `start`: The task has started processing.<br><br>* `success`: The task has completed successfully.<br><br>* `failed_run`: The task failed.<br><br>* `user_canceled`: The user has canceled the task. |
|Message |String |`Video editing test.` |Task information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Message</code> parameter may generate task error information. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/byteplus-vod/video_editing_error_codes">Video editing error codes</a>.</div><br> |
|OutputVid |String |`v0d5a8g10001***90ebbi8datoks0` |The video ID of the output video. |
|TaskId |String |`367:kAtJNGI****p:default_tob` |The execution ID of the task. |
|Application |String |`VideoTrackToB` |The type of the editing task. The value is `VideoTrackToB`. |
|CreateAt |String |`2022-02-28T16:38:49+08:00` |The creation time of the task in RFC3339 format. |
|FinishAt |String |`2022-02-28T16:39:42+08:00` |The completion time of the task in RFC3339 format. |
|TaskList |String |`async_default` |The task list for throttling. The typical value is `async_default`. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
POST https://vod.byteplusapi.com?Action=GetDirectEditResult&Version=2025-01-01
{
    "ReqIds": [
        "e0102ae2104a4953af14f83b3f8******"
    ]
}
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetDirectEditResult",
        "Version": "2025-01-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": [
        {
            "Uploader": "tob-devide-5555",
            "CallbackUri": "",
            "CallbackArgs": "",
            "Priority": 0,
            "ReqId": "29276c7e3aa74dc4b281c64c****4a85",
            "Status": "success",
            "Message": "Video editing test.",
            "OutputVid": "v0d5a8g10001***90ebbi8datoks0",
            "TaskId": "367:kAtJNGI****p:default_tob",
            "Application": "VideoTrackToB",
            "CreateAt": "2022-02-28T16:38:49+08:00",
            "FinishAt": "2022-02-28T16:39:42+08:00",
            "TaskList": "async_default"
        }
    ]
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|500 |1000 |\- |Internal error. |
|500 |1001 |\- |The database write error. |
|400 |1010 |\- |Parameter error. |
|500 |1014 |\- |The downstream service error. |


#{.custom\-md\-table\-4}#

&nbsp;

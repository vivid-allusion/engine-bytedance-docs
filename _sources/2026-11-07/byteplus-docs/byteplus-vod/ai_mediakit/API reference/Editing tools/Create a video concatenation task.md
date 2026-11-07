---
title: "Create a video concatenation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/concat-video`

To programmatically combine multiple videos into a single file, use this API to submit an asynchronous concatenation task. You can join up to 100 video clips in a specified order and apply transition effects at the joins to create a seamless final video.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-concatenation">Audio and video concatenation</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_urls` |Array |Yes |`["https://example.com/video1.mp4", "https://example.com/video2.mp4"]` |The list of video URLs to be concatenated.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Quantity limit**: A single task supports 1 to 100 URLs.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported.<br><br>* **Output resolution**: When you input multiple videos with inconsistent resolutions, the output resolution matches that of the first video in the list. |
|`transitions` |Array |No |`["1182358", "1182360"]` |The list of transition effect IDs between videos. By default, there are no transitions (hard cuts). When the number of videos is greater than the number of transitions by two or more, the system automatically cycles through the transitions. For a complete list of IDs, see [Transition effects](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task#de99f111). |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to concatenate three video clips into one video, applying the "Fade open" (`1182358`) and "Rotate and zoom" (`1182360`) transition effects at the two joins.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/concat-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": [
    "https://example.com/intro.mp4",
    "https://example.com/main_content.mp4",
    "https://example.com/outro.mp4"
  ],
  "transitions": [
    "1182358",
    "1182360"
  ]
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task#the-error-object) below. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="success"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-concat-video-123456789",
  "request_id": "20240520153000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520153500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `video_urls` must contain at least 1 item.",
    "param": "video_urls",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video concatenation is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=1774504841-...` |The download URL of the generated concatenated video file, in MP4 format. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`132.195` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-concat-video-12345678",
    "task_type": "concat-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 132.195
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "2026072720082006DEEB70BD8F14151010",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


<span id="87c51076"></span>
## Reference

<span id="de99f111"></span>
### Transition effects

The following table lists all currently supported transition effects and their IDs.


|Effect Name |ID |Preview |
|---|---|---|
|Swap |1109556 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79f31d11b46584bdb6fdcc4540ab7261.gif) </span> |
|RotateScaleFade |1109558 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dff3b939cbe6a297ead483206bb97e22.gif) </span> |
|Ripple |1109560 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14f6b3c5ffd25c8cff18dbf593f0d67f.gif) </span> |
|Hexagonalize |1109568 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64c4c859c391edf8bcefceb8c70a918f.gif) </span> |
|GlitchDisplay |1109572 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39d8866189a04200d87ea31a21af3500.gif) </span> |
|Flyeye |1109574 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86c7979c4470b795f5cd2d461c49477d.gif) </span> |
|DreamZoom |1109576 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2135ff204297e0fd2dd8f66ae0e710d5.gif) </span> |
|Doorway |1109578 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_543983c07d3f5c248ed09033bb9db17a.gif) </span> |
|Cube |1109584 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_649c78b8e44e7965950865a9e50c19cb.gif) </span> |
|CrossWrap |1109586 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a57e9728e19e57bb4bf1fc22927f85.gif) </span> |
|ColorPhase |1109588 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9878d7abd8dbd4c72732046966adcd40.gif) </span> |
|CircleCrop |1109594 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_005f1685a105c0e3b617f1f9ea36495c.gif) </span> |


&nbsp;

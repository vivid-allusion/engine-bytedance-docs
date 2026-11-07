---
title: "Create a camera motion task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-camera-motion-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/apply-camera-motion`

To add a camera motion effect to a video, you can call this API to submit an asynchronous task. You can specify the motion style and the time range for the effect to apply. The processed video is returned in MP4 format, making this capability ideal for scenarios such as video re\-editing, marketing intros, and dynamic effects for short\-form dramas.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-apply-camera-motion">Apply camera motion</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution limit**: Up to 1080p is supported.<br><br>* **Duration limit**: Must not exceed 5 minutes. |
|`motion_style` |String |No |`pan-zoom` |The camera motion style. The following preset effects are supported:<br><br><br>* `zoom`<br><br>* `pan-zoom`<br><br>* `orbit-360`<br><br>* `bounce`<br><br><br>For effect previews, see [Demo](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-apply-camera-motion#effect-preview). |
|`start_time` |Number |No |`5` |The start time of the camera motion, defaulting to `0`, which means starting from the beginning of the video. If only `end_time` is provided, `0` is used as the start time. Supports up to 2 decimal places, in seconds. Must not be less than `0`. |
|`end_time` |Number |No |`12.5` |The end time of the camera motion, defaulting to the end of the video. If only `start_time` is provided, the motion continues to the end of the video. If the value exceeds the actual video duration, it is automatically capped at the video duration. Must be greater than `start_time`. Supports up to 2 decimal places, in seconds. |
|`client_token` |String |No |`your_unique_request_id_133` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to apply a `pan-zoom` camera motion effect to a video from the 5th second to the 12.5th second.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/apply-camera-motion' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/input_video.mp4",
  "motion_style": "pan-zoom",
  "start_time": 5,
  "end_time": 12.5
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/120415#the-error-object) below. |


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

<span id="d060510e"></span>
#### Success

```JSON
{
   "success": true,
   "task_id": "amk-tool-apply-camera-motion-123456789",
   "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="1e612af7"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521113500XYZW54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `video_url` is required.",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Camera motion is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL of the processed video file, in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`resolution` |String |`"1080p"` |The resolution of the output video. |
|`duration` |Number |`125.8` |The total duration of the output video, in seconds. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-apply-camera-motion-123456789",
    "task_type": "apply-camera-motion",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/motion_output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20240521113000ABCDEFG12345",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

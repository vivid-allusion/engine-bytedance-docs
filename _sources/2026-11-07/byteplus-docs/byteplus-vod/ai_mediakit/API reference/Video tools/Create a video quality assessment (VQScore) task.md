---
title: "Create a video quality assessment (VQScore) task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-quality-assessment-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/assess-video-quality`

To objectively assess the visual quality of a video without a reference source, you can call this API to submit an asynchronous video quality (VQScore) assessment task. The underlying VQScore algorithm scores video quality by simulating human perception, unlike traditional methods that require a reference video.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/120666">Video quality assessment (VQScore)</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be assessed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution limit**: The input video supports up to 4K (3840×2160) resolution. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a video quality assessment task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/assess-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{ 
    "video_url": "https://example.com/your_video.mp4"
}'
```


<span id="response"></span>
## Response

After you call the API to submit the task, the interface immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

<span id="0c5c79fc"></span>
### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-quality-assessment-task#b13e387a) below. |


<span id="b13e387a"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="914f44a4"></span>
### Response example

<span id="8f0c8bf3"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-assess-video-quality-12345",
    "request_id": "20240523110000ABCDEFG98765"
}
```


<span id="e7a656db"></span>
#### Failure

```JSON
{
    "success": false, 
    "task_id": "",
    "request_id": "20240523110500XYZW54321",
    "error": {
        "code": "InvalidParameter",
        "message": "The parameter 'video_url' is missing or invalid.",
        "type": "BadRequest"
    }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video quality assessment is an asynchronous task. The execution status and final result are not returned synchronously at submission time. You can obtain the task result in the following two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When the task is successfully completed, the `result` field in the task information you obtain contains the following:


|Parameter |Type |Description |
|---|---|---|
|`vq_score` |Number |The VQScore quality score, ranging from `[0,100]`; a higher score indicates better quality.<br><br><br>* `[0, 60)`: Poor subjective perception<br><br>* `[60, 70)`: Good subjective perception<br><br>* `[70, 100]`: Excellent subjective perception |
|`duration` |Number |The duration of the input video, in seconds. |


Example of a complete final task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-assess-video-quality-12345",
    "request_id": "20240523110000ABCDEFG98765",
    "status": "completed",
    "result": {
        "vq_score": 88.5,
        "duration": 91.2
    },
    "expires_at": 1777534898,
    "created_at": 1777362013,
    "finished_at": 1777362599
}
```

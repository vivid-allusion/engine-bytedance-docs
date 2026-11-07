---
title: "Create a reframe-to-vertical task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-reframe-to-vertical-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/reframe-video-to-vertical`

The reframe\-to\-vertical API automatically converts landscape videos into a vertical format (9:16) suitable for social media. It submits an asynchronous task that uses AI to perform intelligent cropping, subject tracking, and active speaker detection, delivering a production\-ready vertical video without any manual editing.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-reframe-video-to-vertical">Reframe video to vertical</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/landscape.mp4` |The URL of the landscape video to be converted.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: `MP4`, `MOV`, `MKV`, `AVI`, `FLV`.<br><br>* **Aspect ratio**: The input should be in a landscape aspect ratio. `16:9`, `4:3`, and `21:9` are supported.<br><br>* **Video duration**: No more than 4 hours.<br><br>* **File size**: No more than 20 GB per file. |
|`subtitle_url` |String |No |`https://example.com/subtitle.srt` |The URL of a subtitle file, used to burn subtitles into the output vertical video. If this parameter is omitted, no subtitles are added to the output video.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: subtitle files such as `SRT` and `ASS`.<br><br>*  **<b\>Quantity limit**: At most one subtitle file can be provided. |
|`client_token` |String |No |`your_unique_request_id_180` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a reframe\-to\-vertical task: upload a landscape source video and burn an external subtitle file into the output vertical video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/reframe-video-to-vertical' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_landscape_video.mp4",
  "subtitle_url": "https://example.com/your_subtitle.srt"
}'
```


<span id="response"></span>
## Response

After you call the API to submit the task, the interface immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

<span id="response-parameters"></span>
### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-reframe-to-vertical-task#error-object) below. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="success-response"></span>
#### Success response

```JSON
{
  "success": true,
  "task_id": "amk-tool-reframe-video-to-vertical-123456789",
  "request_id": "20260908130000ABCDEFG12345"
}
```


<span id="failure-response"></span>
#### Failure response

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20260908130500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "must specify video_url",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Reframe to vertical is an asynchronous task. The execution status and final result are not returned synchronously at submission time. You can obtain the task result in the following two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When the task is successfully completed, the `result` field in the task information you obtain contains the following:


|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/vertical_output.mp4?auth_key=...` |The download URL of the reframed vertical video. This is an HTTPS temporary download link, valid for **24 hours**; please download and save the file promptly. |
|`duration` |Number |`120.5` |The output video duration, in seconds, used for metering and billing. |


Example of a complete final task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-reframe-video-to-vertical-123456789",
    "request_id": "20260908130000ABCDEFG12345",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/vertical_output.mp4?auth_key=...",
        "duration": 120.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777292051
}
```

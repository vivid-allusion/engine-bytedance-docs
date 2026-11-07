---
title: "Create a face blurring task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-face-mosaic-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video`

This API submits an asynchronous video face blurring task that automatically and accurately detects face regions in a video and applies a blur or mosaic to all faces. It is suitable for scenarios that require protecting facial privacy, such as short\-drama content anonymization and preprocessing reference material for generative video.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-face-mosaic">Face mosaic</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/full_video.mp4` |The URL of the video to be masked.<br><br><br>* **Video source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution**: Up to 4K; 1080P is recommended.<br><br>* **Duration**: Must not exceed 10 minutes.<br><br>* **Frame rate**: Must be within 25–60. |
|`face_confidence` |Number |No |`0.35` |The confidence threshold for face detection. The value range is `[0.1, 1.0]`. Detection results below this value are discarded. The higher the value, the more conservative the detection (requiring higher face similarity). Defaults to `0.35`. |
|`mask_mode` |String |No |`mosaic` |The masking method.<br><br><br>* `mosaic`: (Default) Mosaic.<br><br>* `blur`: Gaussian blur. |
|`mask_strength` |String |No |`medium` |The masking strength.<br><br><br>* `low`: Low.<br><br>* `medium`: (Default) Medium.<br><br>* `high`: High. |
|`face_box_expand` |Number |No |`0.2` |The face bounding\-box expansion ratio. The value range is `(0.0, 1.0]`. The system expands the masking area outward from the detected face region by this ratio. For example, `0.2` means expanding 20% outward on each edge of the original bounding box. Defaults to `0.2`. |
|`upright_face_only` |Boolean |No |`true` |Specifies whether to detect only upright faces to optimize processing speed. This parameter controls if the system performs rotation checks to detect non\-upright faces.<br><br><br>* `true`: (Default) The system detects upright and slightly angled faces (including side faces) but does not detect faces that are lying down or upside down. This option significantly reduces processing time.<br><br>* `false`: The system attempts to detect faces in all orientations, offering a wider detection range at the cost of increased processing time. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a face blurring task for a video using the "Gaussian blur" method with "high" strength.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/face-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/sensitive_video.mp4",
  "mask_mode": "blur",
  "mask_strength": "high"
}'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="5caaad7c"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="e369d8af"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="fd1995d2"></span>
### Response example

<span id="5ac2feb6"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-face-blur-video-1703201",
    "task_type":"face-blur-video",
    "request_id": "20260415160000F6DE4C24A6A0D94B8AB2"
}
```


<span id="44ec549a"></span>
#### Failure

```JSON
{
    "success": false,
    "task_id":"amk-tool-face-blur-video-47708906754",
    "task_type":"face-blur-video",
    "request_id":"202605151452382EB49B08B360546311E7",
    "error":{
        "code":"AbilityProcessingError",
        "type":"BadRequest",
        "message":"file upload by url failed, code: DownloadFailed.UrlDownloadFail, message: GetUrlInfo failed, http status code is 403, msg: 403 Forbidden"
    }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Face blurring is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/blurred_video.mp4?auth_key=...` |The download URL for the masked video file. This URL is valid for **24 hours**. Please be sure to save the output file promptly. |
|`duration` |Number |`180.5` |The total duration of the output video (in seconds). |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-face-blur-video-1703201",
    "request_id": "20260415160000F6DE4C24A6A0D94B8AB2",
    "result": {
        "video_url": "https://example.byteplus.com/blurred_video.mp4?auth_key=1775271661-...",
        "duration": 180.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

---
title: "Create a portrait matting task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-portrait-matting-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/matte-portrait-video`

To programmatically remove the background from a video, you can call this API to submit an asynchronous portrait matting task. The service automatically detects the human subject, removes the original background, and generates a video file with a transparent or solid\-color background, suitable for post\-production scenarios such as background replacement.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-matting">Video matting</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/input_video.mp4` |The URL of the video to be matted.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `mkv`, `wmv`. |
|`format` |String |No |`MOV` |The output video format.<br><br><br>* `WEBM`: (default) WebM format, outputs a transparent background, and supports an Alpha transparency channel.<br><br>* `MOV`: QuickTime Movie format, outputs a transparent background, and supports an Alpha transparency channel.<br><br>* `MP4`: MP4 format, outputs a solid\-color background. You can specify the background color with the `background_color` parameter. The default is green. |
|`background_color` |String |No |`green` |The background color of the output video. Only takes effect when `format` is `MP4`. The default is green.<br><br><br>* `black`<br><br>* `white`<br><br>* `green` |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_data` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to perform portrait matting on a video, specifying MOV as the output format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/matte-portrait-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{ 
  "video_url": "https://example.com/input_video.mp4",
  "format": "MOV"
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
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-portrait-matting-task#error-object) below. |


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
  "task_id": "amk-tool-matte-portrait-video-123456789",
  "request_id": "20240521100000ABCDEFG12345"
}
```


<span id="failure-response"></span>
#### Failure response

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521100500XYZW54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `format` is invalid. Supported values are: WEBM, MOV.",
    "param": "format",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Portrait matting is an asynchronous task. The execution status and final result are not returned synchronously at submission time. You can obtain the task result in the following two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When the task is successfully completed, the `result` field in the task information you obtain contains the following:


|Parameter |Type |Description |
|---|---|---|
|`video_url` |String |The URL of the generated matted video file. This is an HTTPS temporary download link, valid for **24 hours**; please download and save the file promptly. |
|`resolution` |String |The resolution of the output video, aligned with the source. One of `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, `4k`, `8k`. |
|`duration` |Number |The duration of the output video, in seconds. |


The following is an example of a complete task information response after task completion:

```JSON
{
    "success": true,
    "task_id": "amk-tool-matte-portrait-video-123456789",
    "task_type":"matte-portrait-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/matted_output.mov?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 15.5
    },
    "expires_at":1785494704,
    "created_at":1785408198,
    "finished_at":1785408305,
    "request_id":"20260730184318DA8200378590270FA22B",
    "queue_id":"q2a028fa533b7fe6a25b018dccd6284"
}
```

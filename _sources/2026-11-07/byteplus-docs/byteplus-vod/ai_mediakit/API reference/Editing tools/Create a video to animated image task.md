---
title: "Create a video to animated image task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-to-animated-image-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-animated-image`

To create an animated image (GIF or WebP) from a specific segment of a video, you can call this API. It submits an asynchronous task that extracts a clip based on a specified start and end time, making it ideal for generating cover animations, marketing materials, and short previews.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-to-animated-image">Video to animated image</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to extract the animated image from.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution limit**: Up to 4K (3840×2160) is supported. |
|`start_time` |Number |Yes |`10.5` |The start time of the segment to extract, in seconds. Supports up to 3 decimal places. Defaults to `0`, which means extracting from the beginning of the video. |
|`end_time` |Number |Yes |`15.0` |The end time of the segment to extract, in seconds. Must be greater than `start_time`. Supports up to 3 decimal places.<br><br>The maximum duration of the output animated image is 60 seconds. |
|`output_format` |String |No |`webp` |The output format of the animated image. Supports `gif` and `webp`. The default is `gif`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to extract a `webp` animated image from 10.5 seconds to 15 seconds of a video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-animated-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{ 
  "video_url": "https://example.com/source_video.mp4",
  "start_time": 10.5,
  "end_time": 15.0,
  "output_format": "webp"
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="b780cf6b"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-filter-task#b52913d5) below. |


<span id="46413be4"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="c2e97b6b"></span>
### Response example

<span id="95570420"></span>
#### Success

```JSON
{
   "success": true,
   "task_id": "amk-tool-extract-animated-image-1400600",
   "request_id": "20260325160500A8DE7F57A9B3E17A0FF5"
}
```


<span id="645df038"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520185500BBCCDD112244",
  "error": {
    "code": "InvalidParameter",
    "message": "The duration (end_time - start_time) cannot exceed 60 seconds.",
    "param": "end_time",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

The video\-to\-animated\-image conversion is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example |Description |
|---|---|---|---|
|`image_url` |String |`https://example.byteplus.com/output.webp?auth_key=...` |The URL of the generated animated image file. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. The frame rate of the output animated image is fixed at 15 fps. |
|`duration` |Number |`4.5` |The duration of the output animated image, in seconds, with up to 3 decimal places. Calculated as `min(end_time, video duration) - start_time`. |
|`resolution` |String |`480p` |The resolution of the output animated image. The maximum resolution of the output animated image is 480p. When the input video resolution is lower than 480p, the output animated image resolution matches the input video's resolution. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-animated-image-1400600",
    "request_id": "20260325160500A8DE7F57A9B3E17A0FF5",
    "result": {
        "image_url": "https://example.byteplus.com/animated_output.webp?auth_key=1774612861-...",
        "duration": 4.5,
        "resolution": "480p"
    },
    "expires_at": 1777464950,
    "created_at": 1777292067,
    "finished_at": 1777292151
}
```

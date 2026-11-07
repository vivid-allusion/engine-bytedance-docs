---
title: "Create a video image overlay task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-image-overlay-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-image-to-video`

To programmatically add a logo, watermark, or other image to a video, you can call this API. It allows you to submit an asynchronous task to overlay a specified image onto a video frame, with control over its size, position, and display duration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-image-overlay">Image overlay on video</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/video.mp4` |The URL of the source video.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported. |
|`sub_image_url` |String |Yes |`https://example.com/logo.png` |The URL of the overlay image.<br><br><br>* **Image source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common image formats such as `PNG`, `JPG`, and `JPEG` are recommended. We recommend using a `PNG` with an alpha channel for the best watermark effect. |
|`sub_image_width` |String |No |`"10%"` |The width of the image. Supports a pixel value (such as `"100"`) or a percentage relative to the video width (such as `"10%"`). The default value is `"10%"`. |
|`sub_image_height` |String |No |`"5%"` |The height of the image. Supports a pixel value (such as `"100"`) or a percentage relative to the video height (such as `"5%"`). The default value is `"5%"`. |
|`sub_image_pos_x` |String |No |`"85%"` |The horizontal (X\-axis) position of the top\-left corner of the image, with the top\-left corner of the video as the origin (`"0"`). Supports a pixel value or a percentage. The default value is `"85%"`. |
|`sub_image_pos_y` |String |No |`"90%"` |The vertical (Y\-axis) position of the top\-left corner of the image, with the top\-left corner of the video as the origin (`"0"`). Supports a pixel value or a percentage. The default value is `"90%"`.<br><br>The default `sub_image_pos_x` and `sub_image_pos_y` values (`"85%"` and `"90%"`) place the image in the bottom\-right area of the video frame, which is suitable for a watermark. |
|`start_time` |Number |No |`0` |The time (in seconds) at which the image starts to appear. The default value is the start of the video. |
|`end_time` |Number |No |`15.5` |The time (in seconds) at which the image stops appearing. The default value is the end of the video.<br><br>If `end_time` exceeds the original video duration, the output video is extended to that `end_time`, and the extended portion will be a black screen with the image still displayed. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to add a PNG image as a watermark in the bottom\-right corner of a video and display it between the 2nd and 10th second of the video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-image-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/source_video.mp4",
  "sub_image_url": "https://example.com/company_logo.png",
  "sub_image_width": "15%",
  "sub_image_pos_x": "82%",
  "sub_image_pos_y": "90%",
  "start_time": 2.0,
  "end_time": 10.0
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-image-overlay-task#the-error-object) below. |


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
  "task_id": "amk-tool-video image overlay-123456789",
  "request_id": "20240520193000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520193500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `sub_image_url` is required.",
    "param": "sub_image_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video image overlay is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/watermarked-video.mp4?auth_key=...` |The URL of the generated video with the overlaid image, in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`duration` |Number |`120.0` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. Possible values include `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, and `4k`. |


Example of complete task information:

```JSON
{
    "success": true,
    "task_id": "amk-tool-video image overlay-123456789",
    "task_type": "video image overlay",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/watermarked-video.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 120.0
    },
    "expires_at": 1775047666,
    "created_at": 1774874853,
    "finished_at": 1774874866,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```

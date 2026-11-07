---
title: "Create a gaussian blur video task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-gaussian-blur-video-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/gaussian-blur-video`

To programmatically mask sensitive information or unwanted elements in a video, you can call this API to submit an asynchronous Gaussian blur task. It allows you to apply a blur effect to specific rectangular regions within defined time ranges. Common use cases include obscuring faces, watermarks, or logos. The processed video is returned in MP4 format, with the resolution defaulting to match the source.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-gaussian-blur">Video gaussian blur</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution limit**: Up to 4K (3840×2160) is supported. |
|`blur_regions` |Array |Yes |`[ { "start_time": 5.0, ... } ]` |An array of Gaussian blur configurations. Each element defines a Gaussian blur region and its effective time range. Up to 3 configurations are supported. See the [The blur region object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-gaussian-blur-video-task#blur-region-object) below. |
|`client_token` |String |No |`your_unique_request_id_134` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="blur-region-object"></span>
#### The blur region object

Each object in the array contains the following fields to define a Gaussian blur region:


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`start_time` |Number |Yes |`5.0` |The start time of the blur effect, in seconds. Supports up to 3 decimal places. |
|`end_time` |Number |Yes |`10.5` |The end time of the blur effect, in seconds. Supports up to 3 decimal places. |
|`top_left_x` |Integer |Yes |`100` |The X coordinate (horizontal) of the top\-left corner of the blur rectangle, in pixels. |
|`top_left_y` |Integer |Yes |`150` |The Y coordinate (vertical) of the top\-left corner of the blur rectangle, in pixels. |
|`bottom_right_x` |Integer |Yes |`300` |The X coordinate (horizontal) of the bottom\-right corner of the blur rectangle, in pixels. Must be greater than `top_left_x`. |
|`bottom_right_y` |Integer |Yes |`400` |The Y coordinate (vertical) of the bottom\-right corner of the blur rectangle, in pixels. Must be greater than `top_left_y`. |


Suppose you want to mask the blue region in the following diagram. The parameters are set as follows:


* `top_left_x`: The X coordinate of the top\-left corner of the rectangle (b1 in the diagram).

* `top_left_y`: The Y coordinate of the top\-left corner of the rectangle (a1 in the diagram).

* `bottom_right_x`: The X coordinate of the bottom\-right corner of the rectangle (b2 in the diagram).

* `bottom_right_y`: The Y coordinate of the bottom\-right corner of the rectangle (a2 in the diagram).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c5328cc6af7493eba25d602a20217be~tplv-goo7wpa0wc-image.image) </span>

<span id="request-example"></span>
## Request example

The following example demonstrates how to apply two Gaussian blur effects to a video:


* From the 5th second to the 10.5th second, blur the region from `(100, 150)` to `(300, 400)`.

* From the 15th second to the 20th second, blur the region from `(500, 600)` to `(700, 800)`.


```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/gaussian-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/input_video.mp4",
  "blur_regions": [
    {
      "start_time": 5.0,
      "end_time": 10.5,
      "top_left_x": 100,
      "top_left_y": 150,
      "bottom_right_x": 300,
      "bottom_right_y": 400
    },
    {
      "start_time": 15.0,
      "end_time": 20.0,
      "top_left_x": 500,
      "top_left_y": 600,
      "bottom_right_x": 700,
      "bottom_right_y": 800
    }
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-gaussian-blur-video-task#the-error-object) below. |


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
   "task_id": "amk-tool-gaussian-blur-video-123456789",
   "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521113500XYZW54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The number of items in 'blur_regions' must be between 1 and 3.",
    "param": "blur_regions",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Gaussian blur video is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). When a task is successfully completed, the `result` field in the task information you retrieve contains the following:



|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL of the processed video file, in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`resolution` |String |`1080p` |The resolution of the output video, such as `720p`, `1080p`, `2k`, or `4k`. |
|`duration` |Number |`125.8` |The total duration of the output video, in seconds. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-gaussian-blur-video-123456789",
    "request_id": "20240521113000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/blurred_output.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

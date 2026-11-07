---
title: "Create an image-to-video task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/image-to-video`

This API submits an asynchronous image\-to\-video task that combines multiple images in order and can optionally configure transition animations and in\-image animations to produce a dynamic video.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-to-video">Image to video</a>.</div>


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
|`images` |Array |Yes |`-` |The list of image objects that define the content of each frame of the video. For the detailed structure, see the [Image object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task#image-object) below.<br><br>**Quantity limit**: A single task supports 1 to 100 image objects. |
|`transitions` |Array |No |`["1109558"]` |The list of transition effect IDs between images. By default, there are no transitions (hard cuts). If the length of the list is less than the number of transitions needed (`number of images - 1`), the system cycles through the effects in the list. For detailed IDs, see [Transition effects](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task#b0e75726). |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="image-object"></span>
### Image object

Each object in the `images` array represents an image and its animation effects, and contains the following fields:


|Parameter |Type |Required |Description |
|---|---|---|---|
|`image_url` |String |Yes |The URL of the image.<br><br><br>* **Image source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common static image formats such as `jpg` and `png`. |
|`duration` |Number |No |The display duration of the image, in seconds. Supports up to two decimal places. The default value is `3`. |
|`animation_type` |String |No |The type of in\-image animation applied during the display of the image. There is no animation by default. Supported values:<br><br><br>* `move_up`<br><br>* `move_down`<br><br>* `move_left`<br><br>* `move_right`<br><br>* `zoom_in`<br><br>* `zoom_out` |
|`animation_in` |Number |No |The start time of the animation (in seconds), relative to the start of that image segment. Takes effect only after `animation_type` is set. Supports two decimal places. The default value is `0`, meaning the animation starts from the first frame in which the image is displayed. |
|`animation_out` |Number |No |The end time of the animation (in seconds), relative to the start of that image segment. Takes effect only after `animation_type` is set. Supports two decimal places. The default value is the image's `duration` value, meaning the animation ends on the last frame in which the image is displayed. |


<span id="request-example"></span>
## Request example

The following example demonstrates how to generate a video from two images:


* The first image is displayed for 3 seconds with a "zoom in" animation applied.

* The second image is displayed for 2.5 seconds with a "move right" animation applied.

* A "Rotate and zoom" (`1182360`) transition effect is used between the two images.


```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/image-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "images": [
    {
      "image_url": "https://example.com/scene1.jpg",
      "duration": 3.0,
      "animation_type": "zoom_in"
    },
    {
      "image_url": "https://example.com/scene2.png",
      "duration": 2.5,
      "animation_type": "move_right"
    }
  ],
  "transitions": [
    "1109558"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task#the-error-object) below. |


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
    "task_id": "amk-tool-image-to-video-1602100",
    "request_id": "20260410110000E7CF5D35B7A1E05A8EE2"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521140000AABBCC889900",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `images` must contain at least 1 item.",
    "param": "images",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Image\-to\-video is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL of the generated video file, in MP4 format. This URL is a temporary HTTPS download link valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`5.5` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk_tool_image_to_video_1602100",
    "request_id": "20260410110000E7CF5D35B7A1E05A8EE2",
    "result": {
        "video_url": "https://example.byteplus.com/i2v_output.mp4?auth_key=1775012461-...",
        "duration": 5.5,
        "resolution": "1080p"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<span id="90134339"></span>
## Reference

<span id="b0e75726"></span>
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

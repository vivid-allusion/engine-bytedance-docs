---
title: "Create a video compositing task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-composition-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/stitch-video`

To combine multiple videos into a single composite frame, you can use this API to submit an asynchronous video compositing task. It spatially combines videos horizontally or vertically, making it ideal for scenarios like multi\-view comparison and frame composition.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-visual-transitions">Visual transitions</a>.</div>


* <div data-tips="true" data-tips-type="default">Output video notes:</div>


   * <div data-tips="true" data-tips-type="default">The duration of the output video matches the longest input video. Videos with a shorter duration are padded with a black screen after they finish playing.</div>


   * <div data-tips="true" data-tips-type="default">The audio of the output video is a mix of the audio tracks of all input videos whose <code>keep_audio</code> is set to <code>true</code>.</div>



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
|`videos` |Array |Yes |`[{"video_url": "https://.../video1.mp4"}, {"video_url": "https://.../video2.mp4"}]` |The list of video objects to be stitched. You must provide at least 2 and at most 3. The order in which the frames are stitched matches the list order. For a detailed description of each object in the list, see [The video object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-composition-task#video-object) below. |
|`stitch_direction` |String |Yes |`horizontal` |The compositing method. Possible values:<br><br><br>* `horizontal`: Side\-by\-side compositing.<br><br>* `vertical`: Top\-and\-bottom compositing. |
|`client_token` |String |No |`your_unique_request_id_134` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="video-object"></span>
#### The video object


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/video1.mp4` |The URL of an input video to be stitched.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported. We recommend that the input videos use common aspect ratios such as `16:9`, `9:16`, `1:1`, `4:3`, or `3:4` for better stitching results. |
|`keep_audio` |Boolean |No |`true` |Whether to keep the audio of this video. The default value is `true`. If `false`, the audio track of this video is not mixed into the final output. |


<span id="request-example"></span>
## Request example

The following example demonstrates how to stitch two videos side by side while keeping only the audio of the first video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/stitch-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "videos": [
    {
      "video_url": "https://example.com/left_video.mp4",
      "keep_audio": true
    },
    {
      "video_url": "https://example.com/right_video.mp4",
      "keep_audio": false
    }
  ],
  "stitch_direction": "horizontal"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-composition-task#the-error-object) below. |


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
  "task_id": "amk-tool-stitch-video-345678901",
  "request_id": "20240520170000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520170500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The number of items in `videos` must be at least 2.",
    "param": "videos",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video stitching is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The URL of the generated stitched video file, which is in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`duration` |Number |`120.5` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. Possible values include `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, and `4k`. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-stitch-video-345678901",
    "request_id": "20240520170000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 120.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

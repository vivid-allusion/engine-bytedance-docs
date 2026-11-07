---
title: "Create a subtitle burn-in task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-subtitle-burn-in-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-subtitle-to-video`

To programmatically burn subtitles into a video, you can use this API to submit an asynchronous task. This task burns a specified subtitle file or text content into the video frame with custom styling, producing a new video with embedded subtitles.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-subtitle-burn-in">Subtitle burn\-in</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/video.mp4` |The URL of the video to which subtitles are added.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported. |
|`subtitle_url` |String |No |`https://example.com/sub.srt` |The URL of the subtitle file.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common subtitle formats such as `SRT`, `VTT`, and `ASS`.<br><br><br>`subtitle_url` and `subtitles` are used to provide subtitle content; you must specify one of them. When both are present, the system gives priority to the content of `subtitle_url`. |
|`subtitles` |Array |No |`[{"subtitle_text": "...", "start_time": 0.5, "end_time": 3.0}]` |The list of subtitle content, composed of multiple subtitle objects. Each object contains the subtitle text and the start and end times. For details, see [The subtitle object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-subtitle-burn-in-task#subtitle-object) below.<br><br>`subtitle_url` and `subtitles` are used to provide subtitle content; you must specify one of them. When both are present, the system gives priority to the content of `subtitle_url`. |
|`subtitle_pos_preset` |String |No |`bottom_center` |The preset subtitle position. The default value is `bottom_center`.<br><br><br>* `bottom_center`<br><br>* `top_center`<br><br>* `center`<br><br>* `lower_third` |
|`subtitle_font_size` |Integer |No |`50` |The subtitle font size, in pixels (px). The default value is 50. |
|`subtitle_font_color` |String |No |`#FFFFFFFF` |The subtitle font color, in RGBA format. The default value is `#FFFFFFFF` (opaque white). |
|`subtitle_font_type` |String |No |`sy_black` |The subtitle font. Supported fonts:<br><br><br>* (Default) `inter`<br><br>* `montserrat`<br><br>* `oppo_sans`<br><br>* `roboto`<br><br>* `source_han_serif` |
|`client_token` |String |No |`your_unique_request_id_134` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="subtitle-object"></span>
### The subtitle object


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`subtitle_text` |String |Yes |`Hello, world!` |The text content of a single subtitle. |
|`start_time` |Number |Yes |`0.5` |The time (in seconds) when this subtitle appears. |
|`end_time` |Number |Yes |`3.0` |The time (in seconds) when this subtitle disappears. |


<span id="request-example"></span>
## Request example

<span id="example-1-use-a-subtitle-file-url"></span>
### Example 1: Use a subtitle file URL

The following example demonstrates how to use an SRT subtitle file and customize the subtitle style (Source Han Serif, 48 px, bottom center).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-subtitle-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/source_video.mp4",
  "subtitle_url": "https://example.com/subtitles.srt",
  "subtitle_pos_preset": "bottom_center",
  "subtitle_font_size": 48,
  "subtitle_font_type": "source_han_serif"
}'
```


<span id="example-2-use-inline-subtitle-text"></span>
### Example 2: Use inline subtitle text

The following example demonstrates how to provide a list of subtitle text content directly in the request, using the montserrat font.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-subtitle-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/vlog_video.mp4",
  "subtitles": [
    {
      "subtitle_text": "Hi everyone, welcome to my Vlog!",
      "start_time": 0.5,
      "end_time": 3.0
    },
    {
      "subtitle_text": "The weather is really nice today~",
      "start_time": 3.5,
      "end_time": 5.0
    }
  ],
  "subtitle_font_type": "montserrat"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-subtitle-burn-in-task#the-error-object) below. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-filter-task#b52913d5) below. |
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
  "task_id": "amk-tool-add-subtitle-to-video-123456789",
  "request_id": "20240520183000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520183500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "Either 'subtitle_url' or 'subtitles' parameter must be provided.",
    "param": "subtitle_url,subtitles",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Subtitle burn\-in is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).When a task completes successfully, the `result` field in the retrieved task information contains the following:



|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL of the generated video with embedded subtitles, in MP4 format. This URL is a temporary HTTPS download link valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`125.4` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. Possible values include `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, and `4k`. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-subtitle-to-video-123456789",
    "request_id": "20240520183000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 125.4
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

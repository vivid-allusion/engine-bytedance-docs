---
title: "Create a video metadata acquisition task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-metadata-probe-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/probe-video-metadata`

To obtain standardized technical metadata from a video file, you can use this API. It allows you to submit an asynchronous task by providing a video URL. Upon completion, the task returns comprehensive details about the video, including container\-level information (`format_meta`), video stream properties (`video_stream_meta`), and audio stream characteristics (`audio_stream_meta`).

<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_MediaKit_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/video.mp4` |The URL of the video to be probed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/probe-video-metadata' \
-H 'Authorization: Bearer {Your_MediaKit_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4"
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="b97d0f33"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="9f71ec8d"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="b9ae72d1"></span>
### Response example

<span id="087cfccc"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-video-metadata-1703200",
    "task_type":"probe-video-metadata",
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF1"
}
```


<span id="5f6a747e"></span>
#### Failure

```JSON
{
  "success": false,
  "request_id": "20240521190100AABBCCDDEEFF445566",
  "task_type":"probe-video-metadata",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'video_url' is required and cannot be empty.",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video metadata acquisition is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`format_meta` |Object |Container\-level metadata, including container format, bitrate, duration, size, and more. See [The format meta object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-metadata-probe-task#format-meta-structure). |
|`video_stream_meta` |Object |Metadata of the primary video stream. Returns `null` if the video contains no video stream. See the [The video stream meta object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-metadata-probe-task#video-stream-meta-structure). |
|`audio_stream_meta` |Object |Metadata of the primary audio stream. Returns `null` if the video contains no audio stream. See [The audio stream meta object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-metadata-probe-task#audio-stream-meta-structure). |


<span id="format-meta-structure"></span>
#### The format meta object


|Parameter |Type |Description |
|---|---|---|
|`md5` |String |The MD5 value of the file (if obtainable). |
|`container` |String |The container format (packaging format), such as `MP4`. |
|`bitrate` |Number |The container bitrate, in bps. |
|`duration` |Number |The duration declared by the container, in seconds. |
|`size` |Number |The file size, in bytes. |


<span id="video-stream-meta-structure"></span>
#### The video stream meta object


|Parameter |Type |Description |
|---|---|---|
|`codec` |String |The video codec, such as `h264`. |
|`width` |Number |The display width of the video stream, in pixels (px). |
|`height` |Number |The display height of the video stream, in pixels (px). |
|`duration` |Number |The original duration of the video stream, in seconds. |
|`bitrate` |Number |The video stream bitrate, in bps. |
|`fps` |Number |The video frame rate, in fps. |
|`dynamic_range` |String |The dynamic range, either `HDR` or `SDR`. |


<span id="audio-stream-meta-structure"></span>
#### The audio stream meta object


|Parameter |Type |Description |
|---|---|---|
|`codec` |String |The audio codec, such as `aac`. |
|`duration` |Number |The duration of the audio stream, in seconds. |
|`sample_rate` |Number |The audio sample rate, in Hz. |
|`bitrate` |Number |The audio stream bitrate, in bps. |
|`channels` |Number |The number of audio channels. |


Example of a complete task information response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-probe-video-metadata-3442176",
  "task_type": "probe-video-metadata",
  "status": "completed",
  "result": {
    "audio_stream_meta": {
      "bitrate": 93304,
      "channels": 2,
      "codec": "aac",
      "duration": 555.875,
      "sample_rate": 48000
    },
    "format_meta": {
      "duration": 555.875,
      "md5": "",
      "size": 72951092,
      "bitrate": 1049891,
      "container": "MP4"
    },
    "video_stream_meta": {
      "height": 960,
      "width": 1920,
      "bitrate": 945854,
      "codec": "h264",
      "duration": 555.816,
      "dynamic_range": "SDR",
      "fps": 30
    }
  },
  "expires_at": 1778682292,
  "created_at": 1778595878,
  "finished_at": 1778595893,
  "request_id": "202605122224370A5133983FE83564DCCD"
}
```

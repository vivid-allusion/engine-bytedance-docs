---
title: "Create an audio and video merging task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-audio-and-video-merging-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/mux-audio-video`

This API submits an asynchronous audio and video merging task that combines an input audio stream and video stream into a new video file. You can choose to keep or replace the video's original audio track, and align audio and video that have different durations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-merging">Audio and video merging</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the input video.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported. |
|`audio_url` |String |Yes |`https://example.com/background.mp3` |The URL of the input audio to merge.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common audio formats such as `mp3`, `m4a`, `wav`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB. |
|`is_audio_reserve` |Boolean |No |`false` |Whether to keep the video's original audio track.<br><br><br>* `true`: (Default) Keep the original audio track; the new audio is mixed with the original audio.<br><br>* `false`: Do not keep the original audio track; that is, replace the original audio with the new audio. |
|`is_video_audio_sync` |Boolean |No |`true` |Whether to align the audio and video durations.<br><br><br>* `false`: (Default) Do not align. The duration of the merged video is determined by the longer media stream.<br><br>* `true`: Align. Processing follows the `sync_mode` and `sync_method` configurations below. |
|`sync_mode` |String |No |`video` |The duration alignment basis. **Effective only when ** **`is_video_audio_sync`** ** is ** **`true`** **.** <br><br><br>* `video`: (Default) Use the video duration as the basis. If the audio is longer, the audio is trimmed; if the audio is shorter, it is processed according to `sync_method`.<br><br>* `audio`: Use the audio duration as the basis. If the video is longer, the video is trimmed; if the video is shorter, it is processed according to `sync_method`. |
|`sync_method` |String |No |`trim` |The specific method for duration alignment. **Effective only when ** **`is_video_audio_sync`** ** is ** **`true`** **.** <br><br><br>* `trim`: (Default) Trim. Trim the longer media stream from the end so that it aligns with the shorter one.<br><br>* `speed`: Change speed. Speed up or slow down so that the two media streams have the same duration. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to add background music to a silent video, using the video duration as the basis and trimming the background music for alignment.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/mux-audio-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/silent_video.mp4",
  "audio_url": "https://example.com/long_background_music.mp3",
  "is_audio_reserve": false,
  "is_video_audio_sync": true,
  "sync_mode": "video",
  "sync_method": "trim"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


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
    "task_id": "amk_tool_mux_audio_video_1501800",
    "request_id": "20260401100000C8EF6E46A8B2D06B9FF1"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521110000DDEEFF223344",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `video_url` is required.",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Audio and video merging is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).When a task is successfully completed, the `result` field in the task information you retrieve contains the following:



|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL of the merged video file. The file format is MP4. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`120.5` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk_tool_mux_audio_video_1501800",
    "request_id": "20260401100000C8EF6E46A8B2D06B9FF1",
    "result": {
        "video_url": "https://example.byteplus.com/muxed_output.mp4?auth_key=...",
        "duration": 120.5,
        "resolution": "1080p"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

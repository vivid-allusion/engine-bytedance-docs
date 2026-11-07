---
title: "Create an audio metadata acquisition task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-audio-metadata-probe-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/probe-audio-metadata`

To inspect an audio file and retrieve its technical metadata, you can call this API to submit an asynchronous probe task. The task result provides standardized media metadata, including container\-level information (`format_meta`) and audio stream information (`audio_stream_meta`).

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
|`audio_url` |String |Yes |`https://example.com/audio.mp3` |The URL of the audio to be probed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Audio formats such as `mp3`, `m4a`, `wav`, `wma`, `amr`, `aac`, `ogg`, `flac`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/probe-audio-metadata' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "audio_url": "https://example.com/your_audio.mp3"
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="b98fc48a"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="4468cd2f"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="28273260"></span>
### Response example

<span id="c657d8f9"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-audio-metadata-1703200",
    "task_type":"probe-audio-metadata",
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF1"
}
```


<span id="b4a0585d"></span>
#### Failure

```JSON
{
  "success": false,
  "request_id": "20240521192100AABBCCDDEEFF889900",
  "task_type":"probe-audio-metadata",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'audio_url' is required and cannot be empty.",
    "param": "audio_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Audio metadata probing is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`format_meta` |Object |Container\-level metadata, including container format, bitrate, duration, size, and more. See [The format meta object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-metadata-probe-task#format-meta-object). |
|`audio_stream_meta` |Object |Metadata of the primary audio stream. Returns `null` if no audio stream is found. See [The audio stream meta object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-metadata-probe-task#audio-stream-meta-object). |


<span id="format-meta-object"></span>
### The format meta object


|Parameter |Type |Description |
|---|---|---|
|`md5` |String |The MD5 value of the file (if obtainable). |
|`container` |String |The container format (packaging format), such as `mp3`. |
|`bitrate` |Number |The container bitrate, in bps. |
|`duration` |Number |The duration declared by the container, in seconds. |
|`size` |Number |The file size, in bytes. |


<span id="audio-stream-meta-object"></span>
### The audio stream meta object


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
  "task_id": "amk-tool-probe-audio-metadata-3440896",
  "task_type": "probe-audio-metadata",
  "status": "completed",
  "result": {
    "format_meta": {
      "md5": "fc683910c3d82a45a2b81e6a34ea0d37",
      "size": 210642,
      "bitrate": 129018,
      "container": "MP3",
      "duration": 13.061
    },
    "audio_stream_meta": {
      "codec": "mp3",
      "duration": 13.061,
      "sample_rate": 44100,
      "bitrate": 128000,
      "channels": 2
    }
  },
  "expires_at": 1778682277,
  "created_at": 1778595862,
  "finished_at": 1778595878,
  "request_id": "2026051222242287882A15DC19043115F8"
}
```

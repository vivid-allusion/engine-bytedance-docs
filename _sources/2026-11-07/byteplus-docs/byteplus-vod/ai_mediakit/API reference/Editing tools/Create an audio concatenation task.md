---
title: "Create an audio concatenation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-audio-concatenation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/concat-audio`

This API submits an asynchronous audio concatenation task that joins multiple audio files into a single complete audio file in order.

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
|`audio_urls` |Array |Yes |`["https://example.com/audio.mp3", "https://example.com/audio2.mp3"]` |The list of audio URLs to be concatenated.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Quantity limit**: A single task supports 1 to 100 URLs.<br><br>* **Supported formats**: Common audio formats such as `mp3`, `m4a`, `wav`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB. |
|`format` |String |No |`mp3` |The output audio format. Supported values:<br><br><br>* `m4a`(Default)<br><br>* `mp3`<br><br>* `ogg`<br><br>* `flac`<br><br>* `wav`. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to concatenate three audio clips into one audio file.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/concat-audio' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "audio_urls": [
    "https://example.com/voice_intro.mp3",
    "https://example.com/podcast_segment_1.m4a",
    "https://example.com/outro_music.wav"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-concatenation-task#the-error-object) below. |


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
    "task_id": "amk-tool-concat-audio-1399296",
    "request_id": "20260324135451B9CF8E68B9A4F28F1EB9"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520153500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `audio_urls` must contain at least 1 item.",
    "param": "audio_urls",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Audio concatenation is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`audio_url` |String |`https://example.byteplus.com/output.m4a?auth_key=...` |The download URL of the generated concatenated audio file. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`230.71495` |The total duration of the output audio, in seconds. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-concat-audio-1399296",
    "task_type": "concat-audio",
    "status": "completed",
    "result": {
        "audio_url": "https://example.byteplus.com/output.m4a?auth_key=...",
        "duration": 230.71495
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20260324135451B9CF8E68B9A4F28F1EB9",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

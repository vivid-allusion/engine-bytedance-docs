---
title: "Create a voice activity detection task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-voice-activity-detection-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/detect-voice-activity`

The Voice Activity Detection API processes an audio or video file to identify segments containing human speech. You can use this asynchronous API to automatically locate the start and end times of valid speech, separating it from silence and background noise. The API returns a list of timestamps, providing cleaner audio input for subsequent recognition, analysis, editing, and training.

> **INFO**

> For the complete workflow and application examples, see [Voice activity detection](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-voice-activity-detection).

## Request parameters

### Header parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`video_url` |String |Conditionally required |`https://example.com/media.mp4` |The URL of the video to process.<br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`.<br><br><br>Note: You must provide exactly one of `video_url` and `audio_url`. |
|`audio_url` |String |Conditionally required |`https://example.com/media.mp3` |The URL of the audio to process.<br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common audio formats such as `mp3`, `m4a`, `wav`, `wma`, `amr`, `aac`, `ogg`, and `flac`.<br><br><br>Note: You must provide exactly one of `video_url` and `audio_url`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example shows how to detect the start and end times of speech activity in an audio file.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/detect-voice-activity' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "audio_url": "https://example.com/your_audio.mp3"
}'
```

## Response

After you call the API to submit a task, the API immediately returns a synchronous response indicating whether the task was successfully submitted to the background processing queue.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successfully submitted.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier of the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`error` |Object |The error details object, returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/122470#error-object) below. |

#### The error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error. For example, `BadRequest`. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |
|`param` |String |The specific parameter that caused the error. This field is optional. |

### Response examples

#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-detect-voice-activity-123456789",
  "request_id": "20240521100000ABCDEFG12345"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521100500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "`video_url` and `audio_url` are mutually exclusive; exactly one must be provided.",
    "param": "video_url, audio_url",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Voice Activity Detection is an asynchronous task. The execution status and final result are not returned synchronously when you submit the task. You can use either of the following methods to obtain the task result:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

After the task is successfully completed, the `result` field in the task details contains the following fields.

|Parameter |Type |Description |
|---|---|---|
|`voice_segments` |Array of objects |The list of valid speech segments. If no valid speech is detected, an empty array `[]` is returned. For the structure of each object in the array, see [The voice segment object](https://docs.byteplus.com/docs/byteplus-vod/122470#voice-segment-object) below. |
|`segment_count` |Integer |The number of detected speech segments. If none are detected, the value is `0`. |
|`duration` |Number |The total duration of the input media file, in seconds. |

### The voice segment object

Each object in the `voice_segments` array contains the following fields:

|Parameter |Type |Example value |Description |
|---|---|---|---|
|`start_time` |Number |`0.52` |The start time of the segment, in seconds, accurate to two decimal places. |
|`end_time` |Number |`4.34` |The end time of the segment, in seconds, accurate to two decimal places. |

The following is an example of the complete task details after a task is completed:

```JSON
{
    "success": true,
    "task_id": "amk-tool-detect-voice-activity-123456789",
    "request_id": "20240521100000ABCDEFG12345",
    "result": {
        "voice_segments": [
            {
                "start_time": 0.52,
                "end_time": 4.34
            },
            {
                "start_time": 5.50,
                "end_time": 7.12
            }
        ],
        "segment_count": 2,
        "duration": 15.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

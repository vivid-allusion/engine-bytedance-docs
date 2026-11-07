---
title: "Create a voice and background audio separation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-voice-separation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/separate-voice`

This API submits an asynchronous voice and background audio separation task. General and music scenes output two tracks: vocals and background audio. Short\-form drama, voice\-over, and game scenes output three tracks: vocals, music, and sound effects. The output is in AAC format by default; you can also use the `output_format` parameter to specify `mp3`, `wav`, `m4a`, or `flac`.

> **INFO**

> For a complete usage flow and application examples, please refer to [Voice and background audio separation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-voice-and-background-audio-separation).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Conditionally required |`https://example.com/media.mp4` |The URL of the video to be processed.<br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br><br>One of `video_url` and `audio_url` must be provided. If both are present, `video_url` takes priority. |
|`audio_url` |String |Conditionally required |`https://example.com/media.mp3` |The URL of the audio to be processed.<br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream audio formats such as `mp3`, `m4a`, `wav`.<br><br><br>One of `video_url` and `audio_url` must be provided. If both are present, `video_url` takes priority. |
|`scene` |String |No |`Drama` |The separation scene, used to select a more suitable separation strategy for different content types. Available values:<br><br><br>* `Audio` (default): General scenes. Outputs 2 tracks (vocals and background).<br><br>* `Music`: Music scenes. Outputs 2 tracks (vocals and background).<br><br>* `Drama`: Short\-form drama scenes. Outputs 3 tracks (vocals, music, and sound effects).<br><br>* `Narrate`: Voice\-over (narration) scenes. Outputs 3 tracks (vocals, music, and sound effects).<br><br>* `Game`: Game scenes. Outputs 3 tracks (vocals, music, and sound effects). |
|`output_format` |String |No |`mp3` |The output format of the separated audio. Available values:<br><br><br>* `aac` (default)<br><br>* `mp3`<br><br>* `wav`<br><br>* `m4a`<br><br>* `flac` |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |

## Request example

The following example demonstrates how to separate the vocals and background audio from a video file.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/separate-voice' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4"
}'
```

## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |

#### The error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-separate-voice-123456789",
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
    "message": "Either `video_url` or `audio_url` must be provided.",
    "param": "video_url, audio_url",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Voice and background audio separation is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`voice_audio_url` |String |`https://example.com/voice.aac?sign=...` |The download URL of the separated vocal track. The file format matches the `output_format` in the request (AAC by default). This is an HTTPS temporary download URL, valid for **24 hours**. Please download and save the file promptly. |
|`background_audio_url` |String |`https://example.com/background.aac?sign=...` |The download URL of the separated background track. **Returned only when** **`scene`** ** is ** **`Audio`** ** or ** **`Music`** **.**  The file format matches the `output_format` in the request (AAC by default). This is an HTTPS temporary download URL, valid for **24 hours**. Please download and save the file promptly. |
|`music_audio_url` |String |`https://example.com/music.aac?sign=...` |The download URL of the separated music track. **Returned only when** **`scene`** ** is ** **`Drama`** **, ** **`Narrate`** **, or ** **`Game`** **.**  The file format matches the `output_format` in the request (AAC by default). This is an HTTPS temporary download URL, valid for **24 hours**. Please download and save the file promptly. |
|`sfx_audio_url` |String |`https://example.com/sfx.aac?sign=...` |The download URL of the separated sound\-effects (SFX) track, which contains ambient sounds, effect sounds, and so on. **Returned only when** **`scene`** ** is ** **`Drama`** **, ** **`Narrate`** **, or ** **`Game`** **.**  The file format matches the `output_format` in the request (AAC by default). This is an HTTPS temporary download URL, valid for **24 hours**. Please download and save the file promptly. |
|`duration` |Number |120.5 |The total duration of the input video or audio, in seconds. |

The following is an example of a complete task information response after the task is completed (a Drama scene):

```JSON
{
    "success": true,
    "task_id": "amk-tool-separate-voice-123456789",
    "request_id": "20240521100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "voice_audio_url": "https://example.com/voice.aac?sign=...",
        "music_audio_url": "https://example.com/music.aac?sign=...",
        "sfx_audio_url": "https://example.com/sfx.aac?sign=...",
        "duration": 120.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

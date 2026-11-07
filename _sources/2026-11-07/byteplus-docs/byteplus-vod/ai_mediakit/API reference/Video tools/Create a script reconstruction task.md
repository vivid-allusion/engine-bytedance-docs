---
title: "Create a script reconstruction task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-script-reconstruction-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/drama-script`

To automatically generate a structured script from short\-drama videos, call this API to submit an asynchronous reconstruction task. This service uses large\-model video understanding to convert videos into text, accurately identifying and extracting core elements such as scenes, characters, dialogue, and plot.

> **INFO**

> For a complete workflow and application examples, see [Script reconstruction](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-script-reconstruction).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_urls` |Array |Yes |`["https://...", "https://..."]` |The list of short drama video URLs to process. The system concatenates and analyzes them in array order.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. HLS (M3U8) sources are not supported.<br><br>* Quantity limit: A single task supports 1 to 100 video files.<br><br>* Duration limit: The cumulative duration of all videos in a single task must not exceed 300 minutes, and a single file must not exceed 120 minutes.<br><br>* Content type: Suitable for live\-action content centered on character dialogue and plot development, such as short dramas, series, and films. Not suitable for content lacking coherent live\-action plot or facial\-recognition cues, such as animation, documentaries, ads, or livestream recordings.<br><br>* Resolution limit: All videos submitted in one task must have identical resolution (width and height).<br><br>* Subtitle requirement: Videos must contain embedded (hard) subtitles. |
|`return_pkg` |Boolean |No |`false` |Controls the output packaging format of the task result.<br><br><br>* `false`: (Default) Returns only the core script data. The `result_url` field of the task result points to a Gzip\-compressed JSON file (`.json.gz`).<br><br>* `true`: Packages all task outputs into an archive (`.tar.gz`). In addition to the core script JSON, it also provides analysis outputs such as character names with their images and scene screenshots. The `result_url` of the task result then points to this archive. |
|`voice_language` |String |No |`en-US` |The spoken language in the video, used for speech recognition (ASR).<br><br><br>* Default behavior: If left empty or unset, the tool automatically detects the language. Auto\-detection supports: Chinese, English, Shanghainese, Hokkien, Sichuanese, Shaanxi dialect, and Cantonese.<br><br>* Supported languages: `zh-CN`, `en-US`, `ja-JP`, `id-ID`, `es-MX`, `pt-BR`, `de-DE`, `fr-FR`, `ko-KR`, `fil-PH`, `ms-MY`, `th-TH`, `ar-SA`, `it-IT`, `bn-BD`, `el-GR`, `nl-NL`, `ru-RU`, `tr-TR`, `vi-VN`, `pl-PL`, `ro-RO`, `ne-NP`, `uk-UA`, `yue-CN`. Among these, Chinese (`zh-CN`) and English (`en-US`) are explicitly supported; the other languages are usable but their recognition quality is not guaranteed. |
|`output_language` |String |No |`en-US` |The language of the output script.<br><br><br>* Supported languages: `zh-CN` (Simplified Chinese), `en-US` (US English).<br><br>* Default behavior: If left empty or unset, the default is `en-US`. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_data` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example demonstrates how to submit a script reconstruction task for two episodes of a short drama.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/drama-script' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": [
    "https://example.com/drama_episode_01.mp4",
    "https://example.com/drama_episode_02.mp4"
  ]
}'
```

## Response

After you call the API to submit the task, the interface immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

### Response parameters

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error details object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-script-reconstruction-task#error-object) below. |

#### The error object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success

```JSON
{
   "success": true,
   "task_id": "amk-tool-drama-script-123456789",
   "request_id": "20240521150000ABCDEFG12345"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521150500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The number of items in 'video_urls' must be between 1 and 100.",
    "param": "video_urls",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Script reconstruction is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in the following two ways:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When the task is successfully completed, the `result` field in the task information you obtain contains the following.

|Parameter |Type |Example |Description |
|---|---|---|---|
|`result_url` |String |`https://example.byteplus.com/result.json.gz?auth_key=...` |The download URL of the generated script file. This is a public URL that is valid for **24 hours**, so be sure to save it promptly. |
|`duration` |Number |`245.5` |The total duration of the input videos, in seconds. |
|`drama_script_task_id` |String |`v02bbbg1006***kbdminbj659kvikr0` |The script reconstruction task ID. |

The following is a complete example of the task details returned after a task completes:

```JSON
{
    "success": true,
    "task_id": "amk-tool-drama-script-123456789",
    "request_id": "20240521150000ABCDEFG12345",
    "result": {
        "result_url": "https://example.byteplus.com/result.json.gz?auth_key=1774504841-...",
        "duration": 245.5,
        "drama_script_task_id": "v02bbbg1006***kbdminbj659kvikr0"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

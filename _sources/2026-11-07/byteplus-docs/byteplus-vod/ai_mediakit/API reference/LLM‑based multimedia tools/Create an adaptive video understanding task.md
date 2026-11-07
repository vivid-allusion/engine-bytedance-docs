---
title: "Create an adaptive video understanding task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-understand-router`

Use this API to submit an asynchronous adaptive video understanding task for purposes like content moderation, video retrieval, and tag generation. Powered by ModelArk visual understanding models, this API performs general content analysis on a list of video URLs and returns structured, video\-level understanding results.

> **INFO**

> For the complete usage flow and application examples, see [Adaptive video understanding](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-adaptive-video-understanding).

## Prerequisites

* **Enable the ModelArk service**: The adaptive video understanding tool relies on ModelArk visual understanding models. Go to the [ModelArk Console](https://console.byteplus.com/ark/region:ap-southeast-1/overview) and ensure that a visual understanding model is enabled and available under your account.

* **Perform cross\-service authorization**: Before using the adaptive video understanding tool for the first time, go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console to grant AI MediaKit permission to access your ModelArk resources.

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_urls` |Array of String |Yes |`["https://example.com/video1.mp4", "https://example.com/video2.mp4"]` |The list of video URLs to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Quantity limit**: A single task supports up to 10 video files.<br><br>* **Single\-video duration limit**: A single video must not exceed 2 hours. |
|`prompt` |String |Yes |`Summarize the key events in the video and mark the time range in which each event appears` |The prompt, a natural\-language description used to guide the large model in analyzing the video content. The minimum length is 1. |
|`level` |String |No |`Balanced` |The analysis tier. This parameter determines the task's default frame\-sampling strategy and model selection to balance cost, speed, and quality. For the detailed decision logic, see [How it works](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-adaptive-video-understanding#how-it-works). The following values are supported: <br><br><br>* `Economy`: (Default) The economy tier, speed\-first, suitable for large\-batch content annotation with lower requirements for result details. <br><br>* `Balanced`: The balanced tier, balancing speed and quality, suitable for general content moderation and retrieval scenarios. <br><br>* `Quality`: The quality tier, result\-first, suitable for scenarios requiring finer semantic understanding. |
|`prefer_models` |Array of String |No |`["seed-2-0-lite-260428"]` |The list of preferred **Model IDs**, up to 10. The system selects the final model from the models you specify in combination with the strategy. You can view the available Model IDs on the [ModelArk Console](https://console.byteplus.com/ark/region:ap-southeast-1/overview). |
|`prefer_endpoints` |Array of String |No |`["ep-m-20260703202744-q8tcb"]` |The list of preferred **Endpoint IDs**, up to 10. The system selects the final model from the endpoints you specify in combination with the strategy. You can create and manage endpoints on the [ModelArk Console](https://console.byteplus.com/ark/region:ap-southeast-1/overview).<br><br>**Note**: This parameter takes priority over `prefer_models`. |
|`manual_option` |Object |No |`-` |Manual\-mode parameters. See [The manual option object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task#cde16d50) below. When this field is omitted, the task fully uses the `level` tier strategy without manual overrides. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is in the event notification upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

#### The manual option object

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`max_snapshot_number` |Integer |No |`100` |The maximum number of sampled frames, with a value range of [0, 1000] and a default of 0. When set to 0, the number of snapshots is determined by the `level` tier; setting it explicitly overrides the tier strategy. |
|`fps` |Number |No |`1.0` |The frame\-sampling rate. When set, the system uniformly samples frames at the rate you specify. The value range is [0.2, 5.0], with a default of 1.0. |
|`need_audio` |Boolean |No |`false` |Whether to enable or disable audio analysis. Defaults to `false`.<br><br><br>* `true`: Enables audio analysis. The system selects a model that supports audio\-video multimodal input and analyzes the audio content (speech, dialogue, sound characteristics, and so on). <br><br>* `false`: Disables automatic keyword\-based audio analysis and analyzes only the video's visual content.<br><br><br>**Note**: The system's automatic audio keyword detection only recognizes **Chinese** audio keywords in the `prompt`. If your `prompt` is written in English or another language, audio analysis will **not** be triggered automatically even when it mentions sound, music, or dialogue. To analyze audio for a non\-Chinese `prompt`, you must explicitly set `need_audio` to `true`. |

## Request example

The following example demonstrates how to analyze the content of a publicly accessible video and request a summary of the video content.

```Plain Text
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-understand-router' \
  -H 'Authorization: Bearer {Your_API_Key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "video_urls": [
      "https://example.com/sample_video.mp4"
    ],
    "prompt": "Summarize the key events in the video and mark the time range in which each event appears",
    "level": "Balanced",
    "manual_option": {
      "max_snapshot_number": 100,
      "need_audio": true
    }
  }'
```

## Response

After you call the API to submit the task, the interface immediately returns a synchronous response indicating whether the task was successfully submitted to the background processing queue.

### Response parameters

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully. <br><br><br>* `true`: The task was successfully submitted to the background processing queue. <br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task#5f054d17) below. |

#### The error object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success response

```Plain Text
{
  "success": true,
  "task_id": "amk-tool-video-understand-router-123456789",
  "request_id": "20260624150000ABCDEFG12345"
}
```

#### Failure response

```Plain Text
{
  "success": false,
  "task_id": "",
  "request_id": "20260624150500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `video_urls` exceeds the maximum length of 10.",
    "param": "video_urls",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Video understanding is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in the following two ways:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback URL for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When the task is successfully completed, the `result` field in the task details contains the following.

|Parameter |Type |Description |
|---|---|---|
|`duration` |Number |The sum of the durations of all input videos, in seconds. |
|`contents` |Array of String |The list of video content analysis results. Each item is the analysis result for the video at the same index in the `video_urls` array. |
|`token_usage` |Object |Token usage statistics during large\-model inference. See the [The token usage object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task#1329818e) below. |

### The token usage object

|Parameter |Type |Description |
|---|---|---|
|`input_tokens` |Integer |The number of input tokens. |
|`output_tokens` |Integer |The number of output tokens. |
|`total_tokens` |Integer |The total number of tokens. |

The following is an example of the information for a completed task:

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-understand-router-123456789",
  "request_id": "20260624150000ABCDEFG12345",
  "status": "completed",
  "result": {
    "duration": 120.5,
    "contents": [
      "The video is 120 seconds long and mainly shows city street scenes. 0-30s is a daytime overhead shot of a busy street with traffic and pedestrians; 30-60s cuts to a nighttime neon-light close-up; 60-90s is a follow shot inside a shopping mall; 90-120s ends with a rooftop overhead view. The footage is stable overall, with no violent, vulgar, or otherwise non-compliant content."
    ],
    "token_usage": {
      "input_tokens": 850,
      "output_tokens": 150,
      "total_tokens": 1000
    }
  },
  "expires_at": 1777464650,
  "created_at": 1777291767,
  "finished_at": 1777291851
}
```

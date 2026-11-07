---
title: "Create a video quality enhancement (AI-enhanced) task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-quality-enhancement-ai-enhanced-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative`

Use this API to submit an asynchronous Video Quality Enhancement (AI\-Enhanced) task. The tool uses diffusion models for generative video enhancement and restoration. It restores pixels lost through compression or aging and uses a deep semantic understanding of the video content to reconstruct and generate realistic details, producing natural, high\-fidelity video.

> **INFO**

> For detailed feature descriptions and use cases, see [Video quality enhancement (AI\-enhanced)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-ai-enhanced).

## Request parameters

### Header

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |See [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API key. |

### Body

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be enhanced.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`.<br><br>* File size: The recommended maximum file size is 10 GB.<br><br>* Input video limitations:<br><br>   * Resolutions up to 1080p are supported. The specific requirements are:<br><br>      * Short side: 360–1080 pixels, inclusive.<br><br>      * Long side: 360–1920 pixels, inclusive.<br><br>   * Only SDR video is supported. |
|`resolution` |String |No |`1080p` |The target resolution. Supported values:<br><br><br>* `720p` (default)<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k` |
|`bitrate_level` |String |No |`medium` |The target bitrate level, used to control the average bitrate of the output video. This parameter affects the visual quality and final file size. The default is `medium`.<br><br><br>* `low`: Low bitrate<br><br>* `medium`: Medium bitrate (recommended)<br><br>* `high`: High bitrate<br><br><br>**Note**: The actual output bitrate is automatically calculated based on the target resolution and frame rate. For the target output bitrate of each level, see [Bitrate reference](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-video-quality-enhancement-ai-enhanced-task#7656e3b8). To specify an exact bitrate, use the `bitrate` parameter. |
|`bitrate` |Integer |No |`8000` |The target average bitrate, in kbps. The value must be between 10 and 150000, inclusive. If omitted, the bitrate is automatically calculated based on `bitrate_level`, resolution, and frame rate. When both `bitrate` and `bitrate_level` are specified, only `bitrate` takes effect. |
|`fps` |Number |No |`30` |The target frame rate, in fps. The value must be between 15 and 120, inclusive. We recommend that it not exceed four times the source frame rate. If omitted, the output video retains the same frame rate as the source video. |
|`client_token` |String |No |`your_unique_id_123` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_args` |Custom callback arguments. The content you provide is returned as\-is through an event when the task is complete, allowing you to associate it with your business logic. The maximum field length is 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint for receiving event notifications. If provided, this URL takes precedence over the global callback URL configured in the console. The endpoint must start with `http://` or `https://`. For details about the callback process and payload structure, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`{queue_id}` |The ID of the queue to which the task is submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For details, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example shows how to submit a Video Quality Enhancement (AI\-Enhanced) task with an output resolution of 1080p.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/old_video.mp4",
  "resolution": "1080p"
}'
```

## Response

After you submit the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details. It is returned only when `success` is `false`. See the Error object below. |

#### Error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging. |
|`param` |String |(Optional) The specific parameter that caused the error. |

### Response examples

#### Success

```JSON
{
  "success": true,
  "task_id": "example-enhancement-task-id",
  "request_id": "example-request-id"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "example-failed-request-id",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter `resolution` must be one of [720p, 1080p, 2k, 4k].",
    "param": "resolution",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Video Quality Enhancement (AI\-Enhanced) runs asynchronously. The task status and final result are not returned in the submission response. You can obtain the task result in two ways:

* **Method 1:**  Periodically call [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Configure a callback URL in the AI MediaKit console in advance, or specify a URL for an individual task using the `callback_url` parameter when you submit it. When the task finishes, the system sends detailed results to that URL in an HTTP POST request. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information contains the following:

|Parameter |Type |Description |
|---|---|---|
|`video_url` |String |The URL of the enhanced video file, in MP4 format. This is an HTTPS temporary download link that is valid for **24 hours** by default. Download and save the file promptly. |
|`duration` |Number |The total duration of the output video, in seconds. |
|`resolution` |String |The resolution of the output video. |
|`fps` |Number |The frame rate of the output video. |

The following example shows the task information returned after successful completion:

```JSON
{
    "success": true,
    "task_id": "example-enhancement-task-id",
    "request_id": "example-request-id",
    "status": "completed",
    "result": {
        "video_url": "https://example.com/generative_enhanced_output.mp4",
        "duration": 65.5,
        "resolution": "1080p",
        "fps": 30
    },
    "expires_at": 1777378251,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

## Reference

### Bitrate reference

The following table lists the **target output bitrate** for `bitrate_level` set to `low`, `medium`, and `high` under different resolution and frame rate combinations. To ensure stable quality across different scenarios, the system dynamically adjusts the bitrate based on the complexity of the video content. Therefore, the actual output bitrate usually fluctuates between 0.8 and 1.5 times the target values listed in the table.

|Output resolution |Output frame rate (fps) |Low bitrate (Mbps) |Medium bitrate (Mbps) |High bitrate (Mbps) |
|---|---|---|---|---|
|720p |[15,30] |2.8 |4 |5.2 |
||(30,60] |5.6 |8 |10 |
||(60,120] |8.4 |12 |15 |
|1080p |[15,30] |5 |7 |9 |
||(30,60] |10 |14 |18 |
||(60,120] |15 |22 |28 |
|2K |[15,30] |10 |15 |20 |
||(30,60] |17 |24 |32 |
||(60,120] |28 |40 |52 |
|4K |[15,30] |21 |30 |39 |
||(30,60] |32 |45 |58 |
||(60,120] |53 |75 |100 |

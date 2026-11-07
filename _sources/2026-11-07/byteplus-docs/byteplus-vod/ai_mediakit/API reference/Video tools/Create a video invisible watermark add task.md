---
title: "Create a video invisible watermark add task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-invisible-watermark-add-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-video-invisible-watermark`

To protect your video assets and trace their distribution, you can use this API to submit an asynchronous task that adds an invisible watermark. This process embeds a string of numeric information into a video file without affecting its visual quality, making it ideal for copyright protection, content leak tracing, and file authenticity verification.

> **INFO**

> For the complete workflow and application examples, see [Video invisible watermark](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-invisible-watermark).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to which the invisible watermark will be added.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `mov`, `mkv`, `flv`, `ts`, `avi`, and `wmv`.<br><br>* Resolution: Up to 4K. |
|`watermark_content` |String |Yes |`1234567890123` |The hidden numeric information to embed in the video for copyright tracing. This parameter must be a **string** that represents a positive 64\-bit integer and meets the following requirements:<br><br><br>* Format: A string containing digits only, for example, `"12345"`.<br><br>* Range: The number represented by the string must be between `1` and `9223372036854775807`.<br><br>* Constraints: Leading zeros, such as in `"0123"`, and non\-numeric characters are not allowed. |
|`watermark_level` |String |No |`normal` |The invisible watermark strength. This setting determines the balance between attack resistance—the ability to withstand video compression, transcoding, and other processing—and the impact on the image. Although the watermark is invisible to the naked eye, it modifies the source video's pixel data.<br><br><br>* `normal`: (Default) Standard strength. Balances image quality and attack resistance and is suitable for most scenarios.<br><br>* `high`: High strength. Provides the strongest attack resistance and can withstand more intensive video processing, but may have a relatively greater potential impact on the image. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_data` |Custom callback arguments. The content you provide is returned as\-is through an event when the task is complete, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must start with `http://` or `https://`. For details about the callback process and payload structure, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`{queue_id}` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For details, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example adds an invisible watermark with `normal` strength to a video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-video-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/copyright_video.mp4",
  "watermark_content": "987654321098765",
  "watermark_level": "normal"
}'
```

## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the error object below. |

#### The error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) The specific parameter that caused the error. |

### Response example

#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-add-video-invisible-watermark-example-001",
  "request_id": "req_add_video_watermark_example_001"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "req_add_video_watermark_example_002",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `watermark_content` is invalid. It must be a string of digits representing a positive 64-bit integer.",
    "param": "watermark_content",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Adding a video invisible watermark is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* **Method 1:**  Periodically call [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system POSTs the detailed result to your specified URL. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.com/watermarked_output.mp4` |The temporary HTTPS URL of the video containing the invisible watermark. The URL is valid for 24 hours. Download and save the file promptly. |
|`duration` |Number |`120.5` |The total duration of the input video, in seconds, used for metering and billing. |
|`resolution` |String |`1080p` |The resolution of the input video. |

Example of a complete task information response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-add-video-invisible-watermark-example-001",
  "request_id": "req_add_video_watermark_example_001",
  "status": "succeeded",
  "result": {
    "video_url": "https://example.com/watermarked_output.mp4",
    "duration": 120.5,
    "resolution": "1080p"
  },
  "expires_at": 1777464650,
  "created_at": 1777291767,
  "finished_at": 1777291851
}
```

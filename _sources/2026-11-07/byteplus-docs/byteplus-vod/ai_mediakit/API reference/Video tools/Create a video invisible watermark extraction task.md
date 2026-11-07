---
title: "Create a video invisible watermark extraction task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-invisible-watermark-extraction-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-video-invisible-watermark`

This API submits an asynchronous task to extract invisible watermarks from a video. It parses and restores hidden numeric information, and can extract all watermarks if multiple were embedded in the same video.

> **INFO**

> For the complete workflow and application examples, see [Video invisible watermark](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-invisible-watermark).

## Limits

This API only supports extracting invisible watermarks embedded by the [Create a video invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-video-invisible-watermark-add-task) API. It cannot extract any form of invisible watermark added by third\-party tools.

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/watermarked_video.mp4` |The URL of the video from which to extract the invisible watermark.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream video formats such as `mp4`, `mov`, `mkv`, `flv`, `ts`, `avi`, and `wmv`.<br><br>* Resolution: Up to 4K. |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must start with `http://` or `https://`. For details about the callback process and payload structure, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`{queue_id}` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For details, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example submits a video invisible watermark extraction task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-video-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/watermarked_video.mp4"
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
  "task_id": "amk-tool-extract-video-invisible-watermark-example-001",
  "request_id": "req_extract_video_watermark_example_001"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "req_extract_video_watermark_example_002",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `video_url` is invalid. Provide a supported video URL.",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Extracting a video invisible watermark is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* **Method 1:**  Periodically call [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system POSTs the detailed result to your specified URL. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|Parameter |Type |Example |Description |
|---|---|---|---|
|`watermark_contents` |Array of Object |`[{"watermark_content": "987654321098765"}]` |A list of numeric strings from the extracted invisible watermarks, returned in the order they were extracted. If invisible watermarks were embedded in the video multiple times, the list may contain multiple results. If no invisible watermark is extracted, the list is empty. See the watermark_content object below. |
|`duration` |Number |`120.5` |The total duration of the video, in seconds. |

### The watermark_content object

|Parameter |Type |Example |Description |
|---|---|---|---|
|`watermark_content` |String |`987654321098765` |The extracted invisible watermark numeric string. |

Example of a complete task information response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-extract-video-invisible-watermark-example-001",
  "request_id": "req_extract_video_watermark_example_001",
  "status": "succeeded",
  "result": {
    "watermark_contents": [
      {
        "watermark_content": "987654321098765"
      },
      {
        "watermark_content": "123456789012345"
      }
    ],
    "duration": 120.5
  },
  "expires_at": 1777465650,
  "created_at": 1777292767,
  "finished_at": 1777292851
}
```

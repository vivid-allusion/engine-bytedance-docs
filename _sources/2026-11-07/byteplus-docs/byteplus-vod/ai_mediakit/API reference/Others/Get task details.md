---
title: "Get task details"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details"
---

`GET https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}`

To check the status and retrieve the result of an asynchronous task, you can use this API endpoint with the task's unique `task_id`. After submitting a task, you can poll this endpoint to get updates.

> **INFO**

> For a more efficient approach in production, you can configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification), which allows AI MediaKit to push the result directly to your server, eliminating the need for polling.

## API features

* **Unified query**: Supports querying all types of **asynchronous** tasks under the AI MediaKit service, such as the Enhance Video task.

* **Result validity**: The result data of a successful task (download links) is retained in the system for **24 hours** by default. Please download and save your resources promptly.

* **Automatic renewal**: When the remaining validity period of a task result is less than 2 hours, calling this API will automatically extend its expiration time, preventing the link from expiring prematurely.

## Request parameters

### Path

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`task_id` |String |Yes |`amk-tool-enhance-video-1703200` |The unique identifier of the task. You can obtain this from the response body when submitting an asynchronous task. |

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

## Request example

```Bash
curl -X GET "https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/amk-tool-enhance-video-1703200" \
-H "Authorization: Bearer {your_amk_api_key}" 
```

## Response parameters

The response body is a JSON object containing detailed information about the task.

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether this API request was processed successfully.<br><br><br>* `true`: The server successfully processed the query request.<br><br>* `false`: The request failed. See the `error` field for details.<br><br><br>> This field only represents the success of the query operation itself, not the execution status of the task. |
|`task_id` |String |The unique identifier of the queried task. |
|`task_type` |String |The task type. For video enhancement, the value is `enhance-video`. |
|`status` |String |The current status of the task. Possible values:<br><br><br>* `running`: The task is being processed.<br><br>* `completed`: The task has been successfully completed.<br><br>* `failed`: The task failed to process. |
|`result` |Object |The result object returned **when the task is successful**. This field appears only when `status` is `completed`. Its structure is detailed in the [Result](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details#57cb6192) section below. |
|`error` |Object |The error details object returned **when the task fails**. This field appears only when `status` is `failed`. Its structure is detailed in the [Error](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details#f3800f45) section below. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time in seconds). This field appears only when the task is successful and has a result. |
|`created_at` |Integer |The creation timestamp of the task (Unix time in seconds). |
|`finished_at` |Integer |The completion (success or failure) timestamp of the task (Unix time in seconds). This field appears only when `status` is `completed` or `failed`. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |

### Result

When the `status` is `completed`, the response will include a `result` object. For the Enhance Video task, its structure is as follows.

|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.bytepluscom/output.mp4?auth_key=...` |The download URL for the enhanced video file. This URL is valid for **24 hours**. |
|`duration` |Number |`120.5` |The total duration of the output video (in seconds). |
|`resolution` |String |`1080p` |The resolution of the output video. |
|`fps` |Number |`60` |The frame rate of the output video. |
|`tool_version` |String |`professional` |The tool version actually used for the task. |

### Error

When `success` is `false` or `status` is `failed`, an `error` object containing error details will be returned.

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The error code. For details, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`message` |String |A descriptive message of the error, useful for display or logging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |
|`type` |String |The type of error, such as `TaskError` for task execution errors or `ApiError` for API call errors. |

## Response examples

### Example 1: Task is running

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-1703200",
  "task_type": "enhance-video",
  "status": "running",
  "created_at": 1700484518,
  "request_id": "202603252052226AE61BF072A5A596F761"
}
```

### Example 2: Task completed

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-1703200",
    "task_type": "enhance-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/enhanced_output.mp4?auth_key=...",
        "duration": 120.5,
        "resolution": "1080p",
        "fps": 60,
        "tool_version": "professional"
    },
    "expires_at": 1774615474,
    "created_at": 1774442654,
    "finished_at": 1774442675,
    "request_id": "202603252052226AE61BF072A5A596F761"
}
```

### Example 3: Task failed

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-1703200",
  "task_type": "enhance-video",
  "status": "failed",
  "error": {
    "code": "DownloadFailed",
    "message": "Failed to download file from the provided URL: https://example.com/nonexistent.mp4. Please check if the URL is correct and publicly accessible.",
    "param": "video_url",
    "type": "TaskError"
  },
  "created_at": 1700484518,
  "finished_at": 1700484522,
  "request_id": "202603252052226AE61BF072A5A596F761"
}
```

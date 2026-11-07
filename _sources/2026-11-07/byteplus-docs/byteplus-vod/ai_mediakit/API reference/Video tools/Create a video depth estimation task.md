---
title: "Create a video depth estimation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-depth-estimation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-depth`

To generate a time\-continuous relative depth video from a source video, you can use this API to submit an asynchronous video depth estimation task. This process estimates the spatial layers of each frame, retaining motion contours and camera movement while abstracting details like appearance and background. The resulting depth video is ideal for applications such as AI motion reference, character replacement, camera movement control, and preprocessing for 3D visual effects.

> **Description**

> For a complete workflow and application examples, please refer to [Video depth estimation](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-depth-estimation).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/dance_reference.mp4` |The URL of the video to be processed.<br><br><br>* File source: Use a publicly accessible HTTP/HTTPS URL.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`.<br><br>* Video duration: The duration of a single video must not exceed 10 minutes.<br><br>* Video content: Must contain a valid video stream, and the resolution must not exceed 2K. |
|`model` |String |No |`standard` |The level of the depth estimation model. Only `standard` is supported, and the default value is `standard`. This level processes quickly and is suitable for effect previews and batch processing of single videos. |
|`client_token` |String |No |`video_depth_request_001` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`asset_id_20261021_001` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/en/docs/byteplus-vod/projects-and-queues). |

## Request example

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-depth' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/dance_reference.mp4",
  "model": "standard",
  "client_token": "video_depth_request_001",
  "callback_url": "https://example.com/callback",
  "callback_args": "asset_id_20261021_001"
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
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [Error object](https://docs.byteplus.com/en/docs/25/124500#error-object) below. |

#### Error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-depth-123456789",
  "request_id": "20261021140000ABCDEFG12345"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20261021140100HIJKLMN67890",
  "error": {
    "code": "InvalidParameter",
    "type": "BadRequest",
    "message": "video_url is required",
    "param": "video_url"
  }
}
```

## Asynchronous task result

Video Depth Estimation is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplusvideo.com/video-depth/result.mp4?auth_key=1777464650-example` |The download address of the HEVC\-encoded relative depth video, valid for 24 hours. Please download and save it in time. |
|`duration` |Number |`18.6` |The total duration of the output depth video, in seconds. Note that billing for this tool is based on the **input video duration**. |

The following is an example of the final complete task information:

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-depth-123456789",
  "task_type": "video-depth",
  "status": "completed",
  "result": {
    "video_url": "https://example.byteplusvideo.com/video-depth/result.mp4?auth_key=1777464650-example",
    "duration": 18.6
  },
  "expires_at": 1792591200,
  "created_at": 1792504800,
  "finished_at": 1792504920,
  "request_id": "20261021140000ABCDEFG12345"
}
```

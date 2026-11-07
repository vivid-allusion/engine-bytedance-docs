---
title: "Create a frame extraction task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-frame-extraction-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames`

This API submits an asynchronous frame extraction task. Based on your business scenario, you can choose one of four strategies—**by time interval**, **by specified time points**, **by specified frames (first/last)** , or **by scene change**—to capture one or more still images from a video. The captured images can be used for video covers, preview thumbnails, sprite sheets, or as input for other video understanding tasks.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-frame-extraction">Frame extraction</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/your_video.mp4` |The URL of the video to be processed.<br><br><br>* **Video source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|`snapshot_type` |String |No |`TimeInterval` |The frame\-extraction strategy, which determines how frames are captured. Defaults to `TimeInterval`.<br><br><br>* `TimeInterval`: Extract frames at a fixed time interval; used together with `time_interval`.<br><br>* `SpecifiedTime`: Extract frames at specified time points; used together with `specified_time`.<br><br>* `SpecifiedFrames`: Extract frames at specified frame numbers; used together with `specified_frames`.<br><br>* `SceneChange`: Extract frames on scene changes; used together with `scene_change_threshold`. |
|`time_interval` |Number |No |`10` |The time interval, in seconds, with up to 3 decimal places. Defaults to `1`; the value must be greater than `0.001`. Effective only when `snapshot_type` is `TimeInterval`. |
|`specified_time` |Array<Number\> |No |`[10.5, 25.0, 60.123]` |A list of specified time points, in seconds, with up to 3 decimal places (for example, `[10.5, 25.0, 60.123]`). Up to 1000 time points are supported. Effective and required when `snapshot_type` is `SpecifiedTime`. |
|`specified_frames` |Array<Integer\> |No |`[0, -1]` |A list of specified frame numbers. Up to 2 values are supported. Effective and required when `snapshot_type` is `SpecifiedFrames`. Currently only `0` (the first frame) and `-1` (the last frame) are supported. |
|`scene_change_threshold` |Number |No |`0.2` |The sensitivity threshold for scene\-change detection. The value range is `(0, 1)`, with a default of `0.1`. The smaller the value, the more sensitive the detection to scene changes, which may produce more snapshots. Effective only when `snapshot_type` is `SceneChange`. |
|`snapshot_limit` |Integer |No |`50` |The maximum number of snapshots to generate. The value range is `[1, 1000]`; the actual number of output snapshots may be smaller.<br><br><br>* Effective only when `snapshot_type` is `TimeInterval` or `SceneChange`.<br><br>* When the sprite sheet is enabled (`enable_sprite` is set to `true`), this parameter is the upper limit on the number of **large** sprite sheets; therefore the upper limit on the number of small tiles is `snapshot_limit * sprite_rows * sprite_cols`. |
|`scale_long` |Integer |No |`1280` |The maximum pixel value of the long side of output images. The value range is `[0, 4096]`. The long side of an output image cannot exceed the long side of the original video. For example, setting `scale_long` to `1280` scales the long side to 1280 pixels while the short side scales proportionally. If both `scale_long` and `scale_short` are set, the image is scaled while keeping the original aspect ratio so that the long side does not exceed `scale_long` and the short side does not exceed `scale_short`.<br><br>When `enable_sprite` is `true`, this parameter defines the long side of a single tile. |
|`scale_short` |Integer |No |`720` |The maximum pixel value of the short side of output images. The value range is `[0, 4096]`. The short side of an output image cannot exceed the short side of the original video. For example, setting `scale_short` to `640` scales the short side to 640 pixels while the long side scales proportionally. If both `scale_long` and `scale_short` are set, the image is scaled while keeping the original aspect ratio so that the long side does not exceed `scale_long` and the short side does not exceed `scale_short`. <br><br>When `enable_sprite` is `true`, this parameter defines the short side of a single tile. |
|`enable_sprite` |Boolean |No |`true` |Whether to combine the captured images into a single sprite sheet. Defaults to `false`.<br><br><br>* `false`: Output multiple independent snapshots.<br><br>* `true`: Output a sprite sheet containing all snapshots. |
|`sprite_rows` |Integer |No |`10` |The number of rows in the sprite sheet (the number of tiles along the vertical Y\-axis). Defaults to `10`; the value range is `[1, 100]`. Effective only when `enable_sprite` is `true`.<br><br>**Note**: The final sprite sheet has a size limit (a single side should not exceed 16384 pixels); setting too many rows or columns may cause the task to fail. |
|`sprite_cols` |Integer |No |`10` |The number of columns in the sprite sheet (the number of tiles along the horizontal X\-axis). Defaults to `10`; the value range is `[1, 100]`. Effective only when `enable_sprite` is `true`.<br><br>**Note**: The final sprite sheet has a size limit (a single side should not exceed 16384 pixels); setting too many rows or columns may cause the task to fail. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

<span id="example-1-extract-frames-by-time-interval"></span>
### Example 1: Extract frames by time interval

The following example demonstrates how to capture a frame every 10 seconds starting from second 0, up to a maximum of 5 frames, with the long side of the output images set to 640 pixels.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "snapshot_type": "TimeInterval",
  "time_interval": 10,
  "snapshot_limit": 5,
  "scale_long": 640
}'
```


<span id="example-2-generate-a-sprite-sheet-from-specified-time-points"></span>
### Example 2: Generate a sprite sheet from specified time points

The following example demonstrates how to capture 4 frames at specific time points (10.5s, 25s, 60.123s, 120s) and combine them into a 2x2 sprite sheet.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "snapshot_type": "SpecifiedTime",
  "specified_time": [10.5, 25.0, 60.123, 120.0],
  "enable_sprite": true,
  "sprite_rows": 2,
  "sprite_cols": 2
}'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="30b04288"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="3288f809"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="2f6b6a14"></span>
### Response example

<span id="39e47d55"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-extract-frames-123456789",
  "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="89064b3b"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240523101000WXYZ54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The 'xxx' parameter is required xxx",
    "param": "time_interval",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Frame extraction is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`snapshots` |Array |The list of snapshot results. Each object contains information about one snapshot. See [The snapshot object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-frame-extraction-task#snapshot-structure). |
|`snapshot_count` |Integer |The total number of snapshots successfully generated. In sprite\-sheet mode, this value is the number of small tiles in the sprite sheet. |


<span id="snapshot-structure"></span>
### The snapshot object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The snapshot download URL. This URL is valid for **24 hours**. Please be sure to save the output file promptly. |


**Example of a complete task information response (regular frames):** 

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-frames-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "snapshots": [
            {
                "image_url": "https://example.com/snapshot/frame_0s.jpg?sign=..."
            },
            {
                "image_url": "https://example.com/snapshot/frame_10s.jpg?sign=..."
            },
            {
                "image_url": "https://example.com/snapshot/frame_20s.jpg?sign=..."
            }
        ],
        "snapshot_count": 3
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777359999
}
```


**Example of a complete task information response (sprite sheet):** 

When `enable_sprite` is `true`, the `image_url` in the `snapshots` array points to the combined large sprite sheet.

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-frames-987654321",
    "request_id": "20240523100500XYZABC12345",
    "status": "completed",
    "result": {
        "snapshots": [
            {
                "image_url": "https://example.com/snapshot/sprite.jpg?sign=..."
            }
        ],
        "snapshot_count": 4
    },
    "expires_at": 1777531300,
    "created_at": 1777358420,
    "finished_at": 1777358900
}
```

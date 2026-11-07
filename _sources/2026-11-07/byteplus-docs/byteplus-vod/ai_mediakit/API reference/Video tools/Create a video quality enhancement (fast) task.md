---
title: "Create a video quality enhancement (fast) task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-lite-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast`

Use this API to submit an asynchronous task for fast video quality enhancement, which is ideal for latency\-sensitive scenarios. It leverages a speed\-first algorithm that combines lightweight super\-resolution and intelligent quality enhancement to balance processing efficiency with visual quality.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-lite">Video quality enhancement (fast)</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be enhanced.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB.<br><br>* **Input resolution**: Up to 2K is supported. Specific requirements:<br><br>   * Short side: [360, 1440]<br><br>   * Long side: [360, 2560] |
|`resolution` |String |No |`720p` |The target resolution level. You can use this parameter to upscale the video to a specified level. Supported values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br><br>**Note**: This parameter is mutually exclusive with `resolution_limit`; they cannot be configured at the same time. |
|`resolution_limit` |Integer |No |`1280` |The short\-side pixel limit of the target resolution, ranging from `[128, 2160]`. Based on this value, the system scales the video proportionally while preserving the original aspect ratio.<br><br>**Note**: This parameter is mutually exclusive with `resolution`; they cannot be configured at the same time. |
|`bitrate_level` |String |No |`medium` |The target bitrate level, used to control the average bitrate of the output video. This parameter affects the visual quality and final file size. The default is `medium`.<br><br><br>* `low`: Low bitrate<br><br>* `medium`: Medium bitrate (recommended)<br><br>* `high`: High bitrate<br><br><br>**Note**: The actual bitrate is also automatically calculated based on the target resolution and frame rate. For the target output bitrate of each level, see the [Bitrate reference](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-lite-task#bitrate-reference-table). To specify an exact bitrate, use the `bitrate` parameter. |
|`bitrate` |Integer |No |`8000` |The target average bitrate, in kbps, ranging from `[10, 150000]`. If omitted, it is automatically calculated based on `bitrate_level`, resolution, and frame rate. When both `bitrate` and `bitrate_level` are specified, only `bitrate` takes effect. |
|`fps` |Number |No |`30` |The target frame rate, in fps. If `fps` is not specified, the output video retains the same frame rate as the source. The value ranges from `[15, 120]`. We recommend not exceeding 4x the source frame rate. |
|`client_token` |String |No |`your_unique_id_123` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a fast video enhancement task that enhances the video to 720p with a high bitrate level.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/low_quality_video.mp4",
  "resolution": "720p",
  "bitrate_level": "high"
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="94a3889d"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-rotation-task#the-error-object) below. |


<span id="2a1c5ad0"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="dd755853"></span>
### Response example

<span id="25df72a1"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-fast-987654",
  "request_id": "20240523110000ABCDEFG67890"
}
```


<span id="b5470c8b"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240523110500XYZW54321",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameters 'resolution' and 'resolution_limit' cannot be configured at the same time.",
    "param": "resolution",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video quality enhancement is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The URL of the enhanced video file, in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`duration` |Number |`120.5` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. |
|`fps` |Number |`60` |The frame rate of the output video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-fast-987654",
    "request_id": "20240523110000ABCDEFG67890",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/fast_enhanced_output.mp4?auth_key=...",
        "duration": 65.5,
        "resolution": "720p",
        "fps": 30
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<span id="appendix"></span>
## References

<span id="bitrate-reference-table"></span>
### Bitrate reference

The following table lists the **target output bitrate** for `bitrate_level` set to `low`, `medium`, and `high` under different resolution and frame rate combinations. Note that to ensure quality stability across scenarios, the system dynamically adjusts the bitrate based on content complexity. Therefore, the actual output bitrate usually fluctuates between 0.8x and 1.5x of the target values listed in the table.


|Output resolution |Output frame rate (fps) |Low bitrate (Mbps) |Medium bitrate (Mbps) |High bitrate (Mbps) |
|---|---|---|---|---|
|240p |[15,30] |0.3 |0.45 |0.6 |
| |(30,60] |0.65 |0.9 |1.2 |
| |(60,120] |1.5 |2.2 |2.8 |
|360p |[15,30] |0.6 |0.85 |1.2 |
| |(30,60] |1 |1.5 |2 |
| |(60,120] |1.7 |2.5 |3.2 |
|480p |[15,30] |1.2 |1.8 |2.3 |
| |(30,60] |2.1 |3 |3.9 |
| |(60,120] |3.5 |5 |6.5 |
|540p |[15,30] |1.7 |2.5 |3.2 |
| |(30,60] |2.8 |4 |5.2 |
| |(60,120] |4.2 |6 |7.8 |
|720p |[15,30] |2.8 |4 |5.2 |
| |(30,60] |5.6 |8 |10 |
| |(60,120] |8.4 |12 |15 |
|1080p |[15,30] |5 |7 |9 |
| |(30,60] |10 |14 |18 |
| |(60,120] |15 |22 |28 |
|2K |[15,30] |10 |15 |20 |
| |(30,60] |17 |24 |32 |
| |(60,120] |28 |40 |52 |
|4K |[15,30] |21 |30 |39 |
| |(30,60] |32 |45 |58 |
| |(60,120] |53 |75 |100 |
|8K |[15,30] |42 |60 |78 |
| |(30,60] |63 |90 |120 |
| |(60,120] |84 |120 |150 |

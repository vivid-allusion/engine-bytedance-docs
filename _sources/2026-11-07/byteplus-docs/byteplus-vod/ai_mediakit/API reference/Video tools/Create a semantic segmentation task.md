---
title: "Create a semantic segmentation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment`

To programmatically split a long video into multiple independent and semantically complete clips, you can use this API. It submits an asynchronous task that analyzes a video's visual, audio, and narrative structure, using strategies like shot\-change and speech\-pause detection to identify optimal cut points. This allows you to automatically generate shorter semantic segments from a longer source video.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation">Semantic segmentation</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/media.mp4` |The URL of the video to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Video duration**: A single video must not exceed 3 hours. |
|`min_duration` |Number |No |`3` |The **target minimum duration** of a single segment (in seconds). Segments shorter than this value are merged with adjacent segments (provided the merged result does not exceed `max_duration`) to avoid producing overly short fragments (for example, quick flashback shots). The default is `3`, the minimum is `1`, and it must be less than or equal to `max_duration`. |
|`max_duration` |Number |No |`30` |The **target maximum duration** of a single segment (in seconds). Exceeding this value triggers a forced cut, ensuring segments are not too long. The default is `30`, the minimum is `1`, and it must be greater than or equal to `min_duration`. |
|`max_shift_tolerance` |Number |No |`2` |The cut\-point shift tolerance (in seconds). The default is 0, the minimum is 0, and it must be less than or equal to `min_duration`. When set greater than 0, the algorithm searches within this range around the cut point for a position closer to the semantics (such as the end of a sentence or a pause), so that the cut point falls at a natural pause rather than in the middle of a sentence. The larger this value, the closer the cut point aligns with the semantics, but the greater the fluctuation of the actual segment duration relative to `min_duration` or `max_duration`. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to perform semantic segmentation on a video, specifying the target segment duration range and boundary shift tolerance.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "min_duration": 5,
  "max_duration": 20,
  "max_shift_tolerance": 2
}'
```


<span id="response"></span>
## Response

After you call the API to submit the task, the interface immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

<span id="response-parameters"></span>
### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-task#error-object) below. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The error category, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="success-response"></span>
#### Success response

```JSON
{
  "success": true,
  "task_id": "amk-tool-semantic-segment-123456789",
  "request_id": "20260702130000ABCDEFG12345"
}
```


<span id="failure-response"></span>
#### Failure response

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20260702130500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "`min_duration` must be less than or equal to `max_duration`.",
    "param": "min_duration",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Semantic segmentation is an asynchronous task. The execution status and final result are not returned synchronously at submission time. You can obtain the task result in the following two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When the task is successfully completed, the `result` field in the task information you obtain contains the following:


|Parameter |Type |Description |
|---|---|---|
|`result_url` |String |The URL of the semantic segmentation result file. The file is a **gzip\-compressed JSON** containing fields such as `source`, `duration_ms`, `duration`, `has_audio`, `segment_count`, and `segments`. This is an HTTPS temporary download link, valid for **24 hours**; please download and save the file promptly. |
|`duration` |Number |The total duration of the input video (in seconds). |
|`segment_count` |Integer |The number of semantic segments produced by the final segmentation. |


Example of a complete final task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-semantic-segment-123456789",
    "request_id": "20260702130000ABCDEFG12345",
    "result": {
        "duration": 185.5,
        "segment_count": 12,
        "result_url": "https://example.byteplus.com/semantic_segments.json.gz?auth_key=..."
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


The structure of the JSON result file pointed to by `result_url` is as follows:

```JSON
{
    "duration_ms": 185500,
    "duration": 185.5,
    "has_audio": true,
    "segment_count": 12,
    "segments": [
        {
            "index": 0,
            "start_ms": 0,
            "end_ms": 12350,
            "start": "00:00:00.000",
            "end": "00:00:12.350"
        },
        {
            "index": 1,
            "start_ms": 12350,
            "end_ms": 27800,
            "start": "00:00:12.350",
            "end": "00:00:27.800"
        }
    ]
}
```


<span id="segment-object"></span>
### The segment object


|Parameter |Type |Description |
|---|---|---|
|`index` |Integer |The sequential index of the segment in the result, starting from `0`. |
|`start_ms` |Integer |The start time of the segment (in milliseconds). |
|`end_ms` |Integer |The end time of the segment (in milliseconds). |
|`start` |String |The start time of the segment, in the format `HH:mm:ss.SSS`. |
|`end` |String |The end time of the segment, in the format `HH:mm:ss.SSS`. |

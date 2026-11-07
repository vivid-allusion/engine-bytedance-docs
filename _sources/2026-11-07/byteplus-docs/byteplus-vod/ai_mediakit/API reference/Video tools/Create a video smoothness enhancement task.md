---
title: "Create a video smoothness enhancement task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-smoothness`

Use this API to submit an asynchronous video smoothness enhancement task. Based on the video frames and motion information, the tool automatically identifies stutter issues such as abrupt changes in motion rhythm and duplicate frames. It then uses optical flow, motion vectors, and other algorithms to generate intermediate frames or remove duplicate frames, intelligently repairing anomalous segments and restoring continuous, natural motion.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">By default, the tool enables both periodic stutter detection and duplicate frame detection, automatically repairs the detected issues, and directly returns the repaired video. To disable repair and perform detection only, or to use advanced operations such as manually specifying frame insertion positions, explicitly provide the <code>periodic_stutter_detect</code> and <code>duplicate_frame_detect</code> configuration objects. For the complete workflow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-smoothness-enhancement">Video smoothness enhancement</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header-parameters"></span>
### Header parameters


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/your_video.mp4` |The URL of the video to detect and repair. <br><br><br>* Video source: A publicly accessible HTTP or HTTPS URL.<br><br>* Supported formats: `mp4`, `avi`, `mov`.<br><br>* Resolution: Up to 4K<br><br>* Duration:<br><br>   * Detection and repair: Up to 35 seconds.<br><br>   * Detection only: No duration limit. |
|`periodic_stutter_detect` |Object |No |`{"periodic_stutter_repair": true, "align_source_fps": false}` |The periodic stutter detection and repair configuration. If you omit this object, periodic stutter detection and repair are performed by default. For details, see [The periodic stutter detect object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task#periodicstutterdetect). |
|`duplicate_frame_detect` |Object |No |`{"duplicate_frame_repair": true}` |The duplicate frame detection and repair configuration. If you omit this object, duplicate frame detection and repair are performed by default. For details, see [The duplicate frame detect object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task#duplicateframedetect). |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="periodicstutterdetect"></span>
#### The periodic stutter detect object


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`periodic_stutter_repair` |Boolean |No |`true` |Whether to repair detected periodic stutter. Default: `true`. <br><br><br>* `true`: Detect and repair periodic stutter. <br><br>* `false`: Detect periodic stutter without repairing it. |
|`insert_frame_indices` |Array of Integer |No |`[80, 120]` |An array of manually specified frame insertion positions, used to supplement stutter points that the algorithm may fail to detect. This parameter takes effect only when `periodic_stutter_repair` is `true`. Each array element is a zero\-based frame number. It must be a non\-negative integer, must not be duplicated, and the array must contain at least one element. For example, `[80, 120]` inserts one frame between frames 80 and 81 and another frame between frames 120 and 121. |
|`align_source_fps` |Boolean |No |`false` |Whether to keep the frame rate of the repaired video consistent with that of the source video. Default: `false`. <br><br><br>* `false`: Prioritizes the repair quality. The frame rate and total frame count of the output video may increase because frames are inserted.<br><br>* `true`: While inserting compensation frames, the tool removes the same number of low\-variation frames so that the total frame count and video duration remain unchanged. This option is suitable for scenarios that require a consistent frame rate. |


<span id="duplicateframedetect"></span>
#### The duplicate frame detect object


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`duplicate_frame_repair` |Boolean |No |`true` |Whether to repair detected duplicate frames. Default: `true`. <br><br><br>* `true`: Detect and remove duplicate frames.<br><br>* `false`: Detect duplicate frames without repairing them. |


<span id="request-example"></span>
## Request example

The following example shows how to perform the default stutter detection and repair on a video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-smoothness' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4"
}'
```


<span id="response"></span>
## Response

After you call the API to submit a task, the API immediately returns a synchronous response indicating whether the task was successfully submitted to the background processing queue.

<span id="0b83a9df"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successfully submitted. <br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier of the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task#error) below. |


<span id="error"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general error type, such as `BadRequest`. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |
|`param` |String |The specific parameter that caused the error. This field is optional. |


<span id="response-examples"></span>
### Response examples

<span id="success-response"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-smoothness-123456789",
  "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="failure-response"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240523101000WXYZ54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The 'video_url' parameter is required",
    "param": "video_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video smoothness enhancement is an asynchronous task. The execution status and final result are not returned synchronously when you submit the task. You can use either of the following methods to obtain the task result:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


After the task is successfully completed, the `result` field in the task details contains the following fields.


|Parameter |Type |Description |
|---|---|---|
|`video_url` |String |The URL of the repaired video file. Whether this field is returned determines the billing mode:<br><br><br>* This field is returned: The task performed an actual repair and is billed as **detection and repair**.<br><br>* This field is not returned: No repair was performed because you disabled all repair options, no issues were detected, or repair was automatically skipped after failing the quality evaluation. The task is billed as **detection only**.<br><br><br>The returned HTTPS URL is a temporary download URL that remains valid for 24 hours. Download and save the file promptly. |
|`duration` |Number |The duration of the input video, in seconds. This value is used for usage metering and billing. |
|`inserted_frames_detail` |Object |Details about the frames identified for insertion by periodic stutter detection. This object is returned whenever periodic stutter detection is enabled, which it is by default, regardless of whether repair is performed or automatically skipped after failing the quality evaluation. For details, see [The inserted frames detail object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task#c87c73ca). |
|`duplicate_frames_detail` |Object |Details about duplicate frame detection. This object is returned whenever duplicate frame detection is enabled, which it is by default, regardless of whether repair is performed or automatically skipped after failing the quality evaluation. For details, see [The duplicate frames detail object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-smoothness-enhancement-task#f8e1a1a1) |


<span id="c87c73ca"></span>
### The inserted frames detail object


|Parameter |Type |Description |
|---|---|---|
|`inserted_frame_count` |Integer |The number of frames that the algorithm determines should be inserted to repair periodic stutter in the source video. This value does not include frames manually specified through `insert_frame_indices`. It is a detection result and does not indicate the number of frames that were actually inserted. |


<span id="f8e1a1a1"></span>
### The duplicate frames detail object


|Parameter |Type |Description |
|---|---|---|
|`duplicate_frame_count` |Integer |The number of frames that the algorithm identifies as duplicates of their preceding frames. The basis for this count depends on whether periodic stutter repair is performed:<br><br><br>* If periodic stutter repair is successfully performed, duplicate frame detection processes the repaired intermediate result.<br><br>* If periodic stutter repair is disabled or automatically skipped after failing the quality evaluation, duplicate frame detection processes the source video. |


The following example shows the complete task details after a Video Smoothness Enhancement task is complete:

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-smoothness-123456789",
  "request_id": "20240523100000ABCDEFG12345",
  "status": "completed",
  "result": {
    "video_url": "https://example.com/output/repaired.mp4",
    "duration": 16.0,
    "inserted_frames_detail": {
      "inserted_frame_count": 24
    },
    "duplicate_frames_detail": {
      "duplicate_frame_count": 8
    }
  },
  "expires_at": 1777531298,
  "created_at": 1777358413,
  "finished_at": 1777359999
}
```

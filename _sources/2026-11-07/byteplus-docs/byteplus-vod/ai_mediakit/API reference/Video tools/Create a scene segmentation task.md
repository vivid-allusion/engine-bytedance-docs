---
title: "Create a scene segmentation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-scene-segmentation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/segment-scenes`

This API submits an asynchronous scene segmentation task that automatically splits a video into multiple scene segments based on its transitions and changes in visual content, and outputs the timeline information of each segment along with the corresponding independent video files.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-scene-segmentation">Scene segmentation</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/media.mp4` |The URL of the video to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Video duration**: A single video must not exceed 2 hours. |
|`return_segment_videos` |Boolean |No |`true` |Whether to generate and return clip video files.<br><br><br>* `true`: (default) Generates clip files and returns the download URL of each clip in `result.segments[].segment_video_url`.<br><br>* `false`: Does not generate clip files and returns only the clip timeline (`start_time` / `end_time`), without `segment_video_url`. This is suitable for scenarios where you only need the scene timecodes and handle clipping on your end, which can reduce task processing time. |
|`segment_threshold` |Number |No |`10` |The sensitivity threshold for scene segmentation. The value range is [0, 100). The default is 10.<br><br><br>* The lower the value, the more sensitive the algorithm is to scene changes, resulting in more segments.<br><br>* The higher the value, the more the algorithm tends to treat minor changes as the same scene, resulting in fewer segments.<br><br><br>When you set `min_duration`, `max_duration`, and `segment_threshold` at the same time, the system performs segmentation using the following two\-stage logic to ensure all constraints are satisfied:<br><br><br>1. The algorithm first segments based on the `segment_threshold` and `min_duration` you set.<br><br>2. After the first stage, if any clip exceeds the `max_duration` you set, the system ignores the effect of `segment_threshold` and segments again to ensure that the final durations do not exceed `max_duration`. |
|`min_duration` |Number |No |`3` |The minimum duration (in seconds) of a single clip. Segments shorter than this are merged. The default is 3. It should be less than or equal to `max_duration`. |
|`max_duration` |Number |No |`30` |The maximum duration (in seconds) of a single clip. Segments longer than this are forcibly split. The default is 30. It should be greater than or equal to `min_duration`. |
|`enable_clip_fade` |Boolean |No |`false` |Whether to output the detected fade\-in/fade\-out segments as independent clips. The default is `false`.<br><br><br>* `false`: (Default) Does not output fade transitions as separate clips. Fade\-in/fade\-out segments are treated as part of the preceding or following scene and merged into adjacent clips.<br><br>* `true`: Outputs fade transitions as separate clips. If there is a noticeable fade\-in/fade\-out transition in the video, the system splits it into an independent clip. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to perform scene segmentation on a video and return a separate file for each clip.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/segment-scenes' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "segment_threshold": 10,
  "min_duration": 3,
  "enable_clip_fade": true
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="9da1061c"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="b4ee9b13"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="3e3334fe"></span>
### Response example

<span id="d5a586bd"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-segment-scenes-123456789",
  "request_id": "20240521130000ABCDEFG12345"
}
```


<span id="7032ea46"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240521130500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "`min_duration` cannot be greater than `max_duration`.",
    "param": "min_duration, max_duration",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
### Asynchronous task result

Scene segmentation is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`segments` |Array |The list of clip information. Each element is an object containing information such as the start and end times of a clip. See the [The segment object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-scene-segmentation-task#segment-object) below for the detailed structure. |
|`duration` |Number |The total duration of the input video, in seconds. |


<span id="segment-object"></span>
#### The segment object


|Parameter |Type |Description |
|---|---|---|
|`start_time` |Number |The start time of the clip, in seconds. |
|`end_time` |Number |The end time of the clip, in seconds. |
|`segment_video_url` |String |The download URL for the clip's video file (in MP4 format, valid for 24 hours), which is returned only when `return_segment_videos` is `true`. |


The following is an example of the final complete task information:

```JSON
{
    "success": true,
    "task_id": "amk-tool-segment-scenes-123456789",
    "request_id": "20240521130000ABCDEFG12345",
    "result": {
        "duration": 185.5,
        "segments": [
            {
                "start_time": 0.0,
                "end_time": 15.2,
                "segment_video_url": "https://example.com/segment1.mp4?sign=..."
            },
            {
                "start_time": 15.2,
                "end_time": 45.8,
                "segment_video_url": "https://example.com/segment2.mp4?sign=..."
            },
            {
                "start_time": 45.8,
                "end_time": 185.5,
                "segment_video_url": "https://example.com/segment3.mp4?sign=..."
            }
        ]
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

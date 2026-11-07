---
title: "Create a precision erasure task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/erase-video-subtitle-pro` 

To programmatically remove hardcoded subtitles or other unwanted text from a video, you can call this API to submit an asynchronous precision erasure task. This feature achieves high\-quality, seamless removal by restoring the original picture to the greatest extent possible.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-precision-erasure">Precision erasure</a>.</div>


<span id="8766107c"></span>
## Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="daa922b7"></span>
## Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/video.mp4` |The URL of the video whose subtitles are to be erased. <br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* Supported languages: Chinese and English. Subtitles in other languages might not be recognized accurately.<br><br>* Input resolution: Supports up to 2K.<br><br>* Output resolution: Supports up to 1080P. |
|`model_version` |String |No |`v5` |The erasure algorithm version. The default is `v5`. <br><br><br>* `v5`: (default) Delivers stable erasure quality with fast processing. It optimizes subtitle flicker on AIGC\-generated videos, improves erasure of shadowed subtitles, and reduces mis\-erasure.<br><br>* `v5.6`: On top of V5, effectively mitigates flicker and water\-ripple artifacts after erasure, and adds erasure support for more languages (such as Spanish, Korean, Thai, Indonesian, Vietnamese, Japanese, Portuguese, German, and French). Note that it takes noticeably longer to process than `v5`, and in some scenarios—such as animated text or complex backgrounds—missed or incomplete erasure may still occur. |
|`mode` |String |No |`Subtitle` |The subtitle erasure mode. Defaults to `Subtitle`. <br><br><br>* `Subtitle`: Erase text that OCR detects as subtitles. By default, this mode processes only subtitles in the **lower half (bottom 50%)**  of the video frame. If `erase_ratio_location` is configured, the system erases only the text within the intersection of the custom erasure boxes and the lower\-half region. <br><br>* `Text`: Erase both subtitles and other types of text detected by OCR (such as people names and place names), excluding scene text (such as signboards). This mode performs text detection over the **entire video frame**. If `erase_ratio_location` is configured, the system performs erasure only within the specified boxes. |
|`output_encode_mode` |String |No |`Quality` |The output video encoding mode. Defaults to `Quality`. <br><br><br>* `Quality`: Quality\-first mode. Uses a higher bitrate for better quality, but the file size may be larger. <br><br>* `Size`: Size\-first mode. Keeps the output bitrate close to the source file while ensuring a certain level of quality. |
|`erase_ratio_location` |Array |No |`[{"top_...}, {"top_...}]` |The list of global erasure box positions. When configured, the system performs text erasure only within the specified rectangular regions, in combination with the mode setting. Up to 20 erasure boxes are supported. See [The location object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task#050b9899) below for the detailed structure. <br><br>**Note: ** <br><br><br>* The behavior of this parameter interacts with `mode`. In `Subtitle` mode, the effective erasure region is the intersection of the custom erasure boxes and the lower half of the frame.<br><br>* This parameter (global erasure boxes) is mutually exclusive with `time_segment_filter.segments[].erase_ratio_location` (per\-segment erasure boxes); they cannot be configured in the same request. To set different erasure regions for different time segments, use the per\-segment erasure boxes instead. |
|`time_segment_filter` |Object |No |`{"mode": "selected", ...}` |Restricts erasure to (or excludes) specific time segments of the video. When omitted, the entire video is processed. See [The time segment filter object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task#7d10328b) below for the detailed structure. |
|`subtitle_filter` |Object |No |`{"max_text_height_ratio": 0.15}` |Fine\-tunes the rules used to determine whether detected text is a subtitle in `Subtitle` mode, based on text height and horizontal centering. See [The subtitle filter object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task#e3eda049) below for the detailed structure. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="050b9899"></span>
### The location object

The location object defines a rectangular area for erasure. It uses a normalized coordinate system where the top\-left corner of the video is (0, 0) and the bottom\-right corner is (1, 1). The removal area is determined by specifying the coordinates of its top\-left and bottom\-right vertices.


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`top_left_x` |Number |Yes |`0.1` |The X coordinate of the box's **top\-left** corner, as a horizontal ratio relative to the left edge of the frame. The value range is `[0, 1]`: `0` aligns with the left edge, `1` aligns with the right edge. |
|`top_left_y` |Number |Yes |`0.8` |The Y coordinate of the box's **top\-left** corner, as a vertical ratio relative to the top edge of the frame. The value range is `[0, 1]`: `0` aligns with the top edge, `1` aligns with the bottom edge. |
|`bottom_right_x` |Number |Yes |`0.9` |The X coordinate of the box's **bottom\-right** corner (a horizontal ratio relative to the left edge of the frame). The value range is `[0, 1]`, and it must be greater than `top_left_x`. |
|`bottom_right_y` |Number |Yes |`0.95` |The Y coordinate of the box's **bottom\-right** corner (a vertical ratio relative to the top edge of the frame). The value range is `[0, 1]`, and it must be greater than `top_left_y`. |


The orange dashed box in the figure below represents the erasure area, which corresponds to the following location settings:

```JSON
"erase_ratio_location": [
  {
    "top_left_x": 0.62,
    "top_left_y": 0.86,
    "bottom_right_x": 0.97,
    "bottom_right_y": 0.96
  }
]
```


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a0d280353ea64c889c88d0ddb8539714) </span>

<span id="7d10328b"></span>
### The time segment filter object

The `time_segment_filter` object controls the erasure scope along the time dimension: it erases (or skips) only the specified time segments of the video. It is commonly used to process only the main content while preserving subtitles in the opening or closing credits.


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`mode` |String |Yes |`selected` |How the listed `segments` are applied. <br><br><br>* `selected`: Erase subtitles only within the listed segments. In this mode, you can also specify a separate erasure region for each segment, enabling fine\-grained control that erases different locations in different time segments.<br><br>* `skip`: Skip the listed segments and erase the remainder of the video. |
|`segments` |Array |Yes |`[{"start_time": 10, "end_time": 60}]` |The list of time segments. See [The segment object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task#461da4a0). |


<span id="461da4a0"></span>
### The segment object

The `segment` object represents a single time interval (defined by a start and end time in seconds). It is an element of the `segments` array and is used to precisely specify a portion of the video to process or skip.


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`start_time` |Number |Yes |`10` |The start time of the segment (in seconds). |
|`end_time` |Number |Yes |`60` |The end time of the segment (in seconds). Must be greater than `start_time`. |
|`erase_ratio_location` |Array |No |`[{"top_...}]` |A list of erasure boxes dedicated to this segment, used to assign an independent erasure region to each time segment. Up to 20 erasure boxes are supported per segment. See [The location object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task#050b9899) for the structure. Usage notes:<br><br><br>* Supported only when `time_segment_filter.mode` is `selected`. <br><br>* Per\-segment erasure boxes are mutually exclusive with the global erasure boxes; use one or the other. This parameter cannot be configured together with the top\-level `erase_ratio_location`. <br><br>   * To apply the **same** erasure boxes to all selected segments, use the top\-level `erase_ratio_location` parameter.<br><br>   * To apply **different** erasure boxes to different segments, or to apply erasure boxes to some segments while using the default behavior for others, configure only this per\-segment parameter. For segments that should use the default erasure behavior, set this parameter to an empty array `[]` or omit it. |


<span id="e3eda049"></span>
### The subtitle filter object

The subtitle_filter object helps the system identify subtitles more accurately by setting thresholds for text height and horizontal centering. This prevents accidental erasure of non\-subtitle content such as titles or logos.

> The `subtitle_filter` object takes effect only when `mode` is `Subtitle`.  If not specified, default values are used.



|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`min_text_height_ratio` |Number |No |`0.01` |Minimum text height. The minimum ratio of text height to video height. The value range is `[0, 1]`. Defaults to `0.01` (1%). Text shorter than this is not treated as subtitles. |
|`max_text_height_ratio` |Number |No |`0.1` |Maximum text height. The maximum ratio of text height to video height. The value range is `[0, 1]`. Defaults to `0.1` (10%). Text taller than this is not treated as subtitles. |
|`center_offset_ratio` |Number |No |`0.08` |Horizontal center offset. The maximum allowed ratio of the offset between the text's horizontal center and the video's horizontal center. The value range is `[0, 1]`. Defaults to `0.08`. Text exceeding this offset is not treated as a subtitle. |


The figure below illustrates how the system uses these thresholds to identify subtitles. Only text that meets all conditions (like the "Normal subtitle line" in the figure) will be erased. The thresholds in the figure correspond to the following subtitle_filter settings:

```JSON
"subtitle_filter": {
  "min_text_height_ratio": 0.01,
  "max_text_height_ratio": 0.1,
  "center_offset_ratio": 0.08
}
```


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cb8ca7985b9a4a8cb084aab672fc6cb0) </span>

<span id="87f73173"></span>
## Request example

<span id="bc183f69"></span>
### Example 1: Erasing a bottom\-right watermark

The following example uses `Text` mode to erase a watermark in the bottom\-right corner of the frame by specifying an erasure box.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/erase-video-subtitle-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Text",
  "erase_ratio_location": [
    {
      "top_left_x": 0.62,
      "top_left_y": 0.86,
      "bottom_right_x": 0.97,
      "bottom_right_y": 0.96
    }
  ]
}'
```


<span id="95283dba"></span>
### Example 2: Erasing subtitles only within a time segment

The following example uses the `time_segment_filter` parameter to erase subtitles only within the 10s–60s segment of the video, and uses `subtitle_filter` to constrain the subtitle detection range.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/erase-video-subtitle-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Subtitle",
  "time_segment_filter": {
    "mode": "selected",
    "segments": [
      { "start_time": 10, "end_time": 60 }
    ]
  },
  "subtitle_filter": {
    "min_text_height_ratio": 0.01,
    "max_text_height_ratio": 0.1
  }
}'
```


<span id="b4d024ec"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="3825fbe8"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="804fd75c"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="7c4a5a1e"></span>
### Response example

<span id="2e325efd"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-erase-video-subtitle-pro-123456789",
  "request_id": "20240520203000ABCDEFG12345"
}
```


<span id="31fe4666"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520203500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "`end_time` must be greater than `start_time`.",
    "param": "time_segment_filter.segments[0].end_time",
    "type": "BadRequest"
  }
}
```


<span id="eccf2fdf"></span>
## Asynchronous task result

Precision erasure is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The download URL for the video with subtitles erased. This URL is valid for **24 hours**. Please be sure to save the output file promptly. |
|`duration` |Number |`180.5` |The total duration of the output video (in seconds). |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-erase-video-subtitle-pro-123456789",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "duration": 180.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "202604272009269BA43D771246AFF513F0"
}
```

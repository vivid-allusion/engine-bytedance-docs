---
title: "Precision erasure"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-precision-erasure"
---

The AI MediaKit Precision Erasure tool automatically detects and removes hardcoded subtitles and on\-screen text from videos. Powered by BytePlus' high\-frame\-rate OCR and AIGC inpainting algorithms, it achieves high\-quality, seamless erasure that restores the original picture to the greatest extent possible—ideal for content localization, short\-form drama distribution, and professional creative reuse.

This guide walks you through submitting a precision erasure task via the API, and covers advanced configurations for erasure areas, time segments, and subtitle filtering.

<span id="quickstart-erasing-short-form-drama-subtitles"></span>
## Quickstart: Erasing short\-form drama subtitles

This section demonstrates how to use minimal configuration to automatically detect and erase subtitles for Chinese and English short\-form drama scenarios.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**, which is used for authentication in media processing.

* **Prepare a video file**: Have a video file ready for processing. Make your video file accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Precision erasure is an asynchronous task:


1. Call `POST /api/v1/tools/erase-video-subtitle-pro` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a precision erasure task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task) API. You can copy the following cURL command to submit it directly.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/erase-video-subtitle-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Subtitle"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with your own video URL.</div>


* <div data-tips="true" data-tips-type="default"><code>mode</code>: Set to <code>Subtitle</code>. In this mode, the system automatically detects and erases subtitles that meet the following criteria:</div>


   * <div data-tips="true" data-tips-type="default">Position: Located within the bottom 50% of the video, and horizontally centered.</div>


   * <div data-tips="true" data-tips-type="default">Size: The vertical character height is between 1% and 10% of the total video height.</div>


   * <div data-tips="true" data-tips-type="default">Color: White.</div>



Upon successful submission, you will receive a response containing a `task_id`. Save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-erase-video-subtitle-pro-123456789",
  "request_id": "20240520203000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task completes successfully, you will receive a response similar to the following. The `video_url` in the `result` field is the download URL for the processed video (output is in **MP4** format by default, valid for **24** hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-erase-video-subtitle-pro-123456789",
    "task_type": "erase-video-subtitle-pro",
    "status": "completed",
    "result": {
        "video_url": "https://example.bytepluses.com/erased-video.mp4?auth_key=...",
        "duration": 180.5
    },
    "expires_at": 1775047666,
    "created_at": 1774874853,
    "finished_at": 1774874866,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="e16b642c"></span>
### Choosing the erasure algorithm version

Precision erasure provides two algorithm versions—V5 and V5.6—selected via the `model_version` parameter when you submit a task. The default is `v5`. 


* V5 delivers stable erasure quality with fast processing: it optimizes subtitle flicker on AIGC\-generated videos, improves the erasure of shadowed subtitles, and reduces mis\-erasure. 

* On top of V5, V5.6 further improves erasure quality in two main areas:

   * **Visual stability**: Effectively mitigates flicker and water\-ripple artifacts left after erasure.

   * **Language coverage**: Beyond Chinese and English, adds erasure support for more languages, including Spanish, Korean, Thai, Indonesian, Vietnamese, Japanese, Portuguese, German, and French.


Note that V5.6 takes noticeably longer to process than V5, and in some scenarios—such as animated text or complex backgrounds—missed or incomplete erasure may still occur. Choose a version based on your needs: use V5.6 when you need multilingual subtitle support or higher visual stability, and use V5 in other cases for a balance of processing speed and erasure quality.

<span id="specifying-erasure-areas"></span>
### Specifying erasure areas

In addition to relying on OCR auto\-detection, you can manually specify one or more rectangular areas via the `erase_ratio_location` parameter; the system then erases the text detected within these areas. Erasure boxes are commonly used to remove **fixed\-position** on\-screen elements, such as watermarks, station logos, and fixed\-position text overlays showing names or locations, which are common in short\-form dramas.

Each box is defined by two vertices—its top\-left and bottom\-right corners. All coordinates are **normalized ratios** relative to the video width and height (with the top\-left corner of the frame as the origin `(0, 0)` and the bottom\-right corner as `(1, 1)`, ranging from 0.0 to 1.0), not pixel values:


* `top_left_x`: The X coordinate of the box's top\-left corner (a horizontal ratio relative to the left edge of the frame).

* `top_left_y`: The Y coordinate of the box's top\-left corner (a vertical ratio relative to the top edge of the frame).

* `bottom_right_x`: The X coordinate of the box's bottom\-right corner. Must be greater than `top_left_x`.

* `bottom_right_y`: The Y coordinate of the box's bottom\-right corner. Must be greater than `top_left_y`.


Taking a watermark in the bottom\-right corner of the frame as an example, the orange dashed box in the figure below is the erasure region, and the two orange vertices correspond to `(top_left_x, top_left_y)` and `(bottom_right_x, bottom_right_y)`:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a0d280353ea64c889c88d0ddb8539714) </span>

The behavior of the erasure box interacts with the `mode` parameter:


* In `Text` mode, the system erases only within the box, and the box itself is the final erasure region, so it can be placed anywhere in the frame (such as the bottom\-right corner). To erase fixed\-position elements such as watermarks, station logos, and name/place\-name bars, **use ** **`Text`** ** mode**.

* In `Subtitle` mode, the system processes only the lower half of the frame (Y ≥ 0.5) by default, so the effective erasure region is the intersection of the box and the lower half of the frame.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">To set different erasure regions for different time segments, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-precision-erasure#54146732">Specifying different erasure regions for different time segments</a>.</div>


The following configuration erases a watermark in the bottom\-right corner of the frame; its coordinates match the box in the figure above. `mode` is set to `Text` to ensure the system detects and erases all text types within the region, not just subtitles. To erase multiple fixed\-position elements (such as a station logo in the top\-left corner), add more erasure boxes to the `erase_ratio_location` array.

```JSON
{
  "video_url": "https://example.com/short_drama_clip.mp4",
  "mode": "Text",
  "erase_ratio_location": [
    {
      "top_left_x": 0.62,
      "top_left_y": 0.86,
      "bottom_right_x": 0.97,
      "bottom_right_y": 0.96
    }
  ]
}
```


<span id="specifying-time-segments-to-erase-or-skip"></span>
### Specifying time segments to erase or skip

When you only need to erase subtitles in specific segments of a video (such as the main content) while preserving subtitles in others (such as opening or closing credits), use the `time_segment_filter` parameter to define one or more time segments and apply different actions:


* `selected`: Erase subtitles only within the listed segments.

* `skip`: Skip the listed segments and erase the remainder of the video.


Each segment is defined by `start_time` and `end_time` (in seconds), where `end_time` must be greater than `start_time`.

**Example 1: Erasing subtitles within the 10s–60s segment**

```JSON
{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Subtitle",
  "time_segment_filter": {
    "mode": "selected",
    "segments": [
      { "start_time": 10, "end_time": 60 }
    ]
  }
}
```


**Example 2: Skipping the opening credits (the first 15 seconds)** 

```JSON
{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Subtitle",
  "time_segment_filter": {
    "mode": "skip",
    "segments": [
      { "start_time": 0, "end_time": 15 }
    ]
  }
}
```


<span id="54146732"></span>
### Specifying different erasure regions for different time segments

When the subtitle position differs across time segments of the same video (for example, subtitles at the bottom in the first half and an additional bottom\-right watermark in the second half), you can—when `time_segment_filter.mode` is `selected`—assign a separate erasure box to each segment in `segments` via its own `erase_ratio_location`, enabling fine\-grained control that erases different locations in different time segments. These per\-segment boxes are mutually exclusive with the global erasure box setting; you can only use one or the other. This parameter cannot be configured together with the top\-level `erase_ratio_location` parameter. Usage recommendations:


* To apply the **same** erasure boxes to all selected segments, use the top\-level `erase_ratio_location` parameter. See [Specifying erasure areas](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-precision-erasure#specifying-erasure-areas).

* To apply **different** erasure boxes to different segments, or to apply erasure boxes to some segments while using the default behavior for others, configure only this per\-segment parameter. For segments that should use the default erasure behavior, set this field to an empty array `[]` or omit it.


<span id="77151c6a"></span>
#### Example: Erasing different regions in different time segments

The following example processes only two time segments: from 10s to 60s it erases only the subtitle region at the bottom of the frame, and from 90s to 120s it instead erases the watermark region in the bottom\-right corner; no erasure is performed in any other time segment.

```Plain Text
{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Text",
  "time_segment_filter": {
    "mode": "selected",
    "segments": [
      {
        "start_time": 10,
        "end_time": 60,
        "erase_ratio_location": [
          {
            "top_left_x": 0.1,
            "top_left_y": 0.8,
            "bottom_right_x": 0.9,
            "bottom_right_y": 0.95
          }
        ]
      },
      {
        "start_time": 90,
        "end_time": 120,
        "erase_ratio_location": [
          {
            "top_left_x": 0.62,
            "top_left_y": 0.86,
            "bottom_right_x": 0.97,
            "bottom_right_y": 0.96
          }
        ]
      }
    ]
  }
}
```


<span id="e6ec766e"></span>
### Fine\-tuning subtitle detection (subtitle filter)

In `Subtitle` mode, the system determines which text is a subtitle based on characteristics such as text height and horizontal centering. You can fine\-tune the detection rules via the `subtitle_filter` parameter to adapt to different subtitle styles:


* `min_text_height_ratio`: The minimum text\-height ratio (relative to video height). Defaults to `0.01`. Text shorter than this is not treated as a subtitle.

* `max_text_height_ratio`: The maximum text\-height ratio (relative to video height). Defaults to `0.1`. Text taller than this is not treated as a subtitle.

* `center_offset_ratio`: The maximum offset of the text\-region center relative to the video's horizontal center. Defaults to `0.08`. Text exceeding this offset is not treated as a subtitle.


The figure below uses a portrait short\-form drama as an example to show how these three thresholds together determine whether a piece of text is a subtitle: text is treated as a subtitle and erased only when its height is between the minimum and maximum thresholds and it is sufficiently centered horizontally. Text that is too small (such as watermarks), too large (such as titles), or off\-center (such as station logos) is excluded.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cb8ca7985b9a4a8cb084aab672fc6cb0) </span>

The following example relaxes the maximum subtitle text height to 15% of the frame height to erase larger subtitles:

```JSON
{
  "video_url": "https://example.com/source_video.mp4",
  "mode": "Subtitle",
  "subtitle_filter": {
    "max_text_height_ratio": 0.15
  }
}
```


<span id="reference"></span>
## Reference

<span id="application-scenarios"></span>
### Application scenarios


* **Creative reuse and remixing**: Remove original subtitles before re\-editing or remixing, so you can add custom subtitles or audio that match a new theme and style.

* **Content localization and overseas distribution**: When distributing short\-form dramas overseas, erase the original subtitles before adding target\-language subtitles, and vice versa.

* **AIGC content correction**: When AIGC\-generated videos contain unintended text or subtitles, use this tool for high\-quality, seamless erasure.

* **Advertising and marketing**: Adjust ad videos for different platforms and audiences by erasing existing subtitles and redesigning new ones.


<span id="limitations"></span>
### Limitations


|Item |Description |
|---|---|
|Input file |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Supported languages**: The languages supported by subtitle detection (OCR) depend on the selected `model_version`. `v5` is optimized for **Chinese** and **English**; `v5.6` additionally supports more languages, such as Spanish, Korean, Thai, Indonesian, Vietnamese, Japanese, Portuguese, German, and French. Subtitles in a language that the selected version does not support, or whose language cannot be recognized, may not be recognized accurately, which can affect the erasure result. <br><br>* **Input resolution**: Supports up to 2K. |
|Output resolution |The output resolution matches the input. If the input exceeds 1080p, the output defaults to 1080p. |


<span id="processing-time"></span>
### Processing time

Task processing time depends on the source video duration and the selected algorithm version. RTF (Real\-Time Factor) is the ratio of processing time to video duration; a lower value means faster processing, and you can use it to estimate task duration. The reference RTF values are as follows:


|Video duration |V5 RTF |V5.6 RTF |
|---|---|---|
|Over 1 min |5 |9 |
|Under 1 min |20 |30 |


<span id="related-api-documentation"></span>
## Related APIs


* [Create a precision erasure task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-precision-erasure-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

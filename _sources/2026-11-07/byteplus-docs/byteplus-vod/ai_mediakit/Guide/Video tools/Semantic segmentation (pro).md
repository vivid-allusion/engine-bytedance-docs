---
title: "Semantic segmentation (pro)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-semantic-segmentation-pro"
---

The AI MediaKit semantic segmentation (pro) tool is designed for long\-video understanding, material repurposing, and re\-editing scenarios. Building on the basic edition's semantic segmentation, it further combines shot boundaries, scene semantics, ASR/OCR text, and duration constraints to split a long video into segments that are semantically complete and appropriately sized. Compared with [Semantic segmentation (basic)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation), the pro edition provides three built\-in industry strategies for **short dramas, film and TV series, and mini\-games**, supports a **custom strategy**, and returns detailed segment, shot, scene, and sentence results directly in the response.

This development guide walks you through how to:

* Understand how semantic segmentation (pro) works and its built\-in segmentation strategies.

* Quickly get semantic segmentation results from a video.

* Learn how to select a segmentation strategy for your business scenario, control the segment duration range, and return shot, scene, and sentence details on demand.

## Basic and pro editions

AI MediaKit offers two editions of semantic segmentation—basic and pro—to meet the needs of different scenarios. In general, the basic edition suits general\-purpose, fast video repurposing scenarios, while the pro edition provides more powerful and fine\-grained analysis capabilities and a more convenient way to obtain results, making it well\-suited to scenarios with higher requirements for segmentation quality, analysis dimensions, and integration efficiency. The following table compares the main differences between the two editions:

|Comparison item |Semantic segmentation (basic) |Semantic segmentation (pro) |
|---|---|---|
|Core features |General\-purpose semantic segmentation that comprehensively analyzes picture, speech, and narrative structure. |Provides industry\-oriented segmentation strategies (short drama, film and TV, games) and supports multi\-dimensional analysis (shots, scenes, sentences). |
|Applicable scenarios |Preliminary, fast semantic repurposing of videos. |* Fine\-grained, scenario\-specific repurposing<br><br>* Obtaining structured information such as shots, scenes, and sentences<br><br>* Getting segment videos directly |
|Segmentation strategy |A general\-purpose strategy; the `max_shift_tolerance` parameter can fine\-tune cut points to ensure semantic completeness. |Provides three built\-in industry strategies—`short_drama`, `movie_series`, `mini_game`—as well as a flexibly configurable `custom` strategy. |
|Getting results |After the asynchronous task completes, you download a gzip\-compressed JSON file via the returned `result_url` to get results. |After the asynchronous task completes, all results such as segments, shots, and scenes are returned directly in the `result` field of the Get task details response—no download required. |
|Result content |The result file contains only the timeline information of segments (the `segments` list). |In addition to the `segments` list, the result can include detailed lists of shots (`shots`), scenes (`scenes`), and sentences (`sentences`) on demand. |
|Segment video generation |Not supported. |Supported. By setting the request parameter `return_segment_videos` to `true`, you can get the video file link of each segment directly in the result. |

How to choose:

* If your core need is to quickly split a long video into roughly semantic segments and you do not have high requirements for development cost and integration efficiency, the **basic** edition is a cost\-effective choice.

* If your business scenario (such as short dramas or film/TV re\-cuts) is well defined, you need deeper structured video analysis (shots, scenes, sentences), you want to simplify the development flow (getting results directly instead of downloading a file), or you want to generate segment videos on demand, we recommend the **pro** edition.

## Quickstart: Get semantic segmentation results from a video

This section uses a concrete example to demonstrate how to perform pro semantic segmentation on a video file and get the information of all semantic segments.

### Prerequisites

1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/imp/ai-mediakit/settings) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

2. **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).

### Procedure

Semantic segmentation (pro) is an asynchronous task. The overall flow is as follows:

1. After you successfully call `POST /api/v1/tools/semantic-segment-pro` to submit the task, you obtain a unique `task_id`.

2. You can poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response directly: the `segments` array is always returned and contains the timeline information of all semantic segments; details such as `shots`/`scenes`/`sentences` are returned on demand based on `include_detail_types` and the selected strategy.

#### Step 1: Submit the task

Call the [Create a semantic segmentation (pro) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task) API. You can directly copy the following cURL command to submit a basic pro semantic segmentation task to the API. The pro edition requires you to specify the segmentation strategy via `strategy`; this example uses the short\-drama strategy `short_drama`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "strategy": "short_drama"
}'
```

> **Note**

* > Replace `{Your_API_Key}` with your valid API Key.

* > Replace the value of `video_url` with the URL of your own video file.

* > `strategy` is required. Choose an appropriate segmentation strategy based on your video content (see [Select a segmentation strategy](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation-pro#select-a-segmentation-strategy-strategy) below).

Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-semantic-segment-pro-123456789",
  "request_id": "20260807130000ABCDEFG12345"
}
```

#### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to get the final result until the task status becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```

> **Note**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task is successfully completed, you will receive the following response. Unlike the basic edition, the pro edition's segmentation results are returned directly in the `result` field, and the `segments` array always contains all semantic segments.

```JSON
{
  "success": true,
  "task_id": "amk-tool-semantic-segment-pro-123456789",
  "status": "completed",
  "result": {
    "duration": 185.5,
    "segment_count": 2,
    "segments": [
      {
        "index": 0,
        "start_ms": 0,
        "end_ms": 12500,
        "start": "00:00:00.000",
        "end": "00:00:12.500",
        "shot_ids": [0, 1],
        "text": "Segment text"
      },
      {
        "index": 1,
        "start_ms": 12500,
        "end_ms": 27800,
        "start": "00:00:12.500",
        "end": "00:00:27.800",
        "shot_ids": [2, 3],
        "text": "Segment text"
      }
    ]
  }
}
```

## Advanced usage

### Select a segmentation strategy

The pro edition specifies the segmentation strategy via `strategy`. Choose one based on the type of video content:

* `short_drama`: Short dramas and narrative content. Fuses OCR and ASR and protects sentence integrity.

* `movie_series`: Film and TV series content. Automatically performs scene detection and semantic merging.

* `mini_game`: Mini\-game screen recordings. Filters out static, low\-quality, and pop\-up segments.

* `custom`: Custom scene detection and sentence\-integrity protection. Can be used together with `enable_scene_detection` and `avoid_sentence_cutoff`.

### Control the segment duration range

You can use `min_duration` and `max_duration` to control the target duration range of a single segment (in seconds, both with a value range of `[1, 600]`):

* `min_duration`: The minimum duration of a single segment. Defaults to 3 seconds when omitted, and must not be greater than `max_duration`.

* `max_duration`: The maximum duration of a single segment. Defaults to 30 seconds when omitted, and must not be less than `min_duration`.

### Use the custom strategy

When the built\-in strategies do not meet your needs, you can set `strategy` to `custom` and finely control the segmentation behavior via the following two switches (they take effect only when `strategy=custom`; other strategies use their own built\-in configurations):

* `enable_scene_detection`: Whether to enable scene detection. Defaults to `false`; when enabled, semantic scene merging is performed on top of shot segmentation.

* `avoid_sentence_cutoff`: Whether to enable sentence detection and try to avoid cutting a segment in the middle of a sentence. Defaults to `false`; this capability relies on ASR/OCR, and we recommend disabling it for videos with no recognizable speech or subtitles.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "strategy": "custom",
  "min_duration": 5,
  "max_duration": 20,
  "enable_scene_detection": true,
  "avoid_sentence_cutoff": true
}'
```

### Return shot, scene, and sentence details

By default, the response returns only the segment list `segments`. To additionally get shot, scene, or sentence details in the result, specify them via `include_detail_types` (multiple values allowed):

* `shot_list`: Returns the shot list `shots` and the total number of shots `shot_count`.

* `scene_list`: Returns the scene shot list `scenes` and the total number of scenes `scene_count`; returned only when `strategy=movie_series`, or `strategy=custom` with `enable_scene_detection=true`.

* `sentence_list`: Returns the sentence result list `sentences` and the total number of sentences `sentence_count`; returned only when the selected strategy enables sentence detection and the video contains recognizable speech or subtitles. The `mini_game` strategy never returns this list.

> **Note**: `include_detail_types` controls only the response content and is not passed down to the underlying workflow; the segment list `segments` is always returned.

### Return actual segment videos

By default (`return_segment_videos=false`), the response returns only JSON information such as segment timelines. If you set `return_segment_videos` to `true`, the system also generates a video file for each segment and returns the download link in the response's `segments[].video_url`.

## Reference

### Usage limits

|Limit |Description |
|---|---|
|Input file limits |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* Video duration: A single video must not exceed 3.5 hours. |

### Billing

The semantic segmentation (pro) tool is billed by input video duration. For detailed billing rules and unit prices, see [Semantic segmentation (pro) pricing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#semantic-segmentation-pro-pricing).

## Related APIs

* [Create a semantic segmentation (pro) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

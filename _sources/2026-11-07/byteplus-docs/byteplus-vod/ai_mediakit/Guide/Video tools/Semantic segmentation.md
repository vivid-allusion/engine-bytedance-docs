---
title: "Semantic segmentation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-semantic-segmentation"
---

The AI MediaKit semantic segmentation (basic) tool uses semantic understanding of video content to accurately split a long video into multiple segments, each containing a complete semantic unit, and outputs the start and end timeline information for each segment. Unlike traditional shot segmentation based on transitions or frame differences, semantic segmentation comprehensively analyzes the visuals, speech, and narrative structure to ensure that cut points are semantically complete (for example, it will not cut off in the middle of a sentence), making the segments align better with boundaries that define a complete, self\-contained meaning. This is suitable for scenarios such as short\-video repurposing, editing material retrieval, and multimodal data annotation.

This development guide walks you through how to:


* Understand how semantic segmentation works.

* Quickly get the timecode results of semantic segments from a video.

* Learn how to adjust the target segment duration range and tolerance to fit your business needs.


<span id="quickstart-get-the-semantic-segment-timeline-of-a-video"></span>
## Quickstart: Get the semantic segment timeline of a video

This section uses a concrete example to demonstrate how to perform semantic segmentation on a video file and get the start and end timestamps of all semantic segments.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Semantic segmentation is an asynchronous task. The overall flow is as follows:


1. After you successfully call `POST /api/v1/tools/semantic-segment` to submit the task, you obtain a unique `task_id`.

2. You can poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)API until the task `status` becomes `completed`. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response: `result_url` points to a gzip\-compressed JSON file whose `segments` array contains the timeline information of all semantic segments.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a semantic segmentation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-task)API. You can directly copy the following cURL command to submit a basic semantic segmentation task to the API.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-semantic-segment-123456789",
  "request_id": "20260702130000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to get the final result until the task status becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result_url` in the `result` field points to a gzip\-compressed JSON result file.

```JSON
{
    "success": true,
    "task_id": "amk-tool-semantic-segment-123456789",
    "status": "completed",
    "result": {
        "duration": 185.5,
        "segment_count": 12,
        "result_url": "https://example.byteplus.com/semantic_segments.json.gz?auth_key=..."
    }
}
```


Download and decompress the file pointed to by `result_url` to get the complete segmentation result. The example structure is as follows:

```JSON
{
    "duration_ms": 185500,
    "duration": 185.5,
    "has_audio": true,
    "segment_count": 12,
    "segments": [
        {"index": 0, "start_ms": 0,     "end_ms": 12350, "start": "00:00:00.000", "end": "00:00:12.350"},
        {"index": 1, "start_ms": 12350, "end_ms": 27800, "start": "00:00:12.350", "end": "00:00:27.800"},
        ...
    ]
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="adjust-the-segmentation-granularity"></span>
### Adjust the segmentation granularity

You can use the three parameters `min_duration`, `max_duration`, and `max_shift_tolerance` to finely control the target duration range and boundary tolerance of semantic segments:


* `min_duration`: The target minimum duration of a segment (in seconds). The default is 3, and the minimum is 1. Segments shorter than this value are merged with adjacent segments (provided the merged result does not exceed `max_duration`) to avoid producing overly short fragments (for example, quick flashback shots).

* `max_duration`: The target maximum duration of a segment (in seconds). The default is 30, and the minimum is 1. Exceeding this value triggers a forced cut, ensuring segments are not too long.

* `max_shift_tolerance`: The cut\-point shift tolerance (in seconds). The default is 0, and the minimum is 0. When set greater than 0, the algorithm searches within this range around the cut point for a more semantically appropriate position (such as the end of a sentence or a pause), ensuring the cut point falls at a natural pause rather than in the middle of a sentence. The larger this value, the closer the cut point aligns with the semantics, but the actual segment duration will fluctuate more relative to `min_duration` or `max_duration`.


In the following example, the API will:


* Control the target semantic segment duration to between 5 and 20 seconds;

* Allow a fluctuation of up to ±2 seconds near semantic boundaries to align as much as possible with clearer shots or speech pauses.


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


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Video duration**: A single video must not exceed 3 hours. |


<span id="related-api-references"></span>
## API references


* [Create a semantic segmentation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

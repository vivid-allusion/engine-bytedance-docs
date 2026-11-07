---
title: "Video quality assessment (VQScore)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-quality-assessment"
---

To quantitatively assess and monitor video quality without a reference source, you can use the AI MediaKit video quality assessment tool. It integrates VQScore, a no\-reference algorithm that simulates human perception to provide an objective quality score. This development guide walks you through the API calls to quickly get a VQScore for any video, handle the asynchronous task, and understand the results.

<span id="quickstart-get-the-quality-score-of-a-video"></span>
## Quickstart: Get the quality score of a video

This section demonstrates how to quickly get the VQScore quality score for a specified video URL.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare a video file**: Have a video file ready for assessment, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Video quality assessment is an asynchronous task:


1. After you successfully call `POST /api/v1/tools/assess-video-quality`, the API returns a task ID.

2. You can poll `GET /api/v1/tasks/{task_id}` until the task `status` is `completed`. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task status updates.

3. Once the task is complete, parse the `result` field to get the final quality score from the `vq_score` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a video quality assessment (VQScore) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-quality-assessment-task) API. You can directly copy the following cURL command to submit it.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/assess-video-quality' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/your_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your video.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-assess-video-quality-12345",
  "request_id": "20240523110000ABCDEFG98765"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

The quality assessment task takes some time. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` is `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object from which you can directly get the quality score from the `vq_score` field.

```JSON
{
    "success": true,
    "task_id": "amk-tool-assess-video-quality-12345",
    "request_id": "20240523110000ABCDEFG98765",
    "status": "completed",
    "result": {
        "vq_score": 88.5,
        "duration": 91.2
    },
    "expires_at": 1777534898,
    "created_at": 1777362013,
    "finished_at": 1777362599
}
```


VQScore ranges from `[0, 100]`; a higher score indicates better quality. You can refer to the following table to understand the quality level of different score ranges:


|Score range |Subjective perception |Recommended action |
|---|---|---|
|`[0, 60)` |Poor |The quality is severely damaged and may contain noticeable noise, blur, or compression artifacts. It is recommended to use the [Video quality enhancement (standard/professional)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement) tool to enhance it. |
|`[60, 70)` |Good |Acceptable to most users, but may have minor flaws. Suitable for scenarios with lower quality requirements. |
|`[70, 100]` |Clear |Subjectively clear with well\-preserved details. Suitable for HD distribution scenarios. |


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input video limits |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* Resolution limit: The input video supports up to 4K (3840×2160) resolution. |


<span id="related-api-references"></span>
## API references


* [Create a video quality assessment (VQScore) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-quality-assessment-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

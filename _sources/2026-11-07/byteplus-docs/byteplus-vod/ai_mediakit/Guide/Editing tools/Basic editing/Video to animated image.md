---
title: "Video to animated image"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-to-animated-image"
---

The AI MediaKit animated image extraction tool can extract a segment from a video file over a specified time range and generate a high\-quality animated image (in GIF or WebP format). This tool is suitable for scenarios such as creating highlight previews, social media sharing materials, and product feature demo animations.

This guide walks you through how to:


* Understand the core capabilities and application scenarios of animated image extraction.

* Quickly extract an animated image of a specified duration from a video.

* Learn how to specify the output animated image format.


<span id="quickstart-extract-an-animated-image-from-a-video"></span>
## Quickstart: Extract an animated image from a video

This scenario demonstrates how to extract a segment from 10.5 to 15.0 seconds of a video and generate an animated image in GIF format.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

2. **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Animated image extraction is an asynchronous task:


1. After you successfully call `POST /api/v1/tools/extract-animated-image`, the API returns a task ID.

2. You can poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field to get the download URL of the final animated image file from the `image_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a video to animated image task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-to-animated-image-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-animated-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source_video.mp4",
  "start_time": 10.5,
  "end_time": 15.0
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-extract-animated-image-1400600",
  "request_id": "20260325160500A8DE7F57A9B3E17A0FF5"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object from which you can get the download URL of the animated image from the `image_url` field (valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-animated-image-1400600",
    "status": "completed",
    "result": {
        "image_url": "https://example.byteplus.com/animated_output.webp?auth_key=1774612861-...",
        "duration": 4.5,
        "resolution": "480p"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20260325160500A8DE7F57A9B3E17A0FF5"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="specify-the-output-animated-image-format"></span>
### Specify the output animated image format

By default, the generated animated image is in `gif` format. You can use the `output_format` parameter to specify the `webp` format for better compression and quality.

<span id="example-extract-an-animated-image-from-a-video-and-save-it-as-a-webp-file"></span>
#### Example: Extract an animated image from a video and save it as a WebP file

```JSON
{
   "video_url": "https://example.com/my_video.mp4",
   "start_time": 10.5,
   "end_time": 15.0,
   "output_format": "webp"
}
```


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Video formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Resolution**: Up to 4K (3840×2160) is supported. |
|Output animated image limits |* **Duration**: The output animated image duration (`end_time` \- `start_time`) cannot exceed 60 seconds.<br><br>* **Resolution**: The maximum resolution of the output animated image is 480p. If the input video resolution is lower than 480p, the output resolution matches the input.<br><br>* **Frame rate**: The frame rate of the output animated image is fixed at 15 fps. |


<span id="related-api-references"></span>
## Related API references


* [Create a video to animated image task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-to-animated-image-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

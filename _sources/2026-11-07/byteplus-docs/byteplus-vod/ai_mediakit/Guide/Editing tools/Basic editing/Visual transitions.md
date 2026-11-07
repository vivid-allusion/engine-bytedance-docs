---
title: "Visual transitions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-visual-transitions"
---

AI MediaKit provides a series of visual transformation tools that let you flexibly adjust the spatial properties of a video via API. These tools include:


* **Video flip**: Flip a video horizontally (left\-right mirror) or vertically (top\-bottom).

* **Video rotation**: Rotate the entire video frame 90 degrees to the left, 90 degrees to the right, or 180 degrees.

* **Video cropping**: Crop a rectangular region from the video frame based on specified pixel coordinates to produce a new video.

* **Video compositing**: Spatially combines multiple videos (horizontally or vertically) into a single composite frame.


All visual transformation tools are asynchronous tasks and follow a unified API call flow, making them easy to integrate.

<span id="quickstart-flip-a-video-horizontally"></span>
## Quickstart: Flip a video horizontally

This section uses a concrete example to demonstrate how to flip a video horizontally.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready to be flipped, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

A visual transformation is an asynchronous task. The overall workflow is as follows:


1. After you call the corresponding tool's `POST` endpoint to submit the task, you receive a unique `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task completion notifications.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the transformed video.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a video flip task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-flip-task) API. You can copy the following cURL command to submit a horizontal video flip task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/flip-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_source_video.mp4",
  "is_flip_horizontal": true
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-flip-video-123456789",
  "request_id": "20240520163000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` in the `result` field is the download URL of the flipped video (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-flip-video-123456789",
    "task_type": "flip-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/flipped-video.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 65.88
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```


All visual transformation tools follow the "submit\-and\-query" flow above and support common asynchronous parameters such as `client_token` and `callback_url`. You only need to replace the request **endpoint** and the **core parameters** as needed.

<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Quantity limit**: A single task supports 1 to 100 URLs.<br><br>* **Supported formats**:<br><br>   * Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * Mainstream audio formats such as `mp3`, `m4a`, `wav`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported for input videos. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the video's duration and resolution. The longer the video and the higher the resolution, the longer the processing time. The average RTF (processing time / source duration) is 1.

<span id="related-api-references"></span>
## Related APIs


* [Create a video flip task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-flip-task)

* [Create a video rotation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-rotation-task)

* [Create a video cropping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-cropping-task)

* [Create a video composition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-composition-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

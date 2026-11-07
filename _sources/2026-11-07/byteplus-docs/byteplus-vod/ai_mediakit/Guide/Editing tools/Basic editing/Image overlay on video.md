---
title: "Image overlay on video"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-image-overlay"
---

The AI MediaKit add\-image\-to\-video tool lets you overlay a static image (such as a logo, QR code, watermark, or any decorative element) onto a specified position of a video frame. You can precisely control the size and position of the image as well as the start and end time it appears in the video.

This guide walks you through how to add an image watermark to your video via an API call.

<span id="quickstart-add-a-bottom-right-logo-to-a-video"></span>
## Quickstart: Add a bottom\-right logo to a video

This section uses a concrete example to demonstrate how to add a PNG logo image as a watermark to the bottom\-right corner of a video and keep it displayed throughout the entire video.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare materials**: Upload the following two files to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain URLs that the API can access.

   * **Video file**: Have a video file ready that needs a watermark.

   * **Image file**: Have an image ready to use as the watermark (a PNG with an alpha channel is recommended).


<span id="procedure"></span>
### Procedure

Add\-image\-to\-video is an asynchronous task. The overall workflow is as follows:


1. After you call `POST /api/v1/tools/add-image-to-video` to submit the task successfully, you receive a unique `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task completion notifications.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the processed video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a video image overlay task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-image-overlay-task) API. You can copy the following cURL command to submit a watermark task. This example uses the default parameters, placing the image in the bottom\-right area of the video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-image-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_source_video.mp4",
  "sub_image_url": "https://example.com/your_logo.png"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the values of <code>video_url</code> and <code>sub_image_url</code> with the URLs of your own video and image files.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-add-image-to-video-123456789",
  "request_id": "20240520193000ABCDEFG12345"
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


When the task is successfully completed, you will receive the following response. The `video_url` in the `result` field is the download URL of the video with the image added (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-image-to-video-123456789",
    "task_type": "add-image-to-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/watermarked-video.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 120.0
    },
    "expires_at": 1775047666,
    "created_at": 1774874853,
    "finished_at": 1774874866,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="control-how-long-the-watermark-is-displayed"></span>
### Control how long the watermark is displayed

By default, the added image is displayed from the start of the video to the end. You can use the `start_time` and `end_time` parameters to make the image appear only during a specific time range of the video. For example, the configuration below displays the logo only between the 5th and 15th second of the video.

```JSON
{
  "video_url": "https://example.com/your_source_video.mp4",
  "sub_image_url": "https://example.com/your_logo.png",
  "start_time": 5.0,
  "end_time": 15.0
}
```


<span id="related-api-references"></span>
## Related APIs


* [Create a video image overlay task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-image-overlay-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

---
title: "Video transcoding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-transcoding"
---

The AI MediaKit Video Transcoding tool allows you to flexibly modify a video's encoding standard (such as H.264, H.265), resolution, bitrate, frame rate, and container format (such as MP4, FLV) to suit various business scenarios, playback devices, and network conditions.

This quickstart guide demonstrates how to convert a portrait video to a square (720x720) format by automatically padding the sides with black bars.

<span id="quickstart-basic-transcoding-task"></span>
## Quickstart: Basic transcoding task

This section demonstrates how to convert a portrait video to a 720x720 resolution, automatically padding it with black bars.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Video transcoding is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/transcode-video` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-transcoding-task"></span>
#### Step 1: Submit the transcoding task

You need to call the [Create a video transcoding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-transcoding-task) API. You can copy the following cURL command to submit a task that converts a portrait video to 720x720 resolution and automatically pads it with black bars.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-video' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_url": "https://vod-ai-test.bytepluses.com/demo/demo_480p.mp4",
  "video": {
      "scale_type": 2,
      "scale_width": 720,
      "scale_height": 720,
      "scale_mode": 2
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with your own URL.</div>


* <div data-tips="true" data-tips-type="default">This example demonstrates how to change the aspect ratio of a video. We convert a portrait video to a 1:1 square video. By setting <code>"scale_mode": 2</code>, the system automatically adds black bars on both sides of the video to fit the new resolution without stretching or cropping the picture.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-video-123456789",
    "request_id": "20240523140000ABCDEFG12345"
}
```


<span id="step-2-get-the-transcoding-result"></span>
#### Step 2: Get the transcoding result

Transcoding tasks require some processing time. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. You can find the download URL of the generated video in the `result.video_url` field (valid for **24 hours** by default).

```JSON
{
  "success": true,
  "task_id": "amk-tool-transcode-video-112738623234",
  "task_type": "transcode-video",
  "status": "completed",
  "result": {
    "duration": 15.07,
    "resolution": "720p",
    "video_codec": "h264",
    "video_url": "https://example.com/transcoded_video.mp4?auth_key=..."
  },
  "expires_at": 1780472196,
  "created_at": 1780385775,
  "finished_at": 1780385797,
  "request_id": "20260601153614EA4FAB54AB56A39BC53E",
  "queue_id": "default"
}
```


<span id="related-api-references"></span>
## Related API references


* [Create a video transcoding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-transcoding-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

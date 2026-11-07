---
title: "Remuxing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-remuxing"
---

Remuxing is the process of changing only the file container format without re\-encoding the audio/video bitstreams. Because it does not involve complex codec computation, remuxing offers the advantages of extremely fast processing, no loss of video or audio quality, and very low cost.

The AI MediaKit Remuxing tool supports fast conversion between mainstream formats such as MP4, FLV, and MPEG\-TS, and is widely applicable to scenarios like VOD distribution adaptation, streaming media segment packaging, and multi\-device compatibility.

This guide walks you through how to achieve second\-level video format conversion via API calls.

<span id="quickstart-basic-remuxing-task"></span>
## Quickstart: Basic remuxing task

This section demonstrates how to quickly convert an MP4 video file to FLV format.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Remuxing is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/remux-video` to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-remuxing-task"></span>
#### Step 1: Submit the remuxing task

You need to call the [Create a remuxing task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-remuxing-task) API. You can copy the following cURL command to submit a task that remuxes a video from MP4 to FLV.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/remux-video' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_url": "https://vod-ai-test.bytepluses.com/demo/demo-480p.mp4",
  "container_format": "FLV"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default"><code>video_url</code>: Replace it with your own video URL.</div>


* <div data-tips="true" data-tips-type="default"><code>container_format</code>: Specifies the target container format. Supported values are MP4 (default), FLV, and MPEGTS.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-remux-video-123456789",
  "request_id": "20240522190000ABCDEFG67890"
}
```


<span id="step-2-get-the-remuxing-result"></span>
#### Step 2: Get the remuxing result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


When the task is successfully completed, you will receive the following response. You can find the download URL of the generated FLV video in the `result.video_url` field (valid for **24 hours** by default).

```JSON
{
    "success": true,
    "task_id": "amk-tool-remux-video-123456789",
    "request_id": "20240522190000ABCDEFG67890",
    "result": {
        "video_url": "https://example.com/remux_output.flv?auth_key=...",
        "duration": 180.5
    },
    "expires_at": 1777468800,
    "created_at": 1777292400,
    "finished_at": 1777292402
}
```


<span id="related-api-references"></span>
## Related API references


* [Create a remuxing task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-remuxing-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

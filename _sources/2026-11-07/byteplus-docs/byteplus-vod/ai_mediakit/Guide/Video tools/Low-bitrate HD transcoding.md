---
title: "Low-bitrate HD transcoding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-low-bitrate-hd-transcoding"
---

The AI MediaKit Low\-bitrate HD Transcoding tool, based on the characteristics of the human visual system, intelligently analyzes the scenes, motion, content, and textures of a video during transcoding and selects the optimal encoding parameters. This allows you to output a video with better perceived quality at a relatively lower bitrate, reducing storage and bandwidth costs while delivering a better viewing experience for your users.

This guide walks you through how to quickly use the Low\-bitrate HD Transcoding tool to convert a video into a more compression\-efficient encoding format (such as H.265), effectively reducing the file size while preserving perceived quality.

<span id="quickstart-basic-low-bitrate-hd-transcoding-task"></span>
## Quickstart: Basic low\-bitrate HD transcoding task

This section demonstrates how to use the Low\-bitrate HD Transcoding tool to transcode a video encoded with H.264 into the H.265 format.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a video file**: Have a video file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Low\-bitrate HD transcoding is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/martencode-video` to submit the task and obtain a `task_id` for querying.

2. Poll `GET /api/v1/tasks/{task_id}` until the task is complete, then get the download URL of the optimized video from the `result.video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a low-bitrate HD transcoding task](https://docs.byteplus.com/docs/byteplus-vod/117668) API. You can copy the following cURL command to submit a task that converts an H.264 video into H.265 encoding while preserving the original resolution.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/martencode-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "container_format": "MP4",
  "video": {
    "codec": "h265",
    "scale_type": 0,
    "bitrate_mode": "crf",
    "bitrate_crf": 25,
    "bitrate_kbps": 2000
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>



* <div data-tips="true" data-tips-type="default"><code>video_url</code>: Replace with the URL of your own prepared video file.</div>


* <div data-tips="true" data-tips-type="default">This example demonstrates the core usage of Low\-bitrate HD transcoding:</div>


   * <div data-tips="true" data-tips-type="default"><code>"codec": "h265"</code>: Specifies the more compression\-efficient H.265 output encoding.</div>


   * <div data-tips="true" data-tips-type="default"><code>"scale_type": 0</code>: No scaling is performed, preserving the original resolution of the video.</div>


   * <div data-tips="true" data-tips-type="default"><code>"bitrate_mode": "crf"</code> with <code>"bitrate_kbps": 2000</code>: Used together. This both ensures intelligent bandwidth savings via CRF 25 in everyday scenes and adds a "bitrate ceiling" (not exceeding 2000 Kbps) for complex, high\-motion scenes, preventing playback stutter caused by momentary bitrate spikes.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-martencode-video-123456789",
    "request_id": "20240523150000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

A Low\-bitrate HD transcoding task takes some time to process. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. You can find the download URL of the final output video file in the `result.video_url` field (valid for 24 hours by default).

```JSON
{
    "success": true,
    "task_id": "amk-tool-martencode-video-123456789",
    "task_type": "martencode-video",
    "status": "completed",
    "result": {
        "duration": 15.07,
        "resolution": "480p",
        "video_codec": "h265",
        "video_url": "https://example.byteplus.com/martencode_video.mp4?auth_key=..."
    },
    "expires_at": 1780472196,
    "created_at": 1780385775,
    "finished_at": 1780385797,
    "request_id": "20260601153614EA4FAB54AB56A39BC53E",
    "queue_id": "default"
}
```


Unlike ordinary transcoding, which only changes the resolution or container format, the core advantage of Low\-bitrate HD transcoding lies in the improvement of encoding efficiency. Using the same demo video as input, after Low\-bitrate HD transcoding, the file size and bitrate can be significantly reduced without a noticeable drop in perceived quality.


|**Attribute** |**Input video** |**Output video** |
|---|---|---|
|Video |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/663244dbda7445258423bcb01268f2c5~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1764cddd22f749c0b7540263b3fda457~tplv-goo7wpa0wc-image.image" controls></video><br> |
|Codec |H.264 |H.265 |
|Resolution |496 x 864 |496 x 864 |
|File Size |~ 4.1 MB | **~ 1.8 MB (about 56% savings)**  |
|Bitrate |~ 2.02 Mbps | **~ 0.94 Mbps** |


<span id="related-apis"></span>
## Related APIs


* [Create a low-bitrate HD transcoding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-low-bitrate-HD-transcoding-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

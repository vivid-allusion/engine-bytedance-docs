---
title: "Apply camera motion"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-apply-camera-motion"
---

The AI MediaKit camera motion tool can add professional dynamic camera effects—such as zoom, pan\-and\-zoom, and orbit—to static or steadily shot video footage with one click, significantly enhancing the visual impact and rhythm of the video. This capability is commonly used in scenarios such as re\-editing footage, creating marketing intros, and adding dynamic effects to short dramas.

This guide walks you through how to easily add a camera motion effect to your video via an API call.

<span id="effect-preview"></span>
## Demo

With the camera motion tool, you can add motion to a static shot. For example, after adding a "zoom" motion to a fixed\-position pet video, the footage smoothly moves and zooms in, as if a professional cinematographer had operated the camera.


|Motion name |Effect |Description |
|---|---|---|
|Zoom |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b846a804fb44e29b93958329323deb2~tplv-goo7wpa0wc-image.image" controls></video><br> |Simulates a single zoom effect of the camera pushing forward (Zoom In) or pulling back (Zoom Out). Highlights the subject, emphasizes details, and showcases open environments. |
|Pan and zoom |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/731d5c20247140f2a436916ea4844b17~tplv-goo7wpa0wc-image.image" controls></video><br> |Zooms in or out while the footage moves, for a more dynamic effect. Creates the Ken Burns effect and brings static images or videos to life. |
|360\-degree orbit |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d303776d673743db84aed06c94d96719~tplv-goo7wpa0wc-image.image" controls></video><br> |Simulates the camera orbiting 360 degrees around a center point, creating a strong sense of space and visual focus. Emphasizes the central object and creates a dizzying or dreamlike feel. |
|Bounce |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd0212427f1f473a8eca3a4b9051f589~tplv-goo7wpa0wc-image.image" controls></video><br> |Adds a rhythmic bouncing or slight shaking effect to the footage. Matches the music beat, creates beat\-synced videos, and adds a lively, dynamic feel. |


<span id="quickstart-add-a-zoom-motion"></span>
## Quickstart: Add a zoom motion

This section uses a concrete example to demonstrate how to call the API to add a zoom (`zoom`) effect to a video.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a video file**: Have a video file ready for the camera motion effect, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Applying camera motion is an asynchronous task. The overall API flow is as follows:


1. After you successfully call `POST /api/v1/tools/apply-camera-motion` to submit the task, you obtain a unique `task_id`.

2. You can poll the `GET /api/v1/tasks/{task_id}` API to query the task status until the `status` becomes `completed`. Alternatively, you can configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the video with camera motion from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a camera motion task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-camera-motion-task) API. You can copy the following cURL command to submit the task. This example adds a "zoom motion" effect to the video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/apply-camera-motion' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/input_video.mp4",
  "motion_style": "zoom"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-apply-camera-motion-123456789",
  "request_id": "20240521113000ABCDEFG12345"
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


When the task is successfully completed, you will receive the following response. The `video_url` field within `result` is the download URL of the video with camera motion. This URL is valid for 24 hours, so be sure to download and save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-apply-camera-motion-123456789",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/motion_output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="advanced-usage-add-camera-motion-to-a-specific-time-range"></span>
## Advanced usage: Add camera motion to a specific time range

By default, the camera motion effect is applied to the entire video. If you want to add motion only to a specific segment (such as a climax or an intro), you can use the `start_time` and `end_time` parameters to specify the start and end times of the motion. The following example demonstrates how to add a pan\-and\-zoom (`pan-zoom`) camera motion effect to a video from the 5th second to the 12.5th second:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/apply-camera-motion' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/input_video.mp4",
  "motion_style": "pan-zoom",
  "start_time": 5,
  "end_time": 12.5
}'
```


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`, and more.<br><br>* **Resolution limit**: Up to 1080p is supported.<br><br>* **Duration limit**: Must not exceed 5 minutes. |
|Output format |The output format is MP4, and the resolution matches the source by default. |


<span id="related-api-references"></span>
## Related API references


* [Create a camera motion task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-camera-motion-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

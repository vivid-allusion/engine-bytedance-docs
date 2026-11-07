---
title: "Reframe video to vertical"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-reframe-video-to-vertical"
---

The AI MediaKit Reframe\-to\-Vertical tool intelligently converts landscape videos into a vertical format suitable for social media platforms. By automatically handling subject detection, tracking, and cropping, it produces a production\-ready 9:16 video with no manual editing.

This guide provides the API steps to perform a basic conversion and to burn an external subtitle file into the final video.

<span id="3fc3f3dc"></span>
## Demo


|Input video |Output video |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3b94a359d574416184d12800b93795e0" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7d38996134a5486480d04a250970d476" controls></video><br> |


<span id="quickstart-convert-a-landscape-video-to-vertical"></span>
## Quickstart: Convert a landscape video to vertical

This section demonstrates how to submit a reframe\-to\-vertical task that intelligently converts a 16:9 landscape video into a 9:16 vertical video.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a landscape video file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload). The input should be in a landscape aspect ratio (`16:9`, `4:3`, or `21:9`), no more than 4 hours in duration, and no more than 20 GB per file.


<span id="procedure"></span>
### Procedure

Reframe\-to\-Vertical is an asynchronous task. The overall workflow is as follows:


1. Call `POST /api/v1/tools/reframe-video-to-vertical` to submit the task and get a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the reframed vertical video from `video_url`.


<span id="step-1-submit-the-reframe-to-vertical-task"></span>
#### Step 1: Submit the reframe\-to\-vertical task

Call the [Create a reframe-to-vertical task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-reframe-to-vertical-task) API. You can copy the following cURL command to submit a task that converts a landscape video into a vertical video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/reframe-video-to-vertical' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example.com/your_landscape_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own landscape video.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-reframe-video-to-vertical-123456789",
    "request_id": "20260908130000ABCDEFG12345"
}
```


<span id="step-2-get-the-conversion-result"></span>
#### Step 2: Get the conversion result

Because the reframe\-to\-vertical task takes some time to process, you need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result.video_url` field contains the download URL of the reframed vertical video (valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-reframe-video-to-vertical-123456789",
    "request_id": "20260908130000ABCDEFG12345",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/vertical_output.mp4?auth_key=...",
        "duration": 120.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777292051
}
```


<span id="advanced-usage-burn-external-subtitles-into-the-vertical-video"></span>
## Advanced usage: Burn external subtitles into the vertical video

If you want to burn an external subtitle file into the final vertical video, pass a subtitle file via the `subtitle_url` parameter. The subtitle is only burned in during the finishing stage and is not used in internal processing such as subject recognition, tracking, or cropping. Subtitle files in formats such as `SRT` and `ASS` are supported.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/reframe-video-to-vertical' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example.com/your_landscape_video.mp4",
    "subtitle_url": "https://example.com/your_subtitle.srt"
}'
```


<span id="references"></span>
## References

<span id="pricing"></span>
### Pricing

Reframe\-to\-Vertical is billed based on the **duration of the output video**. For detailed billing rules and examples, see [Reframe to vertical pricing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#eff377c2).

<span id="limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input video limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: `MP4`, `MOV`, `MKV`, `AVI`, `FLV`.<br><br>* **Aspect ratio**: The input should be in a landscape aspect ratio. `16:9`, `4:3`, and `21:9` are supported.<br><br>* **Video duration**: No more than 4 hours.<br><br>* **File size**: No more than 20 GB per file. |
|Subtitle file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: `SRT`, `ASS`.<br><br>* **Quantity limit**: At most one subtitle file can be provided. |


<span id="related-apis"></span>
## API reference


* [Create a reframe-to-vertical task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-reframe-to-vertical-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

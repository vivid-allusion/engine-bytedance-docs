---
title: "Video frame interpolation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-frame-interpolation"
---

To improve the smoothness of your videos and fix issues like stutter or motion discontinuity, you can use the AI MediaKit video frame interpolation tool. It leverages deep learning to intelligently synthesize new frames, boosting the video's frame rate for more natural playback. This guide walks you through how to use the API to quickly interpolate a video to a specified frame rate and understand the relevant usage limits.

This guide walks you through how to:


* Quickly try interpolating a video to a specified frame rate.

* Understand the recommended values and usage limits for the target frame rate.


<span id="effect-preview"></span>
## Effect preview

With the video frame interpolation tool, you can boost a low\-frame\-rate video to a higher frame rate, significantly improving the smoothness of the footage. The following example shows a comparison after boosting a low\-frame\-rate video to 60 fps. Comparing the videos before and after processing, you can observe that the overall visual experience is smoother, stuttering is noticeably reduced, and the motion appears more natural.


|Source video (24 fps) |Interpolated to 60 fps |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f007aa342c47e89e5edd7f4af156a8~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a18dd79474de400b8db245feb4a07ac4~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-interpolate-a-video-to-60-fps"></span>
## Quickstart: Interpolate a video to 60 fps

This section uses interpolating a 24 fps video to 60 fps as an example to demonstrate the complete video frame interpolation flow.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload). For convenient testing, the example code in the following steps provides a demo video URL that you can use directly.


<span id="procedure"></span>
### Procedure

Video frame interpolation is an asynchronous task. The standard workflow is as follows:


1. After you successfully call `POST /api/v1/tools/video-frame-interpolation` to submit the task, you obtain a task ID.

2. You can poll the `GET /api/v1/tasks/{task_id}` API until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the interpolated video from the `video_url` field.


<span id="step-1-submit-the-interpolation-task"></span>
#### Step 1: Submit the interpolation task

You need to call the [Create a video frame interpolation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-frame-interpolation-task) API. You can copy the following cURL command to submit a task that interpolates a video to 60 fps.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-frame-interpolation' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example.com/demo_video_24fps.mp4",
    "fps": 60
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default"><code>video_url</code>: Replace it with your own video URL.</div>


* <div data-tips="true" data-tips-type="default"><code>fps</code>: The target output frame rate, ranging from [15, 120].</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-video-frame-interpolation-123456789",
    "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="step-2-get-the-interpolation-result"></span>
#### Step 2: Get the interpolation result

The interpolation task takes some time to process (related to the video file size and duration). Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. `result.video_url` is the download URL of the interpolated video (valid for **24** hours; please save the output promptly).

```JSON
{
    "success": true,
    "task_id": "amk-tool-video-frame-interpolation-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/output/interpolated.mp4?sign=...",
        "duration": 16.0,
        "resolution": "1080p",
        "fps": 60
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777359999
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Video frame interpolation only boosts the frame rate; it does not change the video resolution or bitrate, which are inherited from the source video. If you need to increase the resolution or clarity at the same time, use it together with the  tool.</div>


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input video limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|Target frame rate limits |Ranges from [15, 120]. We recommend that the target frame rate not exceed 4x the source frame rate. |


<span id="related-api-references"></span>
## Related API references


* [Create a video frame interpolation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-frame-interpolation-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

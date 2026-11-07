---
title: "Volume adjustment and audio fade in/out"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-volume-adjustment-and-audio-fade-in-out"
---

The AI MediaKit volume adjustment and audio fade in/out tools help you easily adjust the volume of a video or audio file, or add smooth fade\-in and fade\-out effects. Whether you need to seamlessly blend background music into a video or normalize the volume of material from different sources, you can accomplish it with a simple API call.

<span id="tool-overview"></span>
## Tool overview

AI MediaKit provides separate APIs for volume adjustment and fade in/out, but both follow the same asynchronous task flow: you submit a task, and then query for the result.


|Feature |API |Core capability |
|---|---|---|
|Volume adjustment (for videos) |[Create a video volume adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-volume-adjustment-task) |Adjust the overall volume of a video's audio track: amplify, reduce, or mute it. |
|Audio track fade in/out (for videos) |[Create an audio track fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-track-fade-in-out-task) |Add a gradual volume increase (fade\-in) or decrease (fade\-out) to the audio track of a **video file**. |
|Audio fade in/out (for audio files) |[Create an audio fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-fade-in-out-task) |Add a fade\-in or fade\-out effect to a **standalone audio file**. |


<span id="prerequisites"></span>
## Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare a media file**: Have a video or audio file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the file to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="scenario-1-global-volume-adjustment"></span>
## Scenario 1: Global volume adjustment

This section demonstrates how to call the API to amplify the overall volume of a video to 2x. 

Volume adjustment is an asynchronous task. The complete workflow is as follows:


1. After you call `POST /api/v1/tools/adjust-video-volume` successfully, the system returns a unique `task_id`.

2. Either poll the `GET /api/v1/tasks/{task_id}` API until the `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. 

3. Once the task is complete, parse the `result` field in the response to get the download URL of the processed video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
### Step 1: Submit the task

You need to call the [Create a video volume adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-volume-adjustment-task) API. You can copy the following cURL command to submit a task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/adjust-video-volume' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "volume": 2.0
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>


* <div data-tips="true" data-tips-type="default">Description of the <code>volume</code> parameter:</div>


   * <div data-tips="true" data-tips-type="default"><code>0</code>: Mute</div>


   * <div data-tips="true" data-tips-type="default"><code>1</code>: Keep the original volume (default value)</div>


   * <div data-tips="true" data-tips-type="default">Between <code>0</code> and <code>1</code>: Reduce the volume (for example, <code>0.5</code> means half the volume</div>


   * <div data-tips="true" data-tips-type="default">Greater than <code>1</code>: Amplify the volume (for example, <code>2.0</code> means double the volume; up to <code>4.0</code> is supported)</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-adjust-video-volume-123456789",
  "request_id": "20240522103000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to get the final result.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` in the `result` field is the download URL of the processed video, valid for **24 hours**; please save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-adjust-video-volume-123456789",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/output_volume.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1785240563,
    "created_at": 1785154101,
    "finished_at": 1785154164,
    "request_id": "20240522103000ABCDEFG12345"
}
```


<span id="scenario-2-add-an-audio-fade-in-out-effect-to-a-video"></span>
## Scenario 2: Adding a fade effect to a video's audio track

This section demonstrates how to add a 3\-second audio fade\-in at the beginning of a video and a 5\-second audio fade\-out at the end to make the audio transitions smoother.

The workflow is as follows:


1. Call the [Create an audio track fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-track-fade-in-out-task) API. If the submission is successful, the system returns a unique `task_id`.

2. Periodically poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API with the `task_id` until the task status becomes completed or failed. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task updates automatically.

3. Once the task is complete, parse the result field in the response to get the download URL of the processed video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
### Step 1: Submit the task

Call the [Create an audio track fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-track-fade-in-out-task) API. You can copy the following cURL command to send the request.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/fade-video-audio' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_video.mp4",
  "fade_in_duration": 3,
  "fade_out_duration": 5
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">说明</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>


* <div data-tips="true" data-tips-type="default"><code>fade_in_duration</code>: The duration of the audio fade\-in (in seconds).</div>


* <div data-tips="true" data-tips-type="default"><code>fade_out_duration</code>: The duration of the audio fade\-out (in seconds).</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-fade-video-audio-123456789",
  "request_id": "20240521103000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to get the final result.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` in the `result` field is the download URL of the processed video, valid for 24 hours; please save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-fade-video-audio-123456789",
    "request_id": "20240521103000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/output_fade.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">If you need to add a fade\-in and fade\-out effect to a standalone audio file, the process is identical to Scenario 2 but uses a different API endpoint and parameter. Simply call the <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-fade-in-out-task">Create an audio fade in/out task</a> API (<code>/api/v1/tools/fade-audio</code>) and change the parameter name from <code>video_url</code> to <code>audio_url</code>.</div>


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**:<br><br>   * Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * Common audio formats such as `mp3`, `m4a`, `wav`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported for input videos. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the media's duration and resolution. The average RTF (processing time / source duration) is 1.

<span id="related-api-references"></span>
## Related API references


* [Create a video volume adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-volume-adjustment-task)

* [Create an audio fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-fade-in-out-task)

* [Create an audio track fade in/out task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-track-fade-in-out-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

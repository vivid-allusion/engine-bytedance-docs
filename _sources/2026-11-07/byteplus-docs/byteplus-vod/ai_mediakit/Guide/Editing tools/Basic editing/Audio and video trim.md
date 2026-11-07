---
title: "Audio and video trim"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-video-trim"
---

The AI MediaKit audio and video trim tool lets you precisely extract any time segment you need from a longer media file, generating a brand\-new media file. Whether you want to clip a highlight moment from a full live\-stream recording or extract the core dialogue from an audio recording, you can do it with a single, simple API call.

<span id="tool-description"></span>
## Tool description

AI MediaKit provides separate APIs for trimming video and audio, but they follow exactly the same asynchronous task flow and use the same API to query task results.


|Tool |API |Core capability |
|---|---|---|
|Video trim |[Create a video trim task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-trim-task) |Extracts a segment from the source video based on the specified start and end time points. |
|Audio trim |[Create an audio trim task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-trim-task) |Extracts a segment from the source audio based on the specified start and end time points. |


<span id="quickstart-clip-a-highlight-from-a-long-video"></span>
## Quickstart: Clip a highlight from a long video

This scenario demonstrates how to trim a highlight segment between **15 min 30 sec** and **16 min** from a full video recording.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for trimming, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio and video trimming is an asynchronous task. The standard workflow is as follows:


1. Call the **Video trim** `POST /api/v1/tools/trim-video` API to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URL of the final trimmed video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a video trim task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-trim-task) API. You can copy the following cURL command to submit a task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/trim-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
   "video_url": "https://example.com/full_game_recording.mp4",
   "start_time": 930,
   "end_time": 960
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with your own video file URL.</div>


* <div data-tips="true" data-tips-type="default"><code>start_time</code> and <code>end_time</code> specify the start and end time points of the trim. In this example, <code>930</code> represents 15 min 30 sec, and <code>960</code> represents 16 min.</div>



Upon a successful request, you will receive the following response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-trim-video-123456789",
  "request_id": "20240520160000ABCDEFG67890"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because trimming takes some time to process, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace the <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object, and you can get the video download URL directly from its `video_url` field (the output is in MP4 format by default and the URL is valid for **24 hours**).

```JSON
{
    "success": true,
    "task_id": "amk-tool-trim-video-123456789",
    "task_type": "trim-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/highlight_clip.mp4?auth_key=...",
        "duration": 30,
        "resolution": "720p"
    },
    "expires_at": 1774878690,
    "finished_at": 1774705891,
    "request_id": "20260419100100H8G7F6E5D4C3B2A1"
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default"><strong>Trimming audio</strong>: The audio trimming flow is exactly the same as above. The only difference is that you call the <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-trim-task">Create an audio trim task</a> API and change the parameter name from <code>video_url</code> to <code>audio_url</code>.</div>


<span id="best-practices"></span>
## Best practices

<span id="validate-the-trim-time-range"></span>
### Validate the trim time range

Before submitting a task, we recommend adding a validation step to your business logic:


1. **Check time validity**: Ensure `end_time` is later than `start_time`.

2. **Compare against file duration**: Ensure both `start_time` and `end_time` fall within the total duration of the source file.


Intercepting invalid parameters early helps you avoid unnecessary API calls and task failures.

<span id="output-specifications"></span>
### Output specifications


* **Output video format**: A video trim task outputs the `mp4` format by default.

* **Output video resolution**: By default, the output resolution matches the resolution of the source video file.

* **Output audio format**: An audio trim task outputs the `m4a` format by default.


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**:<br><br>   * Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * Common audio formats such as `mp3`, `m4a`, `wav`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Input video is supported up to 4K (3840×2160) resolution. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the video duration and resolution: the longer the video and the higher the resolution, the longer it takes. The average RTF (processing time / source duration) is 1.

<span id="related-api-references"></span>
## Related API references


* [Create a video trim task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-trim-task)

* [Create an audio trim task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-trim-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

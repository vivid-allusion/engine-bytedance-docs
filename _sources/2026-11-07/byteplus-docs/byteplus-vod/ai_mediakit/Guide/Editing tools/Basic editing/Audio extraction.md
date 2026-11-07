---
title: "Audio extraction"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-extraction"
---

The AI MediaKit audio extraction tool can quickly separate the audio track from a video file and save it as a standalone audio file (in MP3 or M4A format). This tool is ideal for scenarios such as producing podcast material, preprocessing before video\-to\-text conversion, and extracting background music from film and TV footage.

This guide walks you through how to:


* Understand the core capabilities and application scenarios of audio extraction.

* Quickly extract an audio file from a video.

* Learn how to specify the output audio format.


<span id="quickstart-extract-the-complete-audio-from-a-video"></span>
## Quickstart: Extract the complete audio from a video

This section demonstrates how to extract the complete audio from a video.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio extraction is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/extract-audio` to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URL of the final audio file from the `audio_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create an audio extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-extraction-task) API. You can copy the following cURL command to submit a task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-audio' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
   "video_url": "https://example.com/my_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with the actual URL of your video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-extract-audio-12345678",
  "request_id": "20260417110000A1B2C3D4E5F6G7H8"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object; you can get the extracted audio file's download URL from the `audio_url` field in the result object (the output is in M4A format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-audio-12345678",
    "task_type": "extract-audio",
    "status": "completed",
    "result": {
        "audio_url": "https://example.byteplus.com/extracted_audio.m4a?auth_key=..."
    },
    "expires_at": 1774702280,
    "finished_at": 1774529481,
    "request_id": "20260417110100F8G7H6E5D4C3B2A1"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="specify-the-output-audio-format"></span>
### Specify the output audio format

By default, the extracted audio is saved in `m4a` format. You can use the `format` parameter to specify other formats as needed. Supported values are `mp3`, `m4a`, `ogg`, `flac`, and `wav`. The default is `m4a`.

<span id="example-extract-audio-from-a-video-and-save-it-as-an-mp3-file"></span>
#### Example: Extract audio from a video and save it as an MP3 file

```JSON
{
    "video_url": "https://example.com/my_video.mp4",
    "format": "mp3"
}
```


<span id="reference"></span>
## Reference

<span id="e2bc866d"></span>
### Application scenarios


* **Podcast and audio content production**: Convert video interviews, online courses, meeting recordings, and more directly into audio programs so that listeners can tune in anytime.

* **Music and sound effect extraction**: Separate background music or specific sound effects from music videos, film and TV clips, or game recordings for material collection or creative reuse.

* **Multilingual dubbing workflows**: Extract the target\-language audio track from a video that contains multiple audio tracks, for subsequent translation, proofreading, or archiving.


<span id="usage-limits-and-performance"></span>
### Usage limits and performance


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported for input videos. |


<span id="processing-time"></span>
### Processing time

Processing time is proportional to the video's duration. The average RTF (processing time / source duration) is 1.

<span id="related-api-references"></span>
## Related API references


* [Create an audio extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-extraction-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

---
title: "Audio mixing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-mixing"
---

The AI MediaKit Audio Mixing tool helps you easily mix multiple audio files (such as background music, sound effects, and voiceovers) and generate a new audio file. Whether you want to produce a podcast intro with BGM and sound effects, or merge multiple recordings into a single complete audio track, you can accomplish it with a simple API call.

This guide walks you through:


* Understanding the core capability and use cases of audio mixing.

* Quickly trying out mixing a voiceover with a background music track.

* Understanding the input limits and output specifications of an audio mixing task.


<span id="quickstart-mix-a-voiceover-with-background-music"></span>
## Quickstart: Mix a voiceover with background music

This scenario demonstrates how to mix two separate audio tracks (a voiceover and a background music track) into a single audio file.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare media files**: Have multiple audio files ready for processing, accessible via public HTTP/HTTPS URLs. You can obtain these URLs by uploading the audio to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio mixing is an asynchronous task:


1. After you call `POST /api/v1/tools/mix-audio` successfully, the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URL of the final mixed audio from the `audio_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create an audio mixing task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-mixing-task) API. You can copy the following cURL command to submit an audio mixing task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/mix-audio' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "audio_urls": [
    "https://example.com/narration.mp3",
    "https://example.com/background_music.mp3"
  ]
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the URLs in the <code>audio_urls</code> list with your actual audio file URLs.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-mix-audio-1501200",
  "request_id": "20260326160000B9CF8E68B9A4F28F1EC2"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because audio processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object; you can get the mixed audio's download URL directly from the `audio_url` field within it (the output is in MP3 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-mix-audio-1501200",
    "task_type": "mix-audio",
    "status": "completed",
    "result": {
        "audio_url": "https://example.byteplus.com/mixed_output.mp3?auth_key=...",
        "duration": 185.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20240520153000ABCDEFG12345"
}
```


The total duration of the output audio is determined by the longest input audio. For example, if you mix a 30\-second voiceover with a 60\-second background music track, the final audio file is 60 seconds long. During the first 30 seconds, the voiceover and background music play simultaneously; during the last 30 seconds, only the background music plays.

<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common audio formats such as `mp3`, `wav`, and `flac`.<br><br>* **Number of files**: A single task supports 1 to 100 audio files.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the duration of the longest input audio. The average RTF (processing time / source duration) is about 1.

<span id="related-api-references"></span>
## Related APIs


* [Create an audio mixing task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-mixing-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

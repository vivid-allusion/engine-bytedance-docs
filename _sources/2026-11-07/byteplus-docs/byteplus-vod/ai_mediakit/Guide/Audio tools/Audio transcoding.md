---
title: "Audio transcoding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-transcoding"
---

The AI MediaKit Audio Transcoding tool converts an audio file from one format to another. This includes not only container format conversion (such as WAV to MP3), but also fine\-grained adjustment of encoding parameters (such as sample rate, bitrate, number of channels) and volume. Whether for adapting to different playback devices, optimizing network transmission, or standardizing the loudness of audio in a media library, audio transcoding is a fundamental and critical step.

This guide walks you through:


* A quickstart on how to convert an audio file to standard MP3 format.

* Advanced usage such as bitrate control, volume normalization, and metadata handling.


<span id="quickstart-perform-basic-transcoding"></span>
## Quickstart: Perform basic transcoding

This section uses the most common scenario as an example to demonstrate how to convert a WAV audio file to an MP3 file.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **MediaKit API Key**.

* **Prepare an audio file**: Have an audio file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio transcoding is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/transcode-video` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field in the response to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-transcoding-task"></span>
#### Step 1: Submit the transcoding task

You need to call the [Create an audio transcoding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-transcoding-task) API. The following cURL command demonstrates how to submit a basic MP3 transcoding task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "audio_url": "https://vod-ai-test.bytepluses.com/demo/speech.m4a"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Parameters to replace:</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default"><code>audio_url</code>: A ready\-to\-test demo audio URL is provided in the example. You can also replace it with your own audio URL.</div>


* <div data-tips="true" data-tips-type="default">When no transcoding parameters are specified, the system performs the default operation: transcoding the audio to <strong>MP3</strong> format, with a bitrate of <strong>128kbps</strong> and a sample rate of <strong>48000Hz</strong>. For finer control, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-transcoding#advanced-usage">Advanced usage</a>.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-audio-123456789",
    "request_id": "20240523120000ABCDEFG12345"
}
```


<span id="step-2-get-the-transcoding-result"></span>
#### Step 2: Get the transcoding result

Transcoding tasks require some processing time. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


When the task is successfully completed, you will receive the following response. You can find the download URL of the generated audio file in the `result.audio_url` field (valid for **24 hours** by default).

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-audio-123456789",
    "request_id": "20240523120000ABCDEFG12345",
    "status": "completed",
    "result": {
        "audio_url": "https://example.com/transcode_output.mp3?auth_key=...",
        "duration": 240.8
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777358500
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="control-the-bitrate-balance-quality-and-file-size"></span>
### Control the bitrate: Balance quality and file size

The `bitrate_mode` and `bitrate_kbps` parameters together determine the audio bitrate.


* `cbr` (Constant Bitrate mode): The encoder strictly maintains a constant bitrate. The file size can be precisely predicted, making it suitable for streaming scenarios with high requirements for bandwidth stability.

* `cae` (Constant Adaptive Bitrate mode, AAC only): The encoder dynamically adjusts the bitrate based on audio complexity. At the same average bitrate, it usually provides better quality and a smaller file size.


The following example demonstrates how to use `cae` mode to transcode audio into a high\-quality M4A (AAC) file with an average bitrate of `128kbps`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
    "audio_url": "https://vod-ai-test.bytepluses.com/demo/speech.m4a",
    "container_format": "M4A",
    "audio": {
        "bitrate_mode": "cae",
        "bitrate_kbps": 128
    }
}'
```


<span id="normalize-the-volume-achieve-loudness-balance"></span>
### Normalize the volume: Achieve loudness balance

To ensure a consistent listening experience across audio from different sources, you can use the volume normalization feature. Set `volume_method` to `"2Pass"`, and configure the `volume_integrated_loudness` (target loudness) and `volume_true_peak` (safety peak) parameters.

The following example demonstrates how to normalize the audio loudness to `-14 LUFS` (commonly used by streaming platforms) during transcoding, while ensuring the true peak does not exceed `-1.5 dBTP`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "audio_url": "https://vod-ai-test.bytepluses.com/demo/speech.m4a",
  "audio": {
    "volume_method": "2Pass",
    "volume_integrated_loudness": -14,
    "volume_true_peak": -1.5
  }
}'
```


<span id="manage-audio-metadata"></span>
### Manage audio metadata

During transcoding, you can precisely keep, update, or add audio metadata (such as title, artist, etc.).


* `metadata_keep_tags`: Specifies the list of metadata tags to **keep** from the source file.

* `metadata_add_tags`: **Adds or overwrites** metadata tags. If a `key` here has the same name as a kept tag, its `value` overwrites the source file's value.


The following example demonstrates how to keep the `title` and `artist` from the source file, while updating the `album` information and adding a new `encoded_by` tag.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "audio_url": "https://vod-ai-test.bytepluses.com/demo/speech.m4a",
  "metadata_keep_tags": [
    "title",
    "artist"
  ],
  "metadata_add_tags": [
    {
      "key": "album",
      "value": "Remastered 2024"
    },
    {
      "key": "encoded_by",
      "value": "MyAwesomeService"
    }
  ]
}'
```


<span id="related-api-references"></span>
## Related APIs


* [Create an audio transcoding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-transcoding-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

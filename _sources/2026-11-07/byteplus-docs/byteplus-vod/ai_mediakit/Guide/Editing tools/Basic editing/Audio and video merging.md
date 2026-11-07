---
title: "Audio and video merging"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-video-merging"
---

The AI MediaKit audio and video merging tool helps you easily add a new audio track to an existing video. With this tool, you can mix audio (blending new audio with the video's original audio track) or replace audio (removing the video's original audio track and replacing it with new audio content). Whether you want to add background music (BGM) to a video, replace it with new narration, or blend the two, you can accomplish it with a simple API call.

This guide walks you through how to:


* Understand the core capabilities and application scenarios of audio and video merging.

* Quickly add background music to a video.

* Learn how to control the audio mixing method and duration alignment through parameters.


<span id="quickstart-add-background-music-to-a-video"></span>
## Quickstart: Add background music to a video

This section demonstrates how to add a background music track to a silent video (or a video whose original audio you want to keep).

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare media files**: Have a video file to process and an audio file ready to add, accessible via public HTTP/HTTPS URLs. You can obtain these URLs by uploading the files to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio and video merging is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/mux-audio-video` to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URL of the final merged video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create an audio and video merging task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-and-video-merging-task) API. You can copy the following cURL command to submit an audio and video merging task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/mux-audio-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
   "video_url": "https://example.com/my_vlog.mp4",
   "audio_url": "https://example.com/bgm.mp3"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with the actual URL of your video file.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>audio_url</code> with the actual URL of your audio file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-mux-audio-video-1704500",
  "request_id": "20250324160000F6DE4C24A6A0D94B7FF2"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video composition takes some processing time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object; you can get the merged video's download URL directly from the `video_url` field below it (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-mux-audio-video-1704500",
    "task_type": "mux-audio-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/final_video.mp4?auth_key=..."
    },
    "expires_at": 1774615474,
    "finished_at": 1774442675,
    "request_id": "20250324160500A1B2C3D4E5F6"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="replace-or-keep-the-video-s-original-audio"></span>
### Replace or keep the video's original audio

You can decide whether to keep the video's original audio track (mixing it with the new audio) or replace it entirely.


* **Scenario**: When adding lighter background music to a video with dialogue, choose to keep the original audio. When replacing a video's dubbing or BGM, choose to replace the original audio.

* **Parameter**: `is_audio_reserve`

   * `true`: Keep the original audio track; the new audio is mixed with the original audio. This is the default behavior.

   * `false`: Do not keep the original audio track; that is, replace it with the new audio.


<span id="example-replace-a-video-s-original-audio-with-new-narration"></span>
#### Example: Replace a video's original audio with new narration

```JSON
{
    "video_url": "https://example.com/raw_footage.mp4",
    "audio_url": "https://example.com/voiceover.mp3",
    "is_audio_reserve": false
}
```


<span id="align-audio-and-video-duration"></span>
### Align audio and video duration

When the input video and audio have different durations, you can enable duration alignment by setting `is_video_audio_sync` to `true`, and further determine the final result through `sync_mode` (alignment basis) and `sync_method` (alignment method) to produce a clean final cut. The relevant parameters are described below:


* `is_video_audio_sync`: Set to `true` to enable duration alignment. The default is `false`, meaning duration alignment is not enabled. In that case, the total duration of the output file is determined by the longer of the input streams, as follows:

   * If the audio is longer than the video: after the video stream ends, the output file holds the last frame for the remaining time until the audio ends.

   * If the video is longer than the audio: after the audio stream ends, the output file stays silent for the remaining time until the video ends.

* `sync_mode`: Specifies which file to use as the duration basis.

   * `"video"`: (Default) Use the video duration as the basis.

   * `"audio"`: Use the audio duration as the basis.

* `sync_method`: Specifies the specific alignment method.

   * `"trim"`: (Default) Trim the longer file.

   * `"speed"`: Adjust the playback speed so that the two files have the same duration.


<span id="example-1-use-the-video-duration-as-the-basis-and-trim-the-overly-long-background-music"></span>
#### Example 1: Use the video duration as the basis and trim the overly long background music

This is the most common scenario, such as matching BGM to a Vlog.

```JSON
{
    "video_url": "https://example.com/my_vlog_3min.mp4",
    "audio_url": "https://example.com/bgm_5min.mp3",
    "is_video_audio_sync": true,
    "sync_mode": "video",
    "sync_method": "trim"
}
```


<span id="example-2-use-the-audio-duration-as-the-basis-and-trim-the-overly-long-video"></span>
#### Example 2: Use the audio duration as the basis and trim the overly long video

This scenario applies when editing video footage based on audio content (such as a song or a podcast).

```JSON
{
    "video_url": "https://example.com/footage_collection_10min.mp4",
    "audio_url": "https://example.com/podcast_clip_4min.mp3",
    "is_video_audio_sync": true,
    "sync_mode": "audio",
    "sync_method": "trim"
}
```


<span id="best-practices"></span>
## Best practices

<span id="how-to-choose-a-duration-alignment-method"></span>
### How to choose a duration alignment method


* **Prefer** **`trim`**: In most scenarios, trimming is the best choice. It preserves the original playback rate and pitch of the audio and video, discarding only the extra parts to produce the most natural\-looking and sounding result.

* **Use** **`speed`** ** with caution**: Speed adjustment is suitable for scenarios where the audio and video durations differ only slightly (we recommend within 10%). If the durations differ too much, the following problems may occur:

   * **Video speed change**: The footage shows noticeable stuttering (slow motion) or a jittery effect (fast motion).

   * **Audio speed change**: The pitch of the sound changes (becoming higher or lower), or the audio becomes hard to understand.


<span id="reference"></span>
## Reference

<span id="usage-limits-and-performance"></span>
### Usage limits and performance


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>   * **Video formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * **Audio formats**: Common audio formats such as `mp3`, `aac`, `wav`, `m4a`.<br><br>* **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* **Input resolution**: Up to 4K (3840×2160) is supported for input videos. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the video's duration. The average RTF (processing time / source duration) is 1.

<span id="related-api-references"></span>
## Related API references


* [Create an audio and video merging task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-and-video-merging-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

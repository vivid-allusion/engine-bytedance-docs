---
title: "Voice activity detection"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-voice-activity-detection"
---

The AI MediaKit Voice Activity Detection tool automatically locates the start and end times of valid speech in the audio or video file you provide, separating human speech from invalid segments such as silence and background noise. It returns a list of timestamps for every valid speech segment, providing cleaner audio input for subsequent recognition, analysis, editing, and training.

This development guide walks you through how to:

* Understand the core capability and application scenarios of voice activity detection.

* Quickly detect the timestamps of all valid speech segments in a media file.

## Demo

With the Voice Activity Detection tool, you can achieve the following result:

|Input audio |Detected valid speech segments |
|---|---|
|A female monologue that contains background music, wind noise, and other noise<br><br>[video](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/521283106ad745db896c4bacc51af34a)<br> |```Plain Text```<br>```{```<br>```  "duration": 15.04,```<br>```  "segment_count": 6,```<br>```  "voice_segments": [```<br>```    {"start_time": 0.32, "end_time": 2.24},```<br>```    {"start_time": 2.32, "end_time": 5.2},```<br>```    {"start_time": 5.52, "end_time": 7.92},```<br>```    {"start_time": 9.36, "end_time": 10.96},```<br>```    {"start_time": 11.6, "end_time": 13.28},```<br>```    {"start_time": 13.36, "end_time": 14.8}```<br>```   ]```<br>``` }```<br> |

## Quick start: Detect speech segments in audio

This scenario shows how to detect all segments that contain valid speech, along with their start and end times, in an audio file that contains speech, silence, and background noise.

### Prerequisites

* **Obtain an access credential**: Before you start, go to the [API key management page](https://console.byteplus.com/imp/ai-mediakit/settings) in the AI MediaKit console to create and obtain an AI MediaKit API key (used for authenticating media processing features).

* **Prepare a media file**: Have a video or audio file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the file to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).

### Procedure

Voice activity detection is an asynchronous task. The complete call workflow is as follows:

1. After you successfully call `POST /api/v1/tools/detect-voice-activity` to submit a task, the API returns a task ID (`task_id`).

2. You can poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) until the task `status` changes to `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status changes.

3. After the task is complete, parse the `result` field in the response to obtain the analysis result in the `voice_segments` array.

#### Step 1: Submit the task

Call the [Create a voice activity detection task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-voice-activity-detection-task) API. You can copy the following cURL command directly to submit the request.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/detect-voice-activity' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "audio_url": "https://example.com/demo_audio_noisy_monologue_wind_bgm.wav"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API key.

* > Replace `audio_url` with your own audio URL. To process a video file, use the `video_url` parameter instead.

After the request succeeds, you receive a response that contains a `task_id`, as shown below. Save this ID for subsequent queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-detect-voice-activity-123456789",
  "request_id": "20240521100000ABCDEFG12345"
}
```

#### Step 2: Obtain the result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) until the task `status` changes to `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

After the task is successfully completed, you receive the following response. `result.voice_segments` is an array of objects, where each object contains the `start_time` and `end_time` fields that represent the start and end times (in seconds) of a valid speech segment.

```JSON
{
    "success": true,
    "task_id": "amk-tool-detect-voice-activity-786355206146",
    "task_type": "detect-voice-activity",
    "status": "completed",
    "result": {
        "duration": 15.04,
        "segment_count": 6,
        "voice_segments": [
            {"start_time": 0.32, "end_time": 2.24},
            {"start_time": 2.32, "end_time": 5.2},
            {"start_time": 5.52, "end_time": 7.92},
            {"start_time": 9.36, "end_time": 10.96},
            {"start_time": 11.6, "end_time": 13.28},
            {"start_time": 13.36, "end_time": 14.8}
        ]
    },
    "expires_at": 1788888888,
    "created_at": 1788666666,
    "finished_at": 1788666777,
    "request_id": "202607091640268A72AFA8623C4A0E68C6",
    "queue_id": "q00a9731598092652e4a95292434198"
}
```

## Reference

### Usage limits

|Limit |Description |
|---|---|
|Input file |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats:<br><br>   * Video: Common formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`.<br><br>   * Audio: Common formats such as `mp3`, `m4a`, `wav`, `wma`, `amr`, `aac`, `ogg`, and `flac`. |

## Related APIs

* [Create a voice activity detection task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-voice-activity-detection-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

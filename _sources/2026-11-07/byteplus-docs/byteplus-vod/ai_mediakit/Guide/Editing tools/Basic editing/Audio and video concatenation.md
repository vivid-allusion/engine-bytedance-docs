---
title: "Audio and video concatenation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-audio-video-concatenation"
---

The AI MediaKit audio and video concatenation tools let you join multiple video clips or audio clips into a single new file in a specified order. Whether you want to combine several short clips from daily life into a single Vlog, or merge multiple recordings into a complete podcast episode, you can accomplish it with a simple API call.

<span id="tool-overview"></span>
## Tool overview

AI MediaKit provides separate APIs for video and audio concatenation, but both follow exactly the same asynchronous task flow and use the same API to query task results.


|Tool |API |Core capability |
|---|---|---|
|Video concatenation |[Create a video concatenation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task) |* **Sequential concatenation**: Join multiple video clips end to end in a specified order.<br><br>* **Add transitions**: Add various preset transition effects between clips to make the joins more natural and creative. |
|Audio concatenation |[Create an audio concatenation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-concatenation-task) |**Sequential concatenation**: Join multiple audio clips end to end in a specified order to produce a single audio file. |


<span id="quickstart-concatenate-multiple-video-clips-into-a-highlight-reel-with-transitions"></span>
## Quickstart: Concatenate multiple video clips into a highlight reel with transitions

This section demonstrates how to concatenate three separate short video clips (for example, casual shots from a trip) into a complete travel highlight reel, adding transition effects at the joins.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare video files**: Have multiple video files ready for concatenation, accessible via public HTTP/HTTPS URLs. You can obtain these URLs by uploading the videos to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Audio and video concatenation are asynchronous tasks. The standard workflow is as follows:


1. Call `POST /api/v1/tools/concat-video` to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-video-concatenation-task"></span>
#### Step 1: Submit the video concatenation task

You need to call the [Create a video concatenation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task) API. You can copy the following cURL command to submit a task. Make sure the order of files in the `video_urls` array is the concatenation order you want.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/concat-video' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
   "video_urls": [
     "https://example.com/clip_01_beach.mp4",
     "https://example.com/clip_02_mountain.mp4",
     "https://example.com/clip_03_city.mp4"
   ],
   "transitions": [
        "1182358",
        "1182360"
   ]
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the URLs in the <code>video_urls</code> array with your actual video file URLs.</div>


* <div data-tips="true" data-tips-type="default"><code>transitions</code> is an optional parameter used to specify transition effect IDs. For more IDs, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-concatenation#transition-effects">Transition effects</a>.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-concat-video-123456789",
  "request_id": "20240520153000ABCDEFG12345"
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


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object; you can get the video's download URL directly from the `video_url` field below it (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-concat-video-123456789",
    "task_type": "concat-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/final_travel_vlog.mp4?auth_key=..."
    },
    "expires_at": 1774789885,
    "finished_at": 1774617086,
    "request_id": "20260418150500A1B2C3D4E5F6G7H8"
}
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default"><strong>Audio concatenation</strong>: The process for concatenating audio is exactly the same as above. The only difference is that you need to call the <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-concatenation-task">Create an audio concatenation task</a> API and change the parameter name from <code>video_urls</code> to <code>audio_urls</code>. Audio concatenation does not support transitions.</div>


<span id="best-practices"></span>
## Best practices

<span id="specifications"></span>
### Specifications

For the best concatenation results, we recommend ensuring that all input clips have consistent specifications (such as resolution, frame rate, and sample rate) before concatenation.


* **Output resolution (video)** : By default, the output resolution of a video concatenation task is based on the resolution of the **first video clip** passed in the `video_urls` array. If subsequent clips have different resolutions, they are automatically scaled to align with the first clip, which may cause black bars or stretching.

* **Output format (audio)** : By default, the output audio format of an audio concatenation task is **m4a**.


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Quantity limit**: A single task supports 1 to 100 URLs.<br><br>* **Supported formats:** <br><br>   * Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * Common audio formats such as `mp3`, `m4a`, `wav`.<br><br>   * **File size**: It is recommended that the size of a single input file not exceed 10 GB.<br><br>   * **Input resolution**: Up to 4K (3840×2160) is supported for input videos. |


<span id="processing-time"></span>
### Processing time

Processing time is positively correlated with the video's duration and resolution. The longer the video and the higher the resolution, the longer the processing time. The average RTF (processing time / source duration) is 1.

<span id="transition-effects"></span>
### Transition effects

The following table lists all currently supported transition effects and their IDs.


|Effect Name |ID |Preview |
|---|---|---|
|Swap |1109556 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79f31d11b46584bdb6fdcc4540ab7261.gif) </span> |
|RotateScaleFade |1109558 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dff3b939cbe6a297ead483206bb97e22.gif) </span> |
|Ripple |1109560 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_14f6b3c5ffd25c8cff18dbf593f0d67f.gif) </span> |
|Hexagonalize |1109568 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64c4c859c391edf8bcefceb8c70a918f.gif) </span> |
|GlitchDisplay |1109572 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39d8866189a04200d87ea31a21af3500.gif) </span> |
|Flyeye |1109574 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86c7979c4470b795f5cd2d461c49477d.gif) </span> |
|DreamZoom |1109576 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2135ff204297e0fd2dd8f66ae0e710d5.gif) </span> |
|Doorway |1109578 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_543983c07d3f5c248ed09033bb9db17a.gif) </span> |
|Cube |1109584 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_649c78b8e44e7965950865a9e50c19cb.gif) </span> |
|CrossWrap |1109586 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a57e9728e19e57bb4bf1fc22927f85.gif) </span> |
|ColorPhase |1109588 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9878d7abd8dbd4c72732046966adcd40.gif) </span> |
|CircleCrop |1109594 |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_005f1685a105c0e3b617f1f9ea36495c.gif) </span> |


&nbsp;

<span id="related-api-references"></span>
## Related APIs


* [Create a video concatenation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-concatenation-task)

* [Create an audio concatenation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-concatenation-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

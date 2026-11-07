---
title: "Video quality enhancement (fast)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-lite"
---

The AI MediaKit video quality enhancement (fast) tool integrates lightweight super\-resolution and intelligent quality enhancement. It adopts a speed\-first algorithm strategy that delivers faster processing while still effectively improving visual quality, making it especially suitable for latency\-sensitive business scenarios such as live streaming and short\-video processing.

This guide walks you through how to:


* Quickly try enhancing a low\-definition video to 720p.

* Understand and use the core parameters of the fast video enhancement tool.


<span id="e8af0786"></span>
## Effect preview

With fast video enhancement, you can significantly improve the clarity and viewing experience of a video.


|Input video (480p) |Enhanced video (720p) |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb375ff5ac554499a5e219b7f855adda~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13da6285d2a6419290a6f578ccd384a6~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="6d022a4d"></span>
## Quickstart: Enhance a low\-definition video to 720p

This section demonstrates how to quickly enhance a low\-resolution video to 720p using the fast video enhancement tool.

<span id="28787b75"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

2. **Prepare a video file**: Have a video file ready for enhancement, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="8e93278d"></span>
### Procedure

Fast video enhancement is an asynchronous task:


* After you successfully call `POST /api/v1/tools/enhance-video-fast`, the API returns a task ID.

* You can poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

* Once the task is complete, parse the `result` field to get the download URL of the generated video file from the `video_url` field.


<span id="8d526549"></span>
#### Step 1: Submit the task

You need to call the [Create a video quality enhancement (fast) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-lite-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source_video.mp4",
  "resolution": "720p"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-enhance-video-fast-987654",
  "request_id": "20240523110000ABCDEFG67890"
}
```


<span id="ae71be89"></span>
#### Step 2: Get the result

Fast video enhancement takes some time. Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object from which you can get the download URL of the enhanced video from the `video_url` field (the default output is in **MP4** format, valid for **24** hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-fast-987654",
    "request_id": "20240523110000ABCDEFG67890",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/fast_enhanced_output.mp4?auth_key=...",
        "duration": 65.5,
        "resolution": "720p",
        "fps": 30
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777359999
}
```


<span id="f682047d"></span>
## Advanced usage

<span id="06b26084"></span>
### Configure the output resolution

AI MediaKit provides two mutually exclusive ways to define the output resolution.


|Method |Parameter |Description |
|---|---|---|
|Specify a resolution level |`resolution` |Suitable for standard distribution scenarios (such as `720p`, `1080p`, `4k`, with `4k` being the maximum). The system automatically aligns the video to the preset level. |
|Short\-side pixel limit |`resolution_limit` |Suitable for engineering scenarios with precise output size requirements. The system locks the **short side** of the video to the specified pixel value (ranging from `[128, 2160]`) and scales it proportionally while preserving the original aspect ratio. Example: if the source video is 640x480 (4:3) and `resolution_limit` is set to 720, the short side of the output video is increased to 720, and the width is scaled proportionally to 960. |


<span id="947be075"></span>
#### Example: Upscale a video to 1080p

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source_video.mp4",
  "resolution": "1080p"
}'
```


<span id="ecb604a4"></span>
### Configure the output bitrate

The output bitrate determines the visual quality and final file size of the video. AI MediaKit provides two control methods; when both are specified, only `bitrate` takes effect.


|Method |Parameter |Description |
|---|---|---|
|Bitrate level |`bitrate_level` |Controls the target average bitrate of the output video by level. Options are `low`, `medium` (recommended), and `high`, with `medium` as the default. The actual bitrate is automatically calculated based on the target resolution and frame rate. For the target bitrate of each level, see the [Bitrate reference](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-lite-task#bitrate-reference-table). |
|Exact bitrate |`bitrate` |Directly specifies the target average bitrate, in kbps, ranging from `[10, 150000]`. Suitable for engineering scenarios with precise bitrate requirements. If omitted, it is automatically calculated based on `bitrate_level`, resolution, and frame rate. |


<span id="aedab6c4"></span>
#### Example: Specify an exact output bitrate of 8000 kbps

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source.mp4",
  "resolution": "1080p",
  "bitrate": 8000
}'
```


<span id="c24ebedd"></span>
### Configure the output frame rate

You can use the `fps` parameter to adjust the target frame rate of the video (in fps), ranging from `[15, 120]`. If not specified, the frame rate is kept as close to the source as possible. To keep the footage smooth and natural, we recommend that the target frame rate not exceed 4x the source frame rate.

<span id="4a84d489"></span>
#### Example: Standardize the video frame rate to 30 fps

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-fast' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/source_video.mp4",
  "resolution": "720p",
  "fps": 30
}'
```


<span id="44f6c9e3"></span>
## Reference

<span id="8d2ed5f0"></span>
### Billing

The fast video enhancement tool uses a pay\-as\-you\-go model based on the output file duration, combined with the billing conversion factors for the task's output resolution and output frame rate. For detailed billing rules, conversion factors, and billing examples, see [Video quality enhancement pricing (fast)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#5a4bd706).

<span id="7b7e693b"></span>
### Estimated processing time

The processing time is related to the original duration of the video. You can estimate the task duration using the RTF (Real\-Time Factor), which is the ratio of processing time to source duration. The average RTF of the fast video enhancement tool is about **3**. For example, a 1\-minute video takes about 3 minutes to process.

<span id="e4eb4132"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input video limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB.<br><br>* **Input resolution**: Up to 2K is supported. Specific requirements:<br><br>   * Short side: [360, 1440]<br><br>   * Long side: [360, 2560] |


<span id="c55c7511"></span>
## API references


* [Create a video quality enhancement (fast) task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-lite-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

---
title: "Frame extraction"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-frame-extraction"
---

The AI MediaKit Frame Extraction tool captures one or more still images from a video. Depending on your business scenario, you can choose from four strategies: **by time interval**, **by specified timestamps**, **by specified frames (first/last frame)** , or **by scene change**. The captured images can be used to generate video covers, preview thumbnails, sprite sheets, or as input for other video understanding tasks.

This guide walks you through:


* A quickstart on how to extract frames from a video at a fixed time interval.

* The core parameters for using different extraction strategies.


<span id="quickstart-extract-frames-at-a-uniform-time-interval"></span>
## Quickstart: Extract frames at a uniform time interval

This section uses the "extract by time interval" strategy to demonstrate how to capture one frame every 10 seconds from a video.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing. Make your video file accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Frame extraction is an asynchronous task. The standard workflow is as follows:


1. A successful call to `POST /api/v1/tools/extract-frames` returns a `task_id`.

2. You can either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the image download URLs from `snapshots.image_url`.


<span id="step-1-submit-the-extraction-task"></span>
#### Step 1: Submit the extraction task

You need to call the [Create a frame extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-frame-extraction-task) API. You can copy the following cURL command to submit a task that captures one frame every 10 seconds.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
    "video_url": "https://vod-ai-test.bytepluses.com/demo/dragon.mp4",
    "snapshot_type": "TimeInterval",
    "time_interval": 10
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with your own URL.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-frames-123456789",
    "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Frame extraction requires some processing time. You need to poll the [Get task details](https://docs.byteplus.com/uchbv7an/syjmn7fm) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. Each object in the `result.snapshots` array contains an `image_url`, which is the download URL of a captured image (the output is in **JPG** format by default, and the URL is valid for **24 hours**).

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-frames-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "snapshots": [
            {
                "image_url": "https://example.com/snapshot/frame_0s.jpg?sign=..."
            },
            {
                "image_url": "https://example.com/snapshot/frame_10s.jpg?sign=..."
            }
        ],
        "snapshot_count": 2
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777359999
}
```


In this example, the input video is 16 seconds long, and the task requests one frame every 10 seconds, so 2 images are returned.

<span id="advanced-usage-more-extraction-strategies"></span>
## Advanced usage: More extraction strategies

While the basic workflow remains identical to the one in the Quickstart section, this section provides request examples for the different extraction strategies.

<span id="extract-by-specified-timestamps"></span>
### Extract by specified timestamps

This strategy captures the frames at the exact timestamps you specify. The following example captures one frame each at **5 seconds**, **10 seconds**, and **15 seconds** of the video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
    "video_url": "https://vod-ai-test.bytepluses.com/demo/dragon.mp4",
    "snapshot_type": "SpecifiedTime",
    "specified_time": [5, 10, 15]
}'
```


<span id="extract-by-specified-frames-first-last-frame"></span>
### Extract by specified frames (first/last frame)

This strategy quickly retrieves the first frame (`0`) or the last frame (`-1`) of a video, and is commonly used to generate video covers.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
    "video_url": "https://vod-ai-test.bytepluses.com/demo/dragon.mp4",
    "snapshot_type": "SpecifiedFrames",
    "specified_frames": [0, -1]
}'
```


<span id="extract-by-scene-change"></span>
### Extract by scene change

This strategy uses an intelligent algorithm to automatically detect scene transitions in the video and captures the starting frame of each new scene. The smaller the value of `scene_change_threshold`, the more sensitive the detection. The following example uses the default sensitivity of `0.1` for scene\-based extraction.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{ 
    "video_url": "https://vod-ai-test.bytepluses.com/demo/dragon.mp4",
    "snapshot_type": "SceneChange",
    "scene_change_threshold": 0.1
}'
```


<span id="generate-a-sprite-sheet"></span>
### Generate a sprite sheet

A sprite sheet is a single large image composed of multiple thumbnails arranged in rows and columns. In a video player, it is commonly used to implement the progress\-bar preview feature, allowing users to quickly see video thumbnails while dragging the progress bar. It offers the following advantages:


* **Reduced network requests**: By merging many small images into one large image, the client only needs to make a single request to obtain all preview frames, significantly reducing server load and improving loading speed.

* **Optimized storage and compression**: A single large image is easier to manage and store than a large number of small images, and it usually achieves better compression.


The following example shows how to capture one frame every 10 seconds from a video and compose these images into a 5x5 sprite sheet.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/extract-frames' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_url": "https://vod-ai-test.bytepluses.com/demo/video_cloud.mp4",
  "snapshot_type": "TimeInterval",
  "time_interval": 10,
  "enable_sprite": true,
  "sprite_rows": 5,
  "sprite_cols": 5
}'
```



* Set `enable_sprite` to `true` to enable sprite sheet generation.

* `sprite_rows`/`sprite_cols` define the number of rows and columns of the sprite sheet, used to arrange the thumbnails.

* To control the size of each individual thumbnail, use the `scale_long` and `scale_short` parameters. **Note**: It is recommended that the final dimensions (width or height) of the sprite sheet do not exceed 16384 pixels, otherwise the task may fail. You can control the final size by adjusting the number of rows and columns as well as the scaling parameters.


When the task succeeds, `result.snapshots.image_url` in the task result will point to the URL of the generated sprite sheet.

<span id="references"></span>
## References

<span id="usage-limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input video limits |* **Video source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|Snapshot count limit |The `snapshot_limit` parameter can limit the maximum number of snapshots generated by the `TimeInterval` and `SceneChange` strategies, with an upper limit of 1000. The `SpecifiedTime` strategy supports up to 1000 timestamps. |
|Sprite sheet limit |When `enable_sprite` is set to `true`, the system generates a sprite sheet. It is recommended that the final dimensions (width or height) of the sprite sheet do not exceed 16384 pixels, otherwise the task may fail. You can control the final size by adjusting `sprite_rows`, `sprite_cols`, and the scaling parameters (`scale_long`/`scale_short`). |


<span id="related-api-references"></span>
## Related APIs


* [Create a frame extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-frame-extraction-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

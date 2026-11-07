---
title: "Video depth estimation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-depth-estimation"
---

The AI MediaKit Video Depth Estimation tool can estimate the relative spatial depth of video frames frame by frame, weakening information such as person appearance, clothing, background, and art style, while retaining motion contours, spatial displacement, and camera movement to generate time\-continuous depth videos. You can use the output for AI video motion reference, character replacement and motion replication, camera movement control, as well as 3D content and visual effects preprocessing.

## Demos

With the Video Depth Estimation tool, you can convert an original video into a depth video that retains motion contours, spatial displacement, and camera movement. The examples below show the original video, the depth video output by this tool, and the final product when the depth video is used in downstream video generation.

|Stage |Example 1 |Example 2 |
|---|---|---|
|Original video |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cfaa47ef414f50bca4493d1833c89f~tplv-goo7wpa0wc-raw.image)<br> |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef5cc7089fc248a9a1b611f6ef48ac5c~tplv-goo7wpa0wc-raw.image)<br> |
|Depth video (Tool output) |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afa932c592c9441080530b0ef2b5361b~tplv-goo7wpa0wc-raw.image)<br> |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a8e3a4a84b84cfba1f99ed81e3efbec~tplv-goo7wpa0wc-raw.image)<br> |
|Final product |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/292cee444dca4632a3a7136c86ffb6e1~tplv-goo7wpa0wc-raw.image)<br> |[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/861ae91b98b1475c826238a0c2042e23~tplv-goo7wpa0wc-raw.image)<br> |

> **Note**

> The Video Depth Estimation tool only generates the depth video shown above. The final product is the result of providing the depth video and a reference image to other downstream video generation tools, not a direct output of the video depth estimation tool. The final result depends on the downstream tools and their parameter configurations.

## Scenarios

Video Depth Estimation is suitable for scenarios that require extracting motion and spatial structure information from videos. Typical uses include:

* **AI video motion reference**: Extract motion contours and spatial displacement from live\-action, film, or animation materials, reducing interference from a person's appearance and the background on the generation results.

* **Character replacement and motion replication**: Convert the original video motion into purer spatial control signals for downstream models to replicate continuous motion.

* **Camera movement control**: Retain spatial changes such as zooming in, zooming out, and panning to provide camera movement references for video generation.

* **3D content and visual effects preprocessing**: Provide time\-continuous relative depth videos for 3D reconstruction, image compositing, and visual effects workflows.

## Core concepts

Depth video uses brightness changes to represent the relative distance of objects in the frame. Compared to the original video, it mainly retains motion and spatial structure, which can reduce interference from a person's appearance, texture, and background information in downstream generation.

> **INFO**

> The depth results represent the relative spatial relationship of the frame content, not the actual physical distance from the object to the camera. Currently, only depth videos are output, and frame\-by\-frame depth maps or raw depth matrices are not output.

## Quickstart: Generate a depth video

This section uses a motion reference video as an example to demonstrate the complete process of submitting a video depth estimation task and obtaining a depth video.

### Prerequisites

* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).

### Procedure

Video Depth Estimation is an asynchronous task. The standard workflow is as follows:

1. Call `POST /api/v1/tools/video-depth` and get a `task_id` to query the task status.

2. You can either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the depth video download URL from `video_url`. The output is HEVC\-encoded, and the URL is valid for 24 hours.

#### Step 1: Submit the task

Call the [Create a video depth estimation task](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-depth-estimation-task?lang=en) API. You can copy the following cURL command to submit a basic video depth estimation task to the API.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-depth' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/dance_reference.mp4",
  "model": "standard"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > Replace the value of `video_url` with the URL of your own prepared video file.

* > `model` is used to specify the depth estimation model level. Currently, only `standard` is supported. This parameter can be omitted, and the default value is `standard`.

Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-depth-123456789",
  "request_id": "20261021140000ABCDEFG12345"
}
```

#### Step 2: Get the result

Because video processing takes time, you need to poll the [Get task details](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed` to get the final result. Processing time depends on the video file size, duration, and resolution.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task is successfully completed, you will receive the following response. `result.video_url` is the download URL of the HEVC\-encoded relative depth video. The URL is valid for 24 hours. Download and save the video before the URL expires. `result.duration` is the duration of the output depth video, in seconds. Billing is based on the input video duration.

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-depth-123456789",
  "task_type": "video-depth",
  "status": "completed",
  "result": {
    "video_url": "https://example.byteplusvideo.com/video-depth/result.mp4?auth_key=1777464650-example",
    "duration": 18.6
  },
  "expires_at": 1792591200,
  "created_at": 1792504800,
  "finished_at": 1792504920,
  "request_id": "20261021140000ABCDEFG12345"
}
```

## Reference

### Pricing

Video Depth Estimation is billed on a pay\-as\-you\-go basis. The cost is calculated based on the **input video duration** at  **$0.05/minute**. For detailed billing rules and examples, see [Video depth estimation pricing](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-pricing#video-depth-estimation).

### Usage limits

|Item |Description |
|---|---|
|Input video limits |* File source: Only publicly accessible HTTP/HTTPS URLs are supported. The input URL must remain valid during task execution.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`, and the file must contain a valid video stream.<br><br>* Number of files: Each task processes one video.<br><br>* Video duration: A single video must not exceed 10 minutes.<br><br>* Resolution limit: The input video resolution must not exceed 2K. |

## Related APIs

* [Create a video depth estimation task](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-video-depth-estimation-task?lang=en)

* [Get task details](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification)

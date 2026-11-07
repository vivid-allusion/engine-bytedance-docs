---
title: "Video quality enhancement (AI-enhanced)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-ai-enhanced"
---

The AI MediaKit Video Quality Enhancement (AI\-Enhanced) tool uses diffusion models for generative video enhancement and restoration. It restores pixels lost through compression or aging and uses a deep semantic understanding of the video content to reconstruct and generate realistic details, producing natural, high\-fidelity video.

This guide shows you how to:

* Quickly enhance an AI\-generated low\-resolution video from 480p to 1080p.

* Use the core capabilities and key parameters of Video Quality Enhancement (AI\-Enhanced).

## Quickstart: Enhance a 480p video to 1080p

This section shows you how to use Video Quality Enhancement (AI\-Enhanced) to enhance a 480p video to 1080p HD.

### Prerequisites

* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create your **AI MediaKit API key**. Use this key to authenticate media processing requests.

* **Prepare a video file**: Upload the video you want to enhance to a publicly accessible server or the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can access. If you have not generated a video yet, follow the [ModelArk video generation documentation](https://docs.byteplus.com/en/docs/modelark/seedance-2-0) to generate one and obtain its URL.

> **NOTE**

> Video Quality Enhancement (AI\-Enhanced) has the following input video requirements:

* > Resolution: Input video up to 1080p is supported, with the following dimensions:

   * > Short side: 360–1080 pixels, inclusive.

   * > Long side: 360–1920 pixels, inclusive.

* > Color space: Only SDR video is supported.

* > File size: The recommended maximum file size is 10 GB.

### Procedure

Video Quality Enhancement (AI\-Enhanced) runs asynchronously:

* A successful call to `POST /api/v1/tools/enhance-video-generative` returns a task ID.

* Poll `GET /api/v1/tasks/{task_id}` until the `status` field changes to `completed` or `failed`, or use [Event notification](https://docs.byteplus.com/event-notification) to receive task status updates automatically. If the task fails, check the `error` field for details.

* Once the task is complete, read the `video_url` field in the `result` object to obtain the download URL for the enhanced video.

#### Step 1: Submit the task

Submit a task using the [Create a video quality enhancement (AI-enhanced) task](https://docs.byteplus.com/ai-mediakit-create-video-quality-enhancement-ai-enhanced-task) API. Use the following cURL command:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/demo_video_480p.mp4",
  "resolution": "1080p"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your API key.

* > Replace the value of `video_url` with your video's URL.

If submission succeeds, the response contains a `task_id`. Save this ID to check the task status and retrieve the result.

```JSON
{
  "success": true,
  "task_id": "{task_id}",
  "request_id": "{request_id}"
}
```

#### Step 2: Get the result

Video Quality Enhancement (AI\-Enhanced) is computationally intensive, so processing takes time. Poll the [Get task details](https://docs.byteplus.com/get-task-details) API until the `status` field changes to `completed` or `failed`. If the task fails, stop polling and check the `error` field for details.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task completes successfully, the API returns a response like the following. The `result` field contains a JSON object, and its `video_url` field provides the download URL for the enhanced video. By default, the output is in **MP4** format, and the URL is valid for **24 hours**.

```JSON
{
    "success": true,
    "task_id": "{task_id}",
    "request_id": "{request_id}",
    "status": "completed",
    "result": {
        "video_url": "https://example.com/generative_enhanced_output.mp4",
        "duration": 65.5,
        "resolution": "1080p",
        "fps": 30
    },
    "expires_at": 1777446399,
    "created_at": 1777358413,
    "finished_at": 1777359999
}
```

> **INFO**

> Once you have retrieved the enhanced video, use the [Video quality comparison tool](https://docs.byteplus.com/en/docs/25/124042#9e26ae03) in the AI MediaKit console to compare it with the source video and check whether the results meet your expectations.

## Advanced usage

### Configure the output resolution

Use the `resolution` parameter to specify the enhanced video's output resolution. The following resolutions are supported:

|Resolution |Description |Use cases |
|---|---|---|
|`720p` (default) |Standard HD output; the most cost\-effective option |Short videos, social media content, and mobile playback |
|`1080p` |Full HD output |Playback on PCs and HD televisions |
|`2k` |2K output |Playback on large screens and video restoration that requires high image quality |
|`4k` |Ultra\-HD 4K output |Professional film and television post\-production and use cases that demand the highest image quality |

#### Example: Enhance a video to 2K

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/demo_video_480p.mp4",
  "resolution": "2k"
}'
```

### Configure the output frame rate (smoothness)

Use the `fps` parameter to set the output frame rate from 15 to 120 fps, inclusive. A higher frame rate enables AI\-powered frame interpolation for smoother motion.

* **Default behavior**: If you do not specify `fps`, the output video retains the source video's frame rate.

* **Recommendation**: If the target frame rate exceeds the source video's frame rate, the system automatically applies AI\-powered frame interpolation. To keep motion natural while managing processing costs, we recommend setting the output frame rate to no more than four times the source frame rate.

#### Example: Increase the frame rate to 60 fps using AI\-powered interpolation

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
    "video_url": "https://example.com/demo_video_480p.mp4",
    "resolution": "1080p",
    "fps": 60
}'
```

### Configure the output bitrate

The output bitrate determines the video's visual quality and final file size. AI MediaKit provides two ways to control it. If you specify both `bitrate_level` and `bitrate`, **only** **`bitrate`** ** takes effect**.

|Method |Parameter |Description |
|---|---|---|
|Bitrate level |`bitrate_level` |Sets the output video's target average bitrate using a predefined level. Options are `low`, `medium` (recommended), and `high`. The default is `medium`. The actual bitrate is calculated automatically based on the target resolution and frame rate. For the target bitrate at each level, see [Bitrate reference](https://docs.byteplus.com/create-video-quality-enhancement-ai-enhanced-task#7656e3b8). |
|Exact bitrate |`bitrate` |Sets the target average bitrate directly, in kbps. The value must be within `[10, 150000]`. Use this parameter when you need precise bitrate control. If omitted, the bitrate is calculated automatically based on `bitrate_level`, resolution, and frame rate. |

#### Example: Specify an exact output bitrate of 8000 kbps

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video-generative' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
    "video_url": "https://example.com/demo_video_480p.mp4",
    "resolution": "1080p",
    "bitrate": 8000
}'
```

## Reference

### Estimated processing time

Processing time depends on the source video's duration. To estimate it, use the real\-time factor (RTF): the ratio of processing time to source video duration. The average RTF for Video Quality Enhancement (AI\-Enhanced) is approximately **15–20**, so a 1\-minute video is expected to take **15–20 minutes** to process.

> **INFO**

* > Actual processing time also depends on the input video's resolution and bitrate, as well as the current processing queue. In production, we recommend configuring [Event notification](https://docs.byteplus.com/event-notification) to receive completion notifications in real time.

* > If you need shorter processing times, see [Video quality enhancement (fast)](https://docs.byteplus.com/video-quality-enhancement-lite).

### Billing

Video Quality Enhancement (AI\-Enhanced) uses postpaid, pay\-as\-you\-go billing based on **output video duration**, **output resolution**, and **output frame rate**. The base price is  **$1.50/minute**, multiplied by the billing coefficient for the selected output resolution and frame rate. For the billing formula, coefficients, and an example, see [Video quality enhancement pricing (AI-enhanced)](https://docs.byteplus.com/pricing#video-quality-enhancement-pricing-(ai-enhanced)).

### Video quality comparison tool

The Video quality comparison tool displays the source and enhanced videos side by side so you can compare their clarity, color saturation, and fidelity of visual details. Follow these steps:

1. Go to the [Tool experience](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit) page in the AI MediaKit console and click **Video quality comparison** in the upper\-right corner.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c84b8c20248a42a8a90a10fa15634817~tplv-goo7wpa0wc-topic.webp)

2. Enter the URLs of the source video and the video enhanced by the API, or select downloaded copies of both videos from your device.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/574c92222633403ca277bfb7e4374d59~tplv-goo7wpa0wc-topic.webp)

3. The comparison player automatically loads and displays both videos. Drag the **divider** left or right to compare image quality frame by frame.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4bc44b7340146cfa800f9e2227faab1~tplv-goo7wpa0wc-topic.webp)

## API references

* [Create a video quality enhancement (AI-enhanced) task](https://docs.byteplus.com/create-video-quality-enhancement-ai-enhanced-task)

* [Get task details](https://docs.byteplus.com/get-task-details)

* [Event notification](https://docs.byteplus.com/event-notification)

---
title: "Subtitle burn-in"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-subtitle-burn-in"
---

The AI MediaKit subtitle burn\-in tool lets you burn (also called "hardcode") external subtitle files (such as SRT and ASS) or text content you provide directly into the video frame. Using rich, customizable styles, you can produce a new video with embedded subtitles.

This guide walks you through how to add professional embedded subtitles to your video via API calls.

<span id="quickstart-add-embedded-subtitles-to-a-vlog-video"></span>
## Quickstart: Add embedded subtitles to a Vlog video

This section uses a concrete example to demonstrate how to provide subtitle text and timestamps directly in the API request to add two lines of dialogue subtitles to a Vlog video.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare a video file**: Have a video file ready that needs subtitles, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Subtitle burn\-in is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/add-subtitle-to-video` to submit the task, and you receive a unique `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field to get the download URL of the subtitled video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

Call the [Create a subtitle burn-in task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-subtitle-burn-in-task) API. You can copy the following cURL command to submit a subtitle burn\-in task. This example adds two subtitles and specifies the "Montserrat" font.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/add-subtitle-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_vlog_video.mp4",
  "subtitles": [
    {
      "subtitle_text": "Hi everyone, welcome to my Vlog!",
      "start_time": 0.5,
      "end_time": 3.0
    },
    {
      "subtitle_text": "The weather is really nice today~",
      "start_time": 3.5,
      "end_time": 5.0
    }
  ],
  "subtitle_font_type": "montserrat"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of the video file you prepared.</div>


* <div data-tips="true" data-tips-type="default">You can modify the content in the <code>subtitles</code> array, including the text (<code>subtitle_text</code>) and the start and end times (<code>start_time</code>, <code>end_time</code>).</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-add-subtitle-to-video-123456789",
  "request_id": "20240520183000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to get the final result until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` in the `result` field is the download URL of the subtitled video (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-subtitle-to-video-123456789",
    "task_type": "add-subtitle-to-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/subtitled-video.mp4?auth_key=...",
        "resolution": "1080p",
        "duration": 125.4
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="add-subtitles-from-a-subtitle-file"></span>
### Add subtitles from a subtitle file

In addition to providing subtitle text directly in the request body, you can also provide a publicly accessible subtitle file URL (in formats such as SRT, VTT, or ASS). The system automatically parses it and adds it to the video.

```JSON
{
  "video_url": "https://example.com/your_movie_clip.mp4",
  "subtitle_url": "https://example.com/your_subtitles.srt",
  "subtitle_font_size": 48,
  "subtitle_font_color": "#FFFFFFCC"
}
```


When both `subtitle_url` and `subtitles` are present, the system gives priority to `subtitle_url`.

<span id="customize-subtitle-styles"></span>
### Customize subtitle styles

AI MediaKit lets you customize the visual style of subtitles through a rich set of API parameters, so they fit your video content and brand style perfectly. You can customize the position, font, size, and color of the subtitles.

The main style control parameters are as follows:


* `subtitle_pos_preset`: Quickly place subtitles at common positions in the frame using preset values.

   * `bottom_center`: Bottom center (default)

   * `top_center`: Top center

   * `center`: Center of the frame

   * `lower_third`: Lower third of the frame

* `subtitle_font_type`: Choose from a variety of fonts to match the video's mood.

   * (Default) `inter`

   * `montserrat`

   * `oppo_sans`

   * `roboto`

   * `source_han_serif`

* `subtitle_font_size`: Sets the pixel size of the subtitles. The default is `50`.

* `subtitle_font_color`: Sets the color and opacity using an RGBA hexadecimal format (such as `#RRGGBBAA`). The default value is `#FFFFFFFF` (opaque white).


<span id="example-apply-custom-styles"></span>
#### Example: Apply custom styles

The following example demonstrates how to set the subtitle font to "Source Han Serif", the size to 48 pixels, the color to 75%\-opacity white (#FFFFFFBF), and the position to the bottom center of the frame.

```JSON
{
  "video_url": "https://example.com/your_corporate_video.mp4",
  "subtitle_url": "https://example.com/your_subtitles.srt",
  "subtitle_pos_preset": "bottom_center",
  "subtitle_font_type": "source_han_serif",
  "subtitle_font_size": 48,
  "subtitle_font_color": "#FFFFFFBF"
}
```


<span id="related-api-references"></span>
## API references


* [Create a subtitle burn-in task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-subtitle-burn-in-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

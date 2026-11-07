---
title: "Text-to-scrolling video"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-text-to-scrolling-video"
---

The AI MediaKit text\-to\-scrolling video tool combines a large block of text with a background image and music to quickly generate a professional, smooth vertical (9:16) scrolling text video. It is an excellent choice for scenarios such as novel promos, content explainers, and lyric videos. The output video is in MP4 format. This guide walks you through how to easily turn your text into an engaging scrolling video via an API call.

<span id="effect-preview"></span>
## Demo

With the text\-to\-scrolling video tool, you can turn a block of plain text, a background image, and an audio track into a complete video.


|Input |Output |
|---|---|
|Novel text + a light\-colored background image + a soothing background music track |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58869051080b4b19acc8c92d2c4b641f~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-generate-a-basic-text-to-scrolling-video"></span>
## Quickstart: Generate a basic text\-to\-scrolling video

This section uses a concrete example to demonstrate how to call the API to generate a scrolling video from a block of novel text.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare your materials**:

   * **Text content**: Have the text you want to display ready.

   * **Background image**: Prepare an image to use as the video background, and upload it to a publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can access.


<span id="procedure"></span>
### Procedure

Text\-to\-scrolling video is an asynchronous task. The overall API flow is as follows:


1. After you successfully call `POST /api/v1/tools/text-to-scrolling-video` to submit the task, you obtain a unique `task_id`.

2. You can poll the `GET /api/v1/tasks/{task_id}` API to query the task status until the `status` becomes `completed`. Alternatively, configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the generated video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a text-to-scrolling video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-to-scrolling-video-task) API. You can copy the following cURL command to submit the most basic task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/text-to-scrolling-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "text": "Chapter 1: A New Journey\nIn a faraway land, the story begins. The protagonist faces unprecedented challenges, but is determined to press forward and explore the unknown world.",
  "image_url": "https://example.com/background.jpg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>image_url</code> with the URL of your own background image.</div>


* <div data-tips="true" data-tips-type="default">Replace the content of the <code>text</code> field with your own text.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-text-to-scrolling-video-123456789",
  "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video generation takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` field within `result` is the download URL of the final video. This URL is valid for 24 hours, so be sure to download and save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-text-to-scrolling-video-123456789",
    "request_id": "20240521113000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "720p",
        "duration": 25.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<span id="advanced-usage-customize-video-effects"></span>
## Advanced usage: Customize video effects

Besides the required text and background image, you can fine\-tune the audiovisual effect of the video with a rich set of optional parameters.

<span id="customize-visual-elements-resolution-font-color"></span>
### Customize visual elements (resolution, font, color)


* `resolution`: Sets the video resolution. The default is `720p`. Example: `"resolution": "1080p"`

* `font_type`: Selects a font. The default is `inter`. Supported values include:

   * `inter`: Inter

   * `roboto`: Roboto

   * `source_han_serif`: Source Han Serif

* `font_color`: Sets the text color in 8\-digit RGBA hexadecimal format. The default is `#1F1F1FFF` (opaque dark gray). If you use a dark background, be sure to specify a light font color (such as `#FFFFFFFF`) to ensure the contrast ratio is at least 4.5:1. Example (white font): `"font_color": "#FFFFFFFF"`


<span id="adjust-the-scrolling-rhythm-speed-start-end-hold"></span>
### Adjust the scrolling rhythm (speed, start/end hold)


* This list item is a duplicate of the more detailed one that follows and should be removed.

* `single_roll_duration`: The time it takes for a single page of text to fully scroll across the screen, in seconds. The value must be between 0.5 and 60. A smaller value means faster scrolling. The default is `3`. Example (faster scrolling): `"single_roll_duration": 2.5`

* `start_hold_duration`: The time the text stays still when the video begins, in seconds. The value must be between 0 and 60. The default is `2`. Example (start scrolling immediately): `"start_hold_duration": 0`

* `end_hold_duration`: The time the text stays still when the video ends, in seconds. The value must be between 0 and 60. The default is `2`. Example (extend the ending hold): `"end_hold_duration": 5`


<span id="add-background-music"></span>
### Add background music


* `audio_url`: Provides the URL of the background music. The audio loops until the video ends. Example: `"audio_url": "https://example.com/bgm.mp3"`


<span id="example-create-a-customized-scrolling-video"></span>
### Example: Create a customized scrolling video

The following request generates a 1080p video that uses the Inter font in white, scrolls faster, and includes background music.

```JSON
{
 "text": "...",
 "image_url": "https://example.com/dark_background.png",
 "audio_url": "https://example.com/epic_music.mp3",
 "resolution": "1080p",
 "font_type": "inter",
 "font_color": "#FFFFFFFF",
 "single_roll_duration": 2.5
}
```


<span id="appendix-default-configuration-details"></span>
## Appendix: Default configuration details

To ensure an out\-of\-the\-box experience, the system comes with a set of built\-in default configurations. This appendix details each default setting in the text\-to\-scrolling video generation process.

<span id="2a6b61eb"></span>
### Layout and size


* Output size: The video frame is fixed to a 9:16 vertical orientation. You can select the output resolution level using the `resolution` parameter. The specific pixel dimensions for each level are as follows:

   * `360p`: 360 × 640

   * `480p`: 480 × 854

   * `720p`: 720 × 1280 (default)

   * `1080p`: 1080 × 1920

* Font size: The font size scales linearly with the `resolution` level you select to ensure a consistent visual effect. For example, at `720p`, the font size is about 36px. This scaling is handled automatically by the system and cannot be set directly.

* Margins and spacing: To ensure readability, the system uses fixed text margins and spacing. These cannot be customized.

   * Left and right margins: About 16% of the canvas width. The specific pixel values are as follows: 58px for `360p`, 76px for `480p`, 116px for `720p`, and 172px for `1080p`.

   * Line spacing: 20px.

   * Character spacing: 3px.


<span id="6d32cf46"></span>
### Timing and scrolling


* Start and end hold: The video displays the text statically for a period before scrolling starts and after scrolling ends. You can set these using the `start_hold_duration` (default 2 seconds) and `end_hold_duration` (default 2 seconds) parameters.

* Scrolling speed: This refers to the time it takes for a single page of text to enter and completely exit the frame. You can control it using the `single_roll_duration` parameter, which defaults to 3 seconds per page. A smaller value means faster scrolling.

* Scrolling position: The text scrolls in from the bottom of the screen and scrolls out from the top. This behavior cannot be customized.


<span id="53066b92"></span>
### Font and background


* Font color: You can select a preset font using the `font_type` parameter and customize the font color using the `font_color` parameter (default `#1F1F1FFF`). Note that the default color is only suitable for light backgrounds. If you use a dark background, be sure to specify a light font color with sufficient contrast (such as `#FFFFFFFF`).

* Font background optimization: To prevent black jagged edges or flickering as the text scrolls, the system automatically sets a background for the font that is the same color as the font but fully transparent. This is a built\-in optimization that cannot be disabled or modified.

* Background image processing (top/bottom masks): You must provide a background image via `image_url`. The system automatically crops the top 10% and bottom 10% regions of the background image and overlays them as semi\-transparent masks on the top and bottom of the video to enhance the readability of the scrolling text. Therefore, ensure that the image has no critical information in these two areas.

* Background music processing: You can provide a background music URL via the `audio_url` parameter. The music loops until the video ends. If the music is longer than the video, the excess is automatically truncated.


<span id="related-api-references"></span>
## API references


* [Create a text-to-scrolling video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-to-scrolling-video-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

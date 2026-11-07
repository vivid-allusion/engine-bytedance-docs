---
title: "Create a text-to-scrolling video task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-text-to-scrolling-video-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/text-to-scrolling-video`

To programmatically convert a block of text into a vertical video, you can use this API to submit an asynchronous task. This process generates a 9:16 scrolling text video in MP4 format, which is ideal for use cases like novel promos, content explainers, and lyric videos.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-text-to-scrolling-video">Text\-to\-scrolling video</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`text` |String |Yes |`This is a scrolling video example...\nThis is a new line.` |The text content to scroll. The text is displayed horizontally and left\-aligned. Use `\n` to force a line break. Without `\n`, the text wraps automatically based on the canvas width. Some special characters may need to be manually escaped. For example, to display a single slash character (`/`) in the video, you must input two slashes (`//`) in the `text` field. |
|`image_url` |String |Yes |`https://example.com/background.jpg` |The URL of the background image.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common static image formats such as `jpg`, `png`, and `webp`.<br><br><br>For the best result, we recommend that you:<br><br><br>* Use an image with a **9:16** aspect ratio to match the output video.<br><br>* Keep the image resolution as close as possible to the output `resolution` you select.<br><br>* Ensure the overall tone of the image has sufficient contrast with `font_color`.<br><br><br>**Note**: The top 10% and bottom 10% regions of the image are used as masks. Avoid placing important content in these areas. |
|`audio_url` |String |No |`https://example.com/bgm.mp3` |The URL of the background music. The audio loops seamlessly to cover the entire video duration.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common audio formats such as `mp3`, `m4a`, and `wav`.<br><br>* **File size**: It is recommended that a single input file not exceed 10 GB. |
|`resolution` |String |No |`720p` |The output vertical resolution (fixed at 9:16). The default is `720p`. Supported values: `360p`, `480p`, `720p`, `1080p`. |
|`font_type` |String |No |`sy_black` |The font type of the scrolling text. The default is `inter`. Supported values:<br><br><br>* `inter`<br><br>* `roboto`<br><br>* `source_han_serif` |
|`font_color` |String |No |`#1F1F1FFF` |The text color, which must be in 8\-digit RGBA hexadecimal format (`RRGGBBAA`). The default is `#1F1F1FFF` (opaque dark gray). If you use a dark background image, we recommend a light font color (such as `#FFFFFFFF`) to ensure readability. For optimal legibility, we suggest maintaining a contrast ratio of at least 4.5:1 between the font and the background. |
|`single_roll_duration` |Number |No |`3` |The time it takes for a single page of text to fully scroll across the screen, in seconds. A smaller value means faster scrolling. The default is `3`. The value ranges from `[0.5, 60]`. |
|`start_hold_duration` |Number |No |`2` |The time the text stays still at the starting position when the video begins, in seconds. The default is `2`. The value ranges from `[0, 60]`. |
|`end_hold_duration` |Number |No |`2` |The time the text stays still at the ending position when the video ends, in seconds. The default is `2`. The value ranges from `[0, 60]`. |
|`client_token` |String |No |`your_unique_request_id_136` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to generate a 1080p scrolling text video with background music, using Source Han Sans and a white font color.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/text-to-scrolling-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "text": "Chapter 1: A New Journey\nIn a faraway land, the story begins.\nThe protagonist faces unprecedented challenges, but is determined to press forward and explore the unknown world.",
  "image_url": "https://example.com/dark_background.png",
  "resolution": "1080p",
  "audio_url": "https://example.com/epic_music.mp3",
  "font_type": "inter",
  "font_color": "#FFFFFFFF",
  "single_roll_duration": 4.5
}'
```


<span id="response"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="success"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-text-to-scrolling-video-456789012",
  "request_id": "20240520180000ABCDEFG12345"
}
```


<span id="failure"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240520180500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `image_url` is required.",
    "param": "image_url",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Text\-to\-scrolling video is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4?auth_key=...` |The URL of the generated scrolling text video file, in MP4 format. This is an HTTPS temporary download link, valid for **24 hours** by default; please download and save the file promptly. |
|`duration` |Number |`25.5` |The total duration of the output video, in seconds. |
|`resolution` |String |`1080p` |The resolution of the output video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-text-to-scrolling-video-456789012",
    "request_id": "20240520180000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 25.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```


<span id="appendix-default-configuration-details"></span>
## Appendix: Default configuration details

To ensure an out\-of\-the\-box experience, the system comes with a set of built\-in default configurations. This appendix details each default setting in the text\-to\-scrolling video generation process.

<span id="layout-and-size"></span>
### Layout and size


* Output size: The video frame is fixed to a 9:16 vertical orientation. You can select the output resolution level using the `resolution` parameter. The specific pixel dimensions for each level are as follows:

   * `360p`: 360 × 640

   * `480p`: 480 × 854

   * `720p`: 720 × 1280 (default)

   * `1080p`: 1080 × 1920

* Font size: The font size scales linearly with the `resolution` level you select to ensure a consistent visual effect. For example, at `720p`, the font size is about 36px. This scaling is handled automatically by the system and cannot be set directly.

* Margins and spacing: To ensure reading comfort, the system uses fixed text margins and spacing. These cannot be customized.

   * Left and right margins: About 16% of the canvas width. The specific pixel values are as follows: 58px for `360p`, 76px for `480p`, 116px for `720p`, and 172px for `1080p`.

   * Line spacing: 20px.

   * Character spacing: 3px.


<span id="timing-and-scrolling"></span>
### Timing and scrolling


* Start and end hold: The video displays the text statically for a period before scrolling starts and after scrolling ends. You can set these using the `start_hold_duration` (default 2 seconds) and `end_hold_duration` (default 2 seconds) parameters.

* Scrolling speed: This refers to the time it takes for a single page of text to enter and completely exit the frame. You can control it using the `single_roll_duration` parameter, which defaults to 3 seconds per page. A smaller value means faster scrolling.

* Scrolling position: The text scrolls in from the bottom of the screen and scrolls out from the top. This behavior cannot be customized.


<span id="font-and-background"></span>
### Font and background


* Font color: You can select a preset font type using the `font_type` parameter and customize the font color using the `font_color` parameter (default `#1F1F1FFF`). Note that the default color is only suitable for light backgrounds. If you use a dark background, be sure to pass in a light font color with sufficient contrast (such as `#FFFFFFFF`).

* Font background optimization: To prevent black jagged edges or flickering as the text scrolls, the system automatically sets a background for the font that is the same color as the font but fully transparent. This is a built\-in optimization that cannot be disabled or modified.

* Background image processing (top/bottom masks): You must provide a background image via `image_url`. The system automatically crops the top 10% and bottom 10% regions of the background image and overlays them as semi\-transparent masks on the top and bottom of the video to enhance the readability of the scrolling text. Therefore, ensure that the image has no critical information in these two areas.

* Background music processing: You can provide a background music URL via the `audio_url` parameter. The music loops until the video ends. If the music is longer than the video, the excess is automatically truncated.

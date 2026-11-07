---
title: "Video matting"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-matting"
---

AI MediaKit provides two tools, **portrait matting** and **green screen matting**, that accurately separate the subject in a video (people, objects, and so on) from the background to generate video assets with a transparent or solid\-color background. This offers powerful support for post\-production scenarios such as virtual background replacement, creative compositing, and e\-commerce display. This development guide helps you get started quickly and implement automated video matting through the API.

<span id="tool-overview"></span>
## Tool overview

AI MediaKit provides a separate API for **portrait matting** and **green screen matting**, but both follow the exact same asynchronous task flow and use the same API to query task results.


|Tool |API |Core capability |
|---|---|---|
|Green screen matting |[Create a green screen matting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-green-screen-matting-task) |Performs matting on videos with a green screen or solid\-color background. This feature automatically detects and preserves the subject (such as people, objects, and animals), removes the background, and generates a video with a transparent or solid\-color background. |
|Portrait matting |[Create a portrait matting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-portrait-matting-task) |Automatically detects the human subject in a video, removes the original background, and generates a video file with a transparent or solid\-color background. |


<span id="effect-preview"></span>
## Demo


|Tool |Source video |Matted video |
|---|---|---|
|Green screen matting |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/089c9027293c495da31a491d28c7a66a~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6cc2be2ecf3492e8f414b3e09aa4b90~tplv-goo7wpa0wc-image.image" controls></video><br> |
|Portrait matting |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81da4aecfd514883ac4ed6c67d1f0f47~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32954f0259064f21acbcfb2eec29a0e8~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-implement-portrait-matting-in-one-step"></span>
## Quickstart: Implement portrait matting in one step

This section uses **portrait matting** as an example to demonstrate the complete API call flow.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare a video file**: Have a video file ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Video matting is an asynchronous task. The overall flow is as follows:


1. After you successfully call `POST /api/v1/tools/matte-portrait-video`, the API returns a task ID.

2. You can poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field to get the download URL of the video with a transparent background from the `video_url` field.


<span id="step-1-submit-the-portrait-matting-task"></span>
#### Step 1: Submit the portrait matting task

You can directly copy the following cURL command to submit a portrait matting task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/matte-portrait-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_portrait_video.mp4"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-matte-portrait-video-123456789",
  "request_id": "20240521100000ABCDEFG12345"
}
```


<span id="step-2-get-the-matting-result"></span>
#### Step 2: Get the matting result

You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive a response containing the final result. `result.video_url` is the download URL of the matted video with a transparent background (the default output format is WebM, and the link is valid for **24** hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-matte-portrait-video-123456789",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/matted_output.webm?auth_key=...",
        "resolution": "1080p",
        "duration": 15.5
    },
    ...
}
```


If your video was shot against a green screen or solid\-color background, you can call the [Create a green screen matting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-green-screen-matting-task) API for a more refined result. The flow is similar to portrait matting; you only need to change the API endpoint to `POST /api/v1/tools/matte-greenscreen-video`.

<span id="advanced-usage"></span>
## Advanced usage

<span id="choose-the-output-format-and-background-color"></span>
### Choose the output format and background color

The video matting tool supports three output formats, which you can specify with the `format` parameter when submitting the task:


* `WEBM` (default): Outputs a video with a **transparent background**, offering good compatibility and a smaller file size.

* `MOV`: Outputs a video with a **transparent background**, providing a lossless Alpha channel with a larger file size.

* `MP4`: Outputs a video with a **solid\-color background**. When you select MP4, you can also specify the background color with the `background_color` parameter, which supports `black`, `white`, and `green`. The default background color differs between the two matting tools:

   * Green screen matting: When `format` is `MP4` and `background_color` is not passed, the default background color is `black`.

   * Portrait matting: When `format` is `MP4` and `background_color` is not passed, the default background color is `green`.


The following example demonstrates how to output the portrait matting result as an MP4 video with a white background:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/matte-portrait-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_portrait_video.mp4",
  "format": "MP4",
  "background_color": "white"
}'
```


<span id="reference"></span>
## References

<span id="application-scenarios"></span>
### Application scenarios


* **Virtual backgrounds and live streaming**: In video conferencing, online education, or live streaming, replace a person's background in real time or offline to create professional and engaging virtual scenes.

* **Film and short\-video creation**: Composite captured footage of people or objects with any background or video effects to create imaginative visual results.

* **E\-commerce video production**: Swap in backgrounds of different styles for product showcase videos, or generate assets with a transparent background for reuse across various marketing scenarios.

* **Education and presentations**: Extract the presenter and overlay them onto courseware or presentation content to create more engaging picture\-in\-picture instructional videos.


<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input file |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `mkv`, `wmv`.<br><br>* **File size**: It is recommended that the input file size not exceed 10 GB. |


<span id="processing-time"></span>
### Processing time

The processing time depends on the original duration and resolution of the video, and is typically 1 to 3 times the video duration.

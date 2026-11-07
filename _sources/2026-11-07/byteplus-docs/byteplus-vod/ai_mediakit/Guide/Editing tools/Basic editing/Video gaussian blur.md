---
title: "Video gaussian blur"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-video-gaussian-blur"
---

The AI MediaKit Gaussian blur video tool lets you apply a Gaussian blur effect to one or more specified rectangular regions in a video frame. This capability is commonly used to protect private information (such as faces or ID numbers) and obscure fixed watermarks or corner logos. The output video is in MP4 format.

This guide walks you through how to precisely add a blur effect to your video via an API call.

<span id="effect-preview"></span>
## Demo

With the Gaussian blur video tool, you can dynamically blur specific regions in a video to obscure information.


|Source video |With Gaussian blur added |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8db2fa294a74bab84fe5d91a419ae75~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db1f5dfa45914486848789fe5440400b~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-add-a-blur-to-a-specified-region-in-a-video"></span>
## Quickstart: Add a blur to a specified region in a video

This section uses a concrete example to demonstrate how to call the API to add a Gaussian blur effect to a specified rectangular region from the 5th second to the 10.5th second of a video.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a video file**: Have a video file ready for the blur effect, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Gaussian blur video is an asynchronous task. The overall API flow is as follows:


1. After you successfully call `POST /api/v1/tools/gaussian-blur-video` to submit the task, you obtain a unique `task_id`.

2. You can poll the `GET /api/v1/tasks/{task_id}` API to query the task status until the `status` becomes `completed`. Alternatively, configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the processed video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a gaussian blur video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-gaussian-blur-video-task) API. You can copy the following cURL command to submit the task. This example adds a blur effect to a specified time range and coordinate region of the video.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/gaussian-blur-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/input_video.mp4",
  "blur_regions": [
    {
      "start_time": 5.0,
      "end_time": 10.5,
      "top_left_x": 100,
      "top_left_y": 150,
      "bottom_right_x": 300,
      "bottom_right_y": 400
    }
  ]
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-gaussian-blur-video-123456789",
  "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `video_url` field within `result` is the download URL of the blurred video. This URL is valid for 24 hours, so be sure to download and save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-gaussian-blur-video-123456789",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/blurred_output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="define-blur-regions"></span>
### Define blur regions

You can use the `blur_regions` parameter to manually specify one or more rectangular regions to blur. `blur_regions` is an array that supports up to 3 configurations. Each configuration (a JSON object) defines a blur region and its effective time range.

The position of each region is defined by the coordinates of its top\-left and bottom\-right corners. All coordinate values are in pixels, with the origin `(0, 0)` at the top\-left corner of the video frame.


* `top_left_x`: The X coordinate of the top\-left corner of the rectangle (b1 in the diagram).

* `top_left_y`: The Y coordinate of the top\-left corner of the rectangle (a1 in the diagram).

* `bottom_right_x`: The X coordinate of the bottom\-right corner of the rectangle (b2 in the diagram).

* `bottom_right_y`: The Y coordinate of the bottom\-right corner of the rectangle (a2 in the diagram).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15909af6a6bb4493b351870ff7c571fc~tplv-goo7wpa0wc-image.image) </span>

<span id="example-add-two-blur-regions-to-a-video"></span>
#### Example: Add two blur regions to a video

The following example demonstrates how to add two Gaussian blur effects to a video:


1. From the 5th second to the 10.5th second, blur the region from `(100, 150)` to `(300, 400)`.

2. From the 15th second to the 20th second, blur the region from `(500, 600)` to `(700, 800)`.


```JSON
{
  "video_url": "https://example.com/input_video.mp4",
  "blur_regions": [
    {
      "start_time": 5.0,
      "end_time": 10.5,
      "top_left_x": 100,
      "top_left_y": 150,
      "bottom_right_x": 300,
      "bottom_right_y": 400
    },
    {
      "start_time": 15.0,
      "end_time": 20.0,
      "top_left_x": 500,
      "top_left_y": 600,
      "bottom_right_x": 700,
      "bottom_right_y": 800
    }
  ]
}
```


<span id="related-api-references"></span>
## Related APIs


* [Create a gaussian blur video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-gaussian-blur-video-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

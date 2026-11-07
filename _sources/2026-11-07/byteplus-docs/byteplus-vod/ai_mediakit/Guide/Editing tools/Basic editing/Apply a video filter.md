---
title: "Apply a video filter"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-apply-video-filter"
---

The AI MediaKit video filter tool lets you apply a variety of professional, cinematic preset filters to a video with one click, significantly enhancing its visual atmosphere and artistic quality. The output video is in MP4 format.

This guide walks you through how to easily add a filter effect to your video via an API call.

<span id="effect-preview"></span>
## Demo

With the video filter tool, you can quickly transform an ordinary video into a piece with a specific atmosphere.


|Input video |Output video (with the "vivid" filter) |
|---|---|
|<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ba42983c9da473f9b32d5eb304a2a2a~tplv-goo7wpa0wc-image.image" controls></video><br> |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c1f529acf904ca09dbfbd5d44a1e975~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="quickstart-apply-the-sunset-filter-to-a-landscape-video"></span>
## Quickstart: Apply the "sunset" filter to a landscape video

This section uses a concrete example to demonstrate how to call the API to apply the sunset (`sunset`) filter to a landscape video.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a video file**: Have a video file ready for the filter, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the video to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Applying a video filter is an asynchronous task. The overall API flow is as follows:


1. After you successfully call `POST /api/v1/tools/apply-video-filter` to submit the task, you obtain a unique `task_id`.

2. You can poll the `GET /api/v1/tasks/{task_id}` API to query the task status until the `status` becomes `completed`. Alternatively, you can configure [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the download URL of the filtered video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create a video filter task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-filter-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/apply-video-filter' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_landscape_video.mp4",
  "filter_style": "sunset"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the value of <code>video_url</code> with the URL of your own video file.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-apply-video-filter-123456789",
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


When the task is successfully completed, you will receive the following response. The `video_url` field within `result` is the download URL of the filtered video. This URL is valid for 24 hours, so be sure to download and save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-apply-video-filter-123456789",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/output.mp4?auth_key=1774504841-...",
        "resolution": "1080p",
        "duration": 125.8
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20240521113000ABCDEFG12345"
}
```


<span id="appendix-supported-filter-styles"></span>
## Supported filter styles

In addition to the "sunset" filter, you can specify the following preset styles using the `filter_style` parameter. If this parameter is not specified, the system uses the `spring` filter by default.


|`filter_style`  |Effect |Description |
|---|---|---|
|`spring` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2abc892dfdf46d5af3a753a12c882a2~tplv-goo7wpa0wc-image.image) </span> |An overall fresh and bright tone, suitable for outdoor and natural scenery. |
|`sunset` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faa6fabaa17346d18c1586d974b09c1d~tplv-goo7wpa0wc-image.image) </span> |Enhances warm tones to create a warm, romantic, and retro dusk atmosphere. |
|`vivid` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ab2d9a526674d2d8d74bc78972d2ca3~tplv-goo7wpa0wc-image.image) </span> |Increases color saturation and contrast to make the footage more lively and vivid. |
|`fair_skin` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c15444797874b7c97652906aa0bd053~tplv-goo7wpa0wc-image.image) </span> |Optimized for portraits, brightening skin tones for a natural whitening effect. |
|`food` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7965d4ca4340f3b0da03619df45656~tplv-goo7wpa0wc-image.image) </span> |Increases color saturation and warm tones to make food look more appealing. |


<span id="related-api-references"></span>
## Related APIs


* [Create a video filter task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-filter-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

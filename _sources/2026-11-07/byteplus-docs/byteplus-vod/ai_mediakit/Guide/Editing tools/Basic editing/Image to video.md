---
title: "Image to video"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-to-video"
---

The AI MediaKit image\-to\-video tool lets you combine multiple static images (JPG/PNG) into a single continuous dynamic video. You can set the display duration and a pan or zoom animation for each image individually, and add rich transition effects at the transitions between images. This tool is widely used in scenarios such as creating electronic photo albums, turning slide decks into videos, and automatically generating short videos for social media.

This guide walks you through how to use the image\-to\-video tool to turn a series of static images into a vivid, engaging dynamic video.

<span id="quickstart-create-a-product-showcase-video"></span>
## Quickstart: Create a product showcase video

This section uses a concrete example to demonstrate how to combine three JPG product images into a dynamic video and add transition effects.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare image files**: Have multiple product images ready, preferably in the common JPG or PNG format. Try to ensure the images are clear and that each image is not too large (for example, under 20 MB). Upload these images to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain URLs that the API can call.


<span id="procedure"></span>
### Procedure

Image\-to\-video is an asynchronous task. The standard workflow is as follows:


1. Call `POST /api/v1/tools/image-to-video` to submit the task, and the API returns a `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field to get the download URL of the final video from the `video_url` field.


<span id="step-1-submit-the-task"></span>
#### Step 1: Submit the task

You need to call the [Create an image-to-video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task) API. You can copy the following cURL command to submit an image\-to\-video task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/image-to-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "images": [
    {
      "image_url": "https://example.com/product_front.jpg",
      "duration": 5.0,
      "animation_type": "zoom_in"
    },
    {
      "image_url": "https://example.com/product_detail.jpg",
      "duration": 5.0,
      "animation_type": "move_right"
    },
    {
      "image_url": "https://example.com/product_package.jpg",
      "duration": 5.0
    }
  ],
  "transitions": [
    "1109558",
    "1109560"
  ]
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">说明</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default"><code>image_url</code>: Replace it with your actual image URL. You can also adjust <code>duration</code> and <code>animation_type</code> (the animation within the image).</div>


* <div data-tips="true" data-tips-type="default"><code>transitions</code>: Replace with your preferred transition effect IDs. For more IDs, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task#b0e75726">Transition effects</a>.</div>



Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-image-to-video-92544004610",
  "request_id": "20260415150000F6DE4C24A6A0D94B7FF1"
}
```


<span id="step-2-get-the-result"></span>
#### Step 2: Get the result

Because video composition takes some processing time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


When the task is successfully completed, you will receive the following response. The `result` field is a JSON object; you can get the video's download URL from the `video_url` field within that object (the output is in MP4 format by default and the URL is valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-image-to-video-92544004610",
    "task_type": "image-to-video",
    "status": "completed",
    "result": {
        "video_url": "https://example.byteplus.com/img-to-video-final.mp4?auth_key=...",
        "resolution": "4k",
        "duration": 9
    },
    "expires_at": 1775047666,
    "created_at": 1774874853,
    "finished_at": 1774874866,
    "request_id": "1742012dcc1938455d84dbe56beb7acc"
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="fine-grained-control-over-image-animations"></span>
### Fine\-grained control over image animations

Beyond simply turning on a single animation effect, you can precisely control the start and end points of an animation during a single image's display by combining the `animation_type`, `animation_in`, and `animation_out` parameters. This lets you achieve more complex visual effects such as "static then moving", "moving then static", or "animation in the middle".


* `animation_in`: Defines the **start time** of the animation effect (in seconds), relative to the start of that image segment.

* `animation_out`: Defines the **end time** of the animation effect (in seconds), relative to the start of that image segment.


Example: For an image displayed for 5 seconds, keep it static for the first 2 seconds, start zooming in at the 2\-second mark, end the animation at the 4\-second mark, and keep it static again for the last 1 second.

```JSON
{
    "image_url": "https://example.com/some_image.jpg",
    "duration": 5.0,
    "animation_type": "zoom_in",
    "animation_in": 2.0,
    "animation_out": 4.0
}
```


<span id="cycling-through-transition-effects"></span>
### Cycling through transition effects

When processing multiple images, you do not need to provide a transition effect for every transition. The system supports automatically cycling through the transition effects. If the number of transition effects you provide in the `transitions` array is less than the number of transitions actually needed (that is, `number of images - 1`), the system cycles through your provided list of transition effects from the beginning.

<span id="example-1-apply-the-same-transition-to-all-switch-points"></span>
#### Example 1: Apply the same transition to all switch points

If you have 5 images (which require 4 transitions) but provide only one transition ID, all 4 transitions use that same transition effect.

```JSON
{
  "images": [
    { "image_url": "https://example.com/image1.jpg" },
    { "image_url": "https://example.com/image2.jpg" },
    { "image_url": "https://example.com/image3.jpg" },
    { "image_url": "https://example.com/image4.jpg" },
    { "image_url": "https://example.com/image5.jpg" }
  ],
  "transitions": [
    "1109556"
  ]
}
```


Actual effect: All 4 transitions use the "Swap" effect.

<span id="example-2-alternate-between-two-transitions"></span>
#### Example 2: Alternate between two transitions

If you have 5 images (which require 4 transitions) and provide two transition effects, the system cycles through them in order.

```JSON
{
  "images": [
    { "image_url": "https://example.com/image1.jpg" },
    { "image_url": "https://example.com/image2.jpg" },
    { "image_url": "https://example.com/image3.jpg" },
    { "image_url": "https://example.com/image4.jpg" },
    { "image_url": "https://example.com/image5.jpg" }
  ],
  "transitions": [
    "1109556",
    "1109558"
  ]
}
```


The actual effect is as follows:


* Between images 1 and 2: uses `1109556`

* Between images 2 and 3: uses `1109558`

* Between images 3 and 4: uses `1109556` (cycles back to the first)

* Between images 4 and 5: uses `1109558` (cycles to the second)


<span id="best-practices"></span>
## Best practices

**Pay attention to the clarity and aspect ratio of your source images**: The **resolution** and **aspect ratio** of the output video are both determined by the **first image** you pass in the `images` list. If subsequent images have a different aspect ratio from the first, the system preserves their original ratio, centers them on the video canvas, and fills the extra space with black bars. For the best visual result, we recommend that you:


* **Use a high\-quality first image**: Make sure the first image has the final resolution and aspect ratio you want.

* **Standardize the aspect ratio of your images**: Before submitting the task, try to process all images to a consistent aspect ratio.


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input limits |* **Image source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common static image formats such as `jpg` and `png`.<br><br>* **Number of images**: A single task supports 1 to 100 images. |


<span id="related-api-references"></span>
## Related APIs


* [Create an image-to-video task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-to-video-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)

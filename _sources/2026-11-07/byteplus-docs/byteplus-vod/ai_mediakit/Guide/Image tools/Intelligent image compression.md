---
title: "Intelligent image compression"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-intelligent-image-compression"
---

The AI MediaKit intelligent image compression tool uses advanced AI algorithms to substantially optimize image size, intelligently repairing quality issues introduced by compression—such as jaggies, color noise, and blocking artifacts—and enhancing image edges and texture details to produce an image that is both smaller and clearer than the original. This feature is suitable for a wide range of business scenarios that require large\-scale optimization of image storage costs, faster page loading, and a better image\-display experience for users.

<span id="quickstart-slim-an-image"></span>
## Quickstart: Slim an image

This section uses a concrete example to demonstrate how to call the API to slim an image.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

* **Prepare an image file**: Prepare an image to process and upload it to a publicly accessible server or the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can access.


<span id="procedure"></span>
### Procedure

Intelligent image compression is a **synchronous task**. You only need to call the [Create an intelligent image compression task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-intelligent-image-compression-task) API to get the processed image URL directly in the API response.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can directly copy the following cURL command, replace the parameters, and run it.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/slim-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/large-image.jpg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default"><code>image_url</code>: Replace it with your own image URL.</div>



Upon a successful request, you will receive the following response directly. The `image_url` in the `result` field is the download URL of the slimmed image. This URL is valid for **24 hours**, so be sure to download and save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-slim-image-12345678",
    "result": {
        "image_url": "https://example.byteplus.com/slim_output.png?auth_key=1775271661-...",
        "image_size": 158240,
        "image_format": "png",
        "image_width": 1920,
        "image_height": 1080
    },
    "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
    "expires_at": 1775271661
}
```


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input image limits |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* File size: It is recommended that a single image not exceed 50 MB.<br><br>* Supported formats: `jpeg`, `jpg`, `png`, `heic`, `avif`, `webp`. Animated images are not supported.<br><br>* Resolution limits: Neither the width nor the height of the input image may exceed 10000 pixels. When the input image format is `avif`, it is recommended that the product of the input image's width and height not exceed 100,000; otherwise, the task may fail. |

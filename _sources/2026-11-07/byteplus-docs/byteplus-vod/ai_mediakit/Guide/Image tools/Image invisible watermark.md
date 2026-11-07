---
title: "Image invisible watermark"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-invisible-watermark"
---

The AI MediaKit image invisible watermark tool hides a custom text message in an image without noticeably affecting the image's integrity or quality. This technology is essential for copyright protection, AIGC image compliance, distribution\-path tracking, and content\-theft evidence collection. Even after the image is scaled, compressed, or transcoded, the embedded invisible watermark can still be extracted successfully, providing strong evidence for copyright tracking and rights protection.

This guide walks you through:


* How the image invisible watermark workflow operates.

* How to get started by adding an invisible watermark to an image through the API and successfully extracting it from the processed image.

* How to choose the model version and watermark strength through parameters.


<span id="how-it-works"></span>
## How it works

The core image invisible watermark workflow consists of two main stages, "add" and "extract":


* **Add an invisible watermark**: Takes the original image and a custom text message (the watermark content) as input, and produces a new image that looks identical to the naked eye but contains the hidden information. You must explicitly specify the invisible watermark model version when adding a watermark.

* **Extract an invisible watermark**: Takes a suspected leaked or stolen image as input, and analyzes it through the invisible watermark extraction API to restore the originally embedded text message. You must use the **same model version** for extraction as was used when adding the watermark.


<span id="quickstart-add-and-extract-an-image-invisible-watermark"></span>
## Quickstart: Add and extract an image invisible watermark

This section demonstrates the complete workflow of adding an invisible watermark to an image and extracting it through API calls. Both adding and extracting image invisible watermarks are **synchronous tasks**; your requests return the processing results directly in the response.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

* **Prepare an image file**: Prepare an image and make it accessible via a public HTTP/HTTPS URL by uploading it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

Adding and extracting an invisible watermark is a workflow consisting of two synchronous tasks with the following core steps:


1. **Submit an ** **add** ** task and get the output**: Call the [Create an image invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task), and obtain the URL of the watermarked image (`image_url`) directly in the response's `result` field.

2. **Submit an extract task and get the result**: Call the [Create an image invisible watermark extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task), pass in the image URL obtained in the previous step and the **same ** **`tool_version`**, and obtain the extracted watermark content (`watermark_content`) in the response's `result` field.


<span id="step-1-submit-an-add-task"></span>
#### Step 1: Submit an add task

First, call the [Create an image invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task) to embed the text message you specify in an image. You can copy the following cURL command to submit the task. This example uses the `adapt` model version and embeds the text `copyright-2026` as the invisible watermark content.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/source_image.jpg",
  "tool_version": "adapt",
  "watermark_content": "copyright-2026"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with your own image URL</div>


* <div data-tips="true" data-tips-type="default"><code>tool_version</code>: The invisible watermark model version; this example uses <code>adapt</code>. Be sure to record this version, because you must use the same version for extraction.</div>


* <div data-tips="true" data-tips-type="default"><code>watermark_content</code>: The custom invisible watermark text content, up to 128 characters.</div>



Because this is a synchronous API, after a successful request you will obtain the download URL of the watermarked image directly in the response's `result` field (`image_url`, valid for 24 hours); be sure to save it promptly. An example of a successful response is as follows:

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-image-invisible-watermark-1703200",
    "task_type": "add-image-invisible-watermark",
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF2",
    "result": {
        "image_url": "https://example.com/watermarked_output.png?auth_key=...",
        "image_size": 875321,
        "image_format": "png",
        "image_width": 2048,
        "image_height": 1536
    },
    "expires_at": 1776274800
}
```


<span id="step-2-submit-an-extract-task"></span>
#### Step 2: Submit an extract task

After obtaining the URL of the watermarked image, call the [Create an image invisible watermark extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task) to parse the information hidden in it. Use the `image_url` you obtained in the previous step, pass in the **same ** **`tool_version`** that was used for adding the watermark, and then submit the request.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/extract-image-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/watermarked_output.png?auth_key=...",
  "tool_version": "adapt"
}'
```



* Replace `{Your_API_Key}` with your valid API Key.

* Replace `image_url` with the URL of the watermarked image you obtained in Step 1.

* `tool_version` must be the same as the version used when adding the watermark; otherwise the watermark may not be extracted correctly.


After a successful request, you will obtain the extracted watermark content directly in the response's `result.watermark_content` field. An example of a successful response is as follows:

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-image-invisible-watermark-1703201",
    "task_type": "extract-image-invisible-watermark",
    "request_id": "20260415150030F6DE4C24A6A0D94B7FF2",
    "result": {
        "watermark_content": "copyright-2026"
    },
    "expires_at": 1776274830
}
```


<span id="step-3-compare-the-watermark-content"></span>
#### Step 3: Compare the watermark content

Compare the watermark content extracted in Step 2 (`copyright-2026`) with the watermark content embedded in Step 1. If the two match, the source of the image has been successfully verified.

<span id="advanced-usage"></span>
## Advanced usage

<span id="adjust-the-watermark-strength"></span>
### Adjust the watermark strength

When calling the [Create an image invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task), you can adjust the watermark strength through the `strength_level` parameter. The higher the strength, the stronger the resistance to attacks (processing such as scaling, compression, and transcoding), but the greater the potential impact on the original image (an invisible watermark is still, by nature, a modification of the image's pixel data).


* `low`: Low strength. Suitable for solid\-color images and scenarios with high image\-quality requirements.

* `medium`: (Default) Medium strength. Balances image quality and attack resistance, suitable for most scenarios.

* `strong`: High strength. Suitable for images with rich texture, with the strongest attack resistance.


<span id="example-add-a-high-strength-invisible-watermark-and-specify-the-output-format"></span>
#### Example: Add a high\-strength invisible watermark and specify the output format

```JSON
{
  "image_url": "https://example.com/source.jpg",
  "tool_version": "adapt_resize",
  "watermark_content": "channel-A-user-10086",
  "strength_level": "strong",
  "output_format": "webp",
  "output_quality": 85
}
```


<span id="reference"></span>
## Reference

<span id="limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input image |* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp` are supported. |
|Watermark content |* Format: Custom text content.<br><br>* Length: Up to 128 characters; if the content consists entirely of Chinese characters, it is recommended not to exceed 42 characters. |
|Compatibility |The extraction API only supports extracting watermarks embedded by the AI MediaKit API for adding watermarks, and the `tool_version` used for extraction must be the same as the one used for addition. It cannot extract any form of invisible watermark added by third\-party tools. |

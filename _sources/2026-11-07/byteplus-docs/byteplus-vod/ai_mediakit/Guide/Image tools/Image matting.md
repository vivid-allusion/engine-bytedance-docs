---
title: "Image matting"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-matting"
---

The AI MediaKit Image matting tool can precisely identify the subject in an image (such as a person, product, or object), automatically remove the background, and generate an image with a transparent background. It is suitable for a variety of scenarios such as creating e\-commerce main images, changing the background of ID photos, and compositing marketing posters.

This development guide will walk you through:

* Quickly removing an image background with a single API call.

* Understanding the differences and effects of general, human, product, and other matting scenarios.

* Learning how to use advanced features such as contouring and auto\-cropping to add visual effects to the subject.

## Demo

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d733059d40dd4fd78d2e259847802e6b~tplv-goo7wpa0wc-image.image)

## Quick start: Remove an image background in one step

Image matting is a **synchronous task**: the request you initiate returns the processing result directly in the response, with no need for polling.

### Prerequisites

1. **Obtain access credentials**: Before you start, go to the [API Key management page](https://console.byteplus.com/imp/ai-mediakit/settings) in the AI MediaKit console to create and obtain an **AI MediaKit API Key** (used for authenticating media processing features).

2. **Prepare an image file**: Prepare an image to process and upload it to a publicly accessible server to obtain a URL that the API can call. Local upload and other input methods are also supported.

### Workflow

You only need to call the [Create an image matting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-matting-task) API to obtain the address of the matted image directly in the API response body.

#### Step 1: Submit the task and get the result

You can directly copy the following cURL command to remove the background of an image using the `general` scenario.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/remove-image-background' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/your_object_image.jpg",
  "scene": "general"
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > Replace `image_url` with your actual image address.

#### Step 2: View the response

Because this is a synchronous API, you receive a response containing the final result immediately after a successful request. You can obtain the download address of the matted image directly from the `result.image_url` field (the default output format is PNG, valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-remove-bg-xxxxxxxxxx",
    "request_id": "20240521183140xxxxxxxxxxxxxxxxxx",
    "result": {
        "image_url": "https://example.com/removed_bg_image.png?auth_key=...",
        "image_size": 45875,
        "image_format": "png",
        "image_width": 800,
        "image_height": 600
    }
}
```

## Reference

### Use cases

* **Bullet comments passing behind people**: In video applications such as streaming platforms, achieve an effect where bullet comments pass through people, preventing bullet comments from blocking the video subject and improving the viewing experience.

* **Background replacement**: In scenarios such as online meetings, live streaming, online image editing, or ID photo creation, automatically remove the background of a person or object and replace it with a custom background.

* **Asset generation**: Precisely separate the subject from an image, making it easy for you to use it to create new advertising or promotional assets.

### Usage limits

|Limit |Description |
|---|---|
|Input image limits |The URL of the image to process.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic`.<br><br>* File size: A single image cannot exceed 30 MB.<br><br>* Input image resolution:<br><br>   * When `scene` is `general`:<br><br>      * The long side of the input image cannot exceed 10240 px, and the short side cannot exceed 6000 px.<br><br>      * The total number of pixels of the input image (long side × short side) cannot exceed 40 MP.<br><br>   * When `scene` is `human` or `product`: The long side of the input image cannot exceed 7680 px, and the short side cannot exceed 4320 px. |

## Related APIs

* [Create an image matting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-matting-task)

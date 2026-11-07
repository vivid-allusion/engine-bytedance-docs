---
title: "Image inpainting"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-inpainting"
---

The AI MediaKit image erase and repair tool automatically detects and removes text or common icons from an image, and uses smart\-fill technology to repair the erased areas so that they blend naturally with the background. It is suitable for content cleaning, secondary creation from source materials, and AIGC content correction.

This guide walks you through:


* How to remove all text from an image with a single API call.

* How to use the different erase scenarios: erase specified text and erase icons.


<span id="result-example"></span>
## Demo

With the image erase and repair tool, you can achieve the following results:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9349e182cfa447439cc7c6c3b1917042~tplv-goo7wpa0wc-image.image) </span>

<span id="quickstart-remove-all-text-from-an-image"></span>
## Quickstart: Remove all text from an image

Image erase and repair is a **synchronous task**; the request you submit returns the processing result directly in the response, so no polling is required. The default erase scenario is **full\-screen text erasure**.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

2. **Prepare an image file**: Prepare an image with text, and make it accessible via a public HTTP/HTTPS URL by uploading it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

You only need to call the [Create an image inpainting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-inpainting-task) once to obtain the URL of the processed image directly in the API response body.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can copy the following cURL command to submit an erase task. This example passes no erase parameters, so the system performs **full\-screen text erasure** by default.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/with_watermark.jpg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the actual URL of your image.</div>



<span id="step-2-review-the-response"></span>
#### Step 2: Review the response

Because this is a synchronous API, you will receive a response containing the final result within a few seconds. You can obtain the download URL of the erased and repaired image directly from the `result.image_url` field (valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-erase-image-123456",
    "request_id": "20240520203000ABCDEFG12345",
    "expires_at": 1779183261,
    "result": {
        "image_url": "https://example.com/erased_image.webp?auth_key=...",
        "image_size": 51200,
        "image_format": "webp",
        "image_width": 1920,
        "image_height": 1080
    }
}
```


<span id="advanced-features"></span>
## Advanced features

You can control the erase target more precisely by setting the `standard_scene` parameter.

<span id="erase-icons"></span>
### Erase icons

If the targets you need to remove are icons (such as logos or channel logos), set the `standard_scene` parameter to `full_screen_icon_erase`.

<span id="example-erase-all-common-icons-from-an-image"></span>
#### Example: Erase all common icons from an image

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/with_logo.jpg",
  "standard_scene": "full_screen_icon_erase"
}'
```


<span id="erase-text"></span>
### Erase text

When you need to precisely erase certain specific text watermarks from an image, use the `standard_erase_text` parameter. This feature takes effect only when `standard_scene` is `full_screen_text_erase`.


* **Erase all text**: Use the default scenario (`full_screen_text_erase`) and do not provide the `standard_erase_text` parameter.

* **Erase specified text**: Use the default scenario and specify the text content to erase through the `standard_erase_text` parameter. The system precisely finds and erases the matching text.


<span id="example-erase-all-occurrences-of-internal-use-only-from-an-image"></span>
#### Example: Erase all occurrences of "Internal use only" from an image

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/confidential.jpg",
  "standard_scene": "full_screen_text_erase",
  "standard_erase_text": "Internal use only"
}'
```


<span id="erase-a-specified-area"></span>
### Erase a specified area

When the target you need to erase (such as a stray object or a passer\-by) is neither text nor an icon, or when you need to repair a precise area of an image, set the `standard_scene` parameter to `selected_area_erase`.

In this scenario, you define the erase area in the following two ways. You can use either one alone or both together (in which case the system erases the union of the two defined areas):


* **Coordinate box ** **`selected_area`**: Specifies the erase area by passing the normalized coordinates of a rectangular box. This is suitable for erasing regular rectangular areas. The coordinate system uses the top\-left corner of the image as the origin (0, 0) and the bottom\-right corner as (1, 1). You need to provide the coordinates of the rectangle's top\-left (`top_left_x`, `top_left_y`) and bottom\-right (`bottom_right_x`, `bottom_right_y`).

* **Mask image ** **`mask_url`**: Specifies an arbitrarily shaped erase area by providing the URL of a black\-and\-white mask image. This is more flexible and is suitable for erasing irregular objects.


You can think of the "mask image" as a stencil or template that guides the system through the erasure. It is a black\-and\-white image of the same size as the original:


* White areas: Correspond to the parts you want to erase from the original image.

* Black areas: Correspond to the parts you want to keep in the original image.


By drawing white areas of different shapes, you can erase irregular objects, which is more flexible than using a rectangular box.

<span id="example-1-erase-a-specified-area-with-a-coordinate-box"></span>
#### Example 1: Erase a specified area with a coordinate box

The following example erases a rectangular area in the upper\-left part of the image (10% to 50% horizontally and 10% to 40% vertically).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/with_area.png",
  "standard_scene": "selected_area_erase",
  "selected_area": {
    "top_left_x": 0.1,
    "top_left_y": 0.1,
    "bottom_right_x": 0.5,
    "bottom_right_y": 0.4
  }
}'
```


<span id="example-2-erase-an-irregular-area-with-a-mask-image"></span>
#### Example 2: Erase an irregular area with a mask image

The following example specifies the erase area by providing a mask image URL in the `mask_url` parameter. The white parts of the mask image are the areas to erase, and the mask image must have the same resolution as the input image.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/with_area.png",
  "standard_scene": "selected_area_erase",
  "mask_url": "https://example.com/mask.png"
}'
```


<span id="reference"></span>
## Reference

<span id="use-cases"></span>
### Use cases


* **Content cleaning and distribution**: Before content distribution, automatically remove other platforms' logos, watermarks, or promotional text from images to protect copyright or meet channel requirements.

* **Repurposing source materials**: When designing posters or video covers, erase redundant elements (such as passers\-by or stray objects) from the source material to obtain a clean background.

* **AIGC content correction**: When an AIGC\-generated image contains unexpected text or objects (when negative prompts fail to work), use this feature for high\-quality, trace\-free erasure.

* **Product image processing**: Erase cluttered objects from the background of product images, or remove temporary marks on models, to make product images more professional and attractive.


<span id="limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input image limits |* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Input image resolution:<br><br>   * Must not be smaller than 10x10 pixels.<br><br>   * Must not exceed 2560x1440 pixels (width × height).<br><br>* File size: Each image must not exceed 10 MB.<br><br>* Supported formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic` are supported. |


<span id="related-api-documentation"></span>
## Related APIs


* [Create an image inpainting task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-inpainting-task)

---
title: "Basic image editing"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-basic-image-editing"
---

To programmatically perform basic image edits, you can use the synchronous APIs from AI MediaKit. This guide provides quickstart examples for a variety of tools, including spatial transformations like rotation and flipping, and visual adjustments such as sharpening, blurring, and color correction. By following the cURL examples, you can quickly integrate these features and receive the processed image directly in the API response.

<span id="tool-overview"></span>
## Tool overview

AI MediaKit provides a series of synchronous basic image\-editing APIs. After you call one, the processing result is returned in the response body.


|Tool name |API |Description |
|---|---|---|
|Rounded corners |[Create a rounded corner task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task) |Adds circular or elliptical rounded corners to the four corners of an image. |
|Image rotation |[Create an image rotation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-rotation-task) |Rotates an image counterclockwise by a specified angle, with a configurable fill color for the blank areas. |
|Image flip |[Create an image flip task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-flip-task) |Flips an image horizontally (left\-right mirror) or vertically (top\-bottom flip). |
|Image sharpening |[Create an image sharpening task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-sharpening-task) |Enhances the edge details and overall clarity of an image, with three intensity levels available. |
|Image gaussian blur |[Create an image gaussian blur task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-gaussian-blur-task) |Applies a Gaussian blur to an image, with customizable blur intensity. |
|Image pixelation  |[Create an image pixelation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task) |Applies a pixelation effect to an entire image or a specified rectangular region, and allows you to customize the shape and size of the pixel cells. |
|Add text or an image watermark |[Create a text and image watermark task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task) |Adds a text or image watermark to an image, supporting nine\-grid positioning, tiling, opacity, and various other custom settings. |
|Image color adjustment |[Create an image color adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-color-adjustment-task) |Adjusts the brightness, contrast, and saturation of an image, offering effects such as brighten/darken, increase/decrease contrast, and increase/decrease saturation. |
|Image resizing |[Create an image resize task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task) |Enlarges or reduces an image by a specified size or scaling ratio, supporting multiple scaling modes. |
|Image negative |[Create an image negative task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task) |Inverts the colors of an image to generate a film\-negative\-style artistic effect with one click. |
|Image cropping |[Create an image cropping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-cropping-task) |Crops an input image in multiple modes, including directional cropping, origin cropping, custom cropping, and inscribed\-circle cropping. |
|Image compression |[Create an image compression task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-compression-task) |Provides a one\-stop image size optimization solution, supporting specified compression quality, file size limits, output format conversion, and more. |


<span id="prerequisites"></span>
## Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

* **Prepare an image file**: Have an image ready for processing, accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the image to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="round-corner"></span>
## Rounded corners

The rounded corner tool adds circular or elliptical rounded corners to the four corners of an image, suitable for scenarios such as avatars, cards, and e\-commerce main images.

<span id="effect-preview"></span>
### Demo


|Type |Effect |
|---|---|
|Circular corners |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/722aadf7295b4af9a8bc6a9ed91a210e) </span> |
|Elliptical corners |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0e1dc8e8773540e8a932565d8db68285) </span> |


<span id="quickstart-add-circular-corners-with-a-50px-radius-to-an-image"></span>
### Quickstart: Add circular corners with a 50px radius to an image

You need to call the [Create a rounded corner task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/round-corner-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.png",
  "corner_type": "circle",
  "circle_radius": 50,
  "output_format": "png"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the rounded image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-round-corner-image-12345",
    "result": {
        "image_url": "https://example.byteplus.com/rounded_output.png?auth_key=...",
        "image_size": 98765,
        "image_format": "png",
        "image_width": 800,
        "image_height": 600
    },
    "request_id": "20240521..."
}
```


<span id="image-rotation"></span>
## Image rotation

The image rotation tool rotates an image counterclockwise by a specified angle and supports setting a fill color for the blank areas, suitable for correcting image orientation or creative editing.

<span id="effect-preview"></span>
### Demo


|Original |Rotated 180 degrees |Rotated 60 degrees, with irregular areas filled in white |
|---|---|---|
|<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f7921f0d3ed3dcea5c248d84bb23b55.jpeg) </span><br><br> |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0304ba5af54502b48030305e3b06a3e5.png) </span><br><br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fae9133967f64a19992b98ba0f3524db~tplv-goo7wpa0wc-image.image) </span> |


<span id="quickstart-rotate-an-image-90-degrees-counterclockwise-and-fill-the-blank-areas-in-white"></span>
### Quickstart: Rotate an image 90 degrees counterclockwise and fill the blank areas in white

You need to call the [Create an image rotation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-rotation-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/rotate-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "rotate_angle": 90,
  "fill_color": "White",
  "output_format": "png"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the rotated image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-rotate-image-12346",
    "result": {
        "image_url": "https://example.byteplus.com/rotated_output.png?auth_key=...",
        "image_size": 102480,
        "image_format": "png",
        "image_width": 600,
        "image_height": 800
    },
    "request_id": "20240521..."
}
```


<span id="image-flip"></span>
## Image flip

The image flip tool flips an image horizontally or vertically, suitable for scenarios such as image correction and creating mirrored images.

<span id="effect-preview"></span>
### Demo


|Original |Horizontal flip |Vertical flip |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12c6aaa942f944a4b511df7731507ecd) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/52ba6a4aa30745b3930d87b856ebdc95) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/134be674bb6e417aaa0ca1092030f925) </span> |


<span id="quickstart-flip-an-image-horizontally"></span>
### Quickstart: Flip an image horizontally

You need to call the [Create an image flip task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-flip-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/flip-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "flip_type": "horizontal",
  "output_format": "jpeg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">The following two flip modes are supported:</div>


   * <div data-tips="true" data-tips-type="default"><code>horizontal</code>: Horizontal flip (mirrored left to right).</div>


   * <div data-tips="true" data-tips-type="default"><code>vertical</code>: Vertical flip (mirrored top to bottom).</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the flipped image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-flip-image-12347",
    "result": {
        "image_url": "https://example.byteplus.com/flipped_output.jpeg?auth_key=...",
        "image_size": 85432,
        "image_format": "jpeg",
        "image_width": 800,
        "image_height": 600
    },
    "request_id": "20240521..."
}
```


<span id="image-sharpening"></span>
## Image sharpening

This feature enhances the clarity of an image, making details more prominent.

<span id="effect-preview"></span>
### Demo


|Original |Medium sharpening |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12c6aaa942f944a4b511df7731507ecd) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0e9629d3cb6f4339b8aa3679e5936a3d) </span> |


<span id="quickstart-apply-medium-intensity-sharpening-to-an-image"></span>
### Quickstart: Apply medium\-intensity sharpening to an image

You need to call the [Create an image sharpening task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-sharpening-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/sharpen-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "sharpen_level": "medium",
  "output_format": "jpeg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Control the sharpening intensity through the <code>sharpen_level</code> parameter:</div>


   * <div data-tips="true" data-tips-type="default"><code>low</code>: Light sharpening (default)</div>


   * <div data-tips="true" data-tips-type="default"><code>medium</code>: Medium sharpening</div>


   * <div data-tips="true" data-tips-type="default"><code>high</code>: Heavy sharpening</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the sharpened image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-sharpen-image-12348",
    "result": {
        "image_url": "https://example.byteplus.com/sharpened_output.jpeg?auth_key=...",
        "image_size": 95123,
        "image_format": "jpeg",
        "image_width": 800,
        "image_height": 600
    },
    "request_id": "20240521..."
}
```


<span id="image-gaussian-blur"></span>
## Image Gaussian blur

This feature applies a Gaussian blur effect to an entire image, often used for background defocus or information de\-emphasis.

<span id="effect-preview"></span>
### Demo


|Original |Light blur |Medium blur |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12c6aaa942f944a4b511df7731507ecd) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2add69e0413a4fdca8a8d8bbbaeefdbb) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e73c3761d503404e9d7ad21049e249db) </span> |


<span id="quickstart-apply-a-medium-intensity-gaussian-blur-to-an-image"></span>
### Quickstart: Apply a medium\-intensity Gaussian blur to an image

You need to call the [Create an image gaussian blur task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-gaussian-blur-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/gaussian-blur-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "blur_strength": 30,
  "output_format": "jpeg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Control the Gaussian blur intensity through the <code>blur_strength</code> parameter. The larger the value, the more pronounced the blur effect. Recommended reference values:</div>


   * <div data-tips="true" data-tips-type="default"><code>10</code>: Light blur</div>


   * <div data-tips="true" data-tips-type="default"><code>30</code>: Medium blur</div>


   * <div data-tips="true" data-tips-type="default"><code>100</code>: Heavy blur</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the blurred image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-gaussian-blur-image-12349",
    "result": {
        "image_url": "https://example.byteplus.com/blurred_output.jpeg?auth_key=...",
        "image_size": 79854,
        "image_format": "jpeg",
        "image_width": 800,
        "image_height": 600
    },
    "request_id": "20240521..."
}
```


<span id="94e869bb"></span>
## Image pixelation

This feature applies a pixelation effect to an entire image or a specified rectangular region, and customize the shape and size of the pixel cells.

<span id="868eddfe"></span>
### Quickstart: Apply a pixelation effect to a rectangular region at specified coordinates

You need to call the [Create an image pixelation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/mosaic-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/privacy_image.jpg",
  "mosaic_type": "specify-region",
  "mosaic_regions": [
    {
      "top_left_x": 100,
      "top_left_y": 150,
      "bottom_right_x": 300,
      "bottom_right_y": 250
    }
  ],
  "mosaic_shape": "rectangle",
  "mosaic_step_x": 16,
  "mosaic_step_y": 16,
  "output_format": "jpeg"
}'
```


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">说明</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Mosaic scope: Use <code>mosaic_type</code> to choose <code>full-image</code> (whole image) or <code>specify-region</code> (specified region).</div>


* <div data-tips="true" data-tips-type="default">Pixel\-cell shape: Use <code>mosaic_shape</code> to choose <code>circle</code> (circular) or <code>rectangle</code> (rectangular).</div>


* <div data-tips="true" data-tips-type="default">Granularity: Use <code>mosaic_step_x</code> and <code>mosaic_step_y</code> to control the width and height of the mosaic pixel cells. The larger the values, the coarser the granularity.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the mosaicked image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-mosaic-image-12350",
    "result": {
        "image_url": "https://example.byteplus.com/mosaicked_output.jpeg?auth_key=...",
        "image_size": 88765,
        "image_format": "jpeg",
        "image_width": 800,
        "image_height": 600
    },
    "request_id": "20240521..."
}
```


<span id="6ca51d00"></span>
## Add text or an image watermark

The add image watermark tool supports adding a text or image watermark at any position on an image. You can customize the watermark content, font, size, color, opacity, position, and offset, and it supports a tiled watermark mode, suitable for scenarios such as copyright protection, brand promotion, and preventing unauthorized use of content.

<span id="410a6f0a"></span>
### Quickstart: Add a semi\-transparent red text watermark to the bottom\-right corner of an image

You need to call the [Create a text and image watermark task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/background.jpg",
  "watermark_type": "text",
  "watermark_text": "© MyBrand",
  "watermark_text_font_size": 24,
  "watermark_text_color": "#FF0000",
  "watermark_text_opacity": 50,
  "watermark_position": "bottom_right",
  "watermark_position_offset_x": 20,
  "watermark_position_offset_y": 20
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Specify the watermark type through the <code>watermark_type</code> parameter, where <code>text</code> is a text watermark and <code>image</code> is an image watermark. For more parameters, see the API documentation.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the watermarked image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-image-watermark-1234567",
    "result": {
        "image_url": "https://example.byteplus.com/watermarked_output.jpeg?auth_key=1775271661-...",
        "image_size": 310450,
        "image_format": "jpeg",
        "image_width": 1920,
        "image_height": 1080
    },
    "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f"
}
```


<span id="image-mosaic"></span>
## Image color adjustment

This feature is used to adjust the visual style of an image, supporting enhancement or reduction of brightness, contrast, and saturation for optimizing image assets or artistic processing.

<span id="effect-preview"></span>
### Demo


|Original |Effect | |
|---|---|---|
|<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b9873c9ed614de09430b5b6646e1dc5~tplv-goo7wpa0wc-image.image" width="1000px" /></div><br><br><br><div style="text-align: center"><br></div><br> |**Brightness** | |
||Brighten |Darken |
||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cf66b4376254d7a99b65b764cb67d05~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de503fc5a1e1464098950a1ebd86d819~tplv-goo7wpa0wc-image.image) </span> |
||**Contrast** | |
||Increase contrast |Decrease contrast |
||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af9dc01f9f9b483d87e3ccc2e84eb6a9~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5937d8efefa47e7b3c6bbd514fc8239~tplv-goo7wpa0wc-image.image) </span> |
||**Saturation** | |
||Increase saturation |Decrease saturation |
||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31988ace0adb4adaa64bc952b1d3dab9~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb10532f061147ff8f9b57cffa5e3c28~tplv-goo7wpa0wc-image.image) </span> |


<span id="quickstart-increase-the-contrast-of-an-image"></span>
### Quickstart: Increase the contrast of an image

You need to call the [Create an image color adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-color-adjustment-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/adjust-image-color' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.png",
  "adjust_type": "increase_contrast",
  "output_format": "jpeg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Choose the adjustment type through the <code>adjust_type</code> parameter, for example <code>increase_brightness</code> (brighten) or <code>decrease_saturation</code> (decrease saturation).</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the adjusted image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tooladjust-image-color-1234567",
    "result": {
        "image_url": "https://example.byteplus.com/adjusted_output.jpeg?auth_key=1775271661-...",
        "image_size": 245310,
        "image_format": "jpeg",
        "image_width": 1280,
        "image_height": 720
    },
    "request_id": "02177840..."
}
```


<span id="image-resizing"></span>
## Image resize

This feature supports enlarging or reducing an image by a specified size or ratio, and can be applied to scenarios such as generating multi\-specification thumbnails and preprocessing sizes before content compliance checks.

<span id="c2940321"></span>
### Scaling mode descriptions

When you specify both `resize_long` and `resize_short`, the `resize_mode` parameter controls how the image is scaled to the target `resize_long` × `resize_short` rectangle. All examples below use a 500×300 source image (aspect ratio 5:3) and a target rectangle of 350×240.


|Scaling mode |Description |Example |
|---|---|---|
|`exact` |**Forced scaling.**  Scales the image precisely to the target dimensions. The original aspect ratio is not preserved, so the image may be stretched or compressed and appear distorted. |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/28b178a89ffe48898d5aef9c812dd68d) </span><br><br>The 500×300 source is forced to 350×240. Because the width and height are scaled by different factors, the image is distorted (the circle becomes an ellipse). |
|`contain` (default) |**Proportional scaling, fully contained.**  Scales the image proportionally so that it fits entirely within the target rectangle. Neither the width nor the height of the result exceeds the target values, so one side may end up smaller than the rectangle. |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dd4cdccca98a40679900862392d16a6d) </span><br><br>Scaled by 0.70× so the long edge matches 350. The result is 350×210, fully contained within the 350×240 rectangle with no cropping. |
|`cover` |**Proportional scaling, crop to fill.**  Scales the image proportionally so that it fully fills the target rectangle, then crops any overflow from the center. The final image is exactly the target size. |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/33a4db1bbd304dcc89fd4b81a264d04f) </span><br><br>Scaled by 0.80× to 400×240 so it fully covers the rectangle, then the 50px horizontal overflow is center\-cropped. The final image is 350×240. |


<span id="f3ef1254"></span>
### Quickstart: Scale an image proportionally to a width of 200px

You need to call the [Create an image resize task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task) API. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/resize-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "width": 200
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Scaling is supported through the <code>width</code>, <code>height</code>, or <code>scale</code> parameters. If only the width or only the height is specified, proportional scaling is applied by default.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the resized image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-scale-image-12345",
    "result": {
        "image_url": "https://example.byteplus.com/scaled_output.jpeg?auth_key=...",
        "image_size": 25432,
        "image_format": "jpeg",
        "image_width": 200,
        "image_height": 150
    },
    "request_id": "20240521..."
}
```


<span id="image-negative"></span>
## Image negative

The image negative tool inverts all the colors of an input image to generate a film\-negative\-style artistic effect with one click, suitable for scenarios such as creative visuals and repurposing content.

<span id="effect-preview"></span>
### Demo


|Original |Negative |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/12c6aaa942f944a4b511df7731507ecd) </span> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cfc7d936477a498b9ccf8dd0dc6a5eaf) </span> |


<span id="quickstart-generate-an-image-negative-effect-with-one-click"></span>
### Quickstart: Generate an image negative effect with one click

You need to call the [Create an image negative task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task) API. This feature does not require configuring complex parameters, so you can copy the following cURL command to submit the task directly.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/invert-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace {Your_API_Key} with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace image_url with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">You can also specify the output format (such as <code>webp</code>) through the optional <code>output_format</code> parameter.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the negative image from the `result.image_url` field (valid for 24 hours). Example response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-invert-image-1234567",
    "result": {
        "image_url": "https://example.byteplus.com/inverted_output.jpg?auth_key=1775271661-...",
        "image_size": 910234,
        "image_format": "jpeg",
        "image_width": 1920,
        "image_height": 1080
    },
    "request_id": "02177840...",
    "expires_at": 1775271661
}
```


<span id="140109dd"></span>
## Image cropping

The image cropping tool crops an input image in multiple modes, including directional cropping, origin cropping, custom cropping, and inscribed\-circle cropping, suitable for scenarios such as multi\-device size adaptation, subject retention, removing edges from product images, and specified\-region capture.

<span id="a1e06a5d"></span>
### Cropping mode descriptions

Through the `crop_mode` parameter, you can choose one of the following four cropping modes:

<span id="13560e6e"></span>
#### Directional cropping (`crop_mode: directional`)

Crops from a specific position of the image (such as center, top, bottom, etc.) based on the specified target width and height. This mode is often used to generate fixed\-size views while retaining the content in a specific direction.


* **How it works**: You need to provide the target width (`crop_width`) and height (`crop_height`) of the cropped image and specify a cropping position (`crop_position`). The system captures a region of the corresponding size from the original image, using that position as the reference.

* **Parameter descriptions**:

   * `crop_width` / `crop_height`: Define the size of the cropping region. If one of them is set to 0, the image is scaled adaptively according to the original aspect ratio.

   * `crop_position`: The reference position for cropping, as shown in the figure below. For example, choosing `up` prioritizes retaining the top content of the image. 

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/125b510dec0946c3bb30613c4fb02df3) </span>

* **Example**: The following examples are demonstrated based on an original image of 1024x684 pixels.



|Scenario |Request parameter settings |Demo |
|---|---|---|
|**Center crop to generate a square thumbnail:**  Crop the original image from the center region into a 600x600\-pixel square image. |* `"crop_position": "center"`<br><br>* `"crop_width": 600`<br><br>* `"crop_height": 600` |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9415763a7c814876a5236437a7efb2a2) </span> |
|**Top crop to retain top content:**  Crop a 600x300\-pixel rectangle starting from the top of the original image, often used to create banners or title images. |* `"crop_position": "up"`<br><br>* `"crop_width": 600`<br><br>* `"crop_height": 300` |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6365c41eb7564b2cbc0b54b3adaa34fe) </span><br><br> |
|**Right crop, specifying width only:**  Crop an image with a width of 600 pixels starting from the right of the original image, keeping the height unchanged. |* `"crop_position": "right"`<br><br>* `"crop_width": 600`<br><br>* `crop_height` is omitted or set to 0. |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/40915570500a4b599251106488b291a1) </span> |


<span id="af56c622"></span>
#### Origin cropping (`crop_mode: origin`)

This mode provides flexible control. You can first set an anchor point (one of the nine\-grid positions) on the image, then apply horizontal and vertical offsets based on that anchor, and finally capture a rectangular region of the specified width and height starting from the new, offset origin.


* **How it works**: Precisely define the cropping frame through the anchor point (`origin_gravity`), offsets (`origin_x`, `origin_y`), and target size (`crop_width`, `crop_height`). 

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/31d18eb7e2404812a306a3be07b8f4a1) </span>

* **Example**: The figure below demonstrates setting the cropping anchor at the top\-left corner (`northwest`), then offsetting 100px horizontally to the right and 200px vertically downward, and finally capturing a 600x400 px region from the new origin (100, 200). 

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e78f272bf90e4415938918ea670c36dc) </span>


<span id="a5a3090d"></span>
#### Custom cropping (`crop_mode: custom`)

Define a rectangle for cropping by directly specifying the coordinates of the top\-left and bottom\-right corners of the cropping region. The coordinate origin (0, 0) is the top\-left corner of the image.


* **How it works**: Use `custom_x1`, `custom_y1` to define the top\-left corner coordinates of the cropping frame, and use `custom_x2`, `custom_y2` to define the bottom\-right corner coordinates.

* **Example**: The figure below demonstrates capturing the rectangular region defined by the top\-left corner coordinates (100, 40) and the bottom\-right corner coordinates (400, 400). The cropped image size is 300x360 px. 

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4d55ab1a1bb14d9eb14bdeef990f164f) </span>


<span id="6fcaa775"></span>
#### Inscribed\-circle cropping (`crop_mode: circle`)

Automatically crops the image into the largest inscribed circle, centered on the image center with the shorter side as the diameter.


* **How it works**: In this mode, no other cropping parameters need to be configured. The system automatically calculates and crops out the largest inscribed circle.

* **Output format recommendation**: To ensure that the area outside the circle is transparent, it is recommended to set the output format (`output_format`) to `png` or `webp`. If the output is `jpeg`, the non\-circular area is filled with white by default.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/046a22cb8da04ab0b762953f995cb694) </span>


<span id="c8220e8f"></span>
### Quickstart: Custom\-crop a specified region of an image

You need to call the [Create an image cropping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-cropping-task) API. The following example demonstrates how to capture the rectangular region defined by the top\-left corner coordinates (100, 150) and the bottom\-right corner coordinates (400, 350). You can copy the following cURL command to submit the task.

```Plain Text
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/crop-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/source_image.jpg",
  "crop_mode": "custom",
  "custom_x1": 100,
  "custom_y1": 150,
  "custom_x2": 400,
  "custom_y2": 350,
  "output_format": "png"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Choose the cropping mode through the <code>crop_mode</code> parameter. The <code>custom</code> value used in the example means cropping based on the specified top\-left and bottom\-right corner coordinates.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the cropped image from the result.image_url field (valid for 24 hours). Example response:

```Plain Text
{
    "success": true,
    "task_id": "amk-tool-crop-image-1234567",
    "result": {
        "image_url": "https://example.byteplus.com/cropped_output.png?auth_key=...",
        "image_size": 188080,
        "image_format": "png",
        "image_width": 300,
        "image_height": 200
    },
    "request_id": "20240521..."
}
```


<span id="21fff8d3"></span>
## Image compression

The image compression tool provides a one\-stop image size optimization solution, supporting specified compression quality, file size limits, and output format conversion (such as WebP, AVIF, HEIC), suitable for scenarios such as optimizing image distribution and loading for websites and apps, and managing user\-uploaded images.

<span id="ed88a845"></span>
### Quickstart: Compress an image to WebP format

You need to call the [Create an image compression task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-compression-task) API. The following example demonstrates how to compress an image and convert it to WebP format while specifying a compression quality of 80. You can copy the following cURL command to submit the task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/compress-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/large_image.png",
  "output_format": "webp",
  "quality": 80
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">Specify the compression quality (1\-100) through the <code>quality</code> parameter, or specify the file size limit through the <code>max_size</code> parameter. When both are set, <code>max_size</code> takes precedence.</div>



Because this is a synchronous API, upon a successful request you receive a response containing the processing result directly. You can get the download URL of the compressed image from the result.image_url field (valid for 24 hours). Example response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-compress-image-1234567",
  "result": {
    "image_url": "https://example.byteplus.com/compressed_output.webp?auth_key=...",
    "image_size": 98765,
    "image_format": "webp",
    "image_width": 1920,
    "image_height": 1080
  },
  "request_id": "20240521..."
}
```


<span id="6e21123b"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits

All basic image\-editing tools follow the same unified input limits:


|Limit item |Description |
|---|---|
|Image source |Only publicly accessible HTTP/HTTPS URLs are supported. |
|File size |It is recommended that each image not exceed 35 MB. Files that are too large may cause processing timeouts or failures. |
|Input resolution |Both the width and height of the image must not exceed 10000 pixels. |
|Supported formats |Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp` are supported. Animated images are not supported. |

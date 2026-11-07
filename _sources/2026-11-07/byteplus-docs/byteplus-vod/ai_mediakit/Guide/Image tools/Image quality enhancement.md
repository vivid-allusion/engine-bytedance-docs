---
title: "Image quality enhancement"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-quality-enhancement"
---

The AI MediaKit image quality enhancement tool is built on deep learning and image content understanding. It intelligently selects and applies the appropriate algorithms to improve an image's resolution, clarity, and color quality with one click. It is suitable for a wide range of scenarios, including AIGC image post\-processing, old\-photo restoration, OCR preprocessing, and product image optimization.

This guide walks you through how to:


* Quickly turn a blurry image into a clear one with a single API call.

* Understand the effects and applicable scenarios for the standard, professional, and max (large\-model) enhancement versions.


<span id="effect-preview"></span>
## Demo


|**Before** |**After** | | |
|---|---|---|---|
| |**Standard** |**Professional** |**Max** |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bc317855cbb4a8cb770af3618394106~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 49.61<br><br>* Aesthetics: 49.68 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db1baca77e64cd1b270f288cbae9bb1~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 51.70 (+2)<br><br>* Aesthetics: 72.84 (+23) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac5b3515335842df8ceb22b33ad69e4d~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 70.02 (+20)<br><br>* Aesthetics: 78.27 (+28) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/172ffd9a42ce4c3abefd679d3ce0f39e~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 76.71 (+26)<br><br>* Aesthetics: 77.28 (+28) |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69d17cd2c2e44222b2719a2ae23409c0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 47.29<br><br>* Aesthetics: 51.73 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2d48006d6194873a3b67332717dd51b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 49.52 (+2.23)<br><br>* Aesthetics: 67.15 (+15.42) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d13a59f8c064405f9bf976fc3b99e734~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 72.33 (+25.04)<br><br>* Aesthetics: 77.20 (+25.47) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16beb141c1b340e89906019045729e52~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 74.99 (+27.70)<br><br>* Aesthetics: 83.36 (+31.63) |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1257258a4f774af59baaf8d708ea2370~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 48.43<br><br>* Aesthetics: 63.81 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0580bfab5bc4c8dbe3ee522157a731a~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 58.26 (+9.83)<br><br>* Aesthetics: 74.38 (+10.57) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ae00042d7bd4a178bfd86c8185c82b1~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 72.11 (+23.68)<br><br>* Aesthetics: 79.80 (+15.99) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6326f9eb962411bb0f01878b4447873~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Clarity: 75.22 (+26.79)<br><br>* Aesthetics: 79.54 (+15.73) |


<span id="quickstart-improve-image-clarity-with-one-click"></span>
## Quickstart: Improve image clarity with one click

Image quality enhancement is a synchronous task: the request you submit returns the processing result directly in the response.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used for authenticating media processing features).

2. **Prepare an image file**: Prepare an image to enhance and upload it to a publicly accessible server or the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can access.


<span id="procedure"></span>
### Procedure

You only need to call the [Create an image quality enhancement task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task) API to obtain the URL of the enhanced image directly in the API response.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can copy the following cURL command, replace the parameters, and run it.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/enhance-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/blurry_image.jpg",
  "multiple": 2
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the URL of your own image.</div>


* <div data-tips="true" data-tips-type="default">In the example, <code>"multiple": 2</code> scales the image resolution up by 2x.</div>



<span id="step-2-view-the-response"></span>
#### Step 2: Check the response

Because this is a synchronous API, you receive a response containing the final result within a few seconds of a successful request. You can get the download URL of the enhanced image directly from the `result.image_url` field (valid for 24 hours).

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-image-1234567",
    "task_type": "enhance-image",
    "request_id": "20260415160000F6DE4C24A6A0D94B7FF2",
    "result": {
        "image_url": "https://example.byteplus.com/enhanced_output.jpg?auth_key=1775271661-...",
        "image_size": 875321,
        "image_format": "jpeg",
        "image_width": 2048,
        "image_height": 1536
    },
    "expires_at": 1778573984
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="model-versions"></span>
### Model versions

The image quality enhancement tool supports three versions—standard, professional, and max (large\-model)—which have different effects, applicable scenarios, and cost. You can select a version using the `tool_version` parameter.


|Feature |Standard |Professional |Max |
|---|---|---|---|
|Description |Balances processing speed, bitrate growth, and quality. Based on an analysis of quality issues, it intelligently selects which enhancement operators to use (super\-resolution, artifact removal, denoising, deblurring, sharpening, portrait enhancement, text enhancement, color enhancement, and more) to adaptively improve image clarity and texture. |Fine\-grained quality enhancement that adds natural texture detail while balancing fidelity, significantly improving the clarity and color quality of low\-quality images. |Based on a generative large model, it repairs image quality and generates natural texture detail while trying to preserve global structure and semantic consistency. For low\-quality images, it can significantly improve detail richness and clarity. |
|Applicable scenarios |Suitable for quality improvement in image distribution scenarios such as OCR / large\-model reference image preprocessing, UGC illustrations, and video thumbnails. |Suitable for quality improvement in high\-resolution, large\-image production scenarios such as fixing flaws in AIGC\-generated images, restoring old photos, product images, portrait photography, and print posters. |Suitable for quality improvement in scenarios such as fixing flaws in AIGC\-generated images and restoring lower\-quality images (for example, old photos and low\-resolution images). |
|Input resolution range |* 16 px ⩽ short side ≤ 1440 px<br><br>* 16 px ⩽ long side ≤ 2160 px |* short side ⩾ 256 px<br><br>* long side ⩽ 2048 px |* short side ⩾ 64 px<br><br>* long side ⩽ 6240 px |
|Output resolution range |* short side ⩽ 6144 px<br><br>* long side ⩽ 6144 px |long side ⩽ 10240 px |long side ⩽ 10240 px |
|Magnification |1–8x |1–30x |1–30x |
|Cost |Contact your account manager for pricing. |Contact your account manager for pricing. |Contact your account manager for pricing. |


<span id="configure-the-output-resolution"></span>
### Configure the output resolution

You can control the resolution of the output image using the `multiple`, `target_width`, and `target_height` parameters. If they are set together, the API processes them in the priority order of `multiple` \> (`target_width`, `target_height`). If none are set, the image is enhanced at 2x by default.


|Method |Parameter |Description |
|---|---|---|
|Scale by factor |`multiple` |Specifies the magnification of the output image relative to the original. For example, 2.0 means both width and height are enlarged 2x.<br><br><br>* Standard: value range [1, 8].<br><br>* Professional/Max: value range [1, 30]. |
|Specify output dimensions |* `target_width`<br><br>* `target_height` |Specifies the target width or height of the output image, in pixels.<br><br><br>* Standard: value range [original width or height, 6144], and the final magnification cannot exceed 8x.<br><br>* Professional / Max: value range [64, 10240].<br><br><br>When you specify the output dimensions using `target_width` or `target_height`, the final result considers both the target dimensions you set and the original aspect ratio, following these principles:<br><br><br>* **Specifying only one side (width or height)** : The system scales the specified side to the target value while preserving the original aspect ratio, and scales the other side proportionally.<br><br>* **Specifying both width and height**: If the target aspect ratio differs from the original, the system scales to the largest size that fits entirely within the target bounding box while preserving the original aspect ratio. For example, for a 100x100 (1:1) image with a target size of 400x300 (4:3), the system outputs a 300x300 image to preserve the original 1:1 ratio.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div><br><br><br><div data-tips="true" data-tips-type="default">For the max version, we recommend keeping the target output resolution within 8000x8000 to avoid timeouts caused by long processing times when handling very high\-resolution images.</div><br> |


<span id="example-1-scale-an-image-up-by-2-5x"></span>
#### Example 1: Scale an image up by 2.5x

```JSON
{
  "image_url": "https://example.com/source.jpg",
  "multiple": 2.5
}
```


<span id="example-2-set-the-image-width-to-1920px-and-scale-the-height-proportionally"></span>
#### Example 2: Set the image width to 1920px and scale the height proportionally

```JSON
{
  "image_url": "https://example.com/source.jpg",
  "target_width": 1920
}
```


<span id="choose-a-generative-enhancement-strategy-fidelity-first-vs-generative-first"></span>
### Choose a generative enhancement strategy: fidelity\-first vs. generative\-first

When you use the Professional or Max version, you can set the `generative_enhance_mode` parameter to guide how the model balances "staying faithful to the original" against "creative restoration".


|Mode |fidelity_first |generative_first |
|---|---|---|
|Effect |This mode focuses more on preserving and enhancing the existing details of the image (such as facial features and original textures), minimizing changes to the original content. |This mode intelligently generates richer, more natural texture detail while preserving the original structure, achieving a superior subjective visual effect. |
|Applicable scenarios |Scenarios that require highly faithful detail restoration, such as portrait photography, product images, text screenshots, and ID photos. |Restoring severely compressed or blurry low\-quality images (such as old photos), or scenarios that require a high degree of clarity and detail. |


<span id="effect-preview"></span>
#### Demo


|Original |fidelity_first |generative_first |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e400198b193f41feb786a079e427eaf8~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a2d92f6a37d40e2ab1fcc8f27a3ee0f~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b18e91e6bd76455b974490b5815217c9~tplv-goo7wpa0wc-image.image) </span> |


<span id="example-use-fidelity-first-mode"></span>
#### Example: Use fidelity\-first mode

The following example demonstrates how to use fidelity\-first mode to process a portrait image.

```JSON
{
  "image_url": "https://example.com/portrait.jpg",
  "tool_version": "professional",
  "generative_enhance_mode": "fidelity_first",
  "multiple": 2
}
```


<span id="reference"></span>
## Reference

<span id="usage-limits"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input image limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: `.png`, `.jpg`, `.jpeg`, and `.webp`.<br><br>* **File size**: A single image must not exceed 10 MB.<br><br>* **Input resolution**: The supported input and output size ranges differ by `tool_version`.<br><br>   * `standard`: 16 px ⩽ short side ≤ 1440 px; 16 px ⩽ long side ≤ 2160 px<br><br>   * `professional`: short side ⩾ 256 px; long side ⩽ 2048 px<br><br>   * `max`: short side ⩾ 64 px; long side ⩽ 6240 px<br><br>* **Aspect ratio limit**: For the `max` version, the ratio of the image's long side to short side must not exceed 32. Exceeding this ratio causes the task to fail. |


<span id="related-api-references"></span>
## API references


* [Create an image quality enhancement task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task)

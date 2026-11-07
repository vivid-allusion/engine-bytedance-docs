---
title: "Image face blurring"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-face-blurring"
---

The AI MediaKit Image Face Blurring tool automatically detects all face regions in an image and applies a mosaic to the detected faces, enabling one\-click facial privacy protection. This tool is suitable for a variety of scenarios that require batch protection of facial privacy, such as social platform content moderation, street\-view or surveillance footage anonymization, news media asset processing, and AI training dataset anonymization.

This guide walks you through:


* A quickstart on masking all faces in an image with a single API call.

* How to fine\-tune the shape, strength, and detection sensitivity of the masking through parameters.


<span id="demo"></span>
## Demo


|Input image |Blurred result |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c79942b0dc1a4f3f9f291cf38db0f9d2~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6296e174acb4f6d9ff739f3a88e7730~tplv-goo7wpa0wc-image.image) </span> |


<span id="quickstart-apply-a-mosaic-to-faces"></span>
## Quickstart: Apply a mosaic to faces

Image face blurring is a **synchronous task**; the request you submit returns the processing result directly in the response.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

* **Prepare an image file**: Have an image ready for processing. Make it accessible via a public HTTP/HTTPS URL by uploading it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

You only need to call the [Create an image face blurring task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-face-blurring-task) API to get the URL of the masked image directly in the API response body.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can copy the following cURL command, replace the parameters, and run it.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/face-blur-image' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://vod-ai-test.bytepluses.com/demo/street.jpeg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with your own image URL.</div>



<span id="step-2-review-the-response"></span>
#### Step 2: Review the response

Because this is a synchronous API, you will receive a response containing the final result within a few seconds after a successful request. You can get the download URL of the masked image directly from the `result.image_url` field (valid for 24 hours).

```JSON
{
  "success": true,
  "task_id": "amk-tool-face-blur-image-123456789",
  "task_type": "face-blur-image",
  "request_id": "20260617202100EXAMPLE123456789",
  "result": {
    "image_url": "https://example-domain.com/path/to/blurred_image.webp?auth_key=...",
    "image_size": 111174,
    "image_format": "webp",
    "image_width": 2732,
    "image_height": 1534,
    "face_count": 4,
    "face_location": [
      {
        "top_left_x": 2017,
        "top_left_y": 637,
        "bottom_right_x": 2215,
        "bottom_right_y": 894,
        "confidence": 0.9995
      },
      {
        "top_left_x": 581,
        "top_left_y": 576,
        "bottom_right_x": 766,
        "bottom_right_y": 848,
        "confidence": 0.9993
      },
      {
        "top_left_x": 1299,
        "top_left_y": 604,
        "bottom_right_x": 1447,
        "bottom_right_y": 837,
        "confidence": 0.9962
      },
      {
        "top_left_x": 1761,
        "top_left_y": 669,
        "bottom_right_x": 2027,
        "bottom_right_y": 1045,
        "confidence": 0.9907
      }
    ]
  },
  "expires_at": 1781785262
}
```


<span id="advanced-usage"></span>
## Advanced usage

You can fine\-tune the masking effect by configuring different parameters in the request body.

<span id="control-the-masking-style"></span>
### Control the masking style

Use the `blur_shape` and `mosaic_step` parameters to adjust the shape and strength of the masking.


|Parameter |Description |
|---|---|
|`blur_shape` |The shape of the masked face region.<br><br><br>* `circle`: (Default) Circle.<br><br>* `rectangle`: Rectangle. |
|`mosaic_step` |The mosaic cell size, a positive integer in pixels. The larger the value, the coarser the mosaic and the stronger the anonymization. The recommended range is `[5, 100]`. Defaults to `12`. |


<span id="example-use-a-rectangular-high-strength-mosaic"></span>
#### **Example: Use a rectangular, high\-strength mosaic**

```JSON
{
  "image_url": "https://example.com/source.jpg",
  "blur_shape": "rectangle",
  "mosaic_step": 20
}
```


<span id="adjust-the-detection-sensitivity"></span>
### Adjust the detection sensitivity

Use the `face_detect_thresh` parameter to adjust the confidence threshold for face detection. The value range is `(0, 1)`.


* **Increase this value**: Detection becomes stricter, reducing false positives on non\-face regions, but may miss some low\-clarity or non\-frontal faces.

* **Decrease this value**: Detection becomes more lenient, identifying more blurry or occluded faces, but may increase false positives.


<span id="example-lower-the-detection-threshold-to-recall-more-blurry-faces"></span>
#### **Example: Lower the detection threshold to recall more blurry faces**

```JSON
{
  "image_url": "https://example.com/source.jpg",
  "face_detect_thresh": 0.8
}
```


<span id="reference"></span>
## Reference

<span id="performance-and-limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input image limits |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* File size: It is recommended that each image not exceed 35 MB. Files that are too large may cause processing to fail.<br><br>* Resolution limit: The product of the image's width and height must not exceed 400 million pixels.<br><br>* Supported formats: Common image formats such as `.png`, `.jpg`, `.jpeg`, `.webp`, and `.avif` are supported. Animated images are not supported. |

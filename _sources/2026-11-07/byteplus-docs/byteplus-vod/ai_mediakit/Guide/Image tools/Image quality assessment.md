---
title: "Image quality assessment"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-vqscore"
---

The AI MediaKit image quality assessment tool performs multi\-dimensional objective and subjective quality analysis and aesthetic scoring on an input image. It is suitable for media quality monitoring, low\-quality image screening, AIGC content moderation, recommendation\-system ranking, and training\-data cleaning.

This guide walks you through:


* How to obtain an image's quality scores with a single API call.

* The differences and applicable scenarios of the standard and professional assessment models.

* How to interpret the returned quality and aesthetic scores.

* How to specify assessment dimensions based on your needs for more flexible calls.


<span id="quickstart-obtain-image-quality-scores-in-one-call"></span>
## Quickstart: Obtain image quality scores in one call

Image quality assessment is a **synchronous task**; the request you submit returns the assessment result directly in the response.

<span id="prerequisites"></span>
### Prerequisites


* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

* **Prepare an image file**: Prepare an image to be assessed, and make it accessible via a public HTTP/HTTPS URL by uploading it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

You only need to call the [Create an image VQScore task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-vqscore-task) to obtain the assessment scores directly in the API response body.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can copy the following cURL command to submit a quality assessment task. This example uses the default **standard version** model to assess two dimensions: subjective quality (`vqscore`) and noise (`noise`).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/evaluate-image-quality' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/your_image.jpg",
  "tool_version": "standard",
  "standard_evaluate_items": [
    "vqscore",
    "noise"
  ]
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the actual URL of your image.</div>



<span id="step-2-review-the-response-and-interpret-the-scores"></span>
#### Step 2: Review the response and interpret the scores

Because this is a synchronous API, you will immediately receive a response containing the final scores after a successful request. The `result` field is the assessment result.

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-image-quality-12345",
    "request_id": "021778401180935fdbd0ff1ce00652c087a",
    "result": {
        "tool_version": "standard",
        "vqscore": 85.5,
        "noise": 10.2
    }
}
```



* `vqscore`: A score of 85.5 indicates that the image's subjective quality is good.

* `noise`: A score of 10.2 indicates that the image's noise level is low and the image is clear.


<span id="advanced-usage"></span>
## Advanced usage

<span id="standard-versus-professional-version"></span>
### Standard versus professional version

Image quality assessment provides a standard version and a professional version, which you can choose through the `tool_version` parameter.


|Feature |Standard version (`standard`) |Professional version (`professional`) |
|---|---|---|
|Description |Provides 15 basic image quality assessment dimensions and supports flexible selection of some or all dimensions through the `standard_evaluate_items` parameter. |Performs assessment based on a large model and directly returns a fixed set of comprehensive scores (such as aesthetics, sharpness, and noise); it does not support custom assessment dimensions. This version delivers better comprehensive assessment results and is suitable for scenarios with high image\-quality requirements. |


<span id="specify-assessment-dimensions-standard-version-only"></span>
### Specify assessment dimensions (standard version only)

When you use the **standard version**, if you do not need the scores of all 15 dimensions, you can specify the assessment items you need through the `standard_evaluate_items` parameter. This reduces the response body size and keeps the results focused. If this parameter is omitted, the scores of four dimensions — `vqscore`, `noise`, `aesthetic`, and `blur` — are returned by default.

<span id="example-assess-only-contrast-and-brightness"></span>
#### Example: Assess only contrast and brightness

The following request returns only the scores of the `contrast` and `brightness` dimensions.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/evaluate-image-quality' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/your_image.jpg",
  "tool_version": "standard",
  "standard_evaluate_items": [
    "contrast",
    "brightness"
  ]
}'
```


**Response example:** 

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-image-quality-12347",
    "result": {
        "tool_version": "standard",
        "contrast": 85.2,
        "brightness": 128.5
    }
}
```


<span id="reference"></span>
## Reference

<span id="use-cases"></span>
### Use cases


* **AI\-generated image quality screening**: Automatically filter out low\-quality AI/AIGC images. For example, a platform might only allow images with an overall score above 70 to be uploaded.

* **Content moderation**: Automatically identify images that are blurry, noisy, or have compression artifacts to prevent low\-quality content from going live. For example, on an e\-commerce platform, if a product image uploaded by a user has a blur score below 60, it is automatically rejected and must be re\-uploaded.

* **Feedback for image enhancement tools**: In image enhancement tools such as Photoshop plug\-ins or online editing tools, if an image uploaded by a user has a low sharpness score, the tool can suggest deblurring or denoising.

* **AI model training\-data cleaning**: Before training a vision model, automatically remove low\-quality images to avoid affecting model performance. For example, filter out images with a sharpness score below 65 before training a face recognition model.

* **Gallery recommendations**: Automatically assess the quality of uploaded images to decide whether to recommend them to the home page. For example, images with an aesthetic score below 70 do not enter the "editor's picks" feed.

* **Smart album categorization on mobile**: Automatically mark "blurry" or "noisy" photos and suggest that users delete or repair them, similar to the "cleanup suggestions" feature in a smartphone gallery.


<span id="limits"></span>
### Limits


|**Limit** |**Description** |
|---|---|
|Input image limits |* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* File size: Each image must not exceed 10 MB.<br><br>* Supported formats: `png`, `jpeg`, `webp`, and `heic` are supported.<br><br>* Input image resolution:<br><br>   * The short side must not exceed 4320 px.<br><br>   * The long side must not exceed 7680 px. |

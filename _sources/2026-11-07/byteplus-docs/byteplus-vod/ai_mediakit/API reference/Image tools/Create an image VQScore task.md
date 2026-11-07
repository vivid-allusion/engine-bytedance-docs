---
title: "Create an image VQScore task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-vqscore-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/evaluate-image-quality`

This API submits a synchronous task to assess image quality. It performs objective and subjective quality and aesthetic scoring on an input image, making it ideal for use cases like quality monitoring, low\-quality image screening, content moderation, recommendation ranking, and training\-data cleaning.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For complete application examples and usage instructions, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-vqscore">Image VQScore</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to assess.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* File size: Each image must not exceed 10 MB.<br><br>* Supported formats: `png`, `jpeg`, `webp`, and `heic` are supported.<br><br>* Input image resolution:<br><br>   * The short side must not exceed 4320 px.<br><br>   * The long side must not exceed 7680 px. |
|`tool_version` |String |No |`professional` |The model version to use for image quality assessment. Defaults to `standard`.<br><br><br>* `standard`: Standard version, provides 15 basic image quality assessment dimensions and supports flexible selection of some or all dimensions through the `standard_evaluate_items` parameter. This version strikes a good balance between cost and functional flexibility.<br><br>* `professional`: Professional version, performs assessment based on a large model and directly returns a fixed set of comprehensive scores (such as aesthetics, sharpness, and noise); it does not support custom assessment dimensions. This version delivers better comprehensive assessment results and is suitable for scenarios with high image\-quality requirements. |
|`standard_evaluate_items` |Array |No |`["vqscore", "noise"]` |Takes effect only when `tool_version` is `standard`. Specifies the standard\-version assessment dimensions to return. If empty, the four dimensions `vqscore`, `noise`, `aesthetic`, and `blur` are returned by default. The available assessment dimensions are:<br><br><br>* `vqscore`: The image's subjective quality; a higher value indicates better quality.<br><br>* `advcolor`: The image's overall color quality.<br><br>* `blockiness`: The severity of blockiness (mosaic) artifacts.<br><br>* `noise`: The image's noise level.<br><br>* `aesthetic`: A quality score based on popular aesthetics.<br><br>* `blur`: The degree of blurriness.<br><br>* `cg`: Indicates whether the scene is non\-natural (such as a game or screen recording).<br><br>* `contrast`: The image's contrast level.<br><br>* `texture`: The richness of texture.<br><br>* `brightness`: The average brightness.<br><br>* `overexposure`: The degree of overexposure.<br><br>* `hue`: The balance of hue.<br><br>* `saturation`: The balance of saturation.<br><br>* `green`: Green\-area or green\-screen detection.<br><br>* `cmartifacts`: Compression\-artifact detection. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

<span id="example-1-assessment-with-the-standard-version"></span>
### Example 1: Assessment with the standard version

The following request uses the standard\-version model to assess two dimensions: subjective quality (`vqscore`) and noise (`noise`).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/evaluate-image-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/image.jpg",
  "tool_version": "standard",
  "standard_evaluate_items": [
    "vqscore",
    "noise"
  ]
}'
```


<span id="example-2-assessment-with-the-professional-version"></span>
### Example 2: Assessment with the professional version

The following request uses the professional\-version large model to perform a comprehensive assessment of the image.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/evaluate-image-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/image_aigc.png",
  "tool_version": "professional"
}'
```


<span id="response"></span>
## Response

This is a synchronous API; the processing result is returned directly in the response body.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task succeeded.<br><br><br>* `true`: Success. Check the `result` field to get the task result.<br><br>* `false`: Failure. Check the `error` field for detailed error information. |
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see [The result object (when tool_version is standard)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-vqscore-task#the-result-object-when-tool-version-is-standard) and [The result object (when tool_version is professional)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-vqscore-task#the-result-object-when-tool-version-is-professional) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-vqscore-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="the-result-object-when-tool-version-is-standard"></span>
#### The result object (when `tool_version` is standard)


|Parameter |Type |Description |
|---|---|---|
|`tool_version` |String |The image quality assessment version, fixed as `standard`. |
|`vqscore` |Number |The image's subjective quality; a higher value indicates better quality. Range: [0, 100]. |
|`aesthetic` |Number |A quality score based on popular aesthetics; a higher value indicates greater aesthetic appeal. Range: [0, 100]. |
|`advcolor` |Number |The image's overall color quality; a higher value indicates higher color quality.<br><br><br>* [0, 50]: Poor color quality.<br><br>* [50, 60]: Medium color quality.<br><br>* [60, 100]: Good color quality. |
|`blockiness` |Number |The severity of the image's blockiness artifacts; a higher value indicates stronger blockiness.<br><br><br>* [0, 50]: Poor.<br><br>* [50, 60]: Medium.<br><br>* [60, 100]: Good.<br><br>* \-1: The assessed image is a non\-conventional image (such as a game or special\-effects image). |
|`blur` |Number |The blur score, i.e. whether the image is sharp. A higher score means the image is clearer and sharper. Range: [0, 100], supports two decimal places. |
|`brightness` |Number |The average brightness; a higher value indicates greater brightness. Range: [0, 255]. |
|`cg` |Number |Whether the scene is non\-natural. A value close to 0 indicates a natural scene; a value close to 100 indicates a non\-natural scene (game, screen recording, etc.). Range: [0, 100]. |
|`cmartifacts` |Number |The compression\-artifact level; a higher score indicates more significant compression artifacts and lower image quality. Range: [0, 100].<br><br><br>* [0, 30): No or slight compression artifacts.<br><br>* [30, 60): Compression artifacts are present.<br><br>* [60, 100]: Obvious artifacts are present. |
|`contrast` |Number |The contrast level; a lower value indicates lower contrast. Range: [0, 100]. |
|`green` |Number |The area of the image's green region; a larger value means a larger green region and a higher probability of a green screen. Range: [0, 255]. |
|`hue` |Number |The balance of hue; a higher value indicates more balanced hue. Range: [0, 100]. |
|`noise` |Number |The noise score, i.e. whether the image has graininess or random noise. A higher score means the image is cleaner. Range: [0, 100], supports two decimal places. |
|`overexposure` |Number |The area of overexposure; a higher value makes overexposure more likely. Range: [0, 100]. |
|`saturation` |Number |The balance of saturation; a higher value indicates more balanced saturation. Range: [0, 100]. |
|`texture` |Number |The richness of texture; a higher value indicates richer texture. Range: [0, 255]. |


<span id="the-result-object-when-tool-version-is-professional"></span>
#### The result object (when `tool_version` is professional)


|Parameter |Type |Description |
|---|---|---|
|`tool_version` |String |The image quality assessment version, fixed as `professional`. |
|`overall` |Number |The overall score combining the metrics above. A higher score indicates better image quality. Range: [0, 100], supports two decimal places. |
|`aesthetics` |Number |The aesthetics score. A higher score means the image "looks better", with more coordinated composition, colors, and style. Range: [0, 100], supports two decimal places. |
|`artifacts` |Number |The artifacts score, i.e. whether the image has compression, AI\-generation marks, distortion, etc. A higher score means fewer artifacts and a more natural image. Range: [0, 100], supports two decimal places. |
|`blur` |Number |The blur score, i.e. whether the image is sharp. A higher score means the image is clearer and sharper. Range: [0, 100], supports two decimal places. |
|`noise` |Number |The noise score, i.e. whether the image has graininess or random noise. A higher score means the image is cleaner. Range: [0, 100], supports two decimal places. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error. For example: `BadRequest`. |
|`message` |String |A detailed description of the error, useful for debugging. |
|`param` |String |(Optional) The specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="standard-version-response"></span>
#### Standard\-version response

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-image-quality-12345",
    "task_type": "evaluate-image-quality",
    "result": {
        "tool_version": "standard",
        "vqscore": 85.5,
        "noise": 10.2
    },
    "expires_at": 1778573984,
    "request_id": "021778401180935fdbd0ff1ce00652c087a"
}
```


<span id="professional-version-response"></span>
#### Professional\-version response

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-image-quality-12346",
    "task_type": "evaluate-image-quality",
    "result": {
        "tool_version": "professional",
        "overall": 92.15,
        "aesthetics": 95.50,
        "artifacts": 98.20,
        "blur": 88.60,
        "noise": 99.10
    },
    "expires_at": 1778573984,
    "request_id": "021778401180935fdbd0ff1ce00652c087b",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


<span id="failure-response"></span>
#### Failure response

```JSON
{
  "success": false,
  "task_type": "evaluate-image-quality",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'tool_version' must be one of [standard, professional].",
    "param": "tool_version",
    "type": "BadRequest"
  },
  "request_id": "20240521180000AABBCCDD112233",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

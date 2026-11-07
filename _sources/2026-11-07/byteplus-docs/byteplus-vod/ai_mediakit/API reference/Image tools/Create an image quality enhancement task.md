---
title: "Create an image quality enhancement task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/enhance-image`

To programmatically improve the quality of an image, you can call this API to submit a synchronous enhancement task. The service uses intelligent content analysis to comprehensively boost resolution, clarity, and color performance.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a detailed description of this feature, its use cases, and more, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-quality-enhancement">Image quality enhancement</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be enhanced.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Input resolution**: The supported input and output size ranges differ by `tool_version`. For details, see the Model versions and Usage limits sections of the [Image quality enhancement](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-quality-enhancement) guide.<br><br>* **Aspect ratio limit**: For the max version (`tool_version` = `max`), the ratio of the input image's long side to short side must not exceed 32.<br><br>* **File size**: A single image must not exceed 10 MB.<br><br>* **Supported formats**: Common mainstream image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. |
|`tool_version` |String |No |`professional` |The model version used for enhancement. Versions differ in effect, processing range, and price.<br><br><br>* `standard`: (default) Standard version. Balances processing speed, bitrate growth, and quality.<br><br>* `professional`: Professional version. Fine\-grained quality enhancement that adds natural texture detail while balancing fidelity, significantly improving the clarity and color performance of low\-quality images.<br><br>* `max`: Max version. Based on a generative large model, it repairs image quality and generates natural texture detail while trying to preserve global structure and semantic consistency. For low\-quality images, it can significantly improve detail richness and clarity.<br><br><br>For more on each version, including effect comparisons, applicable scenarios, and resolution limits, see the Model versions and Usage limits sections of the [Image quality enhancement](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-quality-enhancement) guide. |
|`multiple` |Number |No |`2.5` |The magnification of the processed image relative to the original, supporting up to 2 decimal places.<br><br><br>* Standard version (`tool_version` = `standard`): value range [1, 8].<br><br>* Professional version (`tool_version` = `professional`): value range [1, 30].<br><br>* Max version (`tool_version` = `max`): value range [1, 30].<br><br><br>The final width and height of the generated image cannot exceed the maximum resolution supported by the selected model version. |
|`target_width` |Integer |No |`1920` |The target width of the processed image, in px.<br><br><br>* Standard version (`tool_version` = `standard`): value range [original width, 6144], and the final magnification cannot exceed 8x.<br><br>* Professional version (`tool_version` = `professional`): value range [64, 10240].<br><br>* Max version (`tool_version` = `max`): value range [64, 10240].<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><code>target_height</code> is typically used together with <code>target_width</code>, or used on its own to preserve the original aspect ratio.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For the max version, we recommend keeping the target output resolution (target_width, target_height) within 8000x8000 to avoid timeouts when processing very high\-resolution images.</div><br> |
|`target_height` |Integer |No |`1080` |The target height of the processed image, in px.<br><br><br>* Standard version (`tool_version` = `standard`): value range [original height, 6144], and the final magnification cannot exceed 8x.<br><br>* Professional version (`tool_version` = `professional`): value range [64, 10240].<br><br>* Max version (`tool_version` = `max`): value range [64, 10240].<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div><br><br><br><div data-tips="true" data-tips-type="default"><code>target_height</code> is typically used together with <code>target_width</code>, or used on its own to preserve the original aspect ratio.</div><br> |
|`enable_correct_color` |Boolean |No |`true` |Whether to enable color correction. This takes effect only when `tool_version` is `max`. Values:<br><br><br>* `true`: (default) Enable color correction. The system tries to keep the colors of the enhanced image consistent with the original.<br><br>* `false`: Disable color correction. If you notice over\-sharpening after enabling color correction, we recommend disabling it. |
|`generative_enhance_mode` |String |No |`generative_first` |The generative enhancement strategy, used to control how the model balances "staying faithful to the original" against "creative restoration". This parameter takes effect only when `tool_version` is `professional` or `max`. Supported values:<br><br><br>* `fidelity_first`: Fidelity\-first. In this mode, the model focuses more on preserving and enhancing the existing details of the image (such as facial features and original textures), minimizing changes to the original content. Applicable scenarios: when you need highly faithful detail restoration, such as portraits, product images, and text screenshots.<br><br>* `generative_first`: (default) Generative\-first. In this mode, the model intelligently generates richer, more natural texture detail while preserving the original structure, achieving an optimal subjective visual effect. Applicable scenarios: restoring severely compressed or blurry low\-quality images, or when you want to significantly improve clarity and detail and can accept some detail re\-creation.<br><br><br>For an effect comparison of the two modes, see [Choose a generative enhancement strategy: fidelity-first vs. generative-first](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-quality-enhancement#choose-a-generative-enhancement-strategy-fidelity-first-vs-generative-first). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a "professional" image quality enhancement task for an image, with a magnification of 2x and JPEG output.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/enhance-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.jpg",
  "tool_version": "professional",
  "multiple": 2
}'
```


<span id="response"></span>
## Response

This is a synchronous API, and the processing result is returned directly in the response body.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Whether the task succeeded.<br><br><br>* `true`: Success. See the `result` field for the task result.<br><br>* `false`: Failure. See the `error` field for detailed error information. |
|`result` |Object |The object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL of the enhanced image file. This URL is valid for **24 hours**, so be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image.<br><br><br>* When the request parameter `tool_version` is `standard` (standard version), the output format is fixed as png.<br><br>* When the request parameter `tool_version` is `professional` (professional version) or `max` (max version), the output format matches the format of the input image. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro category of the error. For example, BadRequest. |
|`message` |String |A detailed description of the error, useful for development and debugging. |


<span id="response-example"></span>
### Response example

Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-image-1234567",
    "task_type": "enhance-image",
    "result": {
        "image_format": "png",
        "image_height": 3264,
        "image_size": 7346551,
        "image_url": "https://example.byteplus.com/enhanced_output.png?auth_key=1775271661-...",
        "image_width": 4896
    },
    "expires_at": 1778573984,
    "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure

```JSON
{
  "success": false,
  "task_id": "amk-tool-enhance-image-5225472",
  "task_type": "enhance-image",
  "error": {
   "code": "AbilityError",
    "type": "InternalServerError",
    "message": "error type: BadRequest, code: AbilityProcessingError, param: , message: Invalid parameter. detail error info: errcode 800012, fail to validate param, super resolution multiple ratio should be between 0 and 8"
   },
  "request_id": "20260512161933F7F3274AA07554196387",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

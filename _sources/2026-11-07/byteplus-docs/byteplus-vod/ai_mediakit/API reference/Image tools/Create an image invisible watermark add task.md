---
title: "Create an image invisible watermark add task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-invisible-watermark`

To protect your image assets, you can use this API to submit a synchronous task that adds an invisible watermark to an image. It hides a custom text message in an image without noticeably affecting its integrity or quality, making it ideal for copyright protection, AIGC image compliance, distribution tracking, and content\-theft evidence collection. You must explicitly specify the invisible watermark model version and use the same version for later extraction.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-invisible-watermark">Image invisible watermark</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source_image.jpg` |The URL of the image to which an invisible watermark will be added.<br><br><br>* **Image source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Common mainstream image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp` are supported. |
|`tool_version` |String |Yes |`adapt` |The invisible watermark model version. Supported values:<br><br><br>* `adapt`: A text\-embedding model for AIGC scenarios. This model strikes a good balance between image\-quality impact and robustness, and can resist attacks such as a certain degree of resolution scaling, cropping, and compression. It is recommended when adding invisible watermarks to AIGC\-generated color images.<br><br>* `adapt_resize`: A text\-embedding model for content\-theft evidence collection. This model resists image scaling and compression attacks more effectively, and is suitable for evidence collection in large\-scale image theft.<br><br><br>Note: Be sure to record this value, because you must use the same version when you later call the [Create an image invisible watermark extraction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task). |
|`watermark_content` |String |Yes |`my-copyright-info` |The custom invisible watermark text content, up to 128 characters. If the content consists entirely of Chinese characters, it is recommended not to exceed 42 characters. |
|`strength_level` |String |No |`medium` |The invisible watermark strength. The higher the strength, the stronger the resistance to attacks (processing such as scaling, compression, and transcoding), but the greater the potential impact on the original image.<br><br><br>* `low`: Low strength, suitable for solid\-color images and scenarios with high image\-quality requirements.<br><br>* `medium`: (Default) Medium strength, balances image quality and attack resistance and is suitable for most scenarios.<br><br>* `strong`: High strength, suitable for images with rich texture, with the strongest attack resistance. |
|`output_format` |String |No |`png` |The output image format. Defaults to `png`. Supports `png`, `jpeg`, and `webp`. |
|`output_quality` |Integer |No |`90` |The output image quality parameter, in the range `[75, 100]`; a lower value means a higher compression rate and lower image quality. Defaults to `90`. It is recommended to set this parameter based on the model version (`tool_version`) and output format (`output_format`):<br><br><br>* When the model version is `adapt`:<br><br>   * For `png` output: It is recommended to use `output_quality` ≥ 75.<br><br>   * For `jpeg` output: It is recommended to use `output_quality` ≥ 78.<br><br>   * For `webp` output: It is recommended to use `output_quality` ≥ 90.<br><br>* When the model version is `adapt_resize`: It is recommended to use `output_quality` ≥ 75. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example adds an `adapt` invisible watermark to an image and writes the text `my-copyright-info`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/source_image.jpg",
  "tool_version": "adapt",
  "watermark_content": "my-copyright-info"
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task#the-result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |


<span id="the-result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL of the image after the invisible watermark was added, valid for 24 hours; be sure to save it promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


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

Success response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-add-image-invisible-watermark-1703200",
    "task_type": "add-image-invisible-watermark",
    "result": {
        "image_url": "https://example.com/watermarked_output.png?auth_key=...",
        "image_size": 875321,
        "image_format": "png",
        "image_width": 2048,
        "image_height": 1536
    },
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF2",
    "expires_at": 1778573984
}
```


Failure response:

```JSON
{
  "success": false,
  "task_type": "add-image-invisible-watermark",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'watermark_content' is required and cannot be empty.",
    "param": "watermark_content",
    "type": "BadRequest"
  },
  "request_id": "20240521184200AABBCCDDEEFF445566"
}
```

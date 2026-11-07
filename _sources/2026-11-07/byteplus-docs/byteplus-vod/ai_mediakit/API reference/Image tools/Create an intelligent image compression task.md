---
title: "Create an intelligent image compression task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-intelligent-image-compression-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/slim-image`

To programmatically reduce image size while improving visual quality, you can call this synchronous API for intelligent image compression. It uses AI technology to substantially reduce file size, repair issues like jaggies and color noise, and enhance texture details, resulting in a lighter and clearer image.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a detailed description and application of this feature, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-intelligent-image-compression">Intelligent image compression</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 50 MB.<br><br>* **Supported formats**: `jpeg`, `jpg`, `png`, `heic`, `avif`, `webp`. Animated images are not supported.<br><br>* **Resolution limits**:<br><br>   * Neither the width nor the height of the input image may exceed 10000 pixels.<br><br>   * When the input image format is `avif`, it is recommended that the product of the input image's width and height not exceed 100,000; otherwise, the task may fail. |
|`output_format` |String |No |`webp` |The format of the output image. Defaults to `original`.<br><br><br>* `original`: Keeps the same format as the source image.<br><br>* `png`<br><br>* `jpeg`<br><br>* `webp`<br><br><br>**About JPEG compression**: Image compression usually reduces file size. However, when both the input and output formats are JPEG, for some already highly compressed source files, the processed size may show no noticeable change and, in a few cases, may even increase slightly. This behavior is normal and is related to the source image's compression parameters and the characteristics of JPEG re\-encoding. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to request intelligent image compression for an image and output it in WebP format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/slim-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/source_image.png",
  "output_format": "webp"
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
|`result` |Object |The object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-intelligent-image-compression-task#the-result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-intelligent-image-compression-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="the-result-object"></span>
#### The result object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`image_url` |String |The download URL for the resulting slimmed image. This URL is valid for **24 hours**, so be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, such as `webp`. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="the-error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general category of the error. For example, `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |


<span id="response-example"></span>
### Response example

Success:

```JSON
{
    "success": true,
    "task_id": "amk-tool-slim-image-12345678",
    "task_type": "slim-image",
    "result": {
        "image_url": "https://example.byteplus.com/slim_output.webp?auth_key=1775271661-...",
        "image_size": 85720,
        "image_format": "webp",
        "image_width": 1920,
        "image_height": 1080
    },
    "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
    "expires_at": 1775271661,
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure:

```JSON
{
  "success": false,
  "task_id": "amk-tool-slim-image-5225472",
  "task_type": "slim-image",
  "error": {
    "code": "InvalidParameter",
    "type": "BadRequest",
    "message": "The value of 'output_format' is not supported. Please use one of [original, png, jpeg, webp]."
  },
  "request_id": "20260512161933F7F3274AA07554196387",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

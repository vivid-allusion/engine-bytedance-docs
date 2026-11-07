---
title: "Create an image compression task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-compression-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/compress-image`

To optimize image size and format, you can use this API to submit a synchronous compression task. It provides a one\-stop solution supporting quality control, maximum file size limits, format conversion (to WebP, AVIF, HEIC), and lossy compression for PNG images. This API is ideal for managing file sizes before users upload images, preprocessing images for AIGC and multimodal models, and optimizing image distribution and loading for websites and apps.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a detailed description and application of this feature, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-image-editing">Basic image editing</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Mainstream image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. Only static images are supported.<br><br>* **Resolution limits**:<br><br>   * Neither the width nor the height of the input image may exceed 10000 pixels.<br><br>   * When the output format is `avif`, it is recommended that the input image resolution (width × height) not exceed 100,000 pixels; otherwise, the task may fail.<br><br>   * When the output format is `heic`, it is recommended that the input image resolution not exceed 4K (about 4096×4096 pixels); otherwise, the task may fail. |
|`output_format` |String |No |`webp` |The format of the output image. The following values are supported:<br><br><br>* `png`<br><br>* `jpeg`<br><br>* `webp`<br><br>* `avif`<br><br>* `heic`<br><br><br>Note: If this parameter is not provided, the format defaults to webp. To preserve the original format, explicitly pass the name of the original format. |
|`quality` |Integer |No |`75` |The compression quality, with a value range of [1, 100]. Defaults to `75`. The smaller the value, the higher the compression rate and the greater the loss of image quality.<br><br>Note: This parameter is ignored when `max_size` is set. |
|`max_size` |Integer |No |`204800` |The maximum output file size, in bytes. For example, `204800` means 200 KB. A recommended value is `10,485,760` bytes (10 MiB). After you set this parameter, the system automatically adjusts the compression parameters to meet this size limit as closely as possible, and the `quality` value you set manually is ignored.<br><br>Note: This takes effect only when `output_format` is `jpeg` or `webp`. |
|`png_lossy` |Boolean |No |`true` |Whether to enable lossy compression for PNG images to achieve a higher compression rate. Defaults to `false`.<br><br>Note: This takes effect only when `output_format` is `png`. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to compress an image and convert it to WebP format while specifying a compression quality of 80.

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


<span id="response"></span>
## Response

This is a synchronous API, and the processing result is returned directly in the response body.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Whether the task succeeded.<br><br><br>* `true`: Success. See the `result` field for the task result.<br><br>* `false`: Failure. See the `error` field for detailed error information. |
|`result` |Object |The object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-compression-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-compression-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL of the processed image file. This URL is valid for **24 hours**, so be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, such as `webp`. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general category of the error. For example, `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |


<span id="response-example"></span>
### Response example

Success:

```JSON
{
  "success": true,
  "task_id": "amk-tool-compress-image-1234567",
  "task_type": "compress-image",
  "result": {
    "image_url": "https://example.byteplus.com/compressed_output.webp?auth_key=1775271661-...",
    "image_size": 98765,
    "image_format": "webp",
    "image_width": 1920,
    "image_height": 1080
  },
  "expires_at": 1778573984,
  "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure:

```JSON
{
  "success":false,
  "task_id":"amk-tool-compress-image-940034677250",
  "task_type":"compress-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

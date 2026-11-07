---
title: "Create an image resize task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/resize-image`

Use this synchronous API to scale an input image for various scenarios, such as multi\-platform asset adaptation, cover and thumbnail generation, and batch image preprocessing. This API supports multiple resizing methods, including scaling to precise dimensions (width and height), resizing by the long or short edge, and several proportional scaling modes.

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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. Only static images are supported.<br><br>* **Resolution**: Both the width and height of the input image must not exceed 10,000 pixels. |
|`resize_long` |Integer |No |`800` |The target long\-edge size of the output image, in pixels.<br><br><br>* **Proportional scaling**: If only this parameter is set (or `resize_short` is set to 0), the image is scaled proportionally so that its long edge matches this value.<br><br>* **Combined use**: When set together with `resize_short`, the scaling behavior is determined by the `resize_mode` parameter.<br><br><br>At least one of this parameter and `resize_short` must be provided with a value greater than 0. |
|`resize_short` |Integer |No |`600` |The target short\-edge size of the output image, in pixels.<br><br><br>* **Proportional scaling**: If only this parameter is set (or `resize_long` is set to 0), the image is scaled proportionally so that its short edge matches this value.<br><br>* **Combined use**: When set together with `resize_long`, the scaling behavior is determined by the `resize_mode` parameter.<br><br><br>At least one of this parameter and `resize_long` must be provided with a value greater than 0. |
|`resize_mode` |String |No |`contain` |The scaling mode, used to define the scaling behavior when you specify both `resize_long` and `resize_short`. Defaults to `contain`.<br><br><br>* `exact`: **Forced scaling**. Scales the image precisely to the dimensions of `resize_long` x `resize_short`, which may cause the image to be stretched or compressed and distorted.<br><br>* `contain`: **Proportional scaling (fully contained)** . Scales the image while preserving the original aspect ratio, ensuring that the scaled image is fully contained within the `resize_long` x `resize_short` rectangle. The width and height of the final image will not exceed the specified values.<br><br>* `cover`: **Proportional scaling (crop to fill)** . Scales the image while preserving the original aspect ratio, ensuring that the scaled image fully fills the `resize_long` x `resize_short` rectangle. Any part that exceeds the rectangle is cropped from the center. |
|`resize_adaptive` |Array |No |`["shrink"]` |The scaling condition, used to ensure that scaling is performed only under specific conditions. If this parameter is not provided, it defaults to `["enlarge", "shrink"]`, meaning scaling is always performed.<br><br><br>* `enlarge`: Enlarge only when the original image size is smaller than the target size.<br><br>* `shrink`: Shrink only when the original image size is larger than the target size. |
|`output_format` |String |No |`jpeg` |The format of the output image. Defaults to `original`.<br><br><br>* `original`: Keep the same format as the source image.<br><br>* `png`<br><br>* `jpeg`<br><br>* `webp` |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to scale an image proportionally so that its long edge is 800 pixels, and output it in JPEG format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/resize-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.png",
  "resize_long": 800,
  "resize_short": 0,
  "resize_mode": "contain",
  "output_format": "jpeg"
}'
```


<span id="response"></span>
## Response

This is a synchronous API; the processing result is returned directly in the response body of this API.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task succeeded.<br><br><br>* `true`: Success. See the `result` field for the task result.<br><br>* `false`: Failure. See the `error` field for detailed error information. |
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task#result-object) below. |
|`error` |Object |An object containing error details. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and produces a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`image_url` |String |The download URL for the processed image file. This link is valid for **24 hours**; be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, for example, webp. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general category of the error, for example, `BadRequest`. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |


<span id="response-example"></span>
### Response example

Example of a successful response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-resize-image-1234567",
  "task_type":"resize-image",
  "result": {
    "image_url": "https://example.byteplus.com/resized_output.jpeg?auth_key=1775271661-...",
    "image_size": 153210,
    "image_format": "jpeg",
    "image_width": 800,
    "image_height": 450
  },
  "expires_at": 1778573984,
  "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Example of a failure response:

```JSON
{
  "success":false,
  "task_id":"amk-tool-resize-image-940034677250",
  "task_type":"resize-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

---
title: "Create an image negative task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/invert-image`

To apply a negative (color\-inversion) effect to an image, you can use this API to submit a synchronous task. It inverts the light\-dark relationship and converts colors to their complementary opposites, making it ideal for creative visual generation, secondary content creation, automated image processing, and artistic stylization.

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
|`image_url` |String |Yes |`https://example.com/source.png` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. Only static images are supported.<br><br>* **Input resolution**: Both the width and height must not exceed 10,000 pixels. |
|`output_format` |String |No |`webp` |The format of the output image. Defaults to `original`.<br><br><br>* `original`: Keep the same format as the source image.<br><br>* `png`<br><br>* `jpeg`<br><br>* `webp` |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit an image inversion task for an image and output it in WebP format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/invert-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{ 
  "image_url": "https://example.com/input_image.jpg",
  "output_format": "webp"
}'
```


<span id="response"></span>
## Response

This is a synchronous API; the processing result is returned directly in the response body.

<span id="response-parameters"></span>
### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task succeeded.<br><br><br>* `true`: Success. See the `result` field for the task result.<br><br>* `false`: Failure. See the `error` field for detailed error information. |
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task#result-object) below. |
|`error` |Object |An object containing error details. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task#error-object)below. |
|`task_id` |String |The unique identifier for the task. You can use this ID to query the task status or for troubleshooting. |
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
|`type` |String |The category of the error, for example, BadRequest. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |


<span id="response-example"></span>
### Response example

Example of a successful response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-invert-image-1234567",
    "task_type": "invert-image",
    "result": {
        "image_url": "https://example.byteplus.com/inverted_output.webp?auth_key=1775271661-...",
        "image_size": 910234,
        "image_format": "webp",
        "image_width": 1920,
        "image_height": 1080
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
  "task_id":"amk-tool-invert-image-940034677250",
  "task_type":"invert-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

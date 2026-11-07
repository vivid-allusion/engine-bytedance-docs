---
title: "Create an image matting task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-matting-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/remove-image-background`

Use this API to submit a synchronous image matting task. It can automatically identify and retain the image subject while removing the background, generating an image with a transparent background.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">To learn about complete application examples and usage, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-matting">Image matting</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header-parameters"></span>
### Header parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to process.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic`.<br><br>* File size: A single image cannot exceed 30 MB.<br><br>* Input image resolution:<br><br>   * When `scene` is `general`:<br><br>      * The long side of the input image resolution cannot exceed 10240 px, and the short side cannot exceed 6000 px.<br><br>      * The total number of pixels of the input image (long side × short side) cannot exceed 40 MP.<br><br>   * When `scene` is `human` or `product`: The long side of the input image resolution cannot exceed 7680 px, and the short side cannot exceed 4320 px. |
|`scene` |String |Yes |`human` |The background removal scenario.<br><br><br>* `general`: General scenario. Suitable for cases where you want to extract the subject from an image but are not sure of its category.<br><br>* `human`: Human matting scenario. Suitable for cases where you only need to extract the human subject from the image.<br><br>* `product`: Product matting scenario. Suitable for cases where you only need to extract the product subject from the image. |
|`need_contour` |Boolean |No |`true` |Whether to generate a contour for the subject. Defaults to `false`. This parameter takes effect only when `scene` is `human` or `product`, and is ignored in the `general` scenario. |
|`contour_color` |String |No |`#FFFFFF` |The color of the subject contour, in hexadecimal RGB format. Defaults to `"#FFFFFF"` (white). This parameter takes effect only when `need_contour` is `true` and `scene` is `human` or `product`. |
|`contour_size` |Integer |No |`10` |The width of the subject contour, in pixels (px). The value range is `[1, 100]`, and the default is `10`. This parameter takes effect only when `need_contour` is `true` and `scene` is `human` or `product`. |
|`need_crop_background` |Boolean |No |`true` |Whether to crop the transparent background of the output image to exactly wrap the subject. Defaults to `false`. This parameter takes effect only when `scene` is `human` or `product`, and is ignored in the `general` scenario. |
|`output_format` |String |No |`png` |The format of the output image.<br><br><br>* `png`: (Default) Supports a transparent background.<br><br>* `jpeg`: Does not support a transparent background; transparent areas are filled with black.<br><br>* `webp`: Supports a transparent background. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-examples"></span>
## Request examples

<span id="example-1-matting-in-the-general-scenario"></span>
### Example 1: Matting in the general scenario

Remove the background of an image with an unknown subject using the `general` scenario.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/remove-image-background' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/object.jpg",
  "scene": "general"
}'
```


<span id="example-2-human-matting-with-a-contour"></span>
### Example 2: Human matting with a contour

Extract a person from an image using the `human` scenario and add a 5 px\-wide white contour.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/remove-image-background' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/portrait.jpg",
  "scene": "human",
  "need_contour": true,
  "contour_color": "#FFFFFF",
  "contour_size": 5
}'
```


<span id="example-3-product-matting-with-background-cropping"></span>
### Example 3: Product matting with background cropping

Extract a product from an image using the `product` scenario and crop the excess transparent background.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/remove-image-background' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/gadget.png",
  "scene": "product",
  "need_crop_background": true
}'
```


<span id="response"></span>
## Response

This is a synchronous API, and the processing result is returned directly in the response body of this API.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successful.<br><br><br>* `true`: Succeeded. Check the `result` field for the task result.<br><br>* `false`: Failed. Check the `error` field for detailed error information. |
|`result` |Object |The object that contains the image processing result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-matting-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-matting-task#error-object) below. |
|`task_id` |String |The unique identifier of the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task is submitted. |


<span id="result-object"></span>
#### The result object


|Parameter |Type |Example value |Description |
|---|---|---|---|
|`image_url` |String |`https://example.com/...?auth_key=...` |The download URL of the image after background removal. This address is valid for **24 hours**, so be sure to save the output promptly. |
|`image_size` |Integer |`45875` |The size of the generated image, in bytes. |
|`image_format` |String |`png` |The format of the generated image. |
|`image_width` |Integer |`800` |The width of the generated image, in pixels (px). |
|`image_height` |Integer |`600` |The height of the generated image, in pixels (px). |


<span id="error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error. For example: `BadRequest`. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |


<span id="response-examples"></span>
### Response examples

Successful response example:

```JSON
{
    "success": true,
    "task_id": "amk-tool-remove-image-background-xxxxxxxxxx",
    "task_type": "remove-image-background",
    "result": {
        "image_url": "https://example.com/removed_bg_image.png?auth_key=...",
        "image_size": 45875,
        "image_format": "png",
        "image_width": 800,
        "image_height": 600
    },
    "expires_at": 1778573984,
    "queue_id": "q2a028fa533b7fe6a25b018dcc******",
    "request_id": "20240521183140xxxxxxxxxxxxxxxxxx"
}
```


Failed response example:

```JSON
{
  "success": false,
  "request_id": "20240521183200xxxxxxxxxxxxxxxxxx",
  "task_type": "remove-image-background",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'scene' must be one of [general, human, product].",
    "param": "scene",
    "type": "BadRequest"
  },
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

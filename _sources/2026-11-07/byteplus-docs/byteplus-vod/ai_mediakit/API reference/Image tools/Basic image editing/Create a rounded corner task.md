---
title: "Create a rounded corner task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/round-corner-image`

To programmatically add rounded corners to an image, you can call this synchronous API. It supports adding circular or elliptical corners and is ideal for visual editing tasks like creating avatars, cards, and e\-commerce main images. This document provides a complete reference for all request parameters and response structures.

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
|`image_url` |String |Yes |`https://example.com/source.png` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that each image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp` are supported. Only static images can be processed.<br><br>* **Input resolution limit**: Both the width and height must not exceed 10000 pixels. |
|`corner_type` |String |No |`ellipse` |The corner type.<br><br><br>* `circle`: (Default) Circular corners. You can configure the radius through the `circle_radius` parameter.<br><br>* `ellipse`: Elliptical corners. You can configure the radii through the `ellipse_radius_x` and `ellipse_radius_y` parameters. |
|`circle_radius` |Integer |No |`50` |The radius of the circular corners, in px. This parameter is required when `corner_type` is `circle`. Value range: `[0, shortest side of the original image / 2]`. If the specified value exceeds this range, it is treated as the maximum inscribed\-circle radius. |
|`ellipse_radius_x` |Integer |No |`40` |The X\-axis (horizontal) radius of the elliptical corners, in px. This parameter is required when `corner_type` is `ellipse`. Value range: greater than or equal to `0`. |
|`ellipse_radius_y` |Integer |No |`60` |The Y\-axis (vertical) radius of the elliptical corners, in px. This parameter is required when `corner_type` is `ellipse`. Value range: greater than or equal to `0`. |
|`output_format` |String |No |`png` |The format of the output image. The default is `webp`.<br><br><br>* `original`: Keeps the original image format.<br><br>* `png`: The area outside the rounded corners is filled with transparency.<br><br>* `webp`: The area outside the rounded corners is filled with transparency.<br><br>* `jpeg`: The area outside the rounded corners is filled with white. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit an "elliptical corner" task for an image, specifying an X\-axis radius of 80px, a Y\-axis radius of 50px, and PNG as the output format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/round-corner-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/input_image.png",
  "corner_type": "ellipse",
  "ellipse_radius_x": 80,
  "ellipse_radius_y": 50,
  "output_format": "png"
}'
```


<span id="response"></span>
## Response

This is a synchronous API, and the processing result is returned directly in the response body.

<span id="response-parameters"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task succeeded.<br><br><br>* `true`: Success. Check the `result` field to get the task result.<br><br>* `false`: Failure. Check the `error` field for detailed error information. |
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`image_url` |String |The download URL of the processed image file. This URL is valid for **24 hours**; be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, for example, webp. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example, `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The type of the error. For example, BadRequest. |
|`message` |String |A detailed description of the error, useful for debugging. |


<span id="response-example"></span>
### Response example

Success:

```JSON
{
    "success": true,
    "task_id": "amk-tool-round-corner-image-1234567",
    "task_type":"round-corner-image",
    "result": {
        "image_url": "https://example.byteplus.com/rounded_output.png?auth_key=1775271661-...",
        "image_size": 987654,
        "image_format": "png",
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
  "task_id":"amk-tool-round-corner-image-940034677250",
  "task_type":"round-corner-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

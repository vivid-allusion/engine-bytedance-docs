---
title: "Create an image cropping task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-cropping-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/crop-image`

To perform various cropping operations on an image, you can call this synchronous API. It supports multiple modes, including directional, origin\-based, custom, and inscribed\-circle cropping, which are ideal for scenarios like multi\-device size adaptation, subject preservation, removing image borders, and capturing specific regions.

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


|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. Only static images are supported.<br><br>* **Special limit**: When using inscribed\-circle cropping (`crop_mode` = `circle`), the shortest side of the original image must not exceed 2048 px. |
|`crop_mode` |String |No |`custom` |The cropping mode, which determines the cropping behavior and required parameters. Defaults to directional.<br><br><br>* `directional`: Directional cropping. Crops based on the specified width, height, and position.<br><br>* `origin`: Origin\-based cropping. Crops based on the specified width and height, offset, and anchor.<br><br>* `custom`: Custom cropping. Crops based on the specified top\-left and bottom\-right coordinates.<br><br>* `circle`: Maximum inscribed\-circle cropping. No other parameters are needed in this mode.<br><br><br>For detailed description of different modes, see [Cropping mode descriptions](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-image-editing#a1e06a5d). |
|`output_format` |String |No |`png` |The format of the output image. Defaults to `original` (keep the original format). Optional values: `png`, `jpeg`, `webp`.<br><br>Note: For inscribed\-circle cropping (`crop_mode` = `circle`), to ensure a transparent background, we recommend setting the output format to `png` or `webp`. If the output is `jpeg`, the non\-circular area is filled with white. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |
|Directional cropping parameters (apply when `crop_mode` is `directional`) |||||
|`crop_width` |Integer |No |`800` |The target width of the cropped image, in px. When `crop_mode` is `directional`, both `crop_width` and `crop_height` must be provided, and they cannot both be `0`. If `crop_width` is set to `0`, the width is automatically calculated based on `crop_height` to maintain the original aspect ratio. |
|`crop_height` |Integer |No |`600` |The target height of the cropped image, in px. When `crop_mode` is `directional`, both `crop_width` and `crop_height` must be provided, and they cannot both be `0`. If `crop_height` is set to `0`, the height is automatically calculated based on `crop_width` to maintain the original aspect ratio. |
|`crop_position` |String |No |`center` |The position of the cropping region. Defaults to `center`. Optional values:<br><br><br>* `center`: Crops from the center.<br><br>* `up`: Crops from the top.<br><br>* `down`: Crops from the bottom.<br><br>* `left`: Crops from the left.<br><br>* `right`: Crops from the right. |
|Origin\-based cropping parameters (apply when `crop_mode` is `origin`) |||||
|`crop_width` |Integer |No |`400` |The target width of the cropped image, in px. Required when `crop_mode` is `origin`. |
|`crop_height` |Integer |No |`300` |The target height of the cropped image, in px. Required when `crop_mode` is `origin`. |
|`origin_gravity` |String |No |`northwest` |The cropping anchor (starting point). Defaults to `northwest` (top\-left corner). Supported values:<br><br><br>* `northwest`<br><br>* `north`<br><br>* `northeast`<br><br>* `west`<br><br>* `center`<br><br>* `east`<br><br>* `southwest`<br><br>* `south`<br><br>* `southeast` |
|`origin_x` |Integer |No |`50` |The horizontal offset of the cropping region relative to the anchor, in px. Required when `crop_mode` is `origin`. Positive values shift the cropping region to the right; negative values shift it to the left. |
|`origin_y` |Integer |No |`100` |The vertical offset of the cropping region relative to the anchor, in px. Required when `crop_mode` is `origin`. Positive values shift the cropping region down; negative values shift it up. |
|Custom cropping parameters (apply when `crop_mode` is `custom`) |||||
|`custom_x1` |Integer |No |`100` |The X\-axis coordinate of the top\-left corner of the cropping region, in px. Required when `crop_mode` is `custom`. |
|`custom_y1` |Integer |No |`150` |The Y\-axis coordinate of the top\-left corner of the cropping region, in px. Required when `crop_mode` is `custom`. |
|`custom_x2` |Integer |No |`400` |The X\-axis coordinate of the bottom\-right corner of the cropping region, in px. Required when `crop_mode` is `custom`. |
|`custom_y2` |Integer |No |`350` |The Y\-axis coordinate of the bottom\-right corner of the cropping region, in px. Required when `crop_mode` is `custom`. |


<span id="request-example"></span>
## Request example

The following example demonstrates how to perform **custom cropping** on an image, capturing the rectangular region bounded by the top\-left coordinate (100, 150) and the bottom\-right coordinate (400, 350), and outputting it in PNG format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/crop-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/source_image.jpg",
  "crop_mode": "custom",
  "custom_x1": 100,
  "custom_y1": 150,
  "custom_x2": 400,
  "custom_y2": 350,
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
|`success` |Boolean |Whether the task succeeded.<br><br>&nbsp;<br><br>\* `true`: Success. See the `result` field for the task result.<br><br>\* `false`: Failure. See the `error` field for detailed error information. |
|`result` |Object |The object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-cropping-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-cropping-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`image_url` |String |The download URL of the processed image file. This URL is valid for **24 hours**, so be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, such as png. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general category of the error. For example, BadRequest. |
|`message` |String |A detailed description of the error, useful for development and debugging. |


<span id="response-example"></span>
### Response example

Success:

```JSON
{
    "success": true,
    "task_id": "amk-tool-crop-image-1234567",
    "task_type": "crop-image",
    "result": {
        "image_url": "https://example.byteplus.com/cropped_output.png?auth_key=1775271661-...",
        "image_size": 188080,
        "image_format": "png",
        "image_width": 300,
        "image_height": 200
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
  "task_id":"amk-tool-crop-image-940034677250",
  "task_type": "crop-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

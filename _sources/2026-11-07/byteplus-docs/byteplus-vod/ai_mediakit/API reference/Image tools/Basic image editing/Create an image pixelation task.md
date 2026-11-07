---
title: "Create an image pixelation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/mosaic-image`

To obscure sensitive content in images, you can use this API to submit a synchronous image mosaic task. This document details how to apply a pixelation effect to an entire image or a specified rectangular region, and customize the shape and size of the pixel cells. This tool is ideal for masking faces, ID information, license plates, and chat records.

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
|`mosaic_type` |String |No |`specify-region` |The mosaic scope.<br><br><br>* `full-image`: (default) Apply a mosaic to the entire image.<br><br>* `specify-region`: Apply a mosaic only to the regions specified by `mosaic_regions`. |
|`mosaic_regions` |Array |No |`[{"top_left_x": 100, ...}]` |The list of rectangular coordinates for the regions to be pixelated. Required when `mosaic_type` is `specify-region`. Up to 3 rectangular regions are supported. For the detailed structure, see [The mosaic region object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task#mosaic-region-object) below. |
|`mosaic_shape` |String |No |`rectangle` |The shape of the mosaic pixel cell. Defaults to `circle`.<br><br><br>* `circle`: Round/elliptical pixel cells, for a softer visual effect.<br><br>* `rectangle`: Rectangular pixel cells, for a more regular masking effect. |
|`mosaic_step_x` |Integer |No |`16` |The width of the mosaic pixel cell, in px. The larger the value, the more pronounced the mosaic graininess. Defaults to `12`. Must not be less than `1`. |
|`mosaic_step_y` |Integer |No |`16` |The height of the mosaic pixel cell, in px. The larger the value, the more pronounced the mosaic graininess. Defaults to `12`. Must not be less than `1`. |
|`output_format` |String |No |`jpeg` |The format of the output image. Defaults to `original`.<br><br><br>* `original`: Keep the same format as the source image.<br><br>* `png`<br><br>* `jpeg`<br><br>* `webp` |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="mosaic-region-object"></span>
#### The mosaic region object


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`top_left_x` |Integer |Yes |`100` |The X\-axis coordinate of the top\-left corner of the selected region, in px. The coordinate origin is the top\-left corner of the image. Must not be less than `0`. |
|`top_left_y` |Integer |Yes |`150` |The Y\-axis coordinate of the top\-left corner of the selected region, in px. The coordinate origin is the top\-left corner of the image. Must not be less than `0`. |
|`bottom_right_x` |Integer |Yes |`300` |The X\-axis coordinate of the bottom\-right corner of the selected region, in px. The coordinate origin is the top\-left corner of the image. Must not be less than `0`. |
|`bottom_right_y` |Integer |Yes |`250` |The Y\-axis coordinate of the bottom\-right corner of the selected region, in px. The coordinate origin is the top\-left corner of the image. Must not be less than `0`. |


Suppose you want to use the blue region in the image below as the mosaic region. The parameters are set as follows:


* `top_left_x`: The X coordinate of the top\-left corner of the rectangle (b1 in the image).

* `top_left_y`: The Y coordinate of the top\-left corner of the rectangle (a1 in the image).

* `bottom_right_x`: The X coordinate of the bottom\-right corner of the rectangle (b2 in the image).

* `bottom_right_y`: The Y coordinate of the bottom\-right corner of the rectangle (a2 in the image).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c5328cc6af7493eba25d602a20217be~tplv-goo7wpa0wc-image.image) </span>

<span id="request-example"></span>
## Request example

The following example demonstrates how to apply a `16x16` rectangular mosaic to a specified rectangular region of an image (top\-left corner `(100, 150)`, bottom\-right corner `(300, 250)`) and output it in JPEG format.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/mosaic-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/privacy_image.jpg",
  "mosaic_type": "specify-region",
  "mosaic_regions": [
    {
      "top_left_x": 100,
      "top_left_y": 150,
      "bottom_right_x": 300,
      "bottom_right_y": 250
    }
  ],
  "mosaic_shape": "rectangle",
  "mosaic_step_x": 16,
  "mosaic_step_y": 16,
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task#result-object) below. |
|`error` |Object |An object containing error details. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-pixelation-task#error-object) below. |
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
|`type` |String |The macro category of the error, for example, BadRequest. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |


<span id="response-example"></span>
### Response example

Example of a successful response:

```JSON
{
   "success": true,
   "task_id": "amk-tool-mosaic-image-1234567",
   "task_type":"mosaic-image",
   "result": {
       "image_url": "https://example.byteplus.com/mosaiced_output.jpeg?auth_key=1775271661-...",
       "image_size": 1122334,
       "image_format": "jpeg",
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
  "task_id":"amk-tool-mosaic-image-940034677250",
  "task_type":"mosaic-image",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id": "20260512161933F7F3274AA07554196387",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

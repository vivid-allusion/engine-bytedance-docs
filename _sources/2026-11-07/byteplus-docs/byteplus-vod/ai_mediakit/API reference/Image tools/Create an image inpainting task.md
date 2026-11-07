---
title: "Create an image inpainting task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-inpainting-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image`

To programmatically remove unwanted elements like text or icons from an image, you can call this synchronous API. It automatically detects and erases specified content and uses smart\-fill technology to repair the background for a natural result.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For complete application examples and usage instructions, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-inpainting">Image inpainting</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to process.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Input image resolution:<br><br>   * Must not be smaller than 10x10 pixels.<br><br>   * Must not exceed 2560x1440 pixels (width × height).<br><br>* File size: Each image must not exceed 10 MB.<br><br>* Supported formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic` are supported. |
|`tool_version` |String |No |`standard` |The model version to use for image erase and repair. Currently only `standard` is supported, which applies to simple, well\-defined erase tasks. |
|`standard_scene` |String |No |`full_screen_text_erase` |The standard\-version erase scenario. Takes effect only when `tool_version` is `standard`. Defaults to `full_screen_text_erase`.<br><br><br>* `full_screen_text_erase`: Full\-screen text erasure. You can specify the text to erase through the `standard_erase_text` field; if not specified, all text content is erased by default.<br><br>* `full_screen_icon_erase`: Full\-screen icon erasure.<br><br>* `selected_area_erase`: Specified\-area erasure. When using this scenario, you must provide at least one of `selected_area` (rectangular coordinates) or `mask_url` (mask image) to define the erase range. If both are provided, the system erases the union of the areas they define. |
|`standard_erase_text` |String |No |`Internal use only` |Specifies the text content to erase. Takes effect only when `standard_scene` is `full_screen_text_erase`. If this parameter is not provided, all recognized text is erased. |
|`selected_area` |Object |No |`{"top_left_x": 0.1, "top_left_y": 0.1, "bottom_right_x": 0.5, "bottom_right_y": 0.4}` |Specifies the erase area as a rectangular box. Takes effect only when standard_scene is selected_area_erase. The coordinate system takes the top\-left corner of the input image as the origin, with width and height both normalized to [0,1]; for example, (0.5, 0.5) represents the center point of the image. For details, see  below. If mask_url is also provided, the union of the two specified areas is erased. |
|`mask_url` |String |No |`https://example.com/mask.png` |The URL of the mask image. By uploading a black\-and\-white mask image, you can specify an arbitrarily shaped area to erase. Takes effect only when `standard_scene` is `selected_area_erase`. The mask image requirements are as follows:<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Resolution requirement: Must match the resolution of the input image `image_url`.<br><br>* If selected_area is also provided, the union of the two specified areas is erased. |
|`output_format` |String |No |`png` |The format of the output image.<br><br><br>* `webp` (Default)<br><br>* `png`<br><br>* `jpeg` |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="the-selected-area-object"></span>
#### The selected area object

This object defines a rectangular erase area. It uses a normalized coordinate system with the top\-left corner of the image as the origin (0, 0) and the bottom\-right corner as (1, 1). All coordinate values are proportions of the image's total width or height, in the range `[0.0, 1.0]`.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0a6586d3b5484610ad8a756e93fa14de) </span>


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`top_left_x` |Number |Yes |`0.1` |The x\-coordinate of the top\-left corner of the rectangular box (horizontal position), as a proportion of the image's total width. |
|`top_left_y` |Number |Yes |`0.1` |The y\-coordinate of the top\-left corner of the rectangular box (vertical position), as a proportion of the image's total height. |
|`bottom_right_x` |Number |Yes |`0.5` |The x\-coordinate of the bottom\-right corner of the rectangular box (horizontal position); must be greater than `top_left_x`. |
|`bottom_right_y` |Number |Yes |`0.4` |The y\-coordinate of the bottom\-right corner of the rectangular box (vertical position); must be greater than `top_left_y`. Range: [0, 1]. |


<span id="request-example"></span>
## Request example

<span id="example-1-erase-all-text-in-the-image-default-behavior"></span>
### Example 1: Erase all text in the image (default behavior)

Set `standard_scene` to `full_screen_text_erase` (or use the default) and do not pass `standard_erase_text`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/with_text.png"
}'
```


<span id="example-2-erase-specified-text-in-the-image"></span>
### Example 2: Erase specified text in the image

Set `standard_scene` to `full_screen_text_erase` (or use the default) and pass the `standard_erase_text` parameter to specify the content to erase.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/confidential.jpg",
  "standard_erase_text": "Internal use only"
}'
```


<span id="example-3-erase-all-icons-in-the-image"></span>
### Example 3: Erase all icons in the image

Set `standard_scene` to `full_screen_icon_erase`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/with_logo.png",
  "standard_scene": "full_screen_icon_erase"
}'
```


<span id="example-4-erase-a-specified-area-coordinate-box"></span>
### Example 4: Erase a specified area (coordinate box)

Set standard_scene to selected_area_erase and provide normalized coordinates in selected_area. The following example erases a rectangular area in the upper\-left part of the image.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/with_area.png",
  "standard_scene": "selected_area_erase",
  "selected_area": {
    "top_left_x": 0.1,
    "top_left_y": 0.1,
    "bottom_right_x": 0.5,
    "bottom_right_y": 0.4
  }
}'
```


<span id="example-5-erase-a-specified-area-mask-image"></span>
### Example 5: Erase a specified area (mask image)

Set standard_scene to selected_area_erase and provide the mask using mask_url.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/erase-image' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/with_area.png",
  "standard_scene": "selected_area_erase",
  "mask_url": "https://example.com/mask.png"
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see The result object below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-inpainting-task#the-result-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="the-result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL of the erased and repaired image, valid for **24 hours**; be sure to save the output promptly. |
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


<span id="response-example"></span>
### Response example

Success response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-erase-image-1716288800",
    "task_type": "erase-image",
    "result": {
        "image_url": "https://example.com/erased_image.webp?auth_key=...",
        "image_size": 51200,
        "image_format": "webp",
        "image_width": 1920,
        "image_height": 1080
    },
    "expires_at": 1778573984,
    "request_id": "021778401180935fdbd0ff1ce00652c087a478b3f62d63b5dbf0f",
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure response:

```JSON
{
  "success": false,
  "error": {
    "code": "InvalidParameter",
    "message": "The value of 'selected_area.top_left_x' must be between 0 and 1.",
    "param": "selected_area.top_left_x",
    "type": "BadRequest"
  },
  "request_id": "20240521181500AABBCCDDEEFF445566",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

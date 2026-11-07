---
title: "Create a text and image watermark task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-watermark`

To protect your image assets with copyright marks or prevent hotlinking, you can use this API. This synchronous API allows you to add either a **text or an image watermark** to a source image. You can configure various parameters, including position, opacity, font size, color, and tiling, to customize the appearance of the watermark.

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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be processed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. Only static images are supported.<br><br>* **Input resolution**: Both the width and height must not exceed 10,000 pixels. |
|`watermark_type` |String |No |`text` |The watermark type. Defaults to `text`.<br><br><br>* `text`: Text watermark.<br><br>* `image`: Image watermark. |
|`output_format` |String |No |`jpeg` |The format of the output image. Defaults to `original`.<br><br><br>* `original`: Keep the same format as the source image.<br><br>* `png`<br><br>* `jpeg`<br><br>* `webp` |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |
|<div style="text-align: center"><br>Text watermark parameters (effective when <code>watermark_type</code> is <code>text</code>)</div><br> |||||
|`watermark_text` |String |No |`© MyBrand` |The text content of the watermark. Required when `watermark_type` is `text`. Must not exceed 64 characters. |
|`watermark_text_font` |String |No |`zcool_kuaileti.ttf` |The text font. Defaults to `SourceHanSans-Regular.ttf` (Source Han Sans). Font families such as Source Han Sans, Source Han Serif, ZCOOL, and FZLanTingHei are supported. For specific font file names, see [Supported fonts](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task#supported-fonts). |
|`watermark_text_font_size` |Integer |No |`24` |The text font size, in pixels. Defaults to `30`. The value range is [1, 200]. |
|`watermark_text_color` |String |No |`#FF0000` |The text color. Supports hexadecimal (for example, `#FF0000`), RGB, and other formats. Defaults to `#FFFFFF` (white). |
|`watermark_text_opacity` |Integer |No |`50` |The opacity of the text watermark. The value range is [0, 100]. The smaller the value, the more transparent it is. Defaults to `30`. |
|<div style="text-align: center"><br>Image watermark parameters (effective when <code>watermark_type</code> is <code>image</code>)</div><br> |||||
|`watermark_image_url` |String |No |`https://example.com/logo.png` |The URL of the image watermark. Required when `watermark_type` is `image`.<br><br><br>* **File source**: Must be a publicly accessible HTTP or HTTPS URL.<br><br>* **File size**: It is recommended not to exceed 5 MB.<br><br>* **Supported formats**: Common image formats such as `.jpg`, `.jpeg`, and `.webp`. |
|`watermark_image_opacity` |Integer |No |`50` |The opacity of the image watermark. The value range is `[0,100]`. The smaller the value, the more transparent it is. Defaults to 100. |
|Layout parameters |||||
|`enable_tile` |Boolean |No |`true` |Whether to enable the tiled watermark effect. Defaults to `false`. When enabled, the watermark is repeated and tiled across the entire image at a fixed spacing.<br><br><br>* For **text watermarks**, an additional counterclockwise 30\-degree rotation is applied.<br><br>* For **image watermarks**, only tiling is performed, without rotation. |
|`watermark_position` |String |No |`bottom_right` |The nine\-grid layout position of the watermark on the image. Defaults to `bottom_right` (bottom\-right corner). The available values are as follows:<br><br><br>* `top_left`<br><br>* `top_center`<br><br>* `top_right`<br><br>* `left_center`<br><br>* `center`<br><br>* `right_center`<br><br>* `bottom_left`<br><br>* `bottom_center`<br><br>* `bottom_right`<br><br><br>Note: When using a value that contains `center` (`top_center`, `left_center`, `center`, `right_center`, `bottom_center`), the offset parameters (`watermark_position_offset_x` and `watermark_position_offset_y`) do not take effect. |
|`watermark_position_offset_x` |Integer |No |`20` |The horizontal offset, that is, the fine\-tuning distance of the watermark along the X axis based on `watermark_position`, in pixels. Defaults to `0`. The value must be 0 or greater.<br><br>Note: This parameter takes effect only when the value of `watermark_position` does not contain center. |
|`watermark_position_offset_y` |Integer |No |`20` |The vertical offset, that is, the fine\-tuning distance of the watermark along the Y axis based on `watermark_position`, in pixels. Defaults to `0`. The value must be 0 or greater.<br><br>Note: This parameter takes effect only when the value of `watermark_position` does not contain center. |


<span id="request-example"></span>
## Request example

<span id="example-1-add-a-text-watermark"></span>
### Example 1: Add a text watermark

The following example demonstrates how to add a red text watermark "© MyBrand" to the bottom\-right corner of an image and set an offset.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/background.jpg",
  "watermark_type": "text",
  "watermark_text": "© MyBrand",
  "watermark_text_font_size": 24,
  "watermark_text_color": "#FF0000",
  "watermark_text_opacity": 50,
  "watermark_position": "bottom_right",
  "watermark_position_offset_x": 20,
  "watermark_position_offset_y": 20
}'
```


<span id="example-2-add-an-image-watermark"></span>
### Example 2: Add an image watermark

The following example demonstrates how to add a logo image as a watermark to the top\-left corner and set it to be semi\-transparent.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/add-image-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/background.jpg",
  "watermark_type": "image",
  "watermark_image_url": "https://example.com/logo.png",
  "watermark_image_opacity": 50,
  "watermark_position": "top_left",
  "watermark_position_offset_x": 10,
  "watermark_position_offset_y": 10
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task#result-object) below. |
|`error` |Object |An object containing error details. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-text-and-image-watermark-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and produces a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL for the processed image file. This link is valid for **24 hours**; be sure to save the output promptly. |
|`image_size` |Integer |The size of the generated image, in bytes. |
|`image_format` |String |The format of the generated image, for example, webp. |
|`image_width` |Integer |The width of the generated image, in px. |
|`image_height` |Integer |The height of the generated image, in px. |


<span id="error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general category of the error, for example, BadRequest. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |


<span id="response-example"></span>
### Response example

Example of a successful response:

```JSON
{
  "success": true,
  "task_id": "amk-tool-add-image-watermark-1234567",
  "task_type":"add-image-watermark",
  "result": {
    "image_url": "https://example.byteplus.com/watermarked_output.jpeg?auth_key=1775271661-...",
    "image_size": 310450,
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
  "task_id":"amk-tool-add-image-watermark-940034677250",
  "task_type":"add-image-watermark",
  "error":{
    "code":"InvalidParameter",
    "type":"BadRequest",
    "message":"validating root: required: missing properties: [\"image_url\"]"
  },
  "request_id":"202607291022287DC463A3C5D182BCEE73",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


<span id="appendix"></span>
## Appendix

<span id="supported-fonts"></span>
### Supported fonts


|Font type |Font name |
|---|---|
|Source Han Sans family |SourceHanSans\-Regular.ttf |
||SourceHanSans\-Bold.ttf |
||SourceHanSans\-ExtraLight.ttf |
||SourceHanSans\-Heavy.ttf |
||SourceHanSans\-Light.ttf |
||SourceHanSans\-Medium.ttf |
||SourceHanSans\-Normal.ttf |
||SourceHanSerifCN\-Regular.ttf |
||SourceHanSerifCN\-Bold.ttf |
||SourceHanSerifCN\-ExtraLight.ttf |
||SourceHanSerifCN\-Heavy.ttf |
||SourceHanSerifCN\-Light.ttf |
||SourceHanSerifCN\-SemiBold.ttf |
|ZCOOL family |zcool\-heiti.ttf |
||zcool_gaoduanhei.ttf |
||zcool_kuaileti.ttf |
||zcool_huangyou.ttf |
|FZ family |FZLTHK.TTF |

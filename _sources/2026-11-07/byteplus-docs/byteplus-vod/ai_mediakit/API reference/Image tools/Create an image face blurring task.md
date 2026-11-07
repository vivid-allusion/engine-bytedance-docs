---
title: "Create an image face blurring task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-face-blurring-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/face-blur-image`

Use this API to submit a synchronous image face blurring task. The tool automatically detects all face regions in an image and applies a mosaic to them, enabling one\-click facial privacy protection. It is suitable for scenarios that require batch protection of facial privacy, such as social platform content moderation, street\-view or surveillance footage anonymization, news media asset processing, and AI training dataset anonymization.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-face-blurring">Image face blurring</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/source.jpg` |The URL of the image to be masked.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that each image not exceed 35 MB. Files that are too large may cause processing to fail.<br><br>* **Resolution limit**: The product of the image's width and height must not exceed 400 million pixels.<br><br>* **Supported formats**: Mainstream image formats such as `.png`, `.jpg`, `.jpeg`, `.webp`, and `.avif` are supported. Animated images are not supported. |
|`blur_shape` |String |No |`circle` |The shape of the masked face region.<br><br><br>* `circle`(Default)<br><br>* `rectangle` |
|`mosaic_step` |Integer |No |`12` |The mosaic cell size, in px. A positive integer. The larger the value, the coarser the mosaic and the stronger the anonymization. The recommended range is `[5, 100]`. Defaults to `12`. |
|`face_detect_thresh` |Number |No |`0.9` |The confidence threshold for face detection. The value range is `(0, 1)`. The higher the value, the stricter the filtering: too low may misidentify non\-face regions, while too high may miss faces. Defaults to `0.9`. |
|`output_format` |String |No |`webp` |The format of the output image.<br><br><br>* `png`<br><br>* `jpeg`<br><br>* `webp` (Default) |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/face-blur-image' \
  -H 'Authorization: Bearer {Your_API_Key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "image_url": "https://example.com/group_photo.jpg",
    "blur_shape": "circle",
    "mosaic_step": 16,
    "face_detect_thresh": 0.9,
    "output_format": "jpeg"
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-face-blurring-task#the-result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-face-blurring-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="the-result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`image_url` |String |The download URL of the face\-blurred image file. This URL is valid for **24 hours**; be sure to save the output promptly. |
|`image_size` |Integer |The size of the processed image, in bytes. |
|`image_format` |String |The format of the processed image. |
|`image_width` |Integer |The width of the processed image, in px. |
|`image_height` |Integer |The height of the processed image, in px. |
|`face_count` |Integer |The number of faces detected and masked. `0` means no faces were detected and the original image was not processed; a value greater than `0` means the corresponding number of faces have been masked. |
|`face_location` |Array |An array of information objects for each detected face; an empty array when no faces are detected. For details, see [The face location object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-face-blurring-task#the-face-location-object) below. |


<span id="the-face-location-object"></span>
#### The face location object


|Parameter |Type |Description |
|---|---|---|
|`top_left_x` |Integer |The x\-coordinate of the top\-left corner of the face detection box, in px. |
|`top_left_y` |Integer |The y\-coordinate of the top\-left corner of the face detection box, in px. |
|`bottom_right_x` |Integer |The x\-coordinate of the bottom\-right corner of the face detection box, in px. |
|`bottom_right_y` |Integer |The y\-coordinate of the bottom\-right corner of the face detection box, in px. |
|`confidence` |Number |The face detection confidence. The value range is `(0, 1)`. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error. For example: `BadRequest`. |
|`message` |String |A detailed description of the error, useful for debugging. |


<span id="response-example"></span>
### Response example

Success:

```JSON
{
  "success": true,
  "task_id": "amk-tool-face-blur-image-1234567",
  "task_type": "face-blur-image",
  "result": {
    "image_url": "https://example.byteplus.com/blurred.webp?auth_key=...",
    "image_size": 234112,
    "image_format": "webp",
    "image_width": 1920,
    "image_height": 1280,
    "face_count": 1,
    "face_location": [
      {
        "top_left_x": 120,
        "top_left_y": 200,
        "bottom_right_x": 260,
        "bottom_right_y": 360,
        "confidence": 0.97
      }
    ]
  },
  "expires_at": 1778573984,
  "request_id": "20260512161933F7F3274AA07554196387",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure:

```JSON
{
  "success": false,
  "task_id": "amk-tool-face-blur-image-9876543",
  "task_type": "face-blur-image",
  "error": {
    "code": "InvalidParameter",
    "type": "BadRequest",
    "message": "Parameter 'image_url' is required."
  },
  "request_id": "20260512161933F7F3274AA07554196387",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

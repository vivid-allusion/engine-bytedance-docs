---
title: "Create an image metadata acquisition task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/probe-image-metadata`

This API submits a synchronous image metadata acquisition task. It supports querying four types of information: basic image metadata (`metadata`), the dominant color (`avghue`), the alpha (transparency) channel (`alpha`), and BlurHash (`blurhash`). You can apply this to scenarios such as asset management, AIGC metadata recognition, alpha channel analysis, dominant color extraction, and low\-cost preview generation. As a synchronous API, the processing result is returned directly in the response body.

<span id="special-notes"></span>
## Special notes

<span id="notes-on-retrieving-basic-image-metadata-info-type-metadata"></span>
### Notes on retrieving basic image metadata (`info_type` = `metadata`)


* **Color model retrieval**: Only the `jpeg`, `webp`, `png`, `heic`, and `avif` formats are supported. The color models that each format can return are as follows:

   * **jpeg**: `gray`, `ycbcr`, `rgba`, `cmyk`

   * **webp**: `ycbcr`, `nycbcra`, `nrgba`

   * **png**: `rgba`, `rgba64`, `nrgba`, `nrgba64`, `gray`, `gray16`, `palette`

   * **heic**: `ycbcr`

   * **avif**: `ycbcr`

* **Compression quality parameter retrieval**: Only the `jpeg` format is supported.

* **AIGC metadata retrieval**: Ensure that your image format and the location of the AIGC metadata meet the following requirements:

   * **jpeg**: The AIGC metadata must be located in the XMP element/attribute field, the App 11 field, or the EXIF `Usercomment` field.

   * **png**: The AIGC metadata must be located in the XMP element/attribute field, the tEXt chunk information, or the EXIF `Usercomment` field.

   * **webp**: The AIGC metadata must be located in the XMP element/attribute field or the EXIF `Usercomment` field.

   * **avif/heic**: The AIGC metadata must be located in the EXIF `Usercomment` field.

   * **Note**: If the XMP field of a `jpeg` or `png` image already contains AIGC metadata, the system retrieves it only from that field and does not check other locations.


<span id="notes-on-retrieving-metadata-for-animated-images"></span>
### Notes on retrieving metadata for animated images

If the input is an animated image (such as a GIF), the processing logic differs by `info_type`:


* `info_type` = `metadata`: You can retrieve metadata such as the frame count (`frame_count`) and duration (`duration`) of the animated image.

* `info_type` = `alpha`: Alpha channel analysis is not supported for animated images.

* `info_type` = `avghue` and `blurhash`: Only the first frame of the animated image is processed, and the result is returned as it would be for a static image.


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`image_url` |String |Yes |`https://example.com/image.png` |The URL of the image to be probed.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **File size**: It is recommended that a single image not exceed 35 MB.<br><br>* **Supported formats**: Common image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp`. For the specific processing logic of animated images, see [Notes on retrieving metadata for animated images](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task#notes-on-retrieving-metadata-for-animated-images).<br><br>* **Input resolution**: Neither the width nor the height may exceed 10000 pixels. |
|`info_type` |String |No |`metadata` |The type of information to query. Defaults to `metadata`.<br><br><br>* `metadata`: Retrieve basic image metadata. For specific limits, see  [Notes on retrieving basic image metadata (info_type = metadata)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task#notes-on-retrieving-basic-image-metadata-info-type-metadata).<br><br>* `avghue`: Extract the dominant color of the image.<br><br>* `alpha`: Analyze the alpha (transparency) channel of the image.<br><br>* `blurhash`: Generate the BlurHash value of the image. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/probe-image-metadata' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/your_image.jpg",
  "info_type": "metadata"
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
|`result` |Object |The object containing the image processing result. Returned only when `success` is `true`. See [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task#result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. See [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task#error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="result-object"></span>
#### The result object

<span id="when-info-type-is-metadata-default"></span>
##### When `info_type` is `metadata` (default)

Returns the basic metadata of the image.


|Parameter |Type |Description |
|---|---|---|
|`width` |Number |The image width, in px. |
|`height` |Number |The image height, in px. |
|`format` |String |The image format, such as `jpeg`. |
|`size` |Number |The image size, in bytes. |
|`md5` |String |The MD5 value of the image. |
|`frame_count` |Number |The number of frames in the image. For a static image, this is usually 1. |
|`color_model` |String |The color model, such as `gray`. |
|`duration` |Number |The duration of the animated image, in seconds. This field may not exist for static images. |
|`orientation` |Any |The orientation information of the image. |
|`quality` |Number |The compression quality parameter. |
|`exif` |Object \| Null |The EXIF metadata. `null` if it does not exist. |
|`aigc` |Object \| Null |The AIGC metadata. `null` if it does not exist. |


**`metadata`** ** example**

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-image-metadata-123456",
    "result": {
        "width": 1920,
        "height": 1080,
        "format": "jpeg",
        "size": 256000,
        "md5": "d41d8cd98f00b204e9800998ecf8427e",
        "frame_count": 1,
        "color_model": "gray",
        "orientation": 0,
        "quality": 75,
        "exif": null,
        "aigc": null
    },
    "request_id": "20240523100000AABBCCDDEEFF001122"
}
```


<span id="when-info-type-is-avghue"></span>
##### When `info_type` is `avghue`

Returns the dominant color of the image in hexadecimal format.


|Parameter |Type |Description |
|---|---|---|
|`color` |String |The dominant color in hexadecimal format, such as `#RRGGBB`. |


**`avghue`** ** example**

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-image-metadata-123457",
    "result": {
        "color": "#3B5998"
    },
    "request_id": "20240523100100AABBCCDDEEFF001133"
}
```


<span id="when-info-type-is-alpha"></span>
##### When `info_type` is `alpha`

Returns the alpha (transparency) channel information of the image.


|Parameter |Type |Description |
|---|---|---|
|`format` |String |The image format. |
|`width` |Number |The image width, in px. |
|`height` |Number |The image height, in px. |
|`is_animation` |Boolean |Whether the image is animated. |
|`has_alpha` |Boolean |Whether the image contains an alpha (transparency) channel. |
|`alpha_ratio` |Number |The proportion of alpha pixels (fully transparent or semi\-transparent) in the entire image. |


**`alpha`** ** response example**

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-image-metadata-123458",
    "result": {
        "format": "png",
        "width": 512,
        "height": 512,
        "is_animation": false,
        "has_alpha": true,
        "alpha_ratio": 0.45
    },
    "request_id": "20240523100200AABBCCDDEEFF001144"
}
```


<span id="when-info-type-is-blurhash"></span>
##### When `info_type` is `blurhash`

Returns the BlurHash string of the image.


|Parameter |Type |Description |
|---|---|---|
|`blurhash` |String |The BlurHash\-encoded string. |


**`blurhash`** ** example**

```JSON
{
    "success": true,
    "task_id": "amk-tool-probe-image-metadata-123459",
    "result": {
        "blurhash": "LGF5?x_N_3~q%M_3-;D%?b_3D%M{"
    },
    "request_id": "20240523100300AABBCCDDEEFF001155"
}
```


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro category of the error. For example, BadRequest. |
|`message` |String |A detailed description of the error, useful for development and debugging. |


<span id="error-handling"></span>
##

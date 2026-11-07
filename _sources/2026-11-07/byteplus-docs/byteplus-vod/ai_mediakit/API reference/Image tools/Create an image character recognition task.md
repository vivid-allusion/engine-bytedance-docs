---
title: "Create an image character recognition task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/image-ocr`

To synchronously extract text from an image, you can use this API. It offers two versions to meet different needs: a standard version for general printed Chinese and English text, and an advanced version that recognizes both printed and handwritten text in over 100 languages. The advanced version also supports specialized tasks like keyword matching, making it ideal for scenarios such as extracting specific fields from invoices. The API returns the recognized text content, its position coordinates, and a confidence score.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For complete application examples and usage instructions, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-character-recognition">Image Character Recognition</a>.</div>


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
|`image_url` |String |Yes |`https://example.com/document.png` |The URL of the image to recognize.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Input image resolution:<br><br>   * The short side must not exceed 2160 px.<br><br>   * The long side must not exceed 3840 px.<br><br>* File size: Each image must not exceed 10 MB.<br><br>* Supported formats: `.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic` are supported.<br><br>* Image quality recommendations: For the best recognition results and performance:<br><br>   * Image orientation: Avoid images rotated by more than 30 degrees, to prevent poor recognition results or processing timeouts.<br><br>   * Text density: For images with extremely high text density (such as a densely laid\-out full page), split the image before submitting it for recognition, to avoid timeouts caused by processing too much content. |
|`tool_version` |String |No |`standard` |The model version to use for recognition. Defaults to `standard`.<br><br><br>* `standard`: Standard version, provides general printed\-text recognition and supports Simplified Chinese and English.<br><br>* `max`: Advanced version, delivers higher recognition accuracy and supports a wider range of scenarios:<br><br>   * Supports both general text recognition and keyword matching recognition.<br><br>   * Recognizes both printed and handwritten text.<br><br>   * Supports 100+ languages, with optimal performance for Chinese and English, followed by 13 common languages: German, French, Turkish, Vietnamese, Korean, Malay, Portuguese, Russian, Spanish, Indonesian, Thai, Italian, and Japanese. |
|`task_type` |String |No |`spotting` |The recognition task type. Takes effect only when `tool_version` is `max`. Defaults to `spotting`.<br><br><br>* `spotting`: General text recognition, recognizes text content and coordinates line by line; the result is returned through `ocr_result`.<br><br>* `keyword`: Keyword matching recognition, retrieves matching text according to `max_keywords`; the result is returned through `keyword_result`. |
|`max_keywords` |Array |No |`["Invoice number", "Amount"]` |The keyword matching list. Takes effect, and is required, only when `tool_version` is `max` and `task_type` is `keyword`. Each element of the array is a keyword string to search for. The array must contain at least one element. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

<span id="example-1-standard-general-text-recognition"></span>
### Example 1: Standard general text recognition

The following example submits an image for standard text recognition.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/image-ocr' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/screenshot_with_text.jpg"
}'
```


<span id="example-2-advanced-invoice-recognition"></span>
### Example 2: Advanced invoice recognition

The following example uses the keyword matching feature of the advanced version to extract specified key fields from an invoice image.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/image-ocr' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/invoice.jpg",
  "tool_version": "max",
  "task_type": "keyword",
  "max_keywords": [
    "Invoice number",
    "Invoice date",
    "Seller",
    "Buyer",
    "Amount",
    "Tax",
    "Total"
  ]
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
|`result` |Object |An object containing the image processing result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task#the-result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds and has a result. |
|`queue_id` |String |The ID of the queue to which the task was submitted. |


<span id="the-result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`ocr_result` |Array |The general text recognition result list. Returned for the standard version or for the advanced version when `task_type=spotting`. Each object represents a recognized text block. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task#the-result-object) below. |
|`keyword_result` |Object |The keyword matching recognition result. Returned only for the advanced version when `task_type=keyword`. The keys of the object are the keywords you passed in, and the values are the recognized matching text (String). |


<span id="the-text-block-object"></span>
#### The text block object


|Parameter |Type |Description |
|---|---|---|
|`content` |String |The recognized text content. |
|`confidence` |Number |The confidence of the recognition result, in the range `[0, 1]`; a higher value indicates a more reliable result. **Returned only by the standard version.**  |
|`top_left_x` |Number |The x\-coordinate of the top\-left corner of the text box, in px. |
|`top_left_y` |Number |The y\-coordinate of the top\-left corner of the text box, in px. |
|`bottom_right_x` |Number |The x\-coordinate of the bottom\-right corner of the text box, in px. |
|`bottom_right_y` |Number |The y\-coordinate of the bottom\-right corner of the text box, in px. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error. For example: `BadRequest`. |
|`message` |String |A detailed description of the error, useful for debugging. |
|`param` |String |(Optional) The specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

Standard / general text recognition success response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-image-ocr-1716290500",
    "task_type": "image-ocr",
    "result": {
        "ocr_result": [
            {
                "content": "AI MediaKit",
                "confidence": 0.998,
                "top_left_x": 100,
                "top_left_y": 50,
                "bottom_right_x": 350,
                "bottom_right_y": 100
            },
            {
                "content": "Media processing platform",
                "confidence": 0.985,
                "top_left_x": 102,
                "top_left_y": 120,
                "bottom_right_x": 348,
                "bottom_right_y": 170
            }
        ]
    },
    "request_id": "20240521184140AABBCCDDEEFF112233",
    "expires_at": 1778573984,
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Advanced keyword matching recognition (`task_type=keyword`) success response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-image-ocr-1716290600",
    "task_type": "image-ocr",
    "result": {
        "keyword_result": {
            "Invoice number": "No.01234567",
            "Invoice date": "2026-08-01",
            "Seller": "Example Pte. Ltd.",
            "Total": "USD 1,280.00"
        }
    },
    "request_id": "20240521184240AABBCCDDEEFF223344",
    "expires_at": 1778573984,
    "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```


Failure response:

```JSON
{
  "success": false,
  "task_type": "image-ocr",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'image_url' is required and cannot be empty.",
    "param": "image_url",
    "type": "BadRequest"
  },
  "request_id": "20240521184200AABBCCDDEEFF445566",
  "queue_id": "q2a028fa533b7fe6a25b018dccd6284"
}
```

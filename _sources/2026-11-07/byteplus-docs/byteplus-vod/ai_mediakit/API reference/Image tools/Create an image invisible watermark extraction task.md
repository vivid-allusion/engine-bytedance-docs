---
title: "Create an image invisible watermark extraction task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/extract-image-invisible-watermark`

To verify content ownership or trace distribution, you can use this synchronous API to extract invisible watermarks from an image. The API recognizes whether a watermark is present and restores the originally embedded text content, making it suitable for copyright protection, AIGC content recognition, distribution\-leak tracing, and content\-theft evidence collection.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete workflow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-invisible-watermark">Image invisible watermark</a>.</div>


<span id="limits"></span>
## Limits

This API only supports extracting watermarks embedded by the [Create an image invisible watermark add task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-add-task) API and the `tool_version` used for extraction must be the same as the version used when adding the watermark. It cannot extract any form of invisible watermark added by third\-party tools.

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
|`image_url` |String |Yes |`https://example.com/watermarked_output.png` |The URL of the image from which to extract the invisible watermark.<br><br><br>* Image source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common mainstream image formats such as `.png`, `.jpg`, `.jpeg`, and `.webp` are supported. |
|`tool_version` |String |Yes |`adapt` |The invisible watermark model version. Must be the same as the version used when adding the watermark; otherwise the watermark may not be extracted correctly. Supported values:<br><br><br>* `adapt`: A text\-embedding model for AIGC scenarios. It can resist attacks such as a certain degree of resolution scaling, cropping, and compression, and is recommended when the watermark was added to an AIGC\-generated color image.<br><br>* `adapt_resize`: A text\-embedding model for content\-theft evidence collection. It resists image scaling and compression attacks more effectively, and is suitable for evidence collection in large\-scale image theft. |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-example"></span>
## Request example

The following example extracts the invisible watermark content from an image that already contains a watermark, with `tool_version` set to the same value used when the watermark was added (`adapt`).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/extract-image-invisible-watermark' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "image_url": "https://example.com/watermarked_output.png",
  "tool_version": "adapt"
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
|`result` |Object |An object containing the extraction result. Returned only when `success` is `true`. For details, see [The result object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task#the-result-object) below. |
|`error` |Object |The error details object. Returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-invisible-watermark-extraction-task#the-error-object) below. |
|`task_id` |String |The unique identifier for the task. |
|`task_type` |String |The task type. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`expires_at` |Integer |The expiration timestamp of the task result (Unix time, in seconds). Returned only when the task succeeds. |


<span id="the-result-object"></span>
#### The result object


|Parameter |Type |Description |
|---|---|---|
|`watermark_content` |String |The extracted invisible watermark text content. If no invisible watermark is extracted, an empty string is returned. |


<span id="the-error-object"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code, used to programmatically identify the error type. For example: `InvalidParameter`. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The error category. For example: `BadRequest`. |
|`message` |String |A detailed description of the error, useful for debugging. |
|`param` |String |(Optional) The specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

Success response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-extract-image-invisible-watermark-1703201",
    "task_type": "extract-image-invisible-watermark",
    "result": {
        "watermark_content": "copyright-2026"
    },
    "request_id": "20260415150030F6DE4C24A6A0D94B7FF2",
    "expires_at": 1778573984
}
```


Failure response:

```JSON
{
  "success": false,
  "task_type": "extract-image-invisible-watermark",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter 'tool_version' is required and cannot be empty.",
    "param": "tool_version",
    "type": "BadRequest"
  },
  "request_id": "20240521184200AABBCCDDEEFF445566"
}
```

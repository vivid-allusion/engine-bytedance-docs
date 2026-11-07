---
title: "Image character recognition"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-image-character-recognition"
---

To extract text from images such as scanned documents, screenshots, or posters, you can use the AI MediaKit image character recognition tool. The tool provides two versions:


* Standard: Provides general recognition of printed Simplified Chinese and English text, and returns the content, coordinates, and confidence of each text block.

* Advanced: Delivers higher recognition accuracy and supports a wider range of scenarios than the standard version.


This guide demonstrates how to perform this task with a single synchronous API call, allowing you to quickly obtain the editable content, position coordinates, and confidence of each recognized text block.

<span id="quickstart-recognize-text-in-an-image"></span>
## Quickstart: Recognize text in an image

Image character recognition is a **synchronous task**; the request you submit returns the recognition result directly in the response, so no polling is required.

<span id="prerequisites"></span>
### Prerequisites


1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key** (used to authenticate media processing features).

2. **Prepare an image file**: Prepare an image that contains text, and make it accessible via a public HTTP/HTTPS URL by uploading it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).


<span id="procedure"></span>
### Procedure

You only need to call the [Create an image character recognition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task) API to obtain the recognized text directly in the API response body.

<span id="step-1-submit-the-task-and-get-the-result"></span>
#### Step 1: Submit the task and get the result

You can copy the following cURL command to submit a text recognition task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/image-ocr' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "image_url": "https://example.com/screenshot_with_text.jpg"
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace <code>image_url</code> with the actual URL of your image.</div>



<span id="step-2-review-the-response"></span>
#### Step 2: Review the response

Because this is a synchronous API, you will immediately receive a response containing the final result after a successful request. All recognized text is contained in the `result.ocr_result` array.

```JSON
{
    "success": true,
    "task_id": "amk-tool-image-ocr-1716290500",
    "request_id": "20240521184140AABBCCDDEEFF112233",
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
    }
}
```


<span id="advanced-usage"></span>
## Advanced usage

<span id="choose-a-recognition-version-tool-version"></span>
### Choose a recognition version (`tool_version`)

You can choose a recognition version using the `tool_version` parameter when submitting a task:


|Version |`tool_version` value |Capabilities |
|---|---|---|
|Standard |`standard` (default) |Provides general recognition of printed text in Simplified Chinese and English, and returns the content, coordinates, and confidence of each text block. |
|Advanced |`max` |Delivers higher recognition accuracy and supports a wider range of scenarios than the standard version:<br><br><br>* In addition to general text recognition, it supports keyword matching recognition, which retrieves and returns matching text from an image according to the keywords you specify.<br><br>* It recognizes both printed and handwritten text.<br><br>* It supports 100+ languages, with the best results for Chinese and English, followed by 13 common languages: German, French, Turkish, Vietnamese, Korean, Malay, Portuguese, Russian, Spanish, Indonesian, Thai, Italian, and Japanese. |


> The `confidence` field is returned only by the standard version.


<span id="example-use-the-advanced-version-for-keyword-matching-recognition"></span>
### Example: Use the advanced version for keyword matching recognition

When you only need to extract fixed fields from a specific type of image (such as a receipt or a certificate), set `task_type` to `keyword`, and pass the list of keywords to search for using `max_keywords`. The recognition result is returned in `result.keyword_result`.

The following example shows how to extract key information from an invoice image:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools-sync/image-ocr' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
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


A response example for keyword matching recognition is as follows:

```JSON
{
    "success": true,
    "task_id": "amk-tool-image-ocr-1716290600",
    "request_id": "20240521184240AABBCCDDEEFF223344",
    "result": {
        "keyword_result": {
            "Invoice number": "No.01234567",
            "Invoice date": "2026-08-01",
            "Seller": "Example Pte. Ltd.",
            "Buyer": "Sample Company Inc.",
            "Total": "USD 1,280.00"
        }
    }
}
```


<span id="reference"></span>
## Reference

<span id="use-cases"></span>
### Use cases


* **Credential verification**: In industries such as banking, credit, retail, and e\-commerce, recognize and verify certificates such as business licenses and trademark certificates. This helps reduce labor costs, improve review efficiency, and effectively lower business risk.

* **Content moderation and management**: On social and e\-commerce platforms, recognize non\-compliant text in images, such as abusive, pornographic, or violent content. This helps quickly locate and review problematic images, thereby effectively avoiding business risk.

* **Digitizing paper documents**: Quickly digitize the content of printed materials such as books, papers, archives, and presentations. Recognizing and organizing text from paper documents makes it easier for schools, libraries, enterprises, and public institutions to enter data, improving the efficiency of content organization.


<span id="limits"></span>
### Limits


|Limit |Description |
|---|---|
|Input image source |Only publicly accessible HTTP/HTTPS URLs are supported. |
|Supported formats |`.png`, `.jpg`, `.jpeg`, `.webp`, `.tiff`, `.bmp`, and `.heic` are supported. |
|Supported languages |* **Standard version**: Simplified Chinese and English.<br><br>* **Advanced version**: 100+ languages, with the best results for Chinese and English, followed by 13 common languages: German, French, Turkish, Vietnamese, Korean, Malay, Portuguese, Russian, Spanish, Indonesian, Thai, Italian, and Japanese. |
|Image size |Each image must not exceed 10 MB. |
|Input image resolution |* The short side must not exceed 2160 px.<br><br>* The long side must not exceed 3840 px. |
|Image quality recommendations |For the best recognition results and performance:<br><br><br>* **Image orientation**: Avoid images rotated by more than 30 degrees, to prevent poor recognition results or processing timeouts.<br><br>* **Text density**: For images with extremely high text density (such as a densely laid\-out full page), split the image before submitting it for recognition, to avoid timeouts caused by processing too much content. |


<span id="related-api-documentation"></span>
## Related APIs


* [Create an image character recognition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-character-recognition-task)

---
title: "PDF Document Parsing (Doubao)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/pdf-document-parsing-doubao-22cb891fa6299267"
---

The document content parsing operator supports visual\-model parsing and structured Markdown output for PDF files, Word files (DOC and DOCX), and image files. It accurately parses blurry content, complex layouts, Traditional Chinese, and complex formulas. Word documents are first converted to PDF and then processed through the PDF parsing pipeline.

# Operator introduction

> Operator ID: las_pdf_parse_doubao

## Core capabilities

[video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dfc299cc04242df8879ee2e6dd0e0b3~tplv-goo7wpa0wc-image.image)

* Accurately parses blurry content, complex layouts, Traditional Chinese, and complex formulas, and returns high\-fidelity Markdown. Two parsing modes are available: normal and detail.

   * **normal mode**: Enabled by default. It is faster and suitable for most document scenarios.

   * **detail mode**: Performs more detailed analysis than normal mode, but takes longer and costs more.

* **Encrypted PDF parsing**: Supports PDFs protected with standard RC4, AES\-128, or AES\-256 password encryption. Provide the opening password through `password`.

* **Text recognition within images**: Enable image\-region text recognition through `enable_image_text`. Recognized content is returned as plain text in the corresponding image text block.

* Completely restores the source structure, including heading hierarchy, tables, formulas, and image areas.

   * Automatically identifies image areas and returns bounding\-box information and pre\-signed image URLs.

   * Supports per\-page and full\-document Markdown aggregation for downstream processing and display.

* **Supports intelligent long\-page segmentation**: When the width\-to\-height ratio of an input image or PDF page is lower than the threshold (default: `0.334`), the operator intelligently segments the page, parses each segment, and merges the results to improve parsing quality.

## Effect demonstration

---

**Example 1: PDF report parsing**

* Input example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95844c2805b04b2a96ba3e9432d93c47~tplv-goo7wpa0wc-topic.webp)

* Original input file

   [Multimodal Data Lake Solution White Paper.pdf](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0bfbdb17a90407fa869efda951cc53e~tplv-goo7wpa0wc-image.image)

* Parsing result example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daf2746175a045f2a02033fe0b965341~tplv-goo7wpa0wc-topic.webp)

* High\-fidelity result

   [Multimodal Data Lake Solution - Markdown parsing.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/586c118d53994811aa51f43f39127d8e~tplv-goo7wpa0wc-image.image)

---

**Example 2: Blurry content, ghosting, Traditional Chinese, and vertical layout**

* Input example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbca7ee3f2154e819edd84c0145defe2~tplv-goo7wpa0wc-topic.webp)

* Original input file

   [Writing and Reading.pdf](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/113be043d84240518f20f9f087171362~tplv-goo7wpa0wc-image.image)

* Parsing result example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df7df6dc8d11498d83826968c530a271~tplv-goo7wpa0wc-topic.webp)

* High\-fidelity result

   [Writing and Reading - Markdown parsing.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45c9ca34eece4891b6af0402ca7c8910~tplv-goo7wpa0wc-image.image)

---

**Example 3: Complex formulas**

* Input example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0078d000fab44778bf1b82d1a2338ed~tplv-goo7wpa0wc-topic.webp)

* Original input file

   [The Schrödinger Equation: The Core Language of Quantum Mechanics.pdf](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd8a30b9a61b4056a67a67fe2098386c~tplv-goo7wpa0wc-image.image)

* Parsing result example

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f69005f6ce064780b9d8731720a899f6~tplv-goo7wpa0wc-topic.webp)

> Use a Markdown editor that supports complex formula rendering to view this result.

* High\-fidelity result

   [The Schrödinger Equation - Markdown parsing.zip](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8c7fee54d474abba85ff0746521b09a~tplv-goo7wpa0wc-image.image)

---

## Supported region

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Breakdown item |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Processing time |* Total processing time depends on the number of pages and the network environment.<br><br>* Word documents must first be converted to PDF, which adds processing time.<br><br>* Long\-page segmentation introduces additional model calls and increases processing time.<br><br>* Enabling image\-region text recognition may increase model output. Processing time depends on the amount of text within images.<br><br>* Parsing time and resource usage increase significantly for documents with extremely high resolution or a large number of pages. |

# Input and output requirements

## Input requirements

|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |* Text (PDF and Word)<br><br>* Image |
|Input format: PDF |* Size: A single request can parse up to 400 pages, and the total file size must not exceed 1 GB.<br><br>   * For a document with more than 400 pages, use `start_page` and `num_pages` to parse it in multiple requests.<br><br>* Encryption: Standard password encryption using RC4, AES\-128, or AES\-256 is supported. Provide the correct opening password through `password`.<br><br>* Other requirements: Avoid PDF documents that contain complex dynamic objects.<br><br>   > **Note**<br>   <br><br>   > Only renderable page content is supported. Complex dynamic objects cannot be processed.<br>    |
|Input format: Word |* Format: DOC and DOCX. A Word document is first converted to PDF and then processed through the PDF parsing pipeline.<br><br>* Size: By default, a single Word file can be up to 100 MB. A request can parse up to 400 pages of the converted document.<br><br>* Other requirements: Encrypted Word documents and macro\-enabled DOCX documents are not supported. |
|Input format: Image |\* Format: Common image formats such as PNG, JPEG, BMP, and WebP. |
|Input path requirements |Provide input data through the `url` request parameter. Public URLs and TOS paths are supported.<br><br><br>* **Public URL**: A publicly accessible PDF, Word, or image URL in `http://` or `https://` format.<br><br>   * Public URLs that require a login session or additional header authentication are not supported. A temporary URL must remain valid while the task is running.<br><br>* **TOS path**: Upload the input data to a TOS bucket under the same primary account and in the same region as the current LAS service, and provide a path in the format `tos://bucket/path/file`.<br><br>   * The TOS object must exist, and the calling account must have read permission for it. |

## Output requirements

|Breakdown |Detailed requirements |
|---|---|
|Output data modalities |* Text (Markdown and JSON files)<br><br>* Image |
|Output path: TOS |Use the `output_tos_path` request parameter to specify where the operator stores output results. A TOS path is supported.<br><br><br>* **TOS path**: Specify a writable TOS bucket directory under the same primary account and in the same region as the current LAS service. The calling account must have write permission for the directory. Format: `tos://bucket/output/`.<br><br>* Output directory structure: The output contains `result.md`, `result_preview.md`, `images/`, and `detail.json`.<br><br>   ```text```<br>```   tos://bucket/output/{task_id}/```<br>```   ├── result.md```<br>```   ├── result_preview.md```<br>```   ├── images/```<br>```   │   ├── xxxx.png```<br>```   │   └── xxxx.png```<br>```   └── detail.json```<br>```   ```<br>    |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Usage is calculated from the number of pages after intelligent segmentation of the input PDF, converted Word document, or image.<br><br>> **Note**<br><br><br>> When an input PDF page or image is too long and its width\-to\-height ratio is below the threshold, LAS automatically segments and parses it. The `billable_pages` field returned by Poll is the number of pages after intelligent segmentation.<br> |
   |Billing type |Usage\-based billing in `USD/page`, with charges generated hourly based on actual billable usage. |
   |Unit price |The unit price depends on the selected PDF parsing mode. |

* Billing details

   Billing formula: `Total fee = Unit price × Usage`

   |Scenario |Unit price |
   |---|---|
   |PDF parsing mode: normal |0.006 USD/page |
   |PDF parsing mode: detail |0.015 USD/page |

# Cautions and prerequisites

|Breakdown item |Cautions and prerequisites |
|---|---|
|Enable LAS |Ensure that LAS is enabled for the BytePlus account before calling the operator. Enabling LAS without using billable features does not incur fees. |
|Costs |Review the applicable PDF parsing price for the BytePlus account before calling the operator. |
|Authentication (API Key) |Generate an LAS API Key and configure it as an environment variable before calling the operator. |
|Base URL |Use the Base URL for the region in which LAS is deployed. The examples below use the Asia Pacific (Johor) endpoint. |

# **API call**

## API call description

* This operator uses asynchronous APIs. Call Submit to create a task and obtain a `task_id`, and then call Poll with the `task_id` to query task status and results.

* A `task_id` remains valid for three days after submission. After three days, the task result can no longer be queried with that `task_id`.

## Submit

### Interface description

Call PDF Document Parsing (Doubao) to parse a PDF, Word (DOC or DOCX), or image file from a public URL or TOS path and obtain Markdown or structured output.

### Request parameters

**operator_id** string 必选 `Example value: las_pdf_parse_doubao`

Operator ID. Fixed to `las_pdf_parse_doubao`.

**operator_version** string 必选 `Example value: v1`

Operator version. Fixed to `v1`.

**data** PdfParseUserReqParams 必选

PDF parsing request parameters.

**url** string 必选 `Example value: https://example.com/file.pdf`

Downloadable source\-file URL. Supports PDF, Word (DOC and DOCX), and image formats (PNG, JPEG, BMP, and WebP). Supports `http://`, `https://`, and TOS paths in the format `tos://bucket/key`. The operator automatically detects the input type from the file header.

**password** string `Optional`

Password for opening a PDF document. Default: `null`. Provide the correct password for a password\-protected PDF. This parameter applies only to PDF input; encrypted Word documents remain unsupported. Supported standard encryption types are RC4, AES\-128, and AES\-256.

**start_page** integer `Optional` `Example value: 1`

Start page. `1` indicates the first page. Default: `1`.

**num_pages** integer `Optional`

Number of pages to parse. If omitted, 200 pages are parsed by default. If specified, up to 400 pages are supported.

**parse_mode** string `Optional` `Example value: normal`

Parsing mode for multilingual content, complex layouts, formulas, tables, and blurry pages.

* **normal**: Default. Faster and suitable for most documents.

* **detail**: Performs more detailed analysis based on normal mode, but takes longer.

**enable_image_text** boolean `Optional` `Example value: false`

Whether to recognize text within page image regions. Default: `false`. When `true`, recognized text is stored as plain text in the `text` field of detail text blocks whose `label` is `image`; the field may be empty if no text is recognized.

**output_tos_path** string `Optional` `Example value: tos://example-bucket/path/to/output/`

TOS directory for parsing artifacts. If omitted, artifacts are not written to a user\-specified TOS directory. The directory must be in a TOS bucket under the same primary account and in the same region as the LAS service, and the calling account must have write permission.

The following files are written for batch\-processing and persistence scenarios:

Directory structure: `tos://example-bucket/path/to/output/{task_id}/` containing `result.md`, `result_preview.md`, `images/`, and `detail.json`.

* `result.md`: Complete Markdown with relative links to images under `images/`.

* `result_preview.md`: Complete Markdown with temporary pre\-signed HTTPS image links.

* `images/`: Parsed image results.

* `detail.json`: Page\-by\-page parsing results.

**full_result** boolean `Optional` `Example value: true`

Whether to return the complete result. Default: `true`, in which case `markdown` and `detail` contain values. If set to `false`, `markdown` is an empty string and `detail` is an empty list, which is suitable when only artifact TOS paths are required.

**aspect_ratio_threshold** float `Optional` `Example value: 0.334`

Width\-to\-height ratio threshold for intelligent long\-page segmentation. If an input image or PDF page has a ratio below this value, the operator identifies it as a long page and segments it. Default: `0.334`.

### Response parameters

```mixin-react
const properties = ({
defaultExpandAllRows: true,
  "columns": [
    { "title": "Parameter", "dataIndex": "column_0", "key": "column_0", "width": 300 },
    { "title": "Type", "dataIndex": "column_1", "key": "column_1", "width": 180 },
    { "title": "Example value", "dataIndex": "column_2", "key": "column_2", "width": 300 },
    { "title": "Description", "dataIndex": "column_3", "key": "column_3", "width": 450 }
  ],
  "data": [
    {
      "key": 1,
      "column_0": "metadata",
      "column_1": "metadata",
      "column_2": "",
      "column_3": "Request metadata",
      "children": [
        {
          "key": 11,
          "column_0": "task_id",
          "column_1": "string",
          "column_2": "task-xxx",
          "column_3": "Asynchronous task ID used to query task status."
        },
        {
          "key": 12,
          "column_0": "task_status",
          "column_1": "string",
          "column_2": "PENDING",
          "column_3": <div>Asynchronous task status.<ul><li>PENDING: Request received</li><li>FAILED: Failed</li></ul></div>
        },
        {
          "key": 13,
          "column_0": "business_code",
          "column_1": "string",
          "column_2": "",
          "column_3": "Business code."
        },
        {
          "key": 14,
          "column_0": "error_msg",
          "column_1": "string",
          "column_2": "",
          "column_3": "Detailed error information when an exception occurs."
        }
      ]
    }
  ]
});
return <Table border={{ cell: true, wrapper: true }} pagination={false} {...properties} />;
```

### Example

#### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_pdf_parse_doubao",
  "operator_version": "v1",
  "data": {
    "url": "https://example.com/file.pdf"
  }
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "task-20261125163544-abc123",
    "task_status": "PENDING",
    "business_code": "200",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |Invalid model name. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication. |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API key. |

## Poll

### Interface description

Query the execution status and result of a document parsing task.

### Request parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|operator_id |string |Yes |las_pdf_parse_doubao |Operator ID. |
|operator_version |string |Yes |v1 |Operator version. |
|task_id |string |Yes |task\-xxx |Task ID. |

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Asynchronous task status:

* `PENDING`: The submitted task is queued.

* `RUNNING`: The task is running.

* `COMPLETED`: The task is completed.

* `FAILED`: The task failed.

* `TIMEOUT`: The task timed out.

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time in ISO 8601 format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time in ISO 8601 format.

**business_code** string `Example value: 200`

Business code.

**error_msg** string

Detailed error information when an exception occurs.

**data** PdfParseResponse

Returned data.

**markdown** string

Final merged Markdown content of all pages. If `full_result` is `false`, an empty string is returned. Image links are pre\-signed HTTPS links valid for three days.

**detail** list of page_detail

Page\-by\-page parsing details, including page Markdown, dimensions, and structured text blocks. When `enable_image_text=true`, image\-region text may be included. If `full_result` is `false`, an empty list is returned; complete details can be read from `detail.json` when `output_tos_path` is specified. Image links are pre\-signed HTTPS links valid for three days.

**page_id** integer `Example value: 1`

Page number, starting from `1`.

**page_md** string

Final Markdown for the current page, including bounding\-box\-to\-image replacement.

**page_image_hw** object `Example value: {"h":3508,"w":2480}`

Height and width of the rendered page image in pixels.

**text_blocks** list of text_block

Text blocks in reading order, including structured information for image placeholders.

**text** string

Text in normal or detail mode. For a block whose `label` is `image`, setting `enable_image_text=true` may return text recognized from the image region; when the option is disabled, text within images is not parsed.

**label** string `Example value: text`

`text` or `image` in normal or detail mode.

**box** object `Example value: {"x0":100,"y0":200,"x1":400,"y1":650}`

Coordinates in the original page. Values from 0 to 1000 are mapped proportionally by page width and height.

**norm_box** list of float `Example value: [0.1,0.2,0.4,0.65]`

Normalized bounding box, if available.

**url** string

Pre\-signed URL of the cropped image, valid for three days.

**page_split** page_split

Long\-page segmentation information. Returned only if the page triggers intelligent segmentation; otherwise, an empty object is returned.

**num_pieces** integer `Example value: 3`

Number of segments after splitting the page.

**piece_bboxes** list of object

Positional information for each segment in the original page, in segment order.

**box** object `Example value: {"x0":0,"y0":0,"x1":1000,"y1":333}`

Normalized coordinates of the segment in the original page, from 0 to 1000.

**artifacts** Artifacts

Artifact path information, including each artifact's TOS path or pre\-signed URL.

**markdown_tos_path** string `Example value: tos://example-bucket/path/to/output/{task_id}/result.md`

TOS path of `result.md`. Has a value only if `output_tos_path` is specified.

**detail_tos_path** string `Example value: tos://example-bucket/path/to/output/{task_id}/detail.json`

TOS path of `detail.json`. Has a value only if `output_tos_path` is specified.

**image_tos_path** string `Example value: tos://example-bucket/path/to/output/{task_id}/images/`

TOS path of the `images/` directory. Has a value only if `output_tos_path` is specified.

**result_preview_url** string

Pre\-signed URL of `result_preview.md`, valid for three days.

**num_pages** integer

Number of original pages successfully parsed in this request. Long\-page segmentation does not increase this value. For successfully parsed image input, this value is `1`.

**billable_pages** integer

Total number of billable pages after segmentation. If the input contains a page whose width\-to\-height ratio is below the threshold, the operator segments and parses the page separately. For a regular PDF or an image that does not require segmentation, this value equals `num_pages`.

**error** string

Error information when an exception occurs.

### Example

#### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_pdf_parse_doubao",
  "operator_version": "v1",
  "task_id": "task-20261125163544-abc123"
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "task-20261125163544-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "200",
    "error_msg": ""
  },
  "data": {
    "markdown": "My Little Puppy\nI have a cute little puppy at home. Its name is Xiaobai...",
    "detail": [
      {
        "page_id": 1,
        "page_md": "My Little Puppy\nI have a cute little puppy at home. Its name is Xiaobai...",
        "page_image_hw": {
          "h": 3508,
          "w": 2480
        },
        "text_blocks": [
          {
            "text": "My Little Puppy\nI have a cute little puppy at home. Its name is Xiaobai...",
            "label": "text",
            "box": {
              "x0": 100,
              "y0": 200,
              "x1": 400,
              "y1": 650
            },
            "norm_box": [0.1, 0.2, 0.4, 0.65]
          }
        ],
        "page_split": {}
      }
    ],
    "artifacts": {
      "markdown_tos_path": "",
      "image_tos_path": "",
      "detail_tos_path": "",
      "result_preview_url": "https://example.com/path/to/result_preview.md"
    },
    "num_pages": 1,
    "billable_pages": 1
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Model.InvalidName |The model name is invalid. |Invalid model name. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication. |
|401 |ApiKey.InValid |The api key is invalid. |Invalid API key. |
|400 |Url.Invalid |The url is invalid. |Invalid document URL. |
|400 |Pdf.Invalid |The pdf file is invalid. |Invalid PDF file. |
|400 |Pdf.PasswordRequired |PDF password is required. |The PDF requires an opening password. Provide it through `password`. |
|400 |Pdf.PasswordInvalid |PDF password is invalid. |PDF password authentication failed. Check `password`. |
|400 |Pdf.EncryptionUnsupported |PDF encryption scheme is unsupported. |The PDF uses an unsupported encryption type. Standard RC4, AES\-128, and AES\-256 password encryption are supported. |
|400 |Pdf.RenderFailed |PDF render failed. |PDF rendering failed. |
|400 |Pdf.ModelFailed |VLM call failed. |Visual\-model call failed. |
|400 |Pdf.Timeout |Pdf parse timeout. |PDF parsing timed out. |
|400 |Pdf.PagesExceeded |PDF pages exceeded maximum limit of 400. |The PDF exceeds the page limit. |
|400 |Pdf.PageRangeInvalid |Requested page range is out of bounds. |The requested page range exceeds the total number of document pages. |
|400 |Pdf.FileTooLarge |PDF file size exceeds maximum limit of 1GB. |The PDF exceeds the file\-size limit. |
|400 |Document.Unsupported |Unsupported document format. |Unsupported document format. |
|400 |Document.Invalid |Invalid document input. |The document is empty or corrupted. |
|400 |Word.Encrypted |Encrypted Word input is not supported. |Encrypted Word documents are not supported. |
|400 |Word.TooLarge |Word input exceeds the size limit. |The Word file exceeds the size limit. |
|400 |Word.ConversionFailed |Word conversion failed. |Failed to convert the Word document. |
|400 |Word.InvalidPDF |Converted PDF is invalid. |The PDF converted from Word is invalid. |
|400 |Word.Timeout |Word conversion timed out. |Word conversion timed out. |
|400 |Word.Busy |Word conversion queue timed out. |The Word conversion queue is busy. Try again later. |
|403 |Tos.AccessFailed |Failed to access TOS path. |Failed to access the TOS path. Check permissions for the input object or output directory. |

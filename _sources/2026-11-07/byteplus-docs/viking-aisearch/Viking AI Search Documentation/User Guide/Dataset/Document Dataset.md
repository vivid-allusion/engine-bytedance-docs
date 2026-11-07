---
title: "Document Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Document_Dataset"
---

&nbsp;

<span id="387066e0"></span>
# Introduction to Document Datasets

If you would like your conversational agent to assist users by leveraging your existing document knowledge — providing industry or platform\-specific information in the responses — you can use Document Datasets to import unstructured data and link them to your application.

Unlike Item Datasets which store structured data, Document Datasets support the storage and processing of **unstructured data** (document content). The following formats are currently supported:


* **formatted document data:**  files with pdf, doc, docx, ppt, pptx extensions

* **plain text document data:**  files with md, html, txt extensions

* **spreadsheet files:**  files with xlsx, xls, csv, jsonl extensions

* **Image files:**  bitmap files with extensions JPEG, PNG, WEBP, BMP, TIFF, ICO, DIB, ICNS, SGI, JPEG2000


&nbsp;

You can empower the following scenarios with document knowledge:


* **E\-commerce Shopping Guide:**  Import membership policies, after\-sales policies, product details, and promotion documents to help the Agent answer common questions about member benefits, return processes, and product specifications.

* **Vertical Content Search:**  Import industry\-specific knowledge to help the Agent understand and answer professional questions in a specific field, leading to better query interpretation and search planning.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">difference between spreadsheet files and item datasets</div>


<div data-tips="true" data-tips-type="default">While both are "structured data" with defined and fixed column formats, they serve different purposes in Viking AI Search:</div>



* <div data-tips="true" data-tips-type="default"><strong>Item Datasets:</strong> Used to build structured index data for <strong>Search and Recommendation</strong>. Fields can be designated for specific uses (semantic retrieval, precise filtering, user behavior preference analysis, etc.). If you want your data to be <strong>candidate content</strong> for search or recommendations, you <strong>must</strong> use an Item Dataset.</div>


* <div data-tips="true" data-tips-type="default"><strong>Spreadsheet Documents:</strong> Act as a <strong>Knowledge Base for Q&A</strong>. Suitable for uploading Q&A pairs, reviews, FAQs, or product manuals. These serve as a knowledge source for answering user questions in dialogue but <strong>cannot</strong> be used as search or recommendation candidates.</div>



<span id="951cd50a"></span>
# Create a Document Dataset

You can open the Document Dataset tab under Data Configuration in the application interface to create a document dataset and directly link it to the application, or create a document dataset under Application \> Dataset \> Document Dataset tab and manually link it to an application.

&nbsp;

After clicking create, you need to name the document dataset and import a batch of document files.

&nbsp;

The system will perform format and size validation during import. See [Document Format and Size Limits](https://docs.byteplus.com/docs/393/Document_Dataset#ac881958) for supported document formats and size limits.

You can also enable the document import feature on the Document Dataset detail page under Datasets.

<span id="3da42e78"></span>
# Document Processing and Storage

Once imported, the system automatically performs intelligent processing, including reading, parsing, slicing, index construction, and vector storage to ensure the content is searchable.

&nbsp;

Original documents will be processed into markdown format. Once processing is complete, you can click the `View` button to inspect the processed text content.

&nbsp;

<span id="5af47911"></span>
## Delete Documents

You can delete documents in both the application and dataset document interfaces. After clicking the `Delete` button, you will be asked to confirm the sensitive operation. Click `Confirm` to delete the document.

&nbsp;

<span id="ac881958"></span>
# Document Format and Size Limits

Document data features are currently available for free during the Beta phase. We support uploading and processing the following document types:


|**Document Type** |**Size Limit** |
|---|---|
|**pdf** |A single document must not exceed 100MB or 1000 pages |
|**doc** |A single document must not exceed 100MB or 1000 pages |
|**docx** |A single document must not exceed 100MB or 1000 pages |
|**ppt** |A single document must not exceed 100MB or 1000 pages |
|**pptx** |A single document must not exceed 100MB or 1000 pages |
|**markdown** |Single document no larger than 5 MB |
|**txt** |Single document no larger than 5 MB |
|**html** |Single document no larger than 5 MB |
|**xlsx** |No more than 50 sheets, total rows no more than 30,000 |
|**xls** |No more than 50 sheets, total rows no more than 30,000 |
|**jsonl** |30,000 lines, no line exceeding 65,535 characters |
|**Image files (JPEG, PNG, WEBP, BMP, TIFF, ICO, DIB, ICNS, SGI, JPEG2000)**  |Single file size no larger than 8MB<br><br><br>* Aspect ratio (width/height): limited to the range [1/100, 100]<br><br>* Side length limited to the range [10, 6000] pixels |


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/doc_preview_overview"
---

TOS allows you to preview documents stored in it in image, PDF, or HTML format. This topic covers billing notes, constraints, limitations, and ways to preview documents.

<span id="ae830061"></span>
## Billing notes


* This feature is currently in closed beta. Please contact your account manager for access.

* You can preview documents in image, PDF, or HTML format. Billing varies by preview format. Specifically:

   * Image or PDF: Costs are based on the number of images or PDF pages converted for preview.

   * HTML: Costs are based on the number of previews.

      For billing details, see [Data processing](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).

* Data retrieval fees will apply when previewing documents stored in Infrequent Access Storage or Flashback Archive. These fees are calculated based on file size. For more information, see [Data retrievals](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Constraints and limitations


|**Category** |Description |
|---|---|
|File type |The following file types are supported for preview:<br><br><br>* Presentation files: PPTX and PPT.<br><br>* Word processing files: DOCX and DOC.<br><br>* Spreadsheet files: XLSX and XLS.<br><br>* Others: PDF. |
|Output format |The following output formats are supported: PNG, JPG, PDF, and HTML.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Starting from October 18, 2022, for security and compliance reasons, if you use the bucket's default domain to access web page files with the MIME type text/html and extensions including .htm, .html, .jsp, .plg, .htx, and .stm, the response header will automatically include <code>Content-Disposition:attachment</code>. This means that, when you access web page files via a browser, the website will not preview the content directly. Instead, the content will be downloaded locally.</div><br> |
|File size |The maximum size of a file that can be previewed is 200 MB. |
|Spreadsheet files |When you preview a spreadsheet file in image format, one sheet can be split into multiple images. |
|Server\-side encryption |You can use TOS to preview documents encrypted with SSE\-TOS, SSE\-C, or SSE\-KMS, but there are some limitations to consider:<br><br><br>* When previewing a document encrypted with SSE\-C, you must include the following SSE\-C request headers: `x-tos-server-side-encryption-customer-algorithm`, `x-tos-server-side-encryption-customer-key`, and `x-tos-server-side-encryption-customer-key-MD5`. For more information on SSE\-C headers, see [Using server-side encryption with customer-provided keys (SSE-C)](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview#.5L2_55So55So5oi35o-Q5L6b5a-G6ZKl55qE5pyN5Yqh56uv5Yqg5a-G77yIc3NlLWPvvIk=).<br><br>* You cannot preview documents encrypted with SSE\-KMS via anonymous access. To preview SSE\-KMS\-encrypted documents, you must activate Key Management Service (KMS) and have permission to access the master key. Requests must also be signed using valid credentials. You can use pre\-signed URLs, APIs, or SDKs for this purpose. For more information, see the Using REST APIs section below. |


<span id=".5paH5qGj6aKE6KeI5pa55byP"></span>
## Document preview methods

You can use REST APIs or file URLs to preview documents stored in TOS buckets. TOS lets you preview them as images, PDFs, or HTML.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The processed results are returned immediately and are not saved in your bucket.</div>



* Using REST APIs 

   ```Plain
   GET /example.docx?x-tos-process=doc-preview&x-tos-doc-src-type=docx&x-tos-doc-dst-type=jpg&x-tos-doc-page=1 HTTP/1.1
   Host: endpoint
   X-Tos-Content-Sha256: sha256
   X-Tos-Date: 20220827T132948Z
   Authorization: authorization
   ```
   

* Using file URLs

   `http://bucket.endpoint/example.docx?x-tos-process=doc-preview&x-tos-doc-src-type=docx&x-tos-doc-dst-type=jpg&x-tos-doc-page=1`

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To preview private files, use SDKs to generate pre\-signed URLs that contain the document preview parameter.   </div>
   

<span id="tMAsbZN7"></span>
## Document preview features


|**Feature** |**Parameter** |**Description** |
|---|---|---|
|[Document preview](https://docs.byteplus.com/docs/tos/Doc_preview) |doc\-preview |Displays documents stored in TOS buckets as images, PDFs, or HTML without opening them. |

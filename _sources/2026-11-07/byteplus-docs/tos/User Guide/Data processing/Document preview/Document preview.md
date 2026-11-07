---
title: "Document preview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Doc_preview"
---

The document preview (doc\-preview) feature lets you see document files stored in a bucket online without opening them. This topic introduces the parameters and provides examples of the document preview feature.

<span id="1fb30753"></span>
## Notes


* This feature is currently in closed beta. Please contact your account manager for access.

* You must use custom domains to preview documents in buckets created after January 3, 2024, due to restrictions on domain names. For instructions, see [Setting up a custom domain](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For buckets created after January 3, 2024, accessing objects via the default domain name—whether through a presigned URL or anonymous access—will cause TOS to download the object directly to your device rather than providing an online preview.    </div>
   

<span id=".5Y-C5pWw6K-05piO"></span>
## Supported parameters

<span id="716bac60"></span>
### Request parameters


|**Parameter** |Description |**Value** |**Required** |
|---|---|---|---|
|x\-tos\-doc\-src\-type |Specifies the type of file you want to preview.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, TOS uses the file name extension of an object to determine its source data type during file conversion. This parameter must be specified if an object lacks a file name extension.</div><br> |pptx, ppt, doc, docx, xls, xlsx, and pdf. |No |
|x\-tos\-doc\-dst\-type |Specifies the output format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you preview a spreadsheet file as images, one sheet can be split into several images during conversion.</div><br> |png, jpg, pdf, and html.<br><br>The default value is jpg. |No |
|x\-tos\-doc\-page |Specifies the page number to be converted when the output format is an image.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>page</code> parameter does not apply when the output format is <code>pdf</code> or <code>html</code> because page selection is unavailable for those formats.</div><br> |[1,5000]<br><br>The default value is 1. |No |
|x\-tos\-doc\-image\-dpi |Renders the image at the specified DPI. This parameter only applies when the output format is png or jpg.<br><br>Setting a low value decreases processing time, whereas setting a high value increases it. |[96\-600]<br><br>The default value is 300. |No |
|x\-tos\-doc\-image\-quality |Specifies the quality of the transcoded image.<br><br>For example, a value of 90 indicates 90% image quality. |[1,100]<br><br>The default value is 90. |No |


<span id="c6b66355"></span>
### Response fields


|Field |Description |**Value** |
|---|---|---|
|content\-type |Returns a value based on the actual format of the image. |image/jpeg, image/png, application/pdf, and text/html. |
|x\-tos\-total\-page |Returns the total number of pages in the document. For spreadsheet files, the value of this field indicates the total number of images converted from the current sheet. |\- |


<span id=".56S65L6L"></span>
##

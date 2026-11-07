---
title: "Document Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Document_Processing_"
---

<span id="8dda752e"></span>
# Feature Overview

Document processing involves the use of automated technology to parse document files in multiple formats (e.g. PDF, Word, PPT, HTML, etc.), and to extract, organize, and structure their content. The core goal is to convert the unstructured or semi\-structured information contained in various documents (including text, tables, images, metadata, etc.) into standardized and structured data that can be directly used by downstream systems (such as knowledge bases, search engines, and large language model applications). This article will introduce you to document processing operators.

<span id="c3da3445"></span>
# Operator Introduction

<span id="6db9e6b9"></span>
## **Knowledge segmentation**

Unstructured data can be segmented, text segmentation, text segmentation support related configuration, can be [Import Knowledge Engine](https://docs.byteplus.com/docs/dataagent/Import_Knowledge_Engine)used together, the segmented knowledge into the corresponding knowledge base after slicing.

<span id="90e233be"></span>
### **Operating instructions**

Click the plus sign + and select **Document Processing \> Knowledge Segmentation** operator in Visual Knowledge Processing to segment the data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f94a77c97b8454f8a3d519deec55645~tplv-goo7wpa0wc-image.image) </span>

The specific parameter configuration instructions are as follows:


|Parameter |Explain |
|---|---|
|File address |Take the value from the specified field upstream, the content is generally the address of the TOS file, and the following types of file parsing are supported: pdf, docx, doc, txt, markdown, html, pptx, image, xlsx, email, etc |
|Sliced elements |* Picture: After checking the picture, the content of the knowledge answer will include pictures; if the picture is not checked, the content of the answer will not include picture information.<br><br>* Form: After checking the form, slice the form and recall it according to the slice; if the form is not checked, the form is recalled as a whole. |
|Slicing strategy |* Automatic slicing: Using a general slicing strategy, the model automatically recognizes the document according to the document structure for slicing.<br><br>* Custom slicing: Support custom length, rules, and scene slicing that is closer to business custom rules. You need to set the single slice length and slice rules. |
|Single slice length |Sliced segment size, support selecting the slice size of 1000 characters, 2000 characters, 3000 characters, 4000 characters through the drop\-down box. |
|Slicing rule |Select a symbol for the slice, such as a newline, 2 newlines, Chinese period, Chinese exclamation mark, English period, and English exclamation mark. |
|Output field |The new column name after segmentation, the default value is chunk_result, generally does not need to be changed |


<span id="bdb183c0"></span>
## **Intelligent parsing of PDF documents**

Supports PDF for deep analysis and structured processing. Through layout analysis and text recognition, key information such as text, tables, and pictures in PDF and images are extracted in the order of reading, and finally organized into semi\-structured documents with semantic information and logical structure, and returned in Markdown format.

<span id="04a3544e"></span>
### Operating instructions


1. Click the plus sign + and select **Document Processing \> PDF Document Intelligent Parsing** Operator in Visual Knowledge Processing.

2. Input configuration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92f8789f66e44d1ca3e1ff13ded656a9~tplv-goo7wpa0wc-image.image) </span>

   * Input type: Select file URL address or file base64\-bit encoding.

   * PDF fields: Select the PDF fields to use.

3. Parse configuration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cbafb9f946544b5bd481d13a314b6bf~tplv-goo7wpa0wc-image.image) </span>

   * Start page number: Notes, default values are shown in the figure. (Determined according to technical selection)

   * Parse the number of pages: comments, default values are shown in the figure. (Determined according to technical selection)

4. Advanced configuration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237773ec128f4a23be2cfa9793ff7006~tplv-goo7wpa0wc-image.image) </span>

   The specific parameters are described as follows:

   
   |Configuration item |Explain |
   |---|---|
   |Concurrency |Sets the number of concurrent tasks handled by the node. This field is required.<br><br>Default value: 5 |
   |Polling interval |Sets the time interval for each polling task. The unit is milliseconds.<br><br>Default value: 3000 |
   |Maximum wait time |Sets the maximum wait time for fetching data, beyond which the task will be interrupted. The unit is milliseconds.<br><br>Default value: 300000 |
   |Exception handling |Select the handling method when an exception occurs in the execution of the task. This field is required.<br><br>Optional values:<br><br><br>* Ignore: Ignore the exception and continue with subsequent tasks.<br><br>* Throw: Throws an exception to interrupt task execution. |
   

5. Output configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad828e08bbdf4a518f74043e90e9bf91~tplv-goo7wpa0wc-image.image) </span>

   Output field: Custom output field, default pdf_content. The first space is not supported, the rest are supported, no more than 64 characters.

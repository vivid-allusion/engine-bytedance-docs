---
title: "Knowledge base"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/knowledge-base"
---

The ByteHouse Knowledge Base feature supports uploading your own knowledge base, offering a complete process for knowledge creation, management, and intelligent application. It ensures data security through fine\-grained permission management and suits scenarios such as enterprise business knowledge management and intelligent Q&A support. This tutorial provides a detailed explanation of operations including knowledge base creation, document upload, recall testing, permission management, and intelligent assistant configuration.

<span id="f85c2365"></span>
# Feature Overview

The ByteHouse Knowledge Base is a knowledge management feature designed for enterprises. It integrates business and industry knowledge storage, achieves efficient knowledge utilization through vectorization, semantic search, and QA generation, and supports permission control and effectiveness assessment. Key capabilities include:


* **Enterprise Business Knowledge Management**: ByteHouse builds a default knowledge base based on official documents and also supports uploading and managing enterprise\-specific business and industry knowledge. It provides core functions such as document vector storage, semantic retrieval, and automatic QA generation. After importing knowledge, basic management, such as enabling/disabling and detailed operations like re\-segmentation and adding new paragraphs, can be performed to facilitate efficient knowledge consolidation and easy access.

* **Recall Testing**: ByteHouse allows testing recall of uploaded knowledge to visually evaluate the knowledge base’s coverage and retrieval effectiveness for relevant information, assisting in optimizing knowledge management strategies.

* **Permission Management**: ByteHouse offers fine\-grained permission control, supporting configuration of knowledge base creation, viewing, and management permissions for users or roles, ensuring knowledge data security and control.


<span id="616ed18f"></span>
# Usage restrictions

This feature is in Beta. To use it, submit a support ticket or contact the ByteHouse team to obtain whitelist access.

<span id="e99bf05e"></span>
# Preparation

Prepare the knowledge data you need to upload. ByteHouse currently supports uploading .md format documents with a single file size not exceeding 200 MB.

<span id="ab13513a"></span>
# Quick start: Create and import a knowledge base

<span id="838c7605"></span>
## Step 1: Create a knowledge base


1. Log in to the ByteHouse cloud warehouse console, click the \*\*Diagnostic Analysis \*\*tab, then click **Knowledge base** to enter the knowledge base management interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09395612cc604071bac4468b594ec604~tplv-goo7wpa0wc-image.image) </span>

2. Click the  **+**  **Knowledge base** button to create a knowledge base. In the new knowledge base dialog, fill in the name and description, select the embedding model, then click **Create**. The system will create and activate the knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3f53964abf34d48b599e3f343bd56ce~tplv-goo7wpa0wc-image.image) </span>

   * The embedding model converts natural language into vectors for semantic search and QA generation.

3. After the interface displays “**Creation of Knowledge Base Successful**,” you can view the created knowledge bases in the knowledge base management interface.


<span id="c17a1d94"></span>
## Step 2: Import knowledge


1. Click the knowledge base card to enter the details page, then click the **Document** button to upload documents.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72e8a6d088104d2c9d216f07c1c0bbd4~tplv-goo7wpa0wc-image.image) </span>

2. Click the  **+ button** to upload documents, select the segmentation method as needed, and click **OK**. The system will upload the documents according to the configuration and segment them accordingly.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d996992d13f4532906b4e70dcca9a02~tplv-goo7wpa0wc-image.image) </span>

   Segmentation refers to the method of dividing uploaded documents into different sections. Proper segmentation helps improve the knowledge base’s management and retrieval efficiency of document content, making it easier to quickly locate and access related information based on your needs. ByteHouse currently supports two segmentation methods: title hierarchy and text block size. The detailed explanations are as follows:

   
   |Segmentation Method |Segmentation Description |
   |---|---|
   |By Title Hierarchy |segments the document by its title structure. This applies to documents with clear heading systems (such as multi\-level titles or chapter divisions). Common scenarios include structured documents, preserving content context, and retrieving or reusing document structures by chapters.<br><br>\*\*Hierarchical segmentation \*\*specifies the heading level used for segmentation (e.g., level 1 heading, level 2 heading). The system automatically splits the document based on the selected heading level, with each segment containing the full content under that heading. for example, choosing "level 3 heading" for segmentation splits the document into multiple independent segments based on all level 3 headings. |
   |By Text Block Size |cuts the document into roughly equal\-length independent text blocks based on a set text length. This applies to documents without clear heading structure or those requiring precise keyword matching. Common scenarios include unstructured documents, high\-frequency short keyword matching, or very long documents needing controlled segment length.<br><br><br>* **Suggested Text Block Size**: Set the text length value according to your needs. This value determines approximately how many characters or bytes each segment contains. For example, if set to 1000 bytes, the system will try to split the document according to this length, but the actual length may vary slightly depending on the document's content.<br><br>* **Segment identifier**: It refers to the symbol or character combination used to mark text block boundaries when segmenting by text block size. The system divides content before and after the identifier into different segments. For example, if you use `\\n\\n` as the segmentation identifier, all `\\n\\n` in the document will serve as segment boundaries. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can choose to segment directly with the current recommended parameters or customize parameters before segmenting. You can reconfigure segmentation at any time later; uploaded original files will be retained for 5 days, after which resegmenting the document will no longer be possible.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The current maximum number of segments supported by ByteHouse is 4096. If your chosen segmentation method causes the segment count to exceed 4096, the system will fail to parse and display an error message. You can click <strong>Retry</strong> to resegment the document. The error message is shown as follows:   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7324b871b2040a1a4a27c6bfa0fc21e~tplv-goo7wpa0wc-image.image" width="2900px" />   </div>
   

3. After parsing is complete, you can view the document in the document list with the parsing status as “**Finished**.” If your document is large, the system may take longer to process it. Please wait patiently. If parsing fails, the system will provide the reason, allowing you to take corresponding measures based on it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43a9e01eb80d4ddbac26bbf12c243b91~tplv-goo7wpa0wc-image.image) </span>

4. You can click **document name** to view segment details. If the current segment content does not meet your needs, you can [Resegment](https://docs.byteplus.com/docs/bytehouse/knowledge-base#4bc374b2) for knowledge or [Add paragraph](https://docs.byteplus.com/docs/bytehouse/knowledge-base#61e49762).


<span id="702f60ca"></span>
## Step 3: Recall testing

In ByteHouse, recall testing evaluates the system’s ability to accurately retrieve all segments related to user queries from the documents uploaded to the knowledge base. This test verifies whether ByteHouse can comprehensively extract keyword\-related text snippets from uploaded documents, avoiding the omission of key information.

**Instructions**:


1. On the knowledge base detail page, click **Recall testing** to enter the testing page.

2. Enter the keywords to test in the keyword input box, then click **Test**.

3. The system will recall related paragraphs based on your keywords, and you can view the corresponding segments and recall rate. The higher the recall rate, the fewer relevant information the system misses. If recall rate is low, you can refer to the operations in [Resegment](https://docs.byteplus.com/docs/bytehouse/knowledge-base#4bc374b2) to re\-segment the knowledge.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ecce2ecc3514796b3f4534b00bc405d~tplv-goo7wpa0wc-image.image) </span>


<span id="08a612b3"></span>
## Step 4: Select the knowledge base for the intelligent assistant

Once the knowledge base is created, it is enabled by default. The intelligent assistant will read the knowledge base you created. You can select and link the knowledge base as needed, helping you better use ByteHouse in line with business requirements.

You can click **Intelligent assistant**, then click the **Knowledge base** button at the bottom left of the chat box, check the required knowledge base, which will take effect immediately.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b54f4a22f2194ba9a26660c9c8f479cb~tplv-goo7wpa0wc-image.image) </span>

<span id="70727b4c"></span>
## Next step: using the intelligent assistant

After creating the knowledge base and selecting the required knowledge base for the intelligent assistant, you can use the assistant for intelligent Q&A and log retrieval. For detailed operations, please refer to the following documentation:


* [Intelligent assistant](https://docs.byteplus.com/docs/bytehouse/intelligent-assistant)

* [Log retrieval analysis](https://docs.byteplus.com/docs/bytehouse/log-retrieval-analysis)


<span id="6a1554d1"></span>
# Manage knowledge bases

ByteHouse supports basic management of knowledge bases (such as enabling/disabling knowledge bases, editing names and descriptions) and granular knowledge segmentation management (including re\-segmentation, adding paragraphs, and managing individual segments).

<span id="4566f441"></span>
## Enable/disable knowledge bases

Knowledge bases are enabled by default after creation. To disable a knowledge base, hover over the knowledge base card and click the **Disable** button. The system will temporarily deactivate the knowledge base, preventing it from linking to the intelligent assistant.

To reactivate this knowledge base, click the \*\*Enable \*\*button. After activation, you can select this knowledge base on the intelligent assistant page and use its content to answer business questions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3da5e1802cf547349728bdd490b3f4c5~tplv-goo7wpa0wc-image.image) </span>

<span id="ac018411"></span>
## Edit knowledge base

To modify the knowledge base name and description, hover over the knowledge base card, click the **Edit** button, update the name and description, and click **Save**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e3ebea8cd8c4d11aaacbef511c3cd9f~tplv-goo7wpa0wc-image.image) </span>

<span id="c188340f"></span>
## Enable / disable document

Documents uploaded to the knowledge base are enabled by default. To disable a document, click the \*\*Disable \*\*button in the enable status bar. The system will temporarily deactivate the document and exclude its content when calling the knowledge base.

To reactivate the document, click the \*\*Enable \*\*button in the enable status bar. After activation, the document content is accessible when using the knowledge base containing this document.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15d71af8c06a485289a8986cf98962cc~tplv-goo7wpa0wc-image.image) </span>

<span id="cb8a9179"></span>
## Manage knowledge segments

<span id="4bc374b2"></span>
### Resegment the knowledge

If the current segmented content does not meet your needs, click **Re\-segment** to reselect the segmentation method, then click **OK** to resegment the content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db2f6caa156a42ceaf4310b2944ec494~tplv-goo7wpa0wc-image.image) </span>

<span id="61e49762"></span>
### Add paragraphs

If you need to add a new paragraph to the existing segmentation, click **New paragraph**, enter content in the edit box, then click **Save** to generate a new segment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aeace65272c4c989452c6e6b7a60b40~tplv-goo7wpa0wc-image.image) </span>

<span id="27fc9e1e"></span>
### Manage single segment

Hover over the segment and click the corresponding button to manage the segment as needed:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e07c08bb9d94d90a7669546a5eb9158~tplv-goo7wpa0wc-image.image) </span>


* **Disable/enable segment**: Segments are enabled by default after completion. To disable a segment, click the **Disable** button and then click **OK**. The segment will be disabled and its content will no longer be accessible. To re\-enable the segment, click the **Enable** button. After enabling, this segment's content can be used in documents where the segment applies.

* **Paragraph preview**: click the \*\*Paragraph preview \*\*button to view details of the current segment.

* **Edit segment**: click the **Edit** button to modify the current segment content. Click **Save** to save the changes.

* **Delete segment**: Hover over the segment, click the **Delete** button, and then click **Confirm** to delete the current segment.


<span id="4f75ac7e"></span>
# Manage knowledge base user permissions

ByteHouse supports granting knowledge base permissions to users.


* Users with the SystemAdmin or AccountAdmin role can grant or revoke knowledge base permissions for a user by assigning roles or directly granting resource permissions. These permissions include creating, viewing, and managing all knowledge bases.

* Users with other roles do not have knowledge base permissions by default. To use knowledge base features in the intelligent assistant, these users must be granted knowledge base permissions first.


You can click **Permission Management** in the knowledge base management interface, and the system will redirect to the corresponding page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9b59219376a4630972282ead98e88f7~tplv-goo7wpa0wc-image.image) </span>

For detailed operations, see the following documents:


* Create and manage roles: [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration)

* Manage resource permissions: [Resource privilege management](https://docs.byteplus.com/docs/bytehouse/resource-privilege-management)

* Grant permissions to users: [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

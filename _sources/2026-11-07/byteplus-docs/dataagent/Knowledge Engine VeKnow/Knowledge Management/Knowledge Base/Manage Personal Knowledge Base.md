---
title: "Manage Personal Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Manage_Personal_Knowledge_Base"
---

Enterprise Knowledge Engine provides a personal knowledge base, allowing you to upload your local files or Lark cloud documents to the personal knowledge base for management. The platform provides knowledge analysis, data statistics, intelligent Q&A, and other capabilities to help you build a personal Wiki Workspace. This article describes how to use the **Personal Knowledge Base**.

# Usage restrictions

* The personal knowledge base is visible only to the current login account itself.

* Personal knowledge base data is not isolated from projects.

# Prerequisite

* Enterprise administrators have assigned individual knowledge base seats to employees, for details, please see [Allocate Personal Knowledge Base Seats(Accounts)](https://docs.byteplus.com/docs/dataagent/Allocate_Personal_Knowledge_Base_Seats_Accounts).

* To access the Lark cloud documentation, the enterprise plumber must have configured the Lark application, see [Access Cloud Documents](https://docs.byteplus.com/docs/dataagent/Access_Cloud_Documents).

# Upload knowledge

1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Knowledge Management** \> **Personal Knowledge Base**.

4. Tab the Knowledge Management page to upload the document.

There are two entries for uploading documents, as shown in the figure below. You can manually add knowledge in the left directory or configure the connector to automatically synchronize knowledge; you can also manually upload documents in the knowledge management tab.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3280e15cf9bb40b18505542038df4458~tplv-goo7wpa0wc-image.image)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc9276e5e6d84924aa808dc79312a92d~tplv-goo7wpa0wc-image.image)

Support manual addition or automatic synchronization of knowledge through connectors, as detailed in the following table:

|**Add method** |**Type of support** |**Description** |
|---|---|---|
|Add manually |Local files/local folders |Supports uploading locally stored files or folders to a personal knowledge base. Use restrictions:<br><br><br>* **Local file**<br><br>   * You can upload up to 30 files at a time, and upload file formats and size limits are supported:<br><br>   * General Documentation (docx/doc/wps/txt/md): Single file size docx, doc, wps does not exceed 450MB, txt, md does not exceed 45MB<br><br>   * PDF document (pdf/ofd): A single file size does not exceed 900MB<br><br>   * PowerPoint (ppt/pptx): Single file size up to 500MB<br><br>   * Table (xlsx/et/csv): A single file does not exceed 20MB, the number of rows does not exceed 20,000 rows, and the number of columns does not exceed 200 columns<br><br>   * Image (jpg/jpeg/png): A single file size does not exceed 50MB<br><br>   * Other (html/json): A single file size does not exceed 20MB<br><br>* **Local folder**<br><br>   * Support uploading parent and child folders, which add up to no more than 5 layers with the original directory of the knowledge base.<br><br>   * Upload up to 100 files at a time, and upload file formats and size limits are consistent with **local file** limits.<br><br>   * Excess number of files, folder level, document type, the system will automatically filter. |
||Lark Cloud Documentation |After the enterprise administrator completes the Lark application access and you complete the Lark account authorization in the personal knowledge base, you can add the Lark cloud document with permission. |
||DingTalk Documentation |After the enterprise administrator completes the DingTalk application access and you complete the DingTalk account authorization in the personal knowledge base, you can add the permissioned DingTalk document.<br><br>> **说明**<br><br><br>> Support importing DingTalk online documents and Word, PDF, PPT, tables, pictures and other files, other formats are not supported for the time being.<br> |
||Web link |It supports the import of one or more publicly accessible web articles, and does not support links to web pages that require login, intranet, or video. |
||WeCom Documentation |After authorizing by scanning the code or manually filling in the credentials, you can add the authorized WeCom document.<br><br>> **说明**<br><br><br>> For the time being, only files of type "Document" in WeCom documents are supported.<br> |
|Automatic connector synchronization |WeCom |After authorizing by scanning the code or manually filling in the certificate authorization, the group chat message records within the specified range can be automatically synchronized through the connector.<br><br>> **说明**<br><br><br>> In the connector, only automatic synchronization of WeCom group chat messages is supported, and automatic synchronization of WeCom documents is not supported for the time being (WeCom MCP does not open this type of interface).<br> |
||Lark |Support connecting your Lark account and authorize automatic synchronization of Lark cloud documents, Lark mailboxes or Lark group chat content.<br><br><br>* **Lark Cloud Documents:**  After successful authorization, Lark Cloud Documents can be automatically synchronized, covering Lark Cloud Disk, Knowledge Base, My Document Library and Smart Minutes. For the time being, only Lark native documents are supported, not tables and slides.<br><br>* **Lark mailbox:**  After successful authorization, the mailbox body of the selected mailbox will be automatically synchronized, and the spam/advertising/private emails will be automatically filtered and parsed into storage.<br><br>* **Lark group chat:**  After successful authorization, synchronize the message records of the selected group chat, and each update will summarize all the new messages of the selected group chat. At present, only message text is supported, and image and file parsing are not supported for the time being. |
||DingTalk |Support connecting your DingTalk account, and the DingTalk documents within the selected range can be automatically synchronized after authorization is completed. |
||Email |Connect to the specified mailbox, automatically pull the email through the standard IMAP protocol, the HTML body will be parsed into Markdown, and automatically filter spam/advertising/private emails and put them into storage.<br><br>> **说明**<br><br><br>> It supports connecting multiple mailboxes at the same time, and does not support parsing attachment files for the time being.<br> |

## Upload a local file or folder

1. Select Upload local file or folder.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eff0eb070fc49049a662a856ac928f8~tplv-goo7wpa0wc-image.image)

2. Set the save path and select a local file or folder.

   Local file or folder upload restrictions:

   |**Upload method** |**Restriction** |
   |---|---|
   |**Local file** |You can upload up to 30 files at a time, and upload file formats and size limits are supported:<br><br><br>* General Documentation (docx/doc/wps/txt/md): Single file size docx, doc, wps does not exceed 450MB, txt, md does not exceed 45MB<br><br>* PDF document (pdf/ofd): A single file size does not exceed 900MB<br><br>* PowerPoint (ppt/pptx): Single file size up to 500MB<br><br>* Table (xlsx/et/csv): A single file does not exceed 20MB, the number of rows does not exceed 20,000 rows, and the number of columns does not exceed 200 columns<br><br>* Image (jpg/jpeg/png): A single file size does not exceed 50MB<br><br>* Other (html/json): A single file size does not exceed 20MB |
   |**Local folder** |* Support uploading parent and child folders, which add up to no more than 5 layers with the original directory of the knowledge base.<br><br>* Upload up to 100 files at a time, and upload file formats and size limits are consistent with **local file** limits.<br><br>* Excess number of files, folder level, document type, the system will automatically filter. |

## Upload Lark Cloud Documentation

1. Select Lark Cloud Documentation.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c5cbb91186d4aaa94877276cbc3b7bc~tplv-goo7wpa0wc-image.image)

2. After the enterprise administrator completes the Lark application access, you need to complete the authorization according to the guidelines on the page. After the authorization is completed, you can obtain the authorized Lark cloud document, and then set the save path, tick the document to be uploaded, or enter the cloud document link to add.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c94e14064f9402aaac35447c37d2460~tplv-goo7wpa0wc-image.image)

## Upload DingTalk document

1. Select the DingTalk document.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d6358f2a6d44e629a3e96f6365490a1~tplv-goo7wpa0wc-image.image)

2. After the enterprise administrator completes the DingTalk application access, you need to complete the authorization according to the guidelines on the page. After the authorization is completed, you can obtain the authorized DingTalk cloud document, and then set the save path, tick the document to be uploaded, or enter the cloud document link to add it.

   > **说明**

   > Support importing DingTalk online documents and Word, PDF, PPT, tables, pictures and other files, other formats are not supported for the time being.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91decc2ab46744c2b32fe9a8d50be9bb~tplv-goo7wpa0wc-image.image)

## Upload web link

1. Select a web link.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5909a04f66d4413680a16669b07fa4cd~tplv-goo7wpa0wc-image.image)

2. Complete the following configuration and click **Import**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73af36eea98f472d97fbfbe159c253fb~tplv-goo7wpa0wc-image.image)

   1. Set the save path and enter the web link.

      * Support for importing publicly accessible web articles, but do not support links to web pages that require login, intranet, or video.

      * Multiple links can be separated by spaces or newlines.

   2. If necessary, check the box to import the same site link page at the same time.

      After opening, additional pages from the same website linked to in the current webpage will be imported to help supplement relevant content, and some unrelated pages may be imported. Just drill down one layer, you won't grab indefinitely.

## Upload WeCom Documentation

1. Select the WeCom document.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c6b9b38a7c24737ab42ae85aff58c5d~tplv-goo7wpa0wc-image.image)

2. Authorize by scanning the code or manually filling in the certificate authorization.

   You need to create a WeCom robot in advance, and then scan the code or fill in the robot credentials (Bot ID, Bot Secret).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20904bd4be964d188cc1020477432b7a~tplv-goo7wpa0wc-image.image)

3. After the authorization is completed, you can get the authorized WeCom document, and then set the save path, tick the document to be uploaded, or enter the document link to add it.

   > **说明**

   > For the time being, only files of type "Document" in WeCom documents are supported.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f957e6c8ff94687823c8c69089d3efe~tplv-goo7wpa0wc-image.image)

## Automatic connector synchronization

At present, the configuration of WeCom, Lark, DingTalk, and mailbox connectors is supported. After the configuration is completed, the knowledge can be automatically synchronized to the personal knowledge base. The configuration instructions for each connector are as follows.

1. Go to the personal knowledge base and select **the connector** in the upper left corner.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd7b9fd519444fbeae91167f16b950ab~tplv-goo7wpa0wc-image.image)

2. On **the Connectors** page, select Configure the specified connector.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc04b08396be448eb6bf015fb842670f~tplv-goo7wpa0wc-image.image)

   |**Connector** |**Configuration instructions** |
   |---|---|
   |Lark |Support connecting your Lark account and authorizing access to Lark cloud documents, Lark mailboxes, and Lark group chat content.<br><br><br>* When authorizing, you need to follow the guidelines to configure the synchronization range, save location and other configurations.<br><br>* Support for enabling or disabling automatic synchronization.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/097b4fdf96c9415883a128e63257053a~tplv-goo7wpa0wc-image.image)<br><br><br>* **Lark Cloud Documents:**  After successful authorization, Lark Cloud Documents can be automatically synchronized, covering Lark Cloud Disk, Knowledge Base, My Document Library and Smart Minutes. For the time being, only Lark native documents are supported, not tables and slides.<br><br>* **Lark mailbox:**  After successful authorization, the mailbox body of the selected mailbox will be automatically synchronized, and the spam/advertising/private emails will be automatically filtered and parsed into storage.<br><br>* **Lark group chat:**  After successful authorization, synchronize the message records of the selected group chat, and each update will summarize all the new messages of the selected group chat. At present, only message text is supported, and image and file parsing are not supported for the time being. |
   |Email |Connect to the specified mailbox, automatically pull the email through the standard IMAP protocol, the HTML body will be parsed into Markdown, and automatically filter spam/advertising/private emails and put them into storage.<br><br><br>* It supports connecting multiple mailboxes at the same time, and does not support parsing attachment files for the time being.<br><br>* Support editing email address, authorization code, IMAP server and port.<br><br>* Support deleting connected mailboxes.<br><br>* Support for configuring save locations.<br><br>* Support for enabling or disabling automatic synchronization.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a2978f449c64993890cb5ee0c51259a~tplv-goo7wpa0wc-image.image) |
   |DingTalk |Support connecting your DingTalk account, and the DingTalk documents within the selected range can be automatically synchronized after authorization is completed.<br><br><br>* For the time being, only DingTalk native documents are supported, and other file types such as tables are not supported for the time being.<br><br>* Support for enabling or disabling automatic synchronization.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4eddc910d854e47b7d9301a67299a7c~tplv-goo7wpa0wc-image.image) |
   |WeCom |1. Authorize by scanning the code or manually filling in the certificate authorization.<br><br>   You need to create a WeCom robot in advance, and then scan the code or fill in the robot credentials (Bot ID, Bot Secret).<br><br>2. After successful authorization, configure the synchronization scope and save location. Support for enabling or disabling automatic synchronization.<br><br><br>> **说明**<br><br><br>> In the connector, only automatic synchronization of WeCom group chat messages is supported, and automatic synchronization of WeCom documents is not supported for the time being (WeCom MCP does not open this type of interface).<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c1a0f8827f04bddb7dbeca57d9de115~tplv-goo7wpa0wc-image.image) |

## View the uploaded knowledge in the personal knowledge base

In the directory on the left side of the personal knowledge base, you can view all uploaded knowledge, and support searching for knowledge by keywords.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce126e2560ab4204a455d9e3e4b62bbb~tplv-goo7wpa0wc-image.image)

# Parse knowledge

After uploading the document to the personal knowledge base, the system will automatically parse the document. After the parsing is completed, you can preview the document on the document details page, including the original text, document summary, reading guide, and support knowledge retrieval through intelligent Q&A function.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c5037f62cfa4be287c71b4e72cdc1aa~tplv-goo7wpa0wc-image.image)

# View knowledge statistics

On the homepage of the personal knowledge base, the system displays the asset data statistics of the current knowledge base, the list of commonly used knowledge, and the list of not commonly used knowledge.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96f8678194dc49819f82f6f7e9a1a2ac~tplv-goo7wpa0wc-image.image)

# Search for knowledge

In the **Knowledge Management** tab of the Personal Knowledge Base, enter keywords to search for the specified knowledge.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0cf1a23041b4f7493d1d00186860611~tplv-goo7wpa0wc-image.image)

Click on the knowledge title to redirect to information such as knowledge content, document summaries, and reading guides.

# Q&A

The personal knowledge base provides intelligent Q&A capabilities to consume knowledge accurately and efficiently. The intelligent Q&A entrance includes:

* **Entrance 1:**  Enter the **intelligent Q&A** function on the personal knowledge base **homepage**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fb79949373d41b780f5adc24f8c8580~tplv-goo7wpa0wc-image.image)

* **Entrance 2:**  On a certain knowledge details page, enter the **intelligent question and answer** function.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f26f7c85b3954deea285f718ff20e611~tplv-goo7wpa0wc-image.image)

After entering the intelligent Q&A function, it supports specifying the scope of knowledge retrieval, uploading files on demand or enabling online search and deep thinking functions, and asking AI questions through natural language to achieve knowledge retrieval, conclusion refinement, summary content, and other requirements.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1661adec1048bca19ed73815ccae3e~tplv-goo7wpa0wc-image.image)

|**Operation** |**Description** |
|---|---|
|Session recording |* Click the **conversation history** icon to view the conversation history.<br><br>* Click the New Session chart to create a new session. |
|In the input box |* Click the **plus sign**( **+** ) to upload the file to the model service for inference.<br><br>   * You can upload up to 10 files, with a single file size of no more than 100MB.<br><br>   * Supported file formats: DOC/DOCX/WPS/TXT/MD, PDF/OFD, PPT/PPTX, CSV/XLSX, JPG/JPEG/PNG.<br><br>* Click the icon shown below to enable **Internet search** or **deep thinking**.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e256383069a419ab0b559ca808e33c8~tplv-goo7wpa0wc-image.image)<br><br>* In the scope of knowledge list, the current file is selected by default. Support switching to global search, designated enterprise knowledge base, personal knowledge base or ontology semantics, Knowledge Graph, and subsequent Q&A within the specified scope.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b3e7349f97b4b3989566538ca737088~tplv-goo7wpa0wc-image.image) |
|During multiple rounds of dialogue |* In the output results, support for viewing source knowledge through corner markers or references, and support for downloading the original text.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d488049c7c834cc992f9f339bc1b917c~tplv-goo7wpa0wc-image.image)<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57dcdc1f8e2049678b3dc8da3ec9dd02~tplv-goo7wpa0wc-image.image)<br><br>* Support for regenerating results.<br><br>   In addition, it supports liking or clicking on the feedback of the Q&A results, and supports copying the content of the results.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12fa1a6de8214e0690b5de825625faff~tplv-goo7wpa0wc-image.image)<br><br>* Supports multiple rounds of conversation. During multiple rounds of dialogue, it supports uploading files, enabling or disabling online search or deep thinking functions, and adjusting the scope of the knowledge base.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2405833da15744fab01e64be1966c1ad~tplv-goo7wpa0wc-image.image) |

# Manage directory

In the directory on the left side of the personal knowledge base, the following administrative operations are supported.

|**Operation** |**Schematic diagram** |
|---|---|
|Create a new folder or upload knowledge |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ede74f89b1b44f0ba623582a4bec499~tplv-goo7wpa0wc-image.image) |
|Create a new subfolder or edit or delete a folder |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f428c4ad2170473387333f5aa9d109b7~tplv-goo7wpa0wc-image.image) |
|Refresh directory |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67a6109397f14536955a0131042ab22b~tplv-goo7wpa0wc-image.image) |
|Moving or deleting knowledge |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0147e7505494490c931f0af760c83cb7~tplv-goo7wpa0wc-image.image) |

# Open capability

The personal knowledge base provides knowledge access to the external client side via the standard MCP Streamable HTTP protocol. Enter the **open capability** page in the upper left corner of the personal knowledge base function page, obtain the personal token for MCP authentication, and complete the docking through the MCP Server docking guidelines.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e714e83049f0437380c72ab7bd409c8c~tplv-goo7wpa0wc-image.image)

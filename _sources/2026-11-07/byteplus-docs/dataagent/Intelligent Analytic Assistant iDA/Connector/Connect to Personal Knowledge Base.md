---
title: "Connect to Personal Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Connect_to_Personal_Knowledge_Base"
---

Connector \- Personal Knowledge Base is used to provide a private workspace of personal dimension. You can save personal documents to a knowledge base for search, management, and intelligent Q&A. This feature provides 50 GB of free space for personal knowledge accumulation, private data management, and fragmented knowledge reuse. This document will guide you through how to access and use the Personal Knowledge Base feature.

The personal knowledge base is different from the enterprise knowledge base, it is the knowledge asset of the personal dimension, **only the current account can view**, and the use permission is not affected by the configuration of the agent dimension knowledge base; the configuration of the agent dimension knowledge base only affects the enterprise knowledge base.

<span id="d8afc2ed"></span>
# Prerequisite


* **The account has been opened for iDA use:**  You \*\*\*\* need to log in to the system with an account with iDA access to enter the connector page and view the personal knowledge base entrance;

* **The account has personal knowledge base opening conditions:**  When entering the personal knowledge base for the first time, the system will open and authenticate based on the current account; after meeting the opening conditions, the system will display the personal knowledge base homepage.


<span id="d95929a2"></span>
# Access to personal knowledge base


1. Log into the BytePlus console, search for'iDA 'in the search box, and go to the iDA product page.

2. Select the corresponding agent in the agent list to enter the agent Q&A interface, and select the **Connector** in the side navigation.

3. In the Connector, you can click Personal Knowledge Base, and the system will redirect to the Personal Knowledge Base interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad8d60e7804d468aa5a34a6a8728f999~tplv-goo7wpa0wc-image.image) </span>


<span id="48145095"></span>
# Personal Knowledge Base Homepage

After the system enters the Personal Knowledge Base homepage, the homepage is used to manage personal knowledge content, support viewing data overview, uploading documents, searching documents, browsing common knowledge, and switching to intelligent Q&A. Detailed operation can refer to[ ](https://docs.volcengine.com/docs/86760/2630944?lang=zh)[Manage Personal Knowledge Base](https://docs.byteplus.com/docs/dataagent/Manage_Personal_Knowledge_Base).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8f9782f73374c40a531b65a8291aaa9~tplv-goo7wpa0wc-image.image) </span>

<span id="db9e9e5f"></span>
# Use a personal knowledge base

After uploading or opening the personal knowledge base, you can open the **personal knowledge base retrieval** ability on the agent dialogue page. After opening, the system will automatically retrieve the relevant content in the personal knowledge base when the user asks a question, and use the retrieval results as one of the basis for answering.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Search rule description:</strong> After opening the personal knowledge base, the system will first understand the user's problem, and then recall the relevant content from the personal knowledge base. The search process incorporates semantic relevance and relies not only on keyword matching. If there is relevant information in the personal knowledge base, the answer will be organized, summarized, or generated in combination with the retrieved content; if no relevant information is retrieved, the system will not forcibly quote the content of the personal knowledge base.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3154e595d8d04c30947eff47a03f47e8~tplv-goo7wpa0wc-image.image) </span>

<span id="dd398b9f"></span>
## Precautions


* The Personal Knowledge Base needs to be opened or uploaded before it can participate in the search in the conversation.

* When the Personal Knowledge Base switch is turned off, the conversation does not retrieve Personal Knowledge Base content.

* The system only retrieves the knowledge content that the current account has access to.

* If there are enterprise knowledge base permissions at the same time, the system can answer in combination with the content of the enterprise knowledge base and the personal knowledge base that the user has access to.

* Whether the content of the personal knowledge base is adopted depends on the relevance of the question to the content of the knowledge base.


<span id="a5943632"></span>
## Usage example

After opening the Personal Knowledge Base, you can ask questions to the agent using the following example:


|Usage scenario |Example question |
|---|---|
|Summarize uploaded data |Summarize the core content of the project plan I uploaded. |
|Query document details |Find a description of the contract payment terms in the Personal Knowledge Base. |
|Generated content |Generate a product introduction based on Personal Knowledge Base data. |
|Compare data |Compare the differences between the two plans I uploaded. |
|Refine keypoints |Extracting key conclusions from documents in the Personal Knowledge Base. |

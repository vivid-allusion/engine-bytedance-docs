---
title: "Core process of knowledge Q&A"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/Core_process_of_knowledge_Q-A"
---

<span id="aT5sOe512p"></span>
# Prerequisites


1. Complete account registration and service activation.

2. Complete sub\-account creation and policy configuration.

3. In the console, click [Knowledge Base](https://console.byteplus.com/vikingdb/region:vikingdb+cn-hongkong/home?projectName=default), and enter the knowledge base product.


<span id="x4pDW0MPDi"></span>
# 1. Create a knowledge base

After opening the knowledge base page, go to the knowledge base list. Click [Create Knowledge Base] in the upper left corner of the knowledge base list page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52fa1fc988794dcc8b3e1d3d604ac05c~tplv-goo7wpa0wc-image.image) </span>

The knowledge base supports two specifications: standard version and pro version. The detailed comparison is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41b5611d83424b5c83b371c1e329b1a2~tplv-goo7wpa0wc-image.image) </span>

The pro version supports more advanced knowledge base configurations. Here, the pro version is used as an example to explain all adjustable parameters:

On the **Create Knowledge Base** page, fill in the relevant parameters. The recommended parameter configuration is as follows:


* **Data type**: Supports selecting [Unstructured Data]/[Structured Data], among which

   * The main content of files for [Unstructured Data] is text and charts, such as articles, reports, books, and more. Supported formats include docx, pptx, pdf, markdown, and txt, and are also compatible with csv, xlsx, png, jpeg, and more than 10 other formats.

   * The main content of files for [Structured Data] is structured text, which must have clear field constraints, such as Q&A summaries, policy clauses, data collection, and more. Supported formats include csv, xlsx, and jsonl. To filter and search the content of a specific column, select [Structured Data].

* **Text embedding model**: It is generally recommended to use the [Doubao\-embedding+Multifunctional Version] embedding model. Hybrid retrieval capability can be used to improve recall accuracy.

* **Vector dimension**: In general, the higher the dimension, the more accurate the retrieval. Dimensionality reduction should only be considered if there are extremely high performance requirements and ultra\-large\-scale data volumes.


**When the data type is "Unstructured Data", the "chunking method" must be configured.** 


* **Chunking method**: It is generally recommended to use the [Default Chunking Rule], where the system will automatically retain complete semantics during chunking. If the document has a very clear segmentation rule (such as splitting by line breaks), [Split by delimiter] should be used.

   * When the chunking method is set to [Default Chunking Rule], the following must be configured:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2fcae9a23aa4d339f114e654b18dbaf~tplv-goo7wpa0wc-image.image) </span>

      * **Maximum slice length**: When the "default slicing rule" is selected, you must specify the maximum slice length. The length setting is often related to the information density of the uploaded document. (**When the information density is high** and contextual relevance is low, the slice length can often be set to a shorter value, based on the length of standalone content, for example, around 200–500. This applies to policy information, trending news, laws and regulations, and more; **when the information density is low** and more contextual relevance is needed, the slice length can often be appropriately increased, but should not be too large, for example, around 800–1000. This applies to product manuals, novels, papers, and more.)

      * **Image OCR**: To recognize image content in the document and enhance information input for large models, enable the [Image OCR] switch.

      * **Merge short text slices**: Semantic slicing may produce some independent short text slices, which can lead to uneven distribution of slice character counts. Short, unrelated text slices and longer, related text slices may not be sufficiently distinguished in similarity calculations. Therefore, you can enable the [Merge short text slices] feature to help ensure a more even distribution of slice lengths and improve recall accuracy.

   * When the slicing method [Split by delimiter] is selected, you can choose an existing delimiter or define a custom delimiter. For example, if the document contains clearly defined legal clauses and each line is a separate slice, you can set `\n` as the delimiter.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a341e7cc5344ab1a4d14cc34b13f474~tplv-goo7wpa0wc-image.image) </span>


**When the data type is "structured data", you need to configure "field configuration".** 


* **Field configuration**: Field configuration is used to specify the index for structured data.

   * **Upload document**: The system supports automatic recognition of the document table structure. Please note that the document uploaded here is only used to define the table structure and will not actually be imported into the knowledge base.

   * **Table structure**: It supports specifying which row or column to use as the table header field. If "vector index" is set to "yes", it can be used for retrieval matching; if set to "no", it can only be used for scalar filtering.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b375c66437fc47e5827510dc934f536d~tplv-goo7wpa0wc-image.image) </span>

* **CPU quota**: The CPU quota is related to the QPS requirements for retrieval; typically, 1 CU = 100 QPS.

* **Tag**: Tags can be used to categorize uploaded documents for subsequent operations. During retrieval, document types can be filtered first, followed by content retrieval, which reduces retrieval costs and latency. (For example, if the tag is set to "Document permission," after uploading documents, you can set Document 1's "Document permission" == "Internal," and Document 2's "Document permission" == "Public." During retrieval testing, you can configure the retrieval scope to include all documents whose "Document permission" contains "Internal," enabling hierarchical management of model reference content for different users during document Q&A.)


After completing the entry, click [Create knowledge base] on the right.

<span id="EXLOw6kXRk"></span>
# 2. Import documents

After creating the knowledge base, you can follow the guide to upload documents. The knowledge base supports document upload via local upload, TOS import (TOS must be purchased and authorized first), Feishu import, or public download link.


* When there is a large amount of local data (\>100) that needs to be imported in batches, it is recommended to upload the data to [TOS](https://console.volcengine.com/tos) first, and then import it into the knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc93853324494060ba3d93be3e64965e~tplv-goo7wpa0wc-image.image) </span>


<span id="ILXaqTQRjP"></span>
# 3. Slice details

Click [Slice details] to view the slice content. You can check, but are not limited to, the following aspects:

(1) Whether the slice result is relatively complete in semantics

(2) Whether the character count distribution of the slice results is relatively even

(3) Whether the slice results correctly identify image information

If expectations are not met, you can modify the slice content, readjust the slicing rules, or further standardize the processing of the original document. By default, slices are displayed in card format. You can click the icon to the right of the newly added slice to switch to list format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6eb8557099843238d19c087d30ecfc3~tplv-goo7wpa0wc-image.image) </span>

<span id="MgEmkYCbGo"></span>
# 4. Knowledge retrieval

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Applicable scenarios: knowledge search, text duplication checking, tagging classification, and other scenarios requiring content retrieval</div>


After document processing is complete, click [Knowledge retrieval] to test.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4290b0933ab747e8af7237d65ae6e7ce~tplv-goo7wpa0wc-image.image) </span>

In addition to document processing, retrieval strategy configuration also plays a crucial role in recall effectiveness. The slice retrieval parameter configuration is as follows:


* Retrieval parameters

   * **Number of returned text slices**: The final number of slices retrieved; the recalled text slices serve as input, concatenated and sent to the large model for information enhancement.

   * **Re\-ranking model**: The user's question and the recalled slices are processed through the large model for semantic re\-ranking, improving the ranking and score of accurately recalled slices.

      * **Number of recalled items**: The "number of recalled items" only needs to be configured when the re\-ranking model is enabled. In most cases, the "number of recalled items" should be greater than the "number of returned text slices"; that is, as many similar slices as possible should be recalled, and then, through re\-ranking and truncation, only the most precise subset of slices is sent to the large model.

* More parameters

   * **denseweight**: When using hybrid retrieval mode, the denseweight parameter can adjust the proportion of semantic retrieval. denseweight = 1 means full semantic retrieval.

   * **Scalar filtering**: Used in conjunction with scalar filtering fields when creating the knowledge base. For example, the retrieval scope can be configured so that "document permissions" include all documents marked as "internal," enabling hierarchical management of reference content for different users during document Q&A.


During slice retrieval, the recalled slices are displayed sequentially according to their ranking, allowing intuitive review of whether the slices are correct and whether the scores meet expectations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cf39c135607445b99739d8dcc61e14e~tplv-goo7wpa0wc-image.image) </span>


* **View retrieval history**


Click [Retrieval History] to view historical retrieval records.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e90042abc1eb473aacf92494dbe58673~tplv-goo7wpa0wc-image.image) </span>

<span id="jXIqUytKNn"></span>
# 5. Knowledge Q&A

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Applicable scenarios: intelligent customer service, domain consulting, sales support, copywriting generation, and similar scenarios</div>


After document processing is complete, click [Knowledge Q&A] to run tests.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e9be57bc96c46c08446d21a5c57f820~tplv-goo7wpa0wc-image.image) </span>

In addition to document processing, retrieval strategy configuration also plays a crucial role in recall effectiveness. Slice retrieval parameter configuration is as follows:


* Retrieval parameters

   * **Number of returned text slices**: The final number of slices retrieved; the recalled text slices serve as input, concatenated and sent to the large model for information enhancement.

   * **Question rewriting**: The current question is rewritten based on historical conversations to provide more complete semantic information for more accurate retrieval. Disabled by default. **Caution: Enabling question rewriting will increase retrieval time and consume additional tokens.** 

   * **Re\-ranking model**: User queries and retrieved slices are semantically re\-ranked by a large model to improve the ranking and score of accurately matched slices.

      * **Recall quantity**: The 'recall quantity' must be configured only when the re\-ranking model is enabled. In general, the 'recall quantity' should be greater than the 'number of returned text slices', meaning as many similar slices as possible are recalled, then re\-ranked and truncated to ensure that only the most precise subset of slices is input into the large model.

* More parameters

   * **Denseweight**: When using hybrid retrieval mode, the denseweight parameter can adjust the proportion of semantic retrieval. denseweight = 1 means fully semantic retrieval.

   * **Scalar Filtering**: Used in conjunction with the scalar filtering field when creating a knowledge base. For example, the retrieval scope can be configured so that 'document permissions' include all documents marked as 'internal', allowing hierarchical management of model reference content for different users during document Q&A.

   * **Document aggregation sorting**: Retrieved slices are sorted and aggregated according to the original document order to ensure correct word order and semantics. Enabled by default

* Model parameter configuration is as follows:

   * **Select model**:

      * The platform provides multiple models and versions, supporting selection of public inference endpoints or use of self\-hosted inference endpoints.

      * 'pro' indicates high accuracy, 'lite' indicates high performance, the number indicates the input/output window length of the large model, and the date indicates the model version. The newer the version, the better the overall performance.

   * **Number of concatenated adjacent text slices**: When the character count of a single slice is low, to avoid loss of context information, you can configure concatenation of adjacent text slices to input more comprehensive information into the large model. For example, if the recalled slice is chunk 8 and 'number of concatenated adjacent text slices' == 1, chunk 7, chunk 8, and chunk 9 will be concatenated and input into the large model.

   * **Write prompt**: The system provides a default prompt, and you can also specify more detailed response requirements according to the actual conversation needs. For example, 'Please use the most professional terminology possible in your response.'


When the large model generates an answer, it summarizes based on the retrieved slices and provides reference information for the cited knowledge.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fd90e808dd84eb1a860683af40d6fba~tplv-goo7wpa0wc-image.image) </span>

Click "Recall details" to view more detailed citation information for the answer, which helps locate issues. If the document aggregation sorting parameter is enabled, the platform will display recall sorting based on the semantic information of the documents.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21ee221a98a242aa9ac6cb1edfc3bff1~tplv-goo7wpa0wc-image.image) </span>

Click "tokens" details to view the token consumption throughout the question and answer process. If the question rewriting parameter is enabled, the number of tokens consumed by rewriting will be displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e5b2e7db0e74c0dbe8d8436f0f1b5a7~tplv-goo7wpa0wc-image.image) </span>

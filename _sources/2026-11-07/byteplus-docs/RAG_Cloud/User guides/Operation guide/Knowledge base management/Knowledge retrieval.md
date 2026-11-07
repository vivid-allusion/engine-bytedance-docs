---
title: "Knowledge retrieval"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/knowledge_retrieval"
---

This section describes how to perform online retrieval based on an existing knowledge base. Knowledge retrieval is applicable to various scenarios, including text duplication checking, tagging, classification, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Once the knowledge base is created and documents are imported and processed, online retrieval is available.</div>


* <div data-tips="true" data-tips-type="tip">Before calling the API, complete account registration, identity verification, AK/SK key acquisition, and signature acquisition on the <a href="https://docs.byteplus.com/docs/undefined/698451644de01105f525ec9a">Signature authentication and examples</a> page.</div>



<span id="639e90b2"></span>
# Knowledge retrieval


* Entry 1: On the knowledge base list page, select the corresponding knowledge base, go to the details page, and click the "Knowledge retrieval" button to access the test interface.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec16f1e81aa9407fb392d09704bfa71c~tplv-goo7wpa0wc-image.image) </span>


* Entry 2: On the knowledge base list page, locate the corresponding knowledge base and use the  **···**  in the upper right corner of the knowledge base to enter the retrieval test page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4449c240ea4e4c8cbceb50d23755b49c~tplv-goo7wpa0wc-image.image) </span>


* The retrieval test details page is as follows


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4053206ba28f430390748cd0126c1b5f~tplv-goo7wpa0wc-image.image) </span>

<span id="1782499c"></span>
# Retrieval test

On the knowledge retrieval interface, you can submit your retrieval query, and the system will return several text fragments most relevant to the query:

<span id="f7b8f5c2"></span>
# Parameter description

The left side contains the parameter settings for the knowledge retrieval test, and the right side displays the knowledge retrieval interface. The following table provides detailed information for each parameter:


|**Parameter** |**Function** |**Value range** |
|---|---|---|
|Number of returned text fragments |Controls the number of text fragments returned by the final retrieval.<br><br>If the rerank model is not enabled, this refers to the number of Top N text fragments returned after reranking;<br><br>If the rerank model is enabled, this refers to the top K text fragments in the model's sorted results, where K is the number of returned text fragments. |If the rerank model is not enabled: [1, 1000]<br><br>If the rerank model is enabled: [1, Top K] |
|Enable rerank model |Controls whether to use the rerank model to reorder the retrieved text fragments.<br><br>Enabling the rerank model provides more accurate similarity scoring between the query and text fragments, improving retrieval performance.<br><br>**After enabling, retrieval time will increase slightly and is proportional to the number of recalled text fragments. It is recommended to set the number of recalled text fragments reasonably.**  |base\-multilingual\-rerank: Fast speed, long text, supports 70+ languages (default)<br><br>m3\-v2\-rerank: General text, supports more than 100 languages |
|Recall quantity (Top K) |Recall refers to the process of identifying the K text fragments most relevant to the query from a large pool of candidate fragments. This option can only be set when the rerank model is enabled. It is recommended to set the recall quantity slightly higher than the number of returned text fragments to improve generation accuracy. |[1, 1000] |
|More parameters—Dense Weight |When creating a knowledge base, if the selected embedding model and indexing algorithm support hybrid retrieval, the system will consider both the semantic relevance between the query and candidate text fragments and the degree of literal matching during retrieval, resulting in more accurate retrieval results.<br><br>The Dense Weight parameter controls the importance weight of semantic similarity during retrieval; values closer to 1 indicate a stronger preference for semantic retrieval, while values closer to 0 indicate a stronger preference for keyword matching retrieval. |[0.2, 1] |
|More parameters—Filter document scope by tag |If tag\-based document scope filtering is not configured, no filtering will be applied.<br><br>To filter documents by tag, select the desired tag name from the dropdown list in the add condition section, and choose the corresponding filter condition.<br><br>**Filter conditions** include six types: contains, does not contain, greater than, less than, greater than or equal to, less than or equal to. **Condition relationships** include two types: and, or. |\-\- |

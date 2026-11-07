---
title: "Knowledge Q&A"
product: "VikingDB Knowledge Engine"
product_code: "RAG_Cloud"
source: "https://docs.byteplus.com/en/docs/RAG_Cloud/knowledge_Q-A"
---

To implement powerful Q&A functionality, such as intelligent customer service or a domain\-specific consultant, using your own knowledge base, you must first configure and test the system. This guide details the parameter settings for knowledge\-based Q&A, including retrieval, reranking, and prompt engineering. Following these steps will help you optimize the system to get the most accurate and relevant answers from your documents.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Once the knowledge base is created and documents are imported and processed, knowledge\-based Q&A can be performed.</div>


* <div data-tips="true" data-tips-type="tip">Before calling the API, complete account registration, real\-name authentication, AK/SK key acquisition, and signature acquisition on the <a href="https://docs.byteplus.com/docs/209/Signature_authentication_and_examples">Signature authentication and examples</a> page.</div>



<span id="15ae8092"></span>
# Parameter settings

Select the corresponding knowledge base on the knowledge base list page, go to the details page, and click the "Knowledge\-based Q&A" button to enter the test interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6d9aae4caf54c50a9add16cbb883db1~tplv-goo7wpa0wc-image.image) </span>

<span id="ba518a2c"></span>
# Parameter description

On the test page, the left side is the parameter settings module for knowledge\-based Q&A testing, and the right side is the conversation interface. The following table provides detailed information about each parameter:


|**Parameter** |**Function** |**Value range** |
|---|---|---|
|Number of returned text segments |Controls the number of text segments returned by the final retrieval.<br><br>If the rerank model is not enabled, this indicates the number of Top N text segments returned after reranking by retrieval;<br><br>If the rerank model is enabled, this indicates the top K text segments in the model's sorted results, where K is the number of returned text segments. |If the rerank model is not enabled: [1, 200]<br><br>If the rerank model is enabled: [1, Top K] |
|Question rewriting |When enabled, the current question will be rewritten based on the conversation history to provide more complete semantic information and improve retrieval accuracy.<br><br>**Caution: Rewriting questions will increase retrieval time and consume additional tokens.**  |Disabled by default |
|Enable rerank model |Control whether to use the rerank model to reorder the retrieved text chunks.<br><br>Enabling the rerank model provides more accurate similarity scoring between the question and retrieved text chunks, improving retrieval performance.<br><br>**Retrieval time will slightly increase after enabling, and is proportional to the number of retrieved text chunks. It is recommended to set the number of retrieved text chunks appropriately.**  |base\-multilingual\-rerank: Fast, supports long texts, supports more than 70 languages (default)<br><br>m3\-v2\-rerank: Standard texts, supports more than 100 languages |
|Number of retrieved text chunks (Top K) |Retrieval refers to the process of selecting the K text chunks most relevant to the question from a large pool of candidate text chunks. This option can only be set when the rerank model is enabled. It is recommended to set the number of retrieved text chunks slightly higher than the number of returned text chunks to improve generation accuracy. |[1, 1000] |
|More parameters \- Dense Weight |When creating a knowledge base, if the selected embedding model and indexing algorithm support hybrid retrieval, the system will consider both the semantic relevance between the question and candidate text chunks and the degree of literal matching during retrieval, resulting in more accurate retrieval results.<br><br>The Dense Weight parameter controls the importance weight of semantic similarity during retrieval. The closer to 1, the more semantic retrieval is favored; the closer to 0, the more keyword matching retrieval is favored. |[0.2, 1] |
|More parameters \- Filter document scope by tag |If tag\-based document filtering is not configured, no filtering will be applied.<br><br>To filter documents by tag, select the desired tag name from the dropdown list under Add Condition, and choose the corresponding filter condition.<br><br>**Filter criteria** include six types: contains, does not contain, greater than, less than, greater than or equal to, and less than or equal to. **Condition relationships** include two types: and, or. |\-\- |
|Document aggregation sorting |When enabled, the recalled slices will be sorted and aggregated according to the original document order to ensure correct word order and semantics.<br><br>**It is recommended to enable this for scenarios where the original order of reference materials is important; for scenarios where the content of slices is logically independent, it is recommended to disable it.**  |Enabled by default |
|Large model response |Controls whether to use the large model to summarize background knowledge and answer questions.<br><br>If disabled, the retrieved text slices are returned; if enabled, the response generated by the model based on the assembled text slices and prompt is returned. |\-\- |
|Number of adjacent text slices to concatenate |This value is used as the number of adjacent text slices to concatenate after recall reordering. If the number of text slices after recall reordering is k and this value is p, then the final returned quantity range is [k, k+2*k*p] |[0, 5] |
|Edit prompt |This can be set when "Use large model to generate response" is enabled.<br><br><br>* Prompt composition allows you to configure how the user question and retrieved text slices are assembled when passed to the large model, as well as other response requirements.<br><br>* Prompt composition **must include** two variables, using square brackets plus the variable name as placeholders:<br><br><br>```JSON```<br>```<context>```<br>```  <Documents>```<br>```</context>```<br><br><br><br>* When organizing the prompt, you can provide instructions to the large model. to suit your use case. For example, instruct the large model to use the retrieved text as background information to answer questions, and to transfer to human customer service when the retrieved information cannot answer the user's question, and so on.<br><br><br>The platform also provides prompt templates for several core scenarios and supports one\-click insertion. |\-\- |
|API call |After saving the settings, you can click the "API call" button to obtain the API request body, making it easy to embed the configured settings into your application.<br><br>However, we recommend using **service_chat API, referring to the documentation.**  |\-\- |


<span id="0c721d71"></span>
# Q&A testing

The model assembles the retrieved text segments into the prompt in the prompt orchestration section, then inputs them into the large language model, which answers the question based on the retrieved background information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b27ccc617a74b0bae939fdc700a7d44~tplv-goo7wpa0wc-image.image) </span>

In the prompt editing section, several prompt templates for core scenarios are provided. Clicking "Apply" will overwrite the original prompt.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/993ac23ce50d4bff8f3081e49c0d4155~tplv-goo7wpa0wc-image.image) </span>

The source document of the reference text segment is displayed below the dialog box. Click the "Recall details" button to view the recall score and rerank score of the retrieved text segments.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9da8edce113340758e5a0ca82362c55b~tplv-goo7wpa0wc-image.image) </span>

By switching views, you can see the final complete prompt after assembly.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86c045d9c5454272ba701009965ae787~tplv-goo7wpa0wc-image.image) </span>

Retrieval testing supports multi\-turn conversations, allowing you to rewrite the current question based on the context to obtain more accurate responses. Clicking "Clear conversation" will clear the context.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bed3b7caa014e92958580cdc116eab0~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using the large model, after concatenating adjacent text slices, the platform aggregates text slices from the same source according to the <code>doc_id</code> field, and text slices from the same source are arranged in <code>chunk_id</code> order.</div>


* <div data-tips="true" data-tips-type="tip">The number of input characters for large models is limited. To avoid exceeding this limit, the system truncates overly long text segments when assembling the prompt. Please set a reasonable number of returned text segments based on the input window size of the selected large model.</div>

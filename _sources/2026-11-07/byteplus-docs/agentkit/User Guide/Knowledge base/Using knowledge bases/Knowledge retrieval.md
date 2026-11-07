---
title: "Knowledge retrieval"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Knowledge_retrieval"
---

Applicable for scenarios where the knowledge base is used only for similarity retrieval. Each retrieval is independent, with no reference to multi\-turn information.

<span id="X6wSJP9i"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Knowledge Base".

3. Click the name of the target knowledge base to open the details page of the knowledge base.

4. Click the "Knowledge retrieval" button in the upper right corner of the page.

5. Set the knowledge retrieval parameters.

   
   |**Parameter​**  |**Purpose** |**Value range** |
   |---|---|---|
   |Number of returned results |Configure the number of results retrieved.<br><br><br>* If no reranking model is enabled, this parameter specifies the number of top N results returned by retrieval.<br><br>* If a reranking model is enabled, this parameter specifies the top K text chunks after reranking, where K is the number of returned results. |* If no reranking model is enabled: [1, 1000]<br><br>* If a reranking model is enabled: [1, Top K] |
   |Rerank |Specify whether to use a reranking model to rerank the retrieved chunks.<br><br>Enabling a reranking model delivers more accurate question\-text chunk similarity scores, improving retrieval performance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the reranking model is enabled, the retrieval duration will increase slightly and will be proportional to the number of retrieved text chunks. We recommend that you set an appropriate number of retrieved text chunks.</div><br> |* Doubao\-Seed\-1.6\-rerank (default): Doubao\-Seed\-1.6\-Rerank is a multimodal reranking model developed by ByteDance. It performs fine\-grained semantic matching and relevance scoring on Top\-K candidates retrieved from multimodal content such as text, images, and videos, and outputs optimized ranking results. Threshold filtering and instruction settings are supported.<br><br>* base\-multilingual\-rerank: It features fast speed, and supports long text and more than 70 languages.<br><br>* m3\-v2\-rerank: It is suitable for common text scenarios and supports more than 100 languages. |
   |Number of chunks entering reranking |This parameter is required when "Rerank" is turned on. It controls the number of recalled text chunks that will be fed into the reranking model.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you set the number of recalled chunks slightly larger than the number of returned results to improve retrieval performance.</div><br> |25 |
   |Threshold filtering |When this feature is enabled, you can set a minimum relevance score. Only results meeting or exceeding this score will be returned. The default value is 0.5. |0.5 |
   |Number of recalls (Top K) |Recall refers to the process of retrieving the top K most relevant text chunks from a large number of candidates. This parameter can be configured only when a reranking model is enabled. We recommend that you set the number of recalled chunks slightly larger than the number of returned chunks to improve generation accuracy. |[1, 200] |
   |More parameters \- Dense Weight |When you create a knowledge base, if the selected embedding model and indexing algorithm support hybrid retrieval, the system will consider both the semantic relevance between the question and candidate text chunks and the degree of literal matching during retrieval, resulting in more accurate retrieval results.<br><br>The Dense Weight parameter controls the importance weight of semantic similarity during retrieval. The closer to 1, the more semantic retrieval is favored; the closer to 0, the more keyword matching retrieval is favored. |[0.2, 1] |
   |API call |After saving the settings, you can click "API call" to obtain the API request body, so that you can easily integrate the tested settings into your application. |\-\- |
   

6. Enter your query. The system will return several text chunks most relevant to your question. For more information, see [Knowledge retrieval](https://docs.byteplus.com/en/docs/RAG_Cloud/Knowledge_Retrieval).

---
title: "Knowledge Q&A"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Knowledge_qa_testing"
---

Applicable for scenarios where the knowledge base is used for large model multi\-turn Q&A, providing professional answers based on historical conversations and reference knowledge.

<span id="GrNuJWvq"></span>
## Procedure


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Knowledge Base".

3. Click the name of the target knowledge base to open the details page of the knowledge base.

4. Click the "Knowledge retrieval" button in the upper right corner of the page.

5. Click the "knowledge Q&A" tab to configure retrieval parameters and model response parameters.

   
   |**Parameter​**  |**Purpose** |**Value range** |
   |---|---|---|
   |**Search parameters** |||
   |Number of returned results |Configure the number of results retrieved.<br><br><br>* If no reranking model is enabled, this parameter specifies the number of top N results returned by retrieval.<br><br>* If a reranking model is enabled, this parameter specifies the top K text chunks after reranking, where K is the number of returned results. |* If no reranking model is enabled: [1, 1000]<br><br>* If a reranking model is enabled: [1, Top K] |
   |Rewrite question |When this feature is enabled, the current question will be rewritten based on historical chat to provide complete semantic information, resulting in more accurate retrieval.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Rewriting questions will increase retrieval time and consume additional tokens.</div><br> |Disabled by default |
   |Rerank |Specify whether to use a reranking model to rerank the retrieved chunks.<br><br>Enabling a reranking model delivers more accurate question\-text chunk similarity scores, improving retrieval performance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After the reranking model is enabled, the retrieval duration will increase slightly and will be proportional to the number of retrieved text chunks. We recommend that you set an appropriate number of retrieved text chunks.</div><br> |* Doubao\-Seed\-1.6\-rerank (default): Doubao\-Seed\-1.6\-Rerank is a multimodal reranking model developed by ByteDance. It performs fine\-grained semantic matching and relevance scoring on Top\-K candidates retrieved from multimodal content such as text, images, and videos, and outputs optimized ranking results. Threshold filtering and instruction settings are supported.<br><br>* base\-multilingual\-rerank: It features fast speed, and supports long text and more than 70 languages.<br><br>* m3\-v2\-rerank: It is suitable for common text scenarios and supports more than 100 languages. |
   |Number of chunks entering reranking |This parameter is required when "Rerank" is turned on. It controls the number of recalled text chunks that will be fed into the reranking model.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you set the number of recalled chunks slightly larger than the number of returned results to improve retrieval performance.</div><br> |25 |
   |More parameters \- Dense Weight |When you create a knowledge base, if the selected embedding model and indexing algorithm support hybrid retrieval, the system will consider both the semantic relevance between the question and candidate text chunks and the degree of literal matching during retrieval, resulting in more accurate retrieval results.<br><br>The Dense Weight parameter controls the importance weight of semantic similarity during retrieval. The closer to 1, the more semantic retrieval is favored; the closer to 0, the more keyword matching retrieval is favored. |[0.2, 1] |
   |More parameters \- Document aggregation sorting |When this feature is enabled, the recalled chunks will be sorted and aggregated based on the order of the original document to ensure correct word order and semantic integrity.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>We recommend that you enable this feature in scenarios sensitive to the original document order of reference materials and disable this feature in scenarios where chunk content is logically independent.</strong></div><br> |Enabled by default |
   |**Model answer parameters** |||
   |Select model |Configure the large model used for knowledge base Q&A, as well as its version, inference endpoint, reasoning depth, and other settings. |\-\- |
   |Number of adjacent text slices to concatenate |This parameter specifies the number of adjacent chunks to concatenate after retrieval and reranking. If the number of chunks after retrieval and reranking is k, and the value of this parameter is p, the range of the number of finally returned chunks is [k, k+2*k*p] |[0, 5] |
   |Text slice parameter |Select the parameters and their order to be fed into the large model. After being selected, the parameters will be concatenated in that order to form the prompt, which is then sent to the model. | |
   |Prompt configuration |You can configure this parameter when **Use large model to generate response** is enabled.<br><br><br>* Prompt composition allows you to configure how the user question and retrieved chunks are assembled when they are passed to the large model, as well as other response requirements.<br><br>* Prompt composition must include two variables, using square brackets plus the variable name as placeholders.<br><br>* When organizing the prompt, you can provide instructions to the large model to fit your usage scenario. For example, ask the large model to answer based on the retrieved texts, or transfer to human support if the retrieved information cannot answer the user question.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The platform also provides prompt templates for core scenarios (Customer Service Scenario, Marketing Outreach, Thought Elaboration, Reply Imitation). You can select one based on your business requirements.</div><br> |\-\- |
   |cite the source |After this option is enabled, the sources of the referenced knowledge chunks will be displayed at the end of the response. |\-\- |
   |Mixed text and graphics |When this option is enabled, if the reference material of the large model contains images, the images and text will be displayed together in the response. |\-\- |
   |API call |After saving the settings, you can click "API call" to obtain the API request body, so that you can easily integrate the tested settings into your application. |\-\- |
   

6. Enter the question you want to ask.

   The model assembles the retrieved text chunks into the prompt in the prompt arrangement area, then inputs them into the large model. The large model provides an answer based on the retrieved background information. For more details about the Q&A testing, see [Q&A test](https://docs.byteplus.com/en/docs/RAG_Cloud/Knowledge_QA#qa-testing).

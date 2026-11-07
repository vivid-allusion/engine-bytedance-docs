---
title: "Personal Knowledge Base Search"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/personal-knowledge-base-search"
---

Call this interface to recall the relevant Chunk in the personal knowledge base of the user bound to the current application Token; support qualified documents and recall parameters.

# Interface description

* Interface name: retrieve_personal_knowledge_knowledge_spaces_documents_retrieval_post

* Interface address:/knowledge\-spaces/documents/retrieval

* Request method: POST

# Request parameters

The request body is of type Object, and the personal knowledge base recalls the parameters; KB, tenant, and space attribution are all determined by the server level context. The included parameters are described as follows:

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|question |String |Yes |recall problem |
|doc_ids |Array |No |Restricting the recalled personal library document; no or empty list indicates that the current personal knowledge base is recalled |
|top_k |Number |No |The most recalled slices in the bottom layer |
|top_n |Number |No |The maximum number of slices eventually returned |
|similarity_threshold |Number |No |similarity threshold |
|dense_weight |Number |No |vector similarity weight |
|enable_rerank |Boolean |No |Whether to enable reordering |
|enable_llm_rerank |Boolean |No |Whether to enable large model reordering |
|rerank_score_threshold |Number |No |Rearrangement score threshold |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |total |
|chunks |Array |Yes |Search results, including search slices, are detailed in the **chunks** table below |
|doc_aggs |Array |Yes |Document aggregation, see **doc_aggs** table below |
|summary |String |No |Intelligent retrieval generates summary responses based on recall content |

## chunks

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Array |Yes |Knowledge Base ID |
|kb_name |Array |No |Knowledge base name |
|chunk_id |String |Yes |slice ID |
|content_with_weight |String |Yes |weighted text content |
|doc_id |String |Yes |Document ID |
|important_kwd |Array |Yes |important keywords |
|image_id |String |Yes |image ID |
|similarity |Number |Yes |similarity |
|vector_similarity |Number |Yes |vector similarity |
|term_similarity |Number |Yes |keyword similarity |
|docnm_kwd |String |Yes |document name keyword |
|display_name |String |No |document display name |
|content_ltks |String |Yes |slice content element |
|highlight |String |No |highlight |
|question |String |No |question |
|extra |Object |No |additional data |
|rank_score |Number |No |Sort score |
|source |String |No |source |
|character_count |Number |No |The number of characters in the current slice |
|duration |String |No |Slice duration/location information |
|url |String |No |Document file URL |
|title |Array |No |slice title |
|channel_score |Object |No |Recall link breakdown details, key is channel name; value is JSON parsing result or original string |
|channel_name |String |No |recall link name |
|orig_similarity |Number |No |Original chunk recall similarity (before fusion) |
|orig_rerank_score |Number |No |Raw Rearrangement Score (Before Fusion) |
|doc_meta_recall_similarity |Number |No |Total doc_meta_recall Recall Score (after multiplexing) |
|doc_meta_recall_scores |Object |No |doc_meta_recall fractions per channel, key is channel name |
|doc_meta_recall_channel_name |String |No |Hit the doc_meta_recall channel name; when strategy = weight, it is separated by multiple commas, and other strategies are the one with the highest score |
|is_personal_kb |Boolean |No |Does it come from a personal knowledge base? |

## doc_aggs

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |String |Yes |Document ID |
|tenant_id |Number |No |Tenant ID |
|kb_id |Number |No |Knowledge Base ID |
|doc_name |String |Yes |Document name |
|display_name |String |No |document display name |
|count |Number |Yes |quantity |
|create_time |String |No |creation time |
|labels |Array |No |Document labels, see the **labels** table below |
|avg_score |Number |No |average score |
|semantic_score |Number |No |semantic score |
|text |String |No |Text |
|is_personal_kb |Boolean |No |Does it come from a personal knowledge base? |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|label_id |Number |Yes |Tag ID |
|label_name |String |No |label name |
|label_type |String |Yes |label type |
|label_values |Array |No |List of label values, see **label_values** table below |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |
|prompt_version |String |No |Cue word version |
|label_usage |Number |No |tag usage |

## label_values

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |tag value ID |
|value |String |No |label value |
|value_usage |Number |No |tag value usage |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |

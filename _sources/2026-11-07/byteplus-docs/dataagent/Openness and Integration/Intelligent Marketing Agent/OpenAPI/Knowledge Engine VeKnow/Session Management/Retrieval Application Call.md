---
title: "Retrieval Application Call"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/retrieval-application-call"
---

Call this interface to call the published retrieval application and return the pure recall result.

# **Interface description**

* Interface name: open_retrieval_app_conversation_retrieval_open_post

* Interface address:/conversation/retrieval/open

* Request method: POST

# Header

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|authorization |String |No |Open API Gateway authentication; use /system/api_key generated Bearer API Key when connecting directly to VeraG.<br><br>Example value: "Bearer b6adc01e819c4ad \*\*\*\*" |

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|app_id |Number |No |The search application ID has been published. Required for open calls; dialog_id when not app_id. |
|dialog_id |Number |Yes |Retrieve the application ID. Open calls are required and must be consistent with the application to which the API Key is bound. |
|question |String |Yes |Search for keywords or questions. |
|rag_setting |Object |Yes |Recall parameters for this call. Open Call Required. Detailed parameters are described in the **rag_setting** table below. |
|metadata |Object |No |Extended parameters. Supports overriding recall parameters with metadata rag_setting. |

## rag_setting

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |No |Knowledge base ID list, open call required and cannot be empty. |
|doc_ids |Array |No |List of document IDs qualified for retrieval; null means not qualified by document. |
|graph_ids |Array |No |Knowledge Graph ID list, currently a reserved field. |
|ontology_ids |Array |No |Ontology ID list, currently a reserved field. |
|enable_kb_priority |Boolean |No |Whether to enable Knowledge Base Priority. P0/P1/P2 grouping priority recall by kb_priority when enabled. |
|kb_priority |Object |No |Knowledge base priority configuration, the key is fixed to p0, p1, p2, value is the knowledge base ID list. |
|similarity_threshold |Number |No |Mix the similarity threshold and recall only slices with a composite score greater than or equal to the threshold. |
|dense_weight |Number |No |Vector retrieves weights. The lower the value, the more partial keyword matching, and the higher the value, the more partial semantic vector matching. |
|top_k |Number |No |The number of candidate slices for initial screening. |
|top_n |Number |No |Finally, the number of slices is returned. |
|enable_rerank |Boolean |No |Whether to enable the semantic reordering model. |
|enable_llm_rerank |Boolean |No |Whether to enable large model reordering. |
|rank_score_threshold |Number |No |The reorder score threshold takes effect only in reorder scenarios. |
|label_value_ids |Array < Number \> or Array < String \> |No |List of knowledge tag value IDs. Multiple values within the same label are OR, and between different labels are AND. |
|enable_agent_enhance_search |Boolean |No |Whether to enable intelligent search. After opening, the search keywords will be enhanced through the large model. |
|extra |Object |No |Extension parameters passed through to the underlying recall service. |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |message content |
|data |Object |Yes |For detailed parameter descriptions, see the **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |total |
|chunks |Array |Yes |Search results, detailed parameter descriptions can be found in the following **chunks** table |
|doc_aggs |Array |Yes |Documentation aggregation, detailed parameter description see **doc_aggs** table below |
|summary |String |No |Intelligent retrieval generates summary responses based on recall content |

## chunks

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |Yes |Knowledge Base Identifier |
|chunk_id |String |Yes |segmentation identifier |
|content_with_weight |String |Yes |segment weight |
|doc_id |String |Yes |Document ID |
|important_kwd |Array |Yes |core keywords |
|image_id |String |Yes |Picture ID |
|similarity |Number |Yes |similarity |
|vector_similarity |Number |Yes |vector similarity |
|term_similarity |Number |Yes |term similarity |
|docnm_kwd |String |Yes |document name keyword |
|display_name |String |No |document display name |
|content_ltks |String |Yes |content tag |
|highlight |String |No |highlight segment |
|question |String |No |Search for keywords or questions |
|extra |Object |No |extension parameter |
|rank_score |Number |No |ranking score |
|source |String |No |data source |
|character_count |Number |No |The number of characters in the current slice |
|duration |String |No |Slice duration/location information |
|url |String |No |Document file URL |
|title |String |No |The segment title extracted from the table header |

## doc_aggs

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |String |Yes |Document ID |
|doc_name |String |Yes |Document name |
|display_name |String |No |document display name |
|count |Number |Yes |quantity |
|create_time |String |No |creation time |
|labels |Array |No |Document labels, see the **labels** table below |
|avg_score |Number |No |average score |
|semantic_score |Number |No |semantic division |
|text |String |No |Text |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|label_id |Number |Yes |Tag ID |
|label_name |String |No |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_values |Array |No |List of label values, see **label_values** table below |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |
|prompt_version |String |No |Cue word version |
|label_usage |Number |No |tag usage |

### label_values

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |tag value ID |
|value |String |No |label value |
|value_usage |Number |No |tag value usage |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |

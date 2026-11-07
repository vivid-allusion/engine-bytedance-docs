---
title: "Multi-Knowledge Base Retrieval"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/multi-knowledge-base-retrieval"
---

Calling this interface retrieves multiple knowledge bases in parallel based on semantics or keywords, and fuses and returns related document fragments. The interface follows the knowledge base, documents, tags, permissions, and expiration filter rules.

# Interface description

* Interface name: multi_retrieval_chunk_multi_retrieval_post

* Interface address:/chunk/multi_retrieval

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |No |Knowledge Base ID |
|kb_ids |Array |No |Knowledge Base ID List |
|doc_ids |Array |No |document identifier |
|folder_ids |Array |No |VeRAG directory identifier |
|question |String |Yes |query question |
|similarity_threshold |Number |No |similarity threshold |
|vector_similarity_weight |Number |No |vector similarity weight |
|top_k |Number |No |How many chunks are returned at most each time, the default value is 100 |
|size |Number |No |The maximum number of documents to return is 30. In most cases, a file uploaded corresponds to a document; when there are multiple sheets, a sheet corresponds to a document |
|keyword |Array |No |keyword |
|label_value_ids |Array |No |tag value ID |
|label_values |Array |No |label value |
|llm_id |Number |No |Large Model ID |
|stream |Boolean |No |streaming output |
|enable_filters |Boolean |No |Enable permission/label/expiration filtering |
|enable_keyword |Boolean |No |Enable keyword extraction. After opening, if the keyword is empty, the keyword is extracted; otherwise, the provided keyword is used. |
|enable_rerank |Boolean |No |Enable reordering |
|enable_llm_rerank |Boolean |No |Enable LLM reordering |
|rerank_score_threshold |Number |No |Reorder score threshold |
|enable_kb_priority |Boolean |No |Enable Knowledge Base Priority |
|kb_priority |Object |No |Knowledge base priority grouping, see **kb_priority** table below |
|chunk_recall_config |Object |No |Slice recall configuration: channels + auto build switch, see **chunk_recall_config** table below |
|doc_meta_recall_config |Object |No |Documentation meta information recall configuration: filtering or chunk weighting based entry_id overview/guide/keywords, see below **doc_meta_recall_config** table |
|extra |Object |No |Additional information |
|rag_setting |Object |No |RAG search configuration, see **rag_setting** table below |
|include_personal_kb |Boolean |No |Whether to recall the current user's personal knowledge base at the same time |
|personal_doc_ids |Array |No |Personal Knowledge Base Document Identifier |
|personal_folder_ids |Array |No |Personal Knowledge Base Folder Identifier |

## kb_priority

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|p0 |Array |No |High priority knowledge base ID |
|p1 |Array |No |Middle priority knowledge base ID |
|p2 |Array |No |Low priority knowledge base ID |

## chunk_recall_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|channels |Array |No |Multiple recall channels; if enable_summary/enable_keywords/enable_questions is open when empty, it will be automatically replenished. Please refer to the **channels** table below for details |
|enable_summary |Boolean |No |Channels automatically make up one chunk_summary channel when empty |
|enable_keywords |Boolean |No |Channels is the space\-time control main channel keyword boost;<br><br><br>* True go Sophon default (boost keywords field)<br><br>* False explicitly add main + use_chunk_keyword = false close boost |
|enable_questions |Boolean |No |Channels automatically make up one chunk_questions channel when empty |

### channels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |channel name |
|keywordField |String |No |Keywords Recall field names (e.g. chunk_summary/chunk_questions/chunk_keywords) |
|vectorField |String |No |Vector recall field names (e.g. embedding/embedding_summary) |
|vectorWeight |Number |No |The channel vector weight |
|useChunkKeyword |Boolean |No |* Nil/true: add boost = 2.0 to the keywords field when BM25<br><br>* False: not added |

## doc_meta_recall_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|channels |Array |No |Multi\-channel doc_meta_recall configuration; if enable_overview/enable_guide is turned on when empty, it will be automatically replenished. For details, please refer to the **channels** table below |
|strategy |String |No |Filter/weight, default weight |
|filter_timing |String |No |Pre/post, only valid when strategy = filter |
|weight_mode |String |No |Fusion method of chunk and doc_meta score: multiply (multiplication weighted, default)/linear (linear weighted), only valid when strategy = weight |
|doc_meta_linear_weight |Number |No |doc_meta weights in linear fusion: final = chunk_score \* (1 \- w) + doc_meta_score \* w, only if strategy = weight and weight_mode = linear |
|doc_meta_multiply_weight |Number |No |doc_meta weight in multiplicative fusion: final = chunk_score \* (1 + doc_meta_score \* w), only when strategy = weight and weight_mode = multiply |
|min_confidence |Number |No |doc_meta_recall the maximum score is lower than this value, it is discarded globally |
|channel_fusion |String |No |Multichannel merge strategy: max (maximum)/weight (weighted average by channel_weight, default) |
|enable_overview |Boolean |No |Channels is an overview channel automatically filled with empty time |
|enable_guide |Boolean |No |Channels is a free\-time automatic guide channel |

### channels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |channel name |
|fields |Array |Yes |doc_meta_recall field name list:<br><br><br>* overview<br><br>* guide<br><br>* keywords |
|vector_weight |Number |No |The weight of the path vector is passed through to DocMetaSophonService. Recall |
|channel_weight |Number |No |The weight of the channel in the fusion of multiple channels only takes effect when channel_fusion = weight |

## **rag_setting**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |No |Knowledge Base ID List |
|doc_ids |Array |No |Document ID List |
|folder_ids |Array |No |VeRAG Directory ID List |
|graph_ids |Array |No |graph ID list |
|ontology_ids |Array |No |Ontology ID List |
|enable_kb_priority |Boolean |No |Whether to enable Knowledge Base Priority |
|kb_priority |Object |No |Knowledge base priority grouping, see **kb_priority** table above |
|similarity_threshold |Number |No |recall similarity threshold |
|vector_similarity_weight |Number |No |Vector search weight |
|top_k |Number |No |Maximum number of candidate shardings for a single recall channel |
|top_n |Number |No |Final return recall results upper limit |
|enable_rerank |Boolean |No |Whether to enable semantic rearrangement |
|enable_llm_rerank |Boolean |No |Whether to enable LLM rearrangement |
|rerank_score_threshold |Number |No |Rearrangement score threshold |
|label_value_ids |Array<br><br>Or Array < String \> |No |Label value ID list |
|enable_agent_enhance_search |Boolean |No |Whether to enable Agent Enhanced Retrieval |
|chunkRecallConfig |Object |No |Slice recall configuration: channels + auto\-build switch, see the **chunkRecallConfig** table below for details |
|doc_meta_recall_config |Object |No |Documentation meta information recall configuration: filtering or chunk weighting based entry_id overview/guide/keywords, see below **doc_meta_recall_config** table |
|extra |Object |No |additional search parameters |

## chunkRecallConfig

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|channels |Array |No |Multiple recall channels; if enable_summary/enable_keywords/enable_questions is open when empty, it will be automatically replenished. For details, please refer to the **chunkRecallConfig.channels** table below |
|enable_summary |Boolean |No |Channels automatically make up one chunk_summary channel when empty |
|enable_keywords |Boolean |No |Channels is empty to control the main channel keyword boost; true takes Sophon default (boost keywords field), false explicitly adds main + use_chunk_keyword = false to close boost |
|enable_questions |Boolean |No |Channels automatically make up one chunk_questions channel when empty |

## chunkRecallConfig.channels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |channel name |
|keywordField |String |No |Keywords Recall field names (e.g. chunk_summary/chunk_questions/chunk_keywords) |
|vectorField |String |No |Vector recall field names (e.g. embedding/embedding_summary) |
|vectorWeight |Number |No |The channel vector weight |
|useChunkKeyword |Boolean |No |Nil/true: add boost = 2.0 to the keywords field when BM25; false |

## doc_meta_recall_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|channels |Array |No |Multi\-channel doc_meta_recall configuration; if enable_overview/enable_guide is turned on when empty, it will be automatically replenished. For details, please refer to the **doc_meta_recall_config. Channels** table below |
|strategy |String |No |Filter/weight, default weight |
|filter_timing |String |No |Pre/post, only valid when strategy = filter |
|weight_mode |String |No |Fusion method of chunk and doc_meta score: multiply (multiplication weighted, default)/linear (linear weighted), only valid when strategy = weight |
|doc_meta_linear_weight |Number |No |doc_meta weights in linear fusion: final = chunk_score \* (1 \- w) + doc_meta_score \* w, only if strategy = weight and weight_mode = linear |
|doc_meta_multiply_weight |Number |No |doc_meta weight in multiplicative fusion: final = chunk_score \* (1 + doc_meta_score \* w), only when strategy = weight and weight_mode = multiply |
|min_confidence |Number |No |doc_meta_recall the maximum score is lower than this value, it is discarded globally |
|channel_fusion |String |No |Multichannel merge strategy: max (maximum)/weight (weighted average by channel_weight, default) |
|enable_overview |Boolean |No |Channels is an overview channel automatically filled with empty time |
|enable_guide |Boolean |No |Channels is a free\-time automatic guide channel |

## doc_meta_recall_config.channels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |channel name |
|fields |Array |Yes |doc_meta_recall list of field names: overview/guide/keywords |
|vector_weight |Number |No |The weight of the path vector is passed through to DocMetaSophonService. Recall |
|channel_weight |Number |No |The weight of the channel in the fusion of multiple channels, only channel_fusion = w |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |For details, please refer to the **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |total |
|chunks |Array |Yes |Search results, see the **chunks** table below |
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
|duration |String |No |Slice duration or location information |
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

## **doc_aggs**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |String |Yes |Document ID |
|tenant_id |Number |No |Tenant ID |
|kb_id |Number |No |Knowledge Base ID |
|doc_name |String |Yes |Document name |
|display_name |String |No |document display name |
|count |Number |Yes |quantity |
|create_time |String |No |creation time |
|labels |Array |No |Label information, see the **labels** table below |
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
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
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

---
title: "Recall Structured Knowledge"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/recall-structured-knowledge"
---

Invoke this interface to perform a mixed search by single table scope, exact filtering, semantic fields, return fields, and sort parameters and return data rows.

* Caller: Open API application, external agent, or integration service.

* Prerequisites: The caller has access to the knowledge base, the target asset index is ready, and the selected field capabilities are valid.

# Interface description

* Interface name: recall_structured_knowledge_v1_kbs__kb_id__recall_post

* Interface address:/structured_knowledge/v1/kbs/{kb_id}/recall

* Request method: POST

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |Yes |Structured Knowledge Base ID, returned by the Create Knowledge Base or Query Knowledge Base List interface |

## Request body

Object type, including parameter description as follows:

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|asset_id |String |Yes |The data asset ID limited by this recall only supports single\-form recall. |
|filters |Object |No |Field exact filter conditions; support root node plus a layer of condition group, up to 10 leaf conditions. See the **filters** below for details |
|timezone |String |No |IANA time zone name, such as Asia/Shanghai; required when using dynamic dates |
|semantic_query |String |No |Semantic search keywords, up to 200 characters; pure filtering can be recalled without passing |
|vector_fields |Array |No |The name of the logical field participating in the semantic recall, only fields that have completed vector construction can be selected |
|return_fields |Array |Yes |The recall result needs to return the logical field name, choose at least one |
|candidate_count |Number |No |The number of candidate rows entering the sorting stage must be greater than or equal to top_k |
|top_k |Number |No |The final number of recalled lines returned, ranging from 1 to 100. |
|rank_config |Object |No |See **rank_config** table below for details |
|debug |Boolean |No |Whether debug mode is enabled; open interface responses do not expose underlying compilation requests |

## filters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|logic |String |No |* AND<br><br>* OR |
|conditions |Array |No |List of filter criteria for the root node. See the **conditions** table below |
|groups |Array |No |A layer of nested condition groups; all leaf conditions total up to 10. See the **groups** table below for details |

## conditions

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|field |String |Yes |The name of the logical field participating in the filtering, the field must have conditional filtering enabled |
|operator |String |Yes |* eq<br><br>* ne<br><br>* gt<br><br>* ge<br><br>* lt<br><br>* le<br><br>* between<br><br>* is_null<br><br>* is_not_null<br><br>* contains<br><br>* not_contains<br><br>* in<br><br>* not_in |
|value |AnyOf (AnyOf indicates that the field may return one or more of a variety of data structures<br><br>） |No |Filter values; is_null/is_not_null can be omitted, between uses double\-ended |

## groups

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|logic |String |No |* AND<br><br>* OR |
|conditions |Array |No |A leaf condition in a subgroup; a subgroup cannot be empty and is not allowed to continue nesting. See the **conditions** table above for details |

## rank_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|rank_type |String |No |* none<br><br>* semantic_rerank<br><br>* llm_rerank |
|vector_weight |Number |No |Vector score weights in mixed search, ranging from 0 to 1 |
|hybrid_score_threshold |Number |No |Hybrid recall similarity threshold; candidates below the threshold are filtered |
|rank_score_threshold |Number |No |Semantic rearrangement score threshold; only semantic_rerank |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|rows |Object |No |Recall rows sorted by relevance. See the **rows** table below for details |
|summary |Object |No |See the **summary** table below for details |

## rows

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|rank |Number |Yes |Recall results ranking, starting from 1 |
|row_id |String |Yes |Hit row ID, corresponding to row_key |
|hit_type |String |No |Hit type, such as vector plus filter, vector only, or filter only |
|scores |Object |No |A collection of mixed recall scores, vector scores, or rearrangement scores, with the in\-object data type Number. |
|source_asset |Object |Yes |See **source_asset** table below for details |
|values |Object |No |Row data cropped by return_fields |
|highlight_fields |Array |No |Logical field name for hit filtering or semantic recall |

## source_asset

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |String |No |Structured Knowledge Base ID to which the hit row belongs |
|asset_id |String |No |The data asset ID to which the hit row belongs |

## summary

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |No |The number of rows returned by this recall |
|log_id |String |No |Recall the link log ID for troubleshooting |

---
title: "Graph Retrieval"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/graph-retrieval"
---

Call this interface to perform vector + graph hybrid retrieval on the specified graph, and return the recalled content without going through the large model.

# **Interface description**

* Interface name: graph_retrieval_query_graph_retrieval_post

* Interface address:/query/graph/retrieval

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|query |String |Yes |query statement |
|subject_id |Number |Yes |Graph ID |
|top_k |Number |No |number returned |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|log_id |String |No |log ID |
|message |String |No |error message |
|data |Object |No |Table data, detailed parameter description see below **data**<br><br>table |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |No |total data |
|results |Array |No |List of search results, see the **results** table below for detailed parameter descriptions |

## results

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|query_type |String |Yes |Query type. Enumeration values include:<br><br><br>* vector<br><br>* graph<br><br>* structured<br><br>* cdp |
|rank |Number |Yes |ranking |
|content |String |Yes |content |
|metadata |Object |No |Details of retrieved metadata, detailed parameter descriptions can be found in the following **metadata** table |
|source |Object |Yes |Knowledge base information, detailed parameter description see the **source** table below |

## metadata

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|chunk_id |String |No |Document block ID |
|doc_id |String |No |Document ID |
|similarity |Number |No |similarity |
|vector_similarity |Number |No |vector similarity |
|term_similarity |Number |No |term similarity |
|doc_name |String |No |Document name |
|query_sql |String |No |Query SQL |
|row_data |Object |No |row data |
|data |Error |No |data |

## source

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number or Array <<br><br>Number\> |No |Knowledge base ID, may return multiple |
|kb_type |String |No |Knowledge base types, enumeration values include:<br><br><br>* general<br><br>* subject |
|entity_type |String |No |entity type |

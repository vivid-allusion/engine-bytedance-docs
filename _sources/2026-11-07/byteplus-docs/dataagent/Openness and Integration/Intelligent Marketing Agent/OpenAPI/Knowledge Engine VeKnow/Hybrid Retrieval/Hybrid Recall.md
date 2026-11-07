---
title: "Hybrid Recall"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/hybrid-recall"
---

This interface is called to perform a hybrid recall query on the table of the underlying search engine based on DSL. Before invoking the current interface, you should first call [Create Table Structure](https://docs.byteplus.com/docs/dataagent/create-table-structure) to complete table structure creation, and call [Write Data](https://docs.byteplus.com/docs/dataagent/write-data) to write recallable data.

> **注意**

> For the detailed description of this interface, it is recommended to go to the Enterprise Knowledge Engine console and check the "**Hybrid Retrieval \- Hybrid Recall**" API description in the \*\*\*\* **Project Center** \> **Open API** \> Open Capabilities.

# Interface description

* Interface name: hybrid_recall_sophon_hybridRecall_post

* Interface address:/sophon/hybridRecall

* Request method: POST

# Request parameters

Sophon hybridRecall request, Object type, imported parameters and /query/dsl alignment, the service layer will be converted to Sophon protocol.

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|v |Number |No |v |
|target |Object |Yes |Query target definition: table/knowledge base/CK\-ref<br><br><br>* When type = table: use name as ClickHouse table name (supports db.table or single table name)<br><br>* When type = kb: use kb_id map to internal storage (table name/view), the mapping table is maintained by the translator<br><br>* When type = ck_ref: Use meta_id to resolve to external CK table and data field mapping |
|query |Object |Yes |Top\-level query container |
|select |Array |No |select |
|group_by |Array |No |group_by |
|having |Object |Yes |Aggregate alias\-based filtering (following the filter paradigm, using only the filter field in it) |
|page |Object |No |page |
|sort |Array |No |sort |
|debug |Object |No |Debugging options: whether to return SQL/EXPLAIN/automatic partitioning/execution engine |
|rerankEnabled |Boolean |No |Whether to enable Sophon hybridRecall rerank; mainboard uses default policy when not passing |
|rrfEnabled |Boolean |No |Whether to enable rrf scoring hybridRecall rrfEnabled; when not passed, silently |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon hybrid recall response, see **data** sheet below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|result |Error |No |Sophon hybridRecall returns the original content of the data field |
|log_id |String |No |The logId returned by Sophon |

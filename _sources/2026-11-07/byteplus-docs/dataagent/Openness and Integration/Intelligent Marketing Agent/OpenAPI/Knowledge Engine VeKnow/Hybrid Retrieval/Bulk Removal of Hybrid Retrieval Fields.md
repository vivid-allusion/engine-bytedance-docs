---
title: "Bulk Removal of Hybrid Retrieval Fields"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/bulk-removal-of-hybrid-retrieval-fields"
---

Call this interface to batch delete multiple fields in the table of the underlying search engine. Before calling, you should confirm that the target table and fields exist, and you can call [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) first to view the current table structure.

# Interface description

* Interface name: delete_hybrid_fields_sophon_deleteHybridFields_post

* Interface address:/sophon/deleteHybridFields

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|fieldNames |Array |Yes |List of field names to be deleted |
|userId |String |No |Operator ID |

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
|success |Boolean |Yes |Whether the deletion was successful |
|table_name |String |Yes |target table name |
|field_names |Array |No |List of deleted field names |
|message |String |No |result description |
|raw_data |Object |No |Sophon raw return data |
|log_id |String |No |The logId returned by Sophon |

---
title: "Delete Hybrid Retrieval Field"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-hybrid-retrieval-field"
---

Call this interface to delete a single field in the table of the underlying search engine. Before calling, you should confirm that the target table and fields exist, and you can call [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) first to view the current table structure.

# Interface description

* Interface name: delete_hybrid_field_sophon_deleteHybridField_post

* Interface address:/sophon/deleteHybridField

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|fieldName |String |Yes |Field name to be deleted |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon deletes single\-field responses, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Whether the deletion was successful |
|table_name |String |Yes |target table name |
|field_name |String |Yes |Deleted field name |
|message |String |No |result description |
|raw_data |Object |No |Sophon raw return data |
|log_id |String |No |The logId returned by Sophon |

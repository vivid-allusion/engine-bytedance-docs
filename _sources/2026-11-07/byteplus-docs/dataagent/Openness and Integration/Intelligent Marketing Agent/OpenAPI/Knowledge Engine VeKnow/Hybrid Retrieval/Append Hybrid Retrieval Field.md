---
title: "Append Hybrid Retrieval Field"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/append-hybrid-retrieval-field"
---

Calling this interface for the existing underlying search engine table append fields, and can synchronize the declaration of vector search fields and full\-text search fields. Before calling by [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure)querying the current table structure.

# Interface description

* Interface name: add_hybrid_fields_sophon_addHybridFields_post

* Interface address:/sophon/addHybridFields

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|fieldTypes |Array |Yes |Added field definition list. For details, please refer to the following<br><br>**fieldTypes** table |
|vectorFields |Array |No |A list of field names for vector search needs to be established |
|fullTextFields |Array |No |List of field names required to support full\-text search |
|userId |String |No |Operator ID |

## fieldTypes

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|name |String |Yes |field name |
|type |String |Yes |Field types such as string/long/object |
|uniqueKey |Boolean |No |Is it a unique key, corresponding to Sophon createTableSchema.fieldTypes [] .uniqueKey |
|comment |String |No |Field remarks |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon appends field responses, see **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Whether the addition was successful |
|table_name |String |Yes |target table name |
|message |String |No |result description |
|added_fields_size |Number |No |The number of new fields returned by Sophon |
|raw_data |Object |No |Sophon raw return data |
|log_id |String |No |The logId returned by Sophon |

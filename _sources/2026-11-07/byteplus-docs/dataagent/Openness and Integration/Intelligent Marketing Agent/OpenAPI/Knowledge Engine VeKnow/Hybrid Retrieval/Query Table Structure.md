---
title: "Query Table Structure"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-table-structure"
---

Invoke this interface to query the table structure of the underlying search engine, and return the primary key, field definition, vector field and full\-text search field configuration.

# Interface description

* Interface name: get_table_schema_sophon_getTableSchema_post

* Interface address:/sophon/getTableSchema

* Request method: POST

# Request parameters

Object type Sophon lookup table structure request, the parameter description is as follows:

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon lookup table structure response, see **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|table_name |String |Yes |table name |
|id_field |String |No |Primary key field name |
|field_types |Array |No |field definition list |
|vector_fields |Array |No |Vectorized field list |
|full_text_fields |Array |No |full\-text search field list |
|storage_type |String |No |Storage types, such as OPENSEARCH |
|log_id |String |No |The logId returned by Sophon |

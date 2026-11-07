---
title: "Create Table Structure"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/create-table-structure"
---

Call this interface to create the underlying search engine table structure, declare field definition, vector search field and full\-text search field. Before writing data, you should call the current interface to complete the table construction, and then call the [Write Data](https://docs.byteplus.com/docs/dataagent/write-data) to write data.

# Interface description

* Interface name: create_table_schema_sophon_createTableSchema_post

* Interface address:/sophon/createTableSchema

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|fieldTypes |Array |Yes |Field definition list, corresponding to Sophon createTableSchema.fieldTypes. See the **fieldTypes** table below for details |
|vectorFields |Array |No |A list of field names for vector search needs to be established |
|fullTextFields |Array |No |List of field names required to support full\-text search |

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
|data |Object |Yes |Sophon built the table response, please refer to the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Was created successfully? |
|table_name |String |Yes |target table name |
|message |String |Yes |result description |
|field_count |Number |Yes |number of fields |
|vector_fields |Array |No |Declared vector field |
|full_text_fields |Array |No |Declared full\-text fields |
|log_id |String |No |The logId returned by Sophon |

---
title: "Write Data"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/write-data"
---

Call this interface to write data to the table of the underlying search engine. Before calling the current interface, you should first call [Create Table Structure](https://docs.byteplus.com/docs/dataagent/create-table-structure) to create table structure, or confirm that the target table already exists; after writing, you can call [Hybrid Recall](https://docs.byteplus.com/docs/dataagent/hybrid-recall) to verify the recall effect.

# Interface description

* Interface name: write_data_sophon_writeData_post

* Interface address:/sophon/writeData

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|rawData |Array |Yes |List of data rows to be written, corresponding to Sophon writeData.rawData |
|batchSize |Number |No |Batch size when calling Sophon writeData in batches at the server level |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon writes data response, see **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Is the write successful? |
|table_name |String |Yes |target table name |
|total_rows |Number |Yes |total number of rows requested |
|inserted_rows |Number |Yes |Number of lines successfully written |
|failed_rows |Number |Yes |number of failed lines |
|doc_ids |Array |No |List of document IDs returned by Sophon |
|errors |Array |No |Error message list |
|request_options |Object |No |Additional options used in this request, such as batch_size |
|log_id |String |No |The logId returned by Sophon |

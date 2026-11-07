---
title: "Delete Data"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-data"
---

Call this interface to delete the data in the table of the underlying search engine according to the data ID. Before calling, you can call [Query Table Structure](https://docs.byteplus.com/docs/dataagent/query-table-structure) to confirm that the target table exists, and confirm that the ID comes from [Write Data](https://docs.byteplus.com/docs/dataagent/write-data) the data that has been written.

# Interface description

* Interface name: delete_data_sophon_deleteData_post

* Interface address:/sophon/deleteData

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|ids |Array |Yes |List of data IDs to be deleted, corresponding to Sophon deleteData.ids |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon deletes the data response, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Whether the deletion was successful |
|table_name |String |Yes |target table name |
|requested_count |Number |Yes |The number of IDs deleted in this request (Sophon does not return the actual number of deletions, this is the number of requests) |
|errors |Array |No |Error message list |
|message |String |Yes |result description |
|log_id |String |No |The logId returned by Sophon |

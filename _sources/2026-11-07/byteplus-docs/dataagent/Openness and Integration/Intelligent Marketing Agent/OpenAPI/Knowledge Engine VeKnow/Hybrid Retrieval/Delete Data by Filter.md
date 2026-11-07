---
title: "Delete Data by Filter"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/delete-data-by-filter"
---

Call this interface to delete the data in the table of the underlying search engine according to DSL filtering conditions. Before calling, you can use [Hybrid Recall](https://docs.byteplus.com/docs/dataagent/hybrid-recall) to verify that the filter conditions can accurately hit the data to be deleted to avoid accidental deletion.

# Interface description

* Interface name: delete_by_filter_sophon_deleteByFilter_post

* Interface address:/sophon/deleteByFilter

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|tableName |String |Yes |target table name |
|filter |Error |Yes |Delete filter conditions, DSL format corresponding to Sophon hybridRecall/query, passable object or JSON string |
|userId |String |No |Operator ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Sophon removes responses by filter, see **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success |Boolean |Yes |Whether the deletion was successful |
|table_name |String |Yes |target table name |
|message |String |No |result description |
|raw_data |Object |No |Sophon raw return data |
|log_id |String |No |The logId returned by Sophon |

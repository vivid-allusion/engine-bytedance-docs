---
title: "Batch Export of QA Knowledge"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-export-of-qa-knowledge"
---

Call this interface to export the knowledge items in QA library, Query library or term library in batches, and support the exact export of all matching content according to the entry ID or the query conditions. The interface returns the asynchronous export task ID, and the task results can be viewed later in the download task list.

# Interface description

* Interface name: export_qa_like_chunk_export_post

* Interface address:/chunk/export

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge Base ID |
|ids |Array |No |Specify the exported entry ID; null means all matching content is exported |
|query |String |No |Query conditions when exporting in full |
|format |String |No |Export format:<br><br><br>* csv<br><br>* xlsx |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Batch export results, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|success_ids |Array |Yes |Success ID List |
|failed_ids |Array |Yes |list of failed IDs |
|invalid_ids |Array |Yes |list of invalid IDs |
|errors |Array |No |Error message list |
|task_id |Number |Yes |Task ID |

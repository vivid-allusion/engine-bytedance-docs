---
title: "Batch Import of QA Knowledge"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/batch-import-of-qa-knowledge"
---

Call this interface through the uploaded table file batch import QA library, Query library or term library knowledge.

# Prerequisite

Before calling the current interface, you should first call [Upload File](https://docs.byteplus.com/docs/dataagent/upload-file) to upload xlsx, xls or csv files, and fill the returned file ID into files; the interface will create or reuse the import task, and the import progress can be queried through [Query Knowledge Import Task of QA Type](https://docs.byteplus.com/docs/dataagent/query-knowledge-import-task-of-qa-type).

# Interface description

* Interface name: import_chunk_chunk_import_post

* Interface address:/chunk/import

* Request method: POST

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |No |Knowledge Base ID |
|files |Array |Yes |File ID List |
|task_id |Numbner |No |Task ID; 0 indicates a new import task |
|dedup_strategy |String |No |QA deduplicate policy. Optional values:<br><br><br>* QUESTION: deduplicate by issue (default)<br><br>* QUESTION_LABEL: Questions + Tags |
|dedup_existing |Boolean |No |Whether to deduplicate inventory.<br><br><br>* True: check DB match duplicates<br><br>* False: only deduplicate inside the input (always new, default) |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |List of failed import files, see **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|task_id |Number |No |Task ID, used to query task progress or retry |
|success_count |Number |No |Number of successfully imported items |
|failed_count |Number |No |number of import failures |
|total_count |Number |No |Total number of cases (success + failure) |
|failed_file_download_url |String |No |Failed data download link, empty means no failure or not generated. |
|failed_reason |Object |No |Collections of failure causes grouped by file_id |
|failed_files |Array |No |List of failed files, see **failed_files** table below |

## failed_files

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |File ID |
|name |String |No |file name |
|reason |String |Yes |reason for failure |

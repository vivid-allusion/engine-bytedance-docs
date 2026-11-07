---
title: "Query Knowledge Import Task of QA Type"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-knowledge-import-task-of-qa-type"
---

Page calls this interface to query the batch import task progress of QA library, Query library or term library, and returns the task status, successful quantity, failed quantity and failed file download address. Typically, after calling [Batch Import of QA Knowledge](https://docs.byteplus.com/docs/dataagent/batch-import-of-qa-knowledge), the import results are tracked using the current interface.

# Interface description

* Interface name: import_task_list_chunk_import_task_list_get

* Interface address:/chunk/import/task/list

* Request method: GET

# **Request parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_id |Number |Yes |Knowledge Base ID |
|page |Number |No |page number |
|page_size |Number |No |page size |
|status |String |No |Status filtering; empty or unknown are considered TOTAL |
|keywords |String |No |keyword query |
|kb_type |String |No |Knowledge base type |
|import_source |String |No |task import source |
|source_type |String |No |Task import source type |
|chunk_settings_type |String |No |File parsing type for local tasks |
|update_type |String |No |Mission update_type |

# **Response parameters**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|page |Number |Yes |page number |
|page_size |Number |Yes |number of pages per page |
|total |Number |Yes |total |
|items |Array |No |List of tasks, see the **items** list below |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |Task id; prep maps from id |
|file_id |Number |Yes |File id; prep mapped from schedule_task_id |
|task_name |String |No |Filename; prep mapped from task_name |
|prep_task_id |Number |No |Prep task id |
|import_source |String |No |Mission Source:<br><br><br>* Local: Local files<br><br>* S3: object storage |
|source_type |String |No |Depending on the `import_source`value, the current parameter has different meanings:<br><br><br>* `import_source = local`as file format<br><br>* `import_source = s3`is the object storage type |
|update_type |String |No |Update Type:<br><br><br>* auto<br><br>* manual |
|failed_download_url |String |No |Download address; prep fixed to empty string |
|chunk_total_count |Number |No |Total number of imports; prep fixed to 0 |
|chunk_success_count |Number |No |Number of import successes; prep is fixed to 0 |
|chunk_failed_count |Number |No |Number of import failures; prep is fixed to 0 |
|status |String |No |Status:<br><br><br>* CREATED<br><br>* RUNNING<br><br>* SUCCESS<br><br>* FAILED<br><br>* KILLED<br><br>* TOTAL<br><br>* WAITING_TIME<br><br>* WAITING_DEPENDENCY<br><br>* WAITING_PARALLEL_QUOTA<br><br>* WAITING_SUBMIT<br><br>* WAITING_RESOURCE_QUOTA<br><br>* WAITING_COMPUTE_QUOTA |
|type |String |No |Task type:<br><br><br>* local<br><br>* prep |
|create_by |String |No |Task creator; prep fixed to empty string |
|create_date |String |No |Task creation time; prep maps from schedule_time |
|finish_date |String |No |Task completion time; prep maps from end_time |
|update_date |String |No |Task update time; prep maps from task_time |
|failed_reason |String |No |List of failure causes; local returns collection, prep is empty |
|chunk_settings_type |String |No |Local file \- corresponds to a parse type |

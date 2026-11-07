---
title: "Query Structured Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/query-structured-task"
---

Calling this interface uses unified task_ref to query local file import, Prep dataset import, or asynchronous delete task status.

* Caller: Open API application, external agent, or integration service.

* Precondition: The caller has view rights on the task\-associated knowledge base.

# Interface description

* Interface name: get_structured_task_structured_knowledge_v1_tasks__task_ref__get

* Interface address:/structured_knowledge/v1/tasks/

* Request method: GET

# Request parameters

## Path

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|task_ref |String |Yes |Uniform task reference; return local: < id \> or prep: < asset_id \> using the initiating import or delete interface |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |Yes |Data. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|task_ref |String |Yes |Unified task reference, consistent with the return value of the initiating import or deleting interface |
|status |String |Yes |state<br><br><br>* PENDING<br><br>* RUNNING<br><br>* SUCCEEDED<br><br>* PARTIAL_FAILED<br><br>* FAILED |
|task_type |String |Yes |Type of task, such as STRUCTURED_IMPORT |
|asset_id |String |No |Task associated data asset ID |
|progress |Number |No |Task progress, range 0 to 1 |
|create_time |String |No |task creation time |
|start_time |String |No |Task start time |
|update_time |String |No |Last update time of task |
|end_time |String |No |task end time |
|error_code |String |No |Standardized failure error code; empty without failure |
|error_message |String |No |Failure reason; empty if not failed |

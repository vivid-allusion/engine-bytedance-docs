---
title: "listVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbTask_v2"
---

<span id="overview"></span>
# Overview

Get information for multiple Tasks, returning up to 20 entries at once.

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().list_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.ListVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`. |
|collection_name |str |2 choose 1 |Collection name, corresponds to API field `CollectionName`. |
|resource_id |str | |Collection resource ID, corresponds to API field `ResourceId`. |
|task_status |str |Yes |Task status, corresponds to API field `TaskStatus`, possible values: `init`/`queued`/`running`/`done`/`fail`/`confirm`/`confirmed`. |
|task_type |str |Yes |Task type, corresponds to API field `TaskType`, can be `data_import`, `data_export`, `filter_update`, `filter_delete`. |
|page_number |int |No |Page number, corresponds to API field `PageNumber`, must be ≥0. |
|page_size |int |No |Page size, corresponds to API field `PageSize`, range 1~100. |


<span id="response-parameters"></span>
# Response Parameters

Returns `ListVikingdbTaskResponse` on success, containing pagination information and task list:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|tasks |list[TaskForListVikingdbTaskOutput] |Task list, each element corresponds to a task, see the table below for fields. |
|page_number |int |Current page number, corresponds to API field `PageNumber`. |
|page_size |int |Page size, corresponds to API field `PageSize`. |
|total_count |int |Total number of tasks meeting the criteria, corresponds to API field `TotalCount`. |


Fields for tasks elements:


|**Field** |**Type** |**Description** |
|---|---|---|
|task_id |str |Task ID, API field `TaskId`. |
|task_type |str |Task type, API field `TaskType`. |
|task_status |str |Task status, API field `TaskStatus`. |
|create_time |str |Creation time, API field `CreateTime`. |
|update_time |str |Update time, API field `UpdateTime`. |
|update_person |str |Last updated by, API field `UpdatePerson`. |
|task_config |TaskConfigForListVikingdbTaskOutput |Task configuration, see the table below for fields. |
|task_process_info |TaskProcessInfoForListVikingdbTaskOutput |Task progress information, see the table below for fields. |


task_config field description:


|**Field** |**Type** |**Description** |
|---|---|---|
|collection_name |str |Collection name, API field `CollectionName`. |
|project_name |str |Project name, API field `ProjectName`. |
|resource_id |str |Collection resource ID, API field `ResourceId`. |
|file_type |str |Import/export file format, API field `FileType`. |
|filter_conds |list[object] |Filter condition array, API field `FilterConds`. |
|export_all |bool |Whether to export all data, API field `ExportAll`. |
|ignore_error |bool |Whether to ignore single entry exceptions, API field `IgnoreError`. |
|need_confirm |bool |Whether manual confirmation is required, API field `NeedConfirm`. |
|tos_path |str |TOS path, API field `TosPath`. |
|use_public |bool |Whether to access TOS via public domain, API field `UsePublic`. |
|update_fields |object |Field update configuration, API field `UpdateFields`. |


task_process_info field description:


|**Field** |**Type** |**Description** |
|---|---|---|
|task_progress |str |Task progress information, API field `TaskProgress`. |
|total_data_count |int |Total data volume, API field `TotalDataCount`. |
|total_filter_count |int |Data volume meeting criteria, API field `TotalFilterCount`. |
|scan_data_count |int |Number of data entries scanned, API field `ScanDataCount`. |
|sample_timestamp |str |Sample timestamp, API field `SampleTimestamp`. |
|sample_data |list[object] |Sample results, API field `SampleData`. |
|error_message |str |Error message, API field `ErrorMessage`. |


<span id="example"></span>
# Example

```python
import os
import volcenginesdkcore
import volcenginesdkvikingdb as vdb
from volcenginesdkvikingdb.api.vikingdb_api import VIKINGDBApi

configuration = volcenginesdkcore.Configuration()
configuration.ak = os.environ["VIKINGDB_AK"]
configuration.sk = os.environ["VIKINGDB_SK"]
configuration.region = os.environ["VIKINGDB_REGION"]
configuration.host = os.environ["VIKINGDB_HOST"]
configuration.scheme = "https"
volcenginesdkcore.Configuration.set_default(configuration)

client = VIKINGDBApi()

request = vdb.ListVikingdbTaskRequest(
    collection_name="sdk_demo_collection",
    task_status="running",
    task_type="data_export",
    page_number=0,
    page_size=20,
)
response = client.list_vikingdb_task(request)
print("total:", response.total_count)
for task in response.tasks or []:
    print(task.task_id, task.task_status)
```

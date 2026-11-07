---
title: "getVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbTask_v2"
---

<span id="overview"></span>
# Overview

Query the detailed information and execution progress of a specified Task.

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().get_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.GetVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|task_id |str |Yes |Task ID, corresponds to the API field `TaskId`. |


<span id="response-parameters"></span>
# Response Parameters

The interface returns `GetVikingdbTaskResponse` with the following fields:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|task_id |str |Task ID, corresponds to the API field `TaskId`. |
|task_type |str |Task type, corresponds to the API field `TaskType`. Possible values include `data_import`, `data_export`, `filter_update`, `filter_delete`. |
|task_status |str |Task status, corresponds to the API field `TaskStatus`. Possible values are `init`/`queued`/`confirm`/`confirmed`/`running`/`done`/`fail`. |
|create_time |str |Task creation time (RFC3339), corresponds to the API field `CreateTime`. |
|update_time |str |Last update time, corresponds to the API field `UpdateTime`. |
|update_person |str |Last updated by, corresponds to the API field `UpdatePerson`. |
|task_config |TaskConfigForGetVikingdbTaskOutput |Task configuration details, corresponds to the API field `TaskConfig`. See the table below for fields. |
|task_process_info |TaskProcessInfoForGetVikingdbTaskOutput |Task progress information, corresponds to the API field `TaskProcessInfo`. See the table below for fields. |


`task_config` field description:


|**Field** |**Type** |**Description** |
|---|---|---|
|collection_name |str |The name of the Collection the task acts on, API field `CollectionName`. |
|project_name |str |Project name, API field `ProjectName`. |
|resource_id |str |Collection resource ID, API field `ResourceId`. |
|file_type |str |Import/export file format, API field `FileType`. |
|filter_conds |list[object] |Task filter condition array, API field `FilterConds`. |
|export_all |bool |Whether to export all data, only effective for `data_export` tasks. API field `ExportAll`. |
|ignore_error |bool |Whether to ignore individual errors, API field `IgnoreError`. |
|need_confirm |bool |Whether manual confirmation is required, API field `NeedConfirm`. |
|tos_path |str |TOS path, API field `TosPath`. |
|use_public |bool |Whether to access TOS via public domain, API field `UsePublic`. |
|update_fields |object |Field update configuration, API field `UpdateFields` (used by `filter_update` tasks). |


`task_process_info` field description:


|**Field** |**Type** |**Description** |
|---|---|---|
|task_progress |str |Task progress description, API field `TaskProgress`. |
|total_data_count |int |Total data volume, API field `TotalDataCount`. |
|total_filter_count |int |Data volume matching filter conditions, API field `TotalFilterCount`. |
|scan_data_count |int |Number of scanned data entries, API field `ScanDataCount`. |
|sample_timestamp |str |Sample timestamp, API field `SampleTimestamp`. |
|sample_data |list[object] |Sampled data, API field `SampleData`. |
|error_message |str |Error message, API field `ErrorMessage`. |


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

request = vdb.GetVikingdbTaskRequest(task_id="t-20240201xxxx")
response = client.get_vikingdb_task(request)
print("task:", response.task_id, response.task_status)
if response.task_config:
    print("collection:", response.task_config.collection_name)
if response.task_process_info:
    print("progress:", response.task_process_info.task_progress)
```

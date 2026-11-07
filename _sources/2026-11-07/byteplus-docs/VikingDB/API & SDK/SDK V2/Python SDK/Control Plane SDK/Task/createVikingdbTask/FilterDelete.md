---
title: "FilterDelete"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FilterDelete_v2"
---

<span id="overview"></span>
# Overview

Through the `CreateVikingdbTask` interface with `task_type` set to `filter_delete`, you can batch delete documents in a Collection by conditions.

<span id="method-definition"></span>
# Method Definition

The Python SDK calls through `VIKINGDBApi().create_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters

To back up data to TOS, first authorize VikingDB for cross\-service access to TOS [Authorize Now](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb)


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|project_name | |str |No |The project to which the task belongs, corresponding to API field `ProjectName`, inherits SDK configuration by default. |
|collection_name | |str |1 of 2 required |Collection name, corresponding to API field `CollectionName`. |
|resource_id | |str | |Collection resource ID, corresponding to API field `ResourceId`. |
|task_type | |str |Yes |Task type, corresponding to API field `TaskType`, fixed to `filter_delete` for this interface. |
|task_config | |TaskConfigForCreateVikingdbTaskInput |Yes |Delete task configuration, corresponding to API field `TaskConfig`. |
| |tos_path |str |No |TOS path, format: {bucket name}/{path}, note this is not a domain name. Required if backing up to TOS, corresponding to API field `TosPath`. |
| |file_type |str |No |File type, `json` or `parquet`. Required if backing up to TOS, corresponding to API field `FileType`. |
| |filter_conds |Map |Yes |Filter conditions. Reference: https://www.volcengine.com/docs/84313/1419289, corresponding to API field `FilterConds`. |
| |need_confirm |bool |No |Whether manual confirmation is required, default is `true`, corresponding to API field `NeedConfirm`. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|task_id |str |Task ID |
|message |str |Operation result message |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

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

filter_conditions = [
    { "op": "must", "field": "type", "conds": ["xxx"] },
    { "op": "range", "field": "score", "gt": 5 }
]

task_cfg = vdb.TaskConfigForCreateVikingdbTaskInput(
    filter_conds=filter_conditions,
    need_confirm=True,
)

request = vdb.CreateVikingdbTaskRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    task_type="filter_delete",
    task_config=task_cfg,
)
response = client.create_vikingdb_task(request)
print("task id:", response.task_id)
print("message:", response.message)
```


<span id="post-processing"></span>
## Post\-processing

If `need_confirm=True`, you can confirm in the console or update the task status to `confirmed` via the `VIKINGDBApi().update_vikingdb_task()` call.

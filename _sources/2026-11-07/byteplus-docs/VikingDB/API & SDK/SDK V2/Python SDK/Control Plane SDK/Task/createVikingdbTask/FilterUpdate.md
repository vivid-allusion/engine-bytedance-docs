---
title: "FilterUpdate"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/FilterUpdate_v2"
---

<span id="overview"></span>
# Overview

Through the `CreateVikingdbTask` interface with `task_type=filter_update`, you can batch update scalar fields in a Collection by conditions (vector, sparse_vector, and text types are not supported).

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().create_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|project_name | |str |No |The project to which the task belongs, corresponding to the API field `ProjectName`. |
|collection_name | |str |Either one |Collection name, corresponding to the API field `CollectionName`. |
|resource_id | |str | |Collection resource ID, corresponding to the API field `ResourceId`. |
|task_type | |str |Yes |Task type, corresponding to the API field `TaskType`, fixed as `filter_update`. |
|task_config | |TaskConfigForCreateVikingdbTaskInput |Yes |Update task configuration, corresponding to the API field `TaskConfig`. |
| |filter_conds |list[object] |Yes |Filter conditions. Refer to `https://www.volcengine.com/docs/84313/1419289` for usage, corresponding to the API field `FilterConds`. |
| |update_fields |object |Yes |Field values to be updated. Must be scalar fields; updates of vector, sparse_vector, and text type fields are not supported. Corresponding to the API field `UpdateFields`. |


<span id="response-parameters"></span>
# Response Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|task_id |str |Task ID, corresponding to the API field `TaskId`. |
|message |str |Task creation result description, corresponding to the API field `Message`. |


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

update_fields = {
    "status": "archived",
    "score": 0.5,
}

task_cfg = vdb.TaskConfigForCreateVikingdbTaskInput(
    filter_conds=[
        { "op": "must", "field": "type", "conds": ["xxx"] },
        { "op": "range", "field": "score", "gt": 5 }
    ],
    update_fields=update_fields,
)

request = vdb.CreateVikingdbTaskRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    task_type="filter_update",
    task_config=task_cfg,
)
response = client.create_vikingdb_task(request)
print("task id:", response.task_id)
print("message:", response.message)
```

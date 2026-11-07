---
title: "DataImport"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/DataImport_v2"
---

<span id="overview"></span>
# Overview

Import data files from TOS to the specified Collection via the `CreateVikingdbTask` interface with `task_type=data_import`. The fields must align with the Collection Schema.

Before using, please authorize VikingDB cross\-service access to TOS [Authorize](https://console.volcengine.com/iam/service/attach_role/?ServiceName=vikingdb).

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().create_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Sub\-parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|project_name | |str |No |The project to which the task belongs, corresponding to API field `ProjectName`. If not filled, it uses the SDK default project. |
|collection_name | |str |2 options |Collection name, corresponding to API field `CollectionName`. |
|resource_id | |str | |Collection resource ID, corresponding to API field `ResourceId`. |
|task_type | |str |Yes |Task type, corresponding to API field `TaskType`. For import tasks, this is fixed as `data_import`. |
|task_config | |TaskConfigForCreateVikingdbTaskInput |Yes |Import task configuration, corresponding to API field `TaskConfig`. |
| |tos_path |str |Yes |TOS path of the file to be imported, corresponding to API field `TosPath`. Format: {bucket name}/{path}. Note this is not a domain name. |
| |file_type |str |Yes |TOS file format, corresponding to API field `FileType`. Supports `parquet`, `json`. |
| |ignore_error |bool |No |Whether to ignore single import errors, corresponding to API field `IgnoreError`. |


<span id="response-parameters"></span>
# Response Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|task_id |str |Task ID, corresponding to API field `TaskId` |
|message |str |Task creation result description, corresponding to API field `Message` |


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

task_cfg = vdb.TaskConfigForCreateVikingdbTaskInput(
    file_type="parquet",
    tos_path="your-bucket/path/to/data.parquet",
    ignore_error=False,
)

request = vdb.CreateVikingdbTaskRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    task_type="data_import",
    task_config=task_cfg,
)
response = client.create_vikingdb_task(request)
print("task id:", response.task_id)
print("message:", response.message)
```

---
title: "deleteVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteVikingdbTask_v2"
---

<span id="overview"></span>
# Overview

Deletes the specified task. The task will be terminated after deletion.

<span id="method-definition"></span>
# Method Definition

The Python SDK calls this interface through `VIKINGDBApi().delete_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.DeleteVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|task_id |str |Yes |Task ID, corresponding to API field `TaskId`, which can be obtained from the task creation or query interfaces. |


<span id="response-parameters"></span>
# Response Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|message |str |Operation result description, corresponding to API field `Message`. |


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

request = vdb.DeleteVikingdbTaskRequest(task_id="t-20240201xxxx")
response = client.delete_vikingdb_task(request)
print(response.message or "delete task finished")
```

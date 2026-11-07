---
title: "updateVikingdbTask"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbTask_v2"
---

<span id="overview"></span>
# Overview

Update the specified task. The current task update is only used for the manual confirmation step of **deleting** a task.

<span id="method-definition"></span>
# Method Definition

The Python SDK is called via `VIKINGDBApi().update_vikingdb_task(request)`, where `request` is of type `volcenginesdkvikingdb.UpdateVikingdbTaskRequest`.

<span id="request-parameters"></span>
# Request Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|task_id |str |Yes |Task ID, corresponding to the API field `TaskId`. |
|task_status |str |Yes |New status, corresponding to the API field `TaskStatus`. Currently only supports setting to `confirmed` to confirm a task pending deletion. |


<span id="response-parameters"></span>
# Response Parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|message |str |Operation result description, corresponding to the API field `Message`. |


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

request = vdb.UpdateVikingdbTaskRequest(
    task_id="t-20240201xxxx",
    task_status="confirmed",
)
response = client.update_vikingdb_task(request)
print(response.message or "task confirmed")
```

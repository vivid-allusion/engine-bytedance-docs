---
title: "deleteVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteVikingdbIndex_v2"
---

<span id="Overview"></span>
# Overview

The DeleteVikingdbIndex interface is used to delete an index under a specified Collection, and it cannot be recovered after deletion.

<span id="Method Definition"></span>
# Method Definition

The Python SDK initiates the call through `VIKINGDBApi().delete_vikingdb_index(request)`, where `request` is of type `volcenginesdkvikingdb.DeleteVikingdbIndexRequest`.

<span id="Request Parameters"></span>
# **Request Parameters**


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponding to API field `ProjectName`, default value is default. |
|collection_name |str |One of two is required |The Collection name to which the index belongs, corresponding to API field `CollectionName`. |
|resource_id |str | |Collection resource ID, corresponding to API field `ResourceId`. |
|index_name |str |Yes |The name of the index to be deleted, corresponding to API field `IndexName`. |


<span id="Response Parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|message |str |Status information, corresponding to API field `Message`. |


<span id="Example"></span>
# Example

<span id="Python Example"></span>
## Python Example

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

request = vdb.DeleteVikingdbIndexRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    index_name="sdk_demo_index",
)

response = client.delete_vikingdb_index(request)
print("message:", response.message)
```

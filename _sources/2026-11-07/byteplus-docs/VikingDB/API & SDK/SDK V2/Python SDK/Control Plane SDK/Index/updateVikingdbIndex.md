---
title: "updateVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateVikingdbIndex_v2"
---

<span id="overview"></span>
# Overview

The UpdateVikingdbIndex interface is used to modify the description, scalar index, CPU quota, or sharding policy of an existing index.

<span id="method-definition"></span>
# Method Definition

The Python SDK invokes the method through `VIKINGDBApi().update_vikingdb_index(request)`, where `request` is of type `volcenginesdkvikingdb.UpdateVikingdbIndexRequest`.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`, default value is default. |
|collection_name |str |Either one is required |The dataset to which the index belongs, corresponds to API field `CollectionName`. |
|resource_id |str | |Collection resource ID, corresponds to API field `ResourceId`. |
|index_name |str |Yes |The name of the index to update, corresponds to API field `IndexName`. |
|description |str |No |Index description, corresponds to API field `Description`. |
|cpu_quota |int |No |Available CPU quota for the index, corresponds to API field `CpuQuota`, must be \>= 1. |
|scalar_index |list[str] |No |New list of scalar index fields, corresponds to API field `ScalarIndex`. |
|shard_policy |str |No |Sharding policy, corresponds to API field `ShardPolicy`, supports `auto` and `custom`. |
|shard_count |int |No |Number of shards, corresponds to API field `ShardCount`, only effective when `shard_policy` = `custom`. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Description |
|---|---|---|
|message |str |Request processing result, corresponds to API field `Message`. |


<span id="example"></span>
# Example

<span id="python-example"></span>
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

request = vdb.UpdateVikingdbIndexRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    index_name="sdk_demo_index",
    description="Updated description",
    shard_policy="custom",
    shard_count=2,
)

response = client.update_vikingdb_index(request)
print("message:", response.message)
```

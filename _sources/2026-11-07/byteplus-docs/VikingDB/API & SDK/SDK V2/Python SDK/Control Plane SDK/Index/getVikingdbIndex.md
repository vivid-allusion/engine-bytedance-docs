---
title: "getVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/getVikingdbIndex_v2"
---

<span id="overview"></span>
# Overview

The GetVikingdbIndex interface is used to query the detailed configuration of a single index, including sharding, scalar index, and vector index parameters.

<span id="method-definition"></span>
# Method Definition

The Python SDK initiates the call through `VIKINGDBApi().get_vikingdb_index(request)`, where `request` is of type `volcenginesdkvikingdb.GetVikingdbIndexRequest`.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponding to API field `ProjectName`, default is default. |
|collection_name |str |One of two is required |The name of the dataset to which the index belongs, corresponding to API field `CollectionName`. |
|resource_id |str | |Collection resource ID, corresponding to API field `ResourceId`. |
|index_name |str |Yes |The name of the index to query, corresponding to API field `IndexName`. |


<span id="response-parameters"></span>
# Response Parameters

The return value type is `GetVikingdbIndexResponse`.


|Field |Type |Description |
|---|---|---|
|index_name |str |Index name, corresponding to API field `IndexName`. |
|collection_name |str |The Collection it belongs to, corresponding to API field `CollectionName`. |
|project_name |str |Project name, corresponding to API field `ProjectName`. |
|resource_id |str |Index resource ID, corresponding to API field `ResourceId`. |
|description |str |Index description, corresponding to API field `Description`. |
|cpu_quota |int |Configured CPU quota, corresponding to API field `CpuQuota`. |
|actual_cu |int |Actually used compute units, corresponding to API field `ActualCU`. |
|shard_policy |str |Sharding policy, corresponding to API field `ShardPolicy`. |
|shard_count |int |Number of shards, corresponding to API field `ShardCount`. |
|scalar_index |list[ScalarIndexForGetVikingdbIndexOutput] |Scalar index definition, corresponding to API field `ScalarIndex`, structure see table below. |
|vector_index |VectorIndexForGetVikingdbIndexOutput |Vector index parameters, corresponding to API field `VectorIndex`. |



* ScalarIndexForGetVikingdbIndexOutput



|Field |Type |Description |
|---|---|---|
|field_name |str |Field name, corresponding to API field `FieldName`. |
|field_type |str |Field type, corresponding to API field `FieldType`. |
|dim |int |Dimension (only vector fields have value), corresponding to API field `Dim`. |
|default_value |object |Default value, corresponding to API field `DefaultValue`. |
|is_primary_key |bool |Whether it is a primary key, corresponding to API field `IsPrimaryKey`. |



* VectorIndexForGetVikingdbIndexOutput



|Field |Type |Description |
|---|---|---|
|index_type |str |Index type, corresponding to API field `IndexType`. |
|distance |str |Distance metric, corresponding to API field `Distance`. |
|quant |str |Quantization method, corresponding to API field `Quant`. |
|hnsw_m |int |Number of HNSW neighbors, corresponding to API field `HnswM`. |
|hnsw_cef |int |HNSW construction breadth, corresponding to API field `HnswCef`. |
|hnsw_sef |int |HNSW search breadth, corresponding to API field `HnswSef`. |
|diskann_m |int |DiskANN graph out\-degree, corresponding to API field `DiskannM`. |
|diskann_cef |int |DiskANN expansion factor, corresponding to API field `DiskannCef`. |
|cache_ratio |float |Cache ratio, corresponding to API field `CacheRatio`. |
|pq_code_ratio |float |PQ compression ratio, corresponding to API field `PqCodeRatio`. |


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

request = vdb.GetVikingdbIndexRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    index_name="sdk_demo_index",
)

response = client.get_vikingdb_index(request)
print("index_name:", response.index_name)
print("vector index type:", response.vector_index.index_type if response.vector_index else None)
```

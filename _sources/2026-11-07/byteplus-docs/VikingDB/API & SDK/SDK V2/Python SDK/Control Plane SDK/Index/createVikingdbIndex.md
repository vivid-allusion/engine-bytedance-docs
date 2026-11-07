---
title: "createVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/createVikingdbIndex_v2"
---

The price calculator can output three core estimated results based on your data and index configuration: compute resource (CU) usage, storage resource (disk capacity, in GB), and corresponding cost details.

Access link: https://console.volcengine.com/vikingdb/region:vikingdb+cn\-beijing/bohr/price\-calculator

<span id="overview"></span>
# Overview

The CreateVikingdbIndex interface is used to create an index for a specified Collection to improve vector retrieval performance.

Creating an index can accelerate vector similarity search. It groups and sorts the raw data in the vector library according to the specified index algorithm and data structure, improving the efficiency and accuracy of similarity search. This is the core mechanism that enables vector databases to filter out candidates in a short time.

When the indexed Collection only contains dense vectors (i.e., vector type fields), we call this a pure dense index; when the indexed Collection contains both dense vectors and sparse vectors (vector and sparse_vector type fields), we call this a hybrid index.

<span id="method-definition"></span>
# Method Definition

The Python SDK initiates calls via `VIKINGDBApi().create_vikingdb_index(request)`, where `request` is of type `volcenginesdkvikingdb.CreateVikingdbIndexRequest`.

<span id="request-parameters"></span>
# **Request Parameters**

The table below lists the configurable fields for CreateVikingdbIndexRequest. Field meanings can be understood in conjunction with the examples in `examples/vikingdb_examples.py`.


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponding to the API field `ProjectName`, default is "default". |
|collection_name |str |One of two |Collection name, corresponding to the API field `CollectionName`. At least one of this and `resource_id` must be filled in. |
|resource_id |str |One of two |Collection resource ID, corresponding to the API field `ResourceId`. |
|index_name |str |Yes |Name of the index to create, corresponding to the API field `IndexName`.<br><br><br>* Starts with a letter, can contain letters, numbers, and underscores, length 1\-128 bytes.<br><br>* Must be unique within the same Collection.<br><br>* Maximum 200 indices per account. |
|description |str |No |Index description, corresponding to the API field `Description`, maximum 65535 bytes. |
|cpu_quota |int |No |CPU quota used for index creation/retrieval, corresponding to the API field `CpuQuota`, must be \>= 1. |
|scalar_index |list[str] |No |List of field names to build scalar indexes for, corresponding to the API field `ScalarIndex`. Only existing fields in the Collection are supported. |
|shard_policy |str |No |Sharding policy, corresponding to the API field `ShardPolicy`. Supports `auto` (default) and `custom`. |
|shard_count |int |No |Number of index shards, corresponding to the API field `ShardCount`. Takes effect when `shard_policy` is `custom`. |
|vector_index |VectorIndexForCreateVikingdbIndexInput |No |Vector index configuration, corresponding to the API field `VectorIndex`, see table below. |



* VectorIndexForCreateVikingdbIndexInput parameter structure



|Parameter |Type |Required |Default Value |Description |
|---|---|---|---|---|
|index_type |str |No |*  |Index type, corresponding to the API field `IndexType`. Common values: `hnsw`, `hnsw_hybrid`, `flat`, `diskann`. |
|distance |str |No |*  |Vector distance type, corresponding to the API field `Distance`. Supports `ip`, `cosine`, `l2`. |
|hnsw_m |int |No |*  |Maximum number of neighbors in the HNSW graph, corresponding to the API field `HnswM`. |
|hnsw_cef |int |No |*  |HNSW CEF (search breadth during graph construction), corresponding to the API field `HnswCef`. |
|hnsw_sef |int |No |*  |HNSW SEF (search breadth for online retrieval), corresponding to the API field `HnswSef`. |
|diskann_m |int |No |*  |Out\-degree of each node in the DiskANN graph, corresponding to the API field `DiskannM`. Only effective for DiskANN indexes. |
|diskann_cef |int |No |*  |Expansion factor for DiskANN construction/querying, corresponding to the API field `DiskannCef`. |
|cache_ratio |float |No |*  |Hot cache ratio for disk indexes, corresponding to the API field `CacheRatio`. |
|pq_code_ratio |float |No |*  |PQ compression ratio, corresponding to the API field `PqCodeRatio`. |
|quant |str |No |*  |Quantization type, corresponding to the API field `Quant`. Supports `int8`, `fix16`, `float`, `pq`. |


<span id="response-parameters"></span>
# Response Parameters

Return value type is `CreateVikingdbIndexResponse`.


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |str |success |Request status description, corresponding to the API field `Message`. |


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

request = vdb.CreateVikingdbIndexRequest(
    project_name="default",
    collection_name="sdk_demo_collection",
    index_name="sdk_demo_index",
    description="Demo HNSW index",
    shard_policy="auto",
    vector_index=vdb.VectorIndexForCreateVikingdbIndexInput(
        index_type="hnsw",
        distance="cosine",
        hnsw_m=32,
        hnsw_cef=200,
    ),
)

response = client.create_vikingdb_index(request)
print("message:", response.message)
```

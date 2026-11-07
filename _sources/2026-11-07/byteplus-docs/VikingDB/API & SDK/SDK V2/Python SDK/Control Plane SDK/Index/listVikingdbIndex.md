---
title: "listVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/listVikingdbIndex_v2"
---

<span id="overview"></span>
# Overview

The ListVikingdbIndex interface is used to query the list of indexes under a project, and can be filtered by Collection, index name keyword, or status.

<span id="method-definition"></span>
# Method Definition

The Python SDK initiates calls through `VIKINGDBApi().list_vikingdb_index(request)`, where `request` is of type `volcenginesdkvikingdb.ListVikingdbIndexRequest`.

<span id="request-parameters"></span>
# Request Parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|project_name |str |No |Project name, corresponds to API field `ProjectName`, default is `default`. |
|page_number |int |No |Page number, corresponds to API field `PageNumber`, starting from 1 (passing 0 also indicates the first page). |
|page_size |int |No |Number of items per page, corresponds to API field `PageSize`, range 1\-100. |
|filter |FilterForListVikingdbIndexInput |No |Filter conditions, corresponds to API field `Filter`, structure as follows. |



* FilterForListVikingdbIndexInput



|Parameter |Type |Description |
|---|---|---|
|collection_name |list[str] |Filter by Collection name, corresponds to API field `CollectionName`. |
|index_name_keyword |str |Index name keyword matching, corresponds to API field `IndexNameKeyword`. |
|status |list[str] |Index status filter, corresponds to API field `Status` (e.g., CREATING, ACTIVE, FAILED). |


<span id="response-parameters"></span>
# Response Parameters

The return value type is `ListVikingdbIndexResponse`.


|Parameter |Type |Description |
|---|---|---|
|indexes |list[IndexForListVikingdbIndexOutput] |Index details list, corresponds to API field `Indexes`. |
|page_number |int |Current page number, corresponds to API field `PageNumber`. |
|page_size |int |Number of items per page, corresponds to API field `PageSize`. |
|total_count |int |Total number of indexes meeting the conditions, corresponds to API field `TotalCount`. |



* IndexForListVikingdbIndexOutput



|Field |Type |Description |
|---|---|---|
|index_name |str |Index name, corresponds to API field `IndexName`. |
|collection_name |str |所属 Collection, corresponds to API field `CollectionName`. |
|project_name |str |Project name, corresponds to API field `ProjectName`. |
|resource_id |str |Index resource ID, corresponds to API field `ResourceId`. |
|description |str |Index description, corresponds to API field `Description`. |
|cpu_quota |int |Configured CPU quota, corresponds to API field `CpuQuota`. |
|actual_cu |int |Actual used compute units, corresponds to API field `ActualCU`. |
|shard_policy |str |Sharding policy, corresponds to API field `ShardPolicy`. |
|shard_count |int |Number of shards, corresponds to API field `ShardCount`. |
|scalar_index |list[ScalarIndexForListVikingdbIndexOutput] |Scalar index field definition, corresponds to API field `ScalarIndex`, structure shown in the table below. |
|vector_index |VectorIndexForListVikingdbIndexOutput |Vector index configuration, corresponds to API field `VectorIndex`, structure is consistent with creation. |
|index_names |list[str] |Collection of index names under the Collection, corresponds to API field `IndexNames`. |



* ScalarIndexForListVikingdbIndexOutput



|Field |Type |Description |
|---|---|---|
|field_name |str |Field name, corresponds to API field `FieldName`. |
|field_type |str |Field type, corresponds to API field `FieldType`. |
|dim |int |Vector dimension (if applicable), corresponds to API field `Dim`. |
|default_value |object |Default value, corresponds to API field `DefaultValue`. |
|is_primary_key |bool |Whether it is a primary key, corresponds to API field `IsPrimaryKey`. |



* VectorIndexForListVikingdbIndexOutput



|Field |Type |Description |
|---|---|---|
|index_type |str |Index type, corresponds to API field `IndexType` (e.g., hnsw, diskann, flat, hnsw_hybrid). |
|distance |str |Distance metric, corresponds to API field `Distance` (ip/cosine/l2). |
|quant |str |Quantization method, corresponds to API field `Quant` (int8/fix16/float/pq). |
|hnsw_m |int |Number of HNSW graph neighbors, corresponds to API field `HnswM`. |
|hnsw_cef |int |HNSW construction breadth `HnswCef`. |
|hnsw_sef |int |HNSW online search breadth `HnswSef`. |
|diskann_m |int |DiskANN graph out\-degree, corresponds to API field `DiskannM`. |
|diskann_cef |int |DiskANN expansion factor, corresponds to API field `DiskannCef`. |
|cache_ratio |float |Hot cache ratio, corresponds to API field `CacheRatio`. |
|pq_code_ratio |float |PQ compression ratio, corresponds to API field `PqCodeRatio`. |


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

request = vdb.ListVikingdbIndexRequest(
    project_name="default",
    page_number=1,
    page_size=10,
    filter=vdb.FilterForListVikingdbIndexInput(
        collection_name=["sdk_demo_collection"],
        index_name_keyword="sdk",
    ),
)

response = client.list_vikingdb_index(request)
print("total_count:", response.total_count)
for idx in response.indexes or []:
    print(idx.index_name, idx.vector_index.index_type if idx.vector_index else None)
```

---
title: "Get Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Get_Index_V2"
---

<span id="763bf361"></span>
# Overview

Interface for viewing details of a specified index

<span id="3ae85523"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: https://docs.byteplus.com/en/docs/VikingDB/info1

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter naming style |CamelCase (`IndexName`) |Underscore (`index_name`) |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 interfaces is identical.


<span id="f7e44904"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK, or construct a signature for authentication.</div>


<span id="e6291570"></span>
## Request Parameters

Request parameter Action value: GetVikingdbIndex.

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Required |Description |
|---|---|---|---|
|ProjectName |String |No |Project name |
|CollectionName |String |Conditional |Dataset name |
|ResourceId |String ||Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |String |Yes |Index name |


<span id="7117aafa"></span>
## Response Parameters

The table below only lists the response parameters specific to this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |First\-level Sub\-parameter |Type |Description |
|---|---|---|---|
|CollectionName | |String |Dataset name |
|ProjectName | |String |Project name |
|ResourceId | |String |Resource ID |
|IndexName | |String |Index name |
|CpuQuota | |Integer |CPU quota consumed by index retrieval. |
|ShardPolicy | |String |The index sharding type. Valid values are auto (automatic sharding) and custom (custom sharding). |
|ShardCount | |Integer |Index shard count |
|Description | |String |Index description |
|VectorIndex | |Map |Vector index configuration |
||IndexType |String |Index type |
||Distance |String |Distance type, algorithm for measuring distance between vectors. Values are as follows:<br><br>ip: Stands for Inner Product. This algorithm calculates similarity based on the inner product of two vectors, which is the sum of the products of their corresponding elements. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance. It calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine similarity (also known as cosine distance) is used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. The smaller the cosine value, the larger the angle between the two vectors, indicating greater differences between the vectors.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When the index algorithm selects IVF, the distance type can be ip or cosine.<br><br>For the hnsw_hybrid indexing algorithm, distance type selection only takes effect for dense vectors, and sparse vectors only support inner product. |
||Quant |String |Quantization is the compression method for vectors in the index, which can reduce the complexity of similarity calculations between vectors. Based on the high dimensionality and large scale characteristics of vectors, vector quantization can effectively reduce storage and computational costs of vectors. Values are as follows:<br><br><br>* int8: Compresses 4\-byte float to a single byte to gain memory and computational latency benefits, causing minor precision loss, such as cosine distance may result in scores greater than 1.<br><br>* float: Full precision, with no compression.<br><br>* fix16: Compresses 4\-byte float to two bytes to gain memory and computational latency benefits, causing minor precision loss. By sacrificing certain retrieval accuracy, retrieval performance is improved and resource costs are saved.<br><br>* pq: Converts high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip and cosine.<br><br>float is applicable to hnsw, hnsw_hybrid, flat, and diskann indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>fix16 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>pq is applicable to diskann and ivf indexing algorithms, with distance methods of ip, l2, and cosine. |
||HnswM |Integer |HNSW index parameter, representing the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||HnswCef |Integer |HNSW index parameter, representing the breadth of searching for neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||HnswSef |Integer |HNSW index parameter, representing the search breadth for online retrieval.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||DiskannM |Integer |DiskANN parameter, identifying the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as diskann. |
||DiskannCef |Integer |DiskANN parameter, representing the breadth of searching for neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as diskann. |
||PqCodeRatio |Float |DiskANN parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it will increase memory usage, range (0.0, 0.25].<br><br><br>* Optional configuration when index_type is configured as diskann. |
||CacheRatio |Float |DiskANN parameter, ratio of cached nodes to raw data. Larger values will improve index performance and increase memory usage. Range [0.0,0.3).<br><br><br>* Optional configuration when index_type is configured as diskann. |
|ScalarIndex | |Array of String |Scalar field list<br><br>```Python```<br>```"ScalarIndex": [```<br>```    {```<br>```        "FieldName": "f_int64_1", #string```<br>```        "FieldType": "int64", #string```<br>```        "DefaultValue": 0 #any```<br>```    },```<br> |
|ActualCU | |Integer |Actual CU usage |


<span id="f237f0b1"></span>
## Request Example

```Plain
action = "GetVikingdbIndex",
body = {
  "CollectionName": "coll_test1",
  "IndexName": "idx_test1"
}
```


<span id="5f58809e"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "20250527175301151172242186A24F67",
    "Action": "GetVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "CpuQuota": 1,
    "ShardPolicy": "auto",
    "ShardCount": 1,
    "Description": "",
    "ScalarIndex": [
      "f_string"
    ],
    "VectorIndex": {
      "IndexType": "hnsw",
      "Distance": "ip",
      "Quant": "int8",
      "HnswM": 20,
      "HnswCef": 400,
      "HnswSef": 400,
    },
    "IndexCost": {
      "CpuCore": 1,
      "MemGb": 2
    },
    "CollectionName": "coll_test1",
    "IndexName": "idx_test1",
    "ProjectName": "default",
    "ResourceId": "vdb-abcabcabc"
  }
}
```


<span id="8987d5f3"></span>
## Error Codes

For common error codes, please refer to the linked guide.

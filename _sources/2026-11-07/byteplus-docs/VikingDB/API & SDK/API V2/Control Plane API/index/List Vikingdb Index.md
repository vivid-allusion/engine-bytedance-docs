---
title: "List Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/List_Index_V2"
---

<span id="5022d044"></span>
# Overview

To manage and monitor your vector database resources, you can call the ListVikingdbIndex API. This API allows you to retrieve a paginated list of your indexes and filter the results by index name, status, or collection name.

<span id="2db60e5a"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: https://docs.byteplus.com/en/docs/VikingDB/list2

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter naming style |CamelCase (`IndexName`) |Underscore (`index_name`) |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 interfaces is identical.


<span id="f0a7473f"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="3be892ae"></span>
## Request Parameters

The value of the Action request parameter is ListVikingdbIndex.

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |First\-level Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|PageNumber | |Integer |No |Page number for pagination. Starting from 1. |
|PageSize | |Integer |No |Page size for pagination. |
|Filter | |Map |No |Filter conditions |
||IndexNameKeyword |String |No |Keywords contained in the index name |
||Status |Array of String |No |Index status |
||CollectionName |Array of String |No |Dataset name |


<span id="b17282c8"></span>
## Response Parameters

The table below only lists the response parameters specific to this interface. For more information, please see[Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |First\-level Sub\-parameter |Second\-level Sub\-parameter |Type |Description |
|---|---|---|---|---|
|Indexes | | |Map |Vector database index details list |
||CollectionName | |String |Dataset name |
||ProjectName | |String |Project name |
||ResourceId | |String |Resource ID |
||IndexName | |String |Index name |
||Description | |String |Custom description of the index. |
||VectorIndex | |Map |Vector index configuration |
|||IndexType |String |Index type |
|||Distance |String |Distance type, algorithm for measuring distance between vectors. Values are as follows:<br><br>ip: Full name is Inner Product, inner product. This algorithm calculates similarity based on the inner product of vectors, which is the result of multiplying the corresponding elements of two vectors and summing them. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance, it calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine similarity (Cosine Similarity), also known as cosine distance (Cosine Distance), used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. A smaller cosine value corresponds to a larger angle between the vectors, indicating a greater difference between them.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When the index algorithm selects IVF, the distance type can be ip or cosine.<br><br>For the hnsw_hybrid indexing algorithm, distance type selection only takes effect for dense vectors, and sparse vectors only support inner product. |
|||Quant |String |Quantization method. Quantization method is the compression method for vectors in the index, which can reduce the complexity of similarity calculations between vectors. Based on the high dimensionality and large scale characteristics of vectors, vector quantization can effectively reduce storage and computational costs of vectors. Values are as follows:<br><br><br>* int8: Compresses 4\-byte float to a single byte to gain memory and computational latency benefits, causing minor precision loss, such as cosine distance may result in scores greater than 1.<br><br>* float: Full precision, no compression quantization.<br><br>* This improves retrieval performance and saves resource costs at the expense of some retrieval accuracy.<br><br>* pq: Converts high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip and cosine.<br><br>float is applicable to hnsw, hnsw_hybrid, flat, and diskann indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>fix16 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>pq is applicable to diskann and ivf indexing algorithms, with distance methods of ip, l2, and cosine. |
|||HnswM |Integer |HNSW index parameter, representing the number of neighbor nodes.<br><br><br>* This is an optional parameter when index_type is hnsw or hnsw_hybrid. |
|||HnswCef |Integer |HNSW index parameter, representing the breadth of searching for neighbor nodes when building the graph.<br><br><br>* This is an optional parameter when index_type is hnsw or hnsw_hybrid. |
|||HnswSef |Integer |HNSW index parameter, representing the search breadth for online retrieval.<br><br><br>* This is an optional parameter when index_type is hnsw or hnsw_hybrid. |
|||DiskannM |Integer |DiskANN parameter, identifying the number of neighbor nodes.<br><br><br>* This is an optional parameter when index_type is diskann. |
|||DiskannCef |Integer |DiskANN parameter, representing the breadth of searching for neighbor nodes when building the graph.<br><br><br>* This is an optional parameter when index_type is diskann. |
|||PqCodeRatio |Float |DiskANN parameter, size limit for vector dimension encoding. A larger value results in a higher recall rate but also increases memory usage. The value range is (0.0, 0.25].<br><br><br>* This is an optional parameter when index_type is diskann. |
|||CacheRatio |Float |DiskANN parameter, ratio of cached nodes to raw data. A larger value improves index performance but also increases memory usage. The value range is [0.0, 0.3).<br><br><br>* This is an optional parameter when index_type is diskann. |
||ScalarIndex | |Array of Map |Scalar field list<br><br>```JSON```<br>```"ScalarIndex": [```<br>```    {```<br>```        "FieldName": "f_int64_1", #string```<br>```        "FieldType": "int64", #string```<br>```        "DefaultValue": 0 #any```<br>```    },```<br> |
||CpuQuota | |Integer |CPU quota consumed by index retrieval. |
||ShardPolicy | |String |The index sharding type. `auto` indicates automatic sharding, and `custom` indicates custom sharding. |
||ShardCount | |Integer |Index shard count |
||ActualCU | |Integer |Actual CU usage |
|PageSize | | |Integer |The PageSize value used in the request. If not specified, this is the default value. |
|PageNumber | | |Integer |The PageNumber value used in the request. If not specified, this is the default value. |
|TotalCount | | |Integer |The total count of query results |


<span id="7aaa6c82"></span>
## Request Example

```Plain
action = "ListVikingdbIndex",
body = {
  "PageNumber": 1,
  "PageSize": 10,
  "Filter": {
    "CollectionName": "test_collection",
    "Status": "READY",
    "IndexNameKeyword": "idx"
  },
  "ProjectName": "default"
}
```


<span id="4d9c9c60"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "202506091046060340120112242B5E18",
    "Action": "ListVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Indexes": [
      {
        "ProjectName": "w",
        "ResourceId": "vdb-abcabcabc",
        "CollectionName": "test_collection",
        "IndexName": "idx_1",
        "Description": "",
        "VectorIndex": {
          "IndexType": "hnsw",
          "Distance": "ip",
          "Quant": "int8",
          "HnswM": 20,
          "HnswCef": 400,
          "HnswSef": 400
        },
        "ScalarIndex": [
          "f_string"
        ],
        "CpuQuota": 1,
        "ShardPolicy": "auto",
        "ShardCount": 1,
        "IndexCost": {
          "CpuCore": 1,
          "MemGb": 1
        }
      }
    ],
    "PageSize": 10,
    "PageNumber": 1,
    "TotalCount": 1
  }
}
```


<span id="8f29d968"></span>
## Error Codes

For common error codes, please refer to the  and  documentation.

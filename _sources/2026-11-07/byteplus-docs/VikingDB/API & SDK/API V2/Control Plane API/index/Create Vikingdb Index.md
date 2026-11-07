---
title: " Create Vikingdb Index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_Index_V2"
---

<span id="d07f3366"></span>
# Overview

To enable efficient vector similarity search within a VikingDB collection, you can use the CreateVikingdbIndex API. This reference provides detailed information on all request parameters, including how to configure vector index types (such as HNSW, DiskANN, and flat), define scalar indexes for filtered searches, and set sharding policies to manage large\-scale data.

<span id="0e7d9842"></span>
# Interface Upgrade Notes


* The corresponding V1 interface is: https://docs.byteplus.com/en/docs/VikingDB/create1

* Usage differences:



| |V2 Interface |V1 Interface |
|---|---|---|
|Parameter naming style |CamelCase (`IndexName`) |Underscore (`index_name`) |



* Note: QPS rate limiting is calculated based on the number of data entries, and the rate limiting behavior of V1 and V2 interfaces is identical.


<span id="a0a01701"></span>
# Request API

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you can use AK, SK to construct a signature. Please refer to the <a href="https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2">Control Plane API Calling Process</a>, copy the calling example and fill in the necessary information.</div>


<span id="d3af65bc"></span>
## Request Parameters

Request parameter Action value: CreateVikingdbIndex.

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |First\-level Sub\-parameter |Type |Required |Description |
|---|---|---|---|---|
|ProjectName | |String |No |Project name |
|CollectionName | |String |One of two |Dataset name |
|ResourceId | |String ||Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|Description | |String |No |Custom description of the index. |
|VectorIndex | |Map |Yes |Vector index configuration |
| |IndexType |String |Yes |Vector index type. Values are as follows:<br><br><br>* hnsw: Stands for Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be accessed during the search process by constructing a multi\-layer network. This design enables fast and efficient nearest neighbor searches, making it suitable for scenarios with high search efficiency requirements.<br><br><br>Parameters related to hnsw include **Quant, Distance, HnswM, HnswCef, HnswSef**.<br><br><br>* hnsw_hybrid: HNSW algorithm that supports hybrid indexing. The hybrid indexing algorithm can index both dense and sparse vectors in the dataset simultaneously, and returns results that take into account the similarity of both types during retrieval. It is suitable for scenarios with high search efficiency requirements and the need to retrieve both sparse and dense vectors simultaneously.<br><br><br>Parameters related to hnsw_hybrid include **Quant, Distance, HnswM, HnswCef, HnswSef**.<br><br>The dataset must contain sparse vector data. This means it must either have fields of the sparse_vector type defined or be bound to a pipeline that can generate sparse vectors.<br><br><br>* flat: This is a brute\-force index. During a search, it traverses all vectors in the database and calculates and compares their distances with the target vector. Although the query speed is slow, the flat index provides a 100% retrieval recall rate. It is suitable for scenarios with fewer vector candidates that require a 100% recall rate.<br><br><br>Parameters related to flat include **Quant, Distance**.<br><br><br>* diskann: This is a disk\-based index algorithm based on the Vamana graph, which combines the Vamana graph with a PQ quantization compression scheme to build the DiskANN index. Graph index and raw data are stored on SSD, and compressed index is stored in memory. During retrieval requests, the query vector is compared with cluster centers, and then the corresponding raw data is read from disk for scoring. It is suitable for scenarios with large data volumes where performance is not particularly sensitive, memory costs are lower, and the recall rate is high.<br><br><br>Parameters related to diskann include **Quant, Distance, DiskannM, DiskannCef, CacheRatio, PqCodeRatio.**  |
| |Distance |String |No |Distance type, algorithm for measuring distance between vectors. Values are as follows:<br><br>ip: Inner Product. This algorithm calculates similarity based on the inner product of vectors, which is the result of multiplying the corresponding elements of two vectors and summing them. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance. It calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine similarity (also known as cosine distance) is used to calculate the cosine of the angle between two high\-dimensional vectors to measure their similarity. A smaller cosine similarity value indicates a larger angle between the two vectors and thus a greater difference.<br><br>When distance=cosine, vectors are normalized by default.<br><br>For the hnsw_hybrid indexing algorithm, distance type selection only takes effect for dense vectors, and sparse vectors only support inner product. |
||Quant |String |No |Quantization method. Quantization method is the compression method for vectors in the index, which can reduce the complexity of similarity calculations between vectors. Given the high dimensionality and large scale of vectors, vector quantization can effectively reduce storage and computational costs. Values are as follows:<br><br><br>* int8: This method compresses a 4\-byte float to a single byte to provide memory and computational latency benefits. It causes minor precision loss; for example, the cosine distance may result in scores greater than 1.<br><br>* float: Full precision, no compression quantization.<br><br>* fix16: Compresses 4\-byte float to two bytes to gain memory and computational latency benefits, causing minor precision loss. This method improves retrieval performance and saves resource costs by sacrificing some retrieval accuracy.<br><br>* pq: Converts high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip and cosine.<br><br>float is applicable to hnsw, hnsw_hybrid, flat, and diskann indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>fix16 is applicable to hnsw, hnsw_hybrid, and flat indexing algorithms, with distance methods of ip, l2, and cosine.<br><br>pq is applicable to diskann indexing algorithms, with distance methods of ip, l2, and cosine. |
||HnswM |Integer |No |This is an HNSW index parameter that represents the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||HnswCef |Integer |No |This is an HNSW index parameter that represents the breadth of the search for neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||HnswSef |Integer |No |This is an HNSW index parameter that represents the search breadth for online retrieval.<br><br><br>* Optional configuration when index_type is configured as hnsw and hnsw_hybrid. |
||DiskannM |Integer |No |This is a DiskANN parameter that identifies the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is configured as diskann. |
||DiskannCef |Integer |No |This is a DiskANN parameter that represents the breadth of the search for neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is configured as diskann. |
||PqCodeRatio |Float |No |This is a DiskANN parameter that specifies the size limit for vector dimension encoding. A larger value results in a higher recall rate but also increases memory usage. The range is (0.0, 0.25].<br><br><br>* Optional configuration when index_type is configured as diskann. |
||CacheRatio |Float |No |This is a DiskANN parameter that specifies the ratio of cached nodes to raw data. Larger values will improve index performance and increase memory usage. Range [0.0,0.3).<br><br><br>* Optional configuration when index_type is configured as diskann. |
|ScalarIndex | |Array of String |No |A list of scalar fields to be built into the scalar index. Among them, float and int64 fields can be used for range retrieval, and non\-float fields can be used for enumeration retrieval.<br><br><br>* ScalarIndex defaults to None, indicating that all fields are built into the scalar index.<br><br>* When ScalarIndex is [], it indicates that no scalar index is built.<br><br>* When ScalarIndex is a non\-empty list, it indicates that the fields in the list are built into the scalar index. |
|CpuQuota | |Integer |No |The CPU quota consumed by index retrieval, specified as a positive integer.<br><br>Related to throughput, not latency. 1 CPU core is approximately 100 QPS.<br><br>N shards consume N times the CPU; if the CPU consumed by retrieval exceeds the quota, the index will be rate\-limited.<br><br>Value range: [1, 10240]. |
|ShardPolicy | |String |No |Index sharding type<br><br>The type of index sharding. Optional values are auto (automatic sharding) or custom (custom sharding).<br><br>Index sharding refers to evenly dividing index data into multiple small index data blocks in large data volume scenarios, and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and queries will simultaneously request index data blocks on different nodes. Due to the limited capacity of a single node, it is impossible to store all index data on a single node, so it is necessary to set an appropriate number of index shards, otherwise, it will affect the timeliness of data indexing. In addition, the number of shards is related to cost, and the more shards, the higher the cost. |
|ShardCount | |Integer |No |The custom shard count.<br><br><br>* When ShardPolicy is set to auto, ShardCount does not take effect.<br><br>* When ShardPolicy is set to custom, this parameter is required.<br><br>   * Value range: [1, 256].<br><br>   * The default value is 1. For estimation, use the following reference: estimated data volume / 30 million. |
|IndexName | |String |Yes |Index name |


<span id="3bc86647"></span>
## Response Parameters

The table below only lists the response parameters specific to this interface. For more information, please see [Control Plane API Calling Process](https://docs.byteplus.com/docs/VikingDB/Control_Plane_API_V2).


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Information about the operation result. |


<span id="fb665dd7"></span>
## Request Example

```Plain
action = "CreateVikingdbIndex",
body = {
    "CollectionName": "test_YOURNAMEcoll_2",
    "IndexName": "idx_rs_1",
    "Description": "haha",
    "ShardPolicy": "auto",
    "VectorIndex": {
        "IndexType": "sort",
        "Distance": "ip",
        "Quant": "float",
    }
}
```


<span id="2247f45c"></span>
## Response Example

```Plain
{
  "ResponseMetadata": {
    "RequestId": "202505271754501200391670290C48BB",
    "Action": "CreateVikingdbIndex",
    "Version": "2025-06-09",
    "Service": "vikingdb",
    "Region": "cn-beijing"
  },
  "Result": {
    "Message": "success"
  }
}
```


<span id="6209486b"></span>
## Error Codes

For common error codes, please refer to the [Common Error Codes] and the [API V2 Error Codes and Troubleshooting Guide].

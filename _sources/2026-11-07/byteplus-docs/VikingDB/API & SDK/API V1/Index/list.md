---
title: "list"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/list2"
---

<span id="0fda54c5"></span>
# Overview

To retrieve a list of all indexes associated with a specific collection, you can use the `GET /api/index/list` endpoint. This document provides details on the request parameters, response structure, and includes a complete code example to help you get started.

<span id="f9d3b80c"></span>
# **Request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/list |Uniform Resource Identifier |
|---|---|---|
|**request method** |GET |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="5a118dad"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* Must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="0993690c"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Returned message |
|request_id |A unique identifier for each request |
|Data |Index information. For details, see the Index parameters section below. |


<span id="eea6ca3f"></span>
## Index parameter


|**parameter** |**sub\-parameter** |**type** |**parameter description** |
|---|---|---|---|
|collection_name |*  |String |Displays the name of the Collection to which the index was created. |
|index_name |*  |String |Displays the name of the index created. |
|cpu_quota |*  |Int |The CPU quota consumed by the index for online searches. |
|Description |*  |String |Displays a custom description of the index. |
|shard_policy |*  |String |Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. A query will access index data blocks on different nodes simultaneously. Because a single node has limited capacity, it cannot store all the index data. Therefore, you must set an appropriate number of index shards; otherwise, data indexing performance will be affected. In addition, the number of shards is related to cost, and the more shards, the higher the cost.<br><br><br>* Index sharding type, optional value is auto/custom, auto is automatic sharding, custom is custom sharding. |
|shard_count |*  |Int |Custom sharding number.<br><br><br>* shard_count does not take effect when shard_policy is auto.<br><br>* This parameter is required when shard_policy is set to custom.<br><br>   * Value range: [1,256].<br><br>   * The default value is 1. To estimate the number of shards, use the formula: (estimated data volume) / 30 million. |
|partition_by |*  |String |partition_by is used to divide sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval.<br><br><br>* The field name to partition by. Supported field types are int64, list, string, and list. Partition field value corresponding to field.<br><br>* The recommended number of subindex partitions partition_by partitions should not exceed 1000.<br><br>* partition_by parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: This is suitable for scenarios where the dataset is divided into multiple sub\-datasets and queries are typically confined to a specific sub\-dataset or sub\-index. For example, if you split the dataset by country ID, searching the sub\-index for a specific country ID improves retrieval performance because it eliminates the need to filter by country ID. |
|vector_index |index_type |String |Displays the vector index type. The values are as follows:<br><br><br>* HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and realizes fast and efficient search for nearest neighbors, which is suitable for scenarios that require high search efficiency.<br><br><br>The relevant parameters of hnsw include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br><br>* hnsw_hybrid: HNSW algorithm that supports mixed indexing. The mixed indexing algorithm can index both dense and sparse vectors in the dataset at the same time, and return results that take into account the similarity of the two types when retrieving. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>hnsw_hybrid related parameters include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br>For hnsw_hybrid, the indexed dataset must contain sparse_vector data. This means that fields of type sparse_vector must be defined, or a pipeline that produces sparse_vector vectors must be bound.<br><br><br>* Flat: brute\-force indexing, searching through all vectors of the entire vector database to calculate and compare the distance with the target vector, the query speed is slow, but flat can provide 100% retrieval recall rate, suitable for less vector candidate sets and 100% retrieval recall rate Scenarios.<br><br><br>The relevant parameters of flat include **Quant, distance**.<br><br><br>* Ivf: Inverted index, It uses the concept of an inverted list to store vectors under each cluster center. When a query is performed, it finds the nearest cluster centers and then searches only the vectors within those clusters. The speed is faster, but the accuracy is slightly lower. It is suitable for medium\-scale datasets in scenarios where high search efficiency is prioritized over perfect accuracy.<br><br><br>The relevant parameters of ivf include **Quant, distance**. |
||Distance |String |Displays the distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* IP: The full name is Inner Product, inner product. This algorithm calculates similarity based on the inner product of two vectors, which is the result of multiplying and summing their corresponding elements. The larger the inner product value, the higher the similarity.<br><br>* L2: Euclidean distance, it calculates the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* Cosine: Cosine similarity, also known as cosine distance, is used to calculate the cosine value of the angle between two high\-dimensional vectors to measure the similarity of the vectors. The smaller the cosine value of the angle between the two vectors, the greater the difference between the two vectors.<br><br><br>When distance = cosine, the vector is normalized by default. |
||Quant |String |The quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, the use of vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* Int 8: Compresses a 4\-byte float into a single byte to reduce memory usage and compute latency. This results in a small loss of precision (for example, a cosine distance score might be greater than 1).<br><br>* Float: full precision, no compression quantization.<br><br>* Fix16: Compresses a 4\-byte float into two bytes to reduce memory usage and compute latency, resulting in a small loss of accuracy. This improves search performance and saves resource costs at the expense of some search accuracy.<br><br>* Pq: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
||hnsw_m |Number |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
||hnsw_cef |Number |The hnsw index parameter, which represents the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
||hnsw_sef |Number |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
|enum_index |*  |Array |Infer the names of scalar fields that can be used for enumeration retrieval from scalar_index, and non\-float fields can be used for enumeration retrieval. |
|range_index |*  |Array |According to scalar_index infer the scalar field names that can be used for range retrieval, float, int64 fields can be used for range retrieval. |
|scalar_index |field_name |String |Scalar field name. |
||field_type |String |Scalar field type. |
|Status |*  |String |Index state. The value is as follows:<br><br><br>* INIT: Initialized, in build or load.<br><br>* CHANGING: The index is being modified, which may involve rebuilding or reloading<br><br>* READY: The index is active and ready to serve requests. |
|index_cost |cpu_core |Int |The number of CPU cores occupied by the index. |
||mem_gb |String |The memory size occupied by the index. |
|create_time |*  |String |Index creation time. |
|update_time |*  |String |Index update time. |
|update_person |*  |String |The user who last updated the index. |


<span id="f848faba"></span>
## **status code description**


|**status code** |**HTTP status code** |**Returned message** |**status code description** |
|---|---|---|---|
|0 |200 |List index success |Query the index list of the specified Collection successfully. |
|1000005 |400 |Collection does not exist |The specified Collection does not exist. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="96b6d82d"></span>
# Complete example

<span id="d4d56830"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/list \
  -d '{
    "collection_name": "test_name"
}'
```


<span id="947359c5"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "message":"success",
    "request_id":"021695029757920fd001de6666600000000000000000002569b8f",
    "data": [
        {
            "index_name": "index_test_1",
            "status": "ready",
            "description": "test for index",
            "cpu_quota": 10,
            "vector_index": {
                "index_type": "hnsw",
                "distance": l2,
                "quant": "float"
            },
        "enum_index": ["city", "date"],
        "range_index": ["score"],
        "scalar_index": [
            {
                "field_name":"score",
                "field_type":"float32"
            },
            {
                "field_name":"city",
                "field_type":"string"
            },
            {
                "field_name":"date",
                "field_type":"string"
            }
        ],
        "create_time": "2023-11-21 12:22:57",
        "update_time": "2023-11-22 11:15:45",
        "update_person": "zhangsan",
        },
        {
            "index_name": "index_test_2",
            "status": "init",
            "description": "test for index",
            "cpu_quota": 10,
            "vector_index": {
                "index_type": "hnsw",
                "distance": l2,
                "quant": "float"
            },
        "enum_index": ["city", "date"],
        "range_index": ["score"],
        "scalar_index": [
            {
                "field_name":"score",
                "field_type":"float32"
            },
            {
                "field_name":"city",
                "field_type":"string"
            },
            {
                "field_name":"date",
                "field_type":"string"
            }
        ]
        "create_time": "2023-11-21 10:22:57",
        "update_time": "2023-11-22 12:15:45",
        "update_person": "zhangsan"
        }   
    ] 
}
```


If execution fails, the following is returned:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000005,"message":"collection not exist","request_id":"021695029757920fd001de6666600000000000000000002569b8f"}
```

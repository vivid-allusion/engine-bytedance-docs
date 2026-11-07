---
title: "info"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/info1"
---

<span id="29e1be85"></span>
# Overview

/index/info interface is used to query index details.

<span id="7ee65fc2"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/info |Uniform Resource Identifier |
|---|---|---|
|**request method** |GET |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="b8c980a2"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |String |Yes |Specify the name of the Index to query.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |


<span id="e5611f8f"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique device identifier for each request |
|Data |Index information, see **Index parameter**Explanation. |


<span id="e6467a67"></span>
## **Index parameter**


|**parameter** |**sub\-parameter** |**type** |**parameter description** |
|---|---|---|---|
|Collection |*  |String |Displays the name of the Collection to which the index was created. |
|Index |*  |String |Displays the name of the index created. |
|cpu_quota |*  |Int |Displays the CPU quota consumed by the index line search. |
|Description |*  |String |Displays a custom description of the index. |
|shard_policy |*  |String |Index sharding type<br><br><br>* The optional value is auto/custom, auto is automatic sharding, and custom is custom sharding.<br><br><br>Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. The query will request index data blocks on different nodes at the same time. Due to the limited capacity of a single node, it is impossible to store all the index data in a single node, so it is necessary to set an appropriate number of index shardings, otherwise it will affect the timeliness of indexing the data. In addition, the number of shardings is related to cost, and the more shardings, the higher the cost. |
|shard_count |*  |Int |Custom sharding number.<br><br><br>* shard_count not effective when shard_policy is auto<br><br>* When shard_policy custom, shard_count<br><br>   * Value range: [1,256].<br><br>   * Default is 1, sharding number estimate reference: data estimate data volume/30 million. |
|partition_by |*  |String |partition_by is used to divide sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval.<br><br><br>* partition_by field_name corresponding field name, support field type is int64, list< int64 \>, string, list\ < string \>. Partition field value corresponding to field.<br><br>* The recommended number of subindex partitions partition_by partitions should not exceed 1000.<br><br>* partition_by parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: It is suitable for scenarios where the data set is divided into multiple sub\-datasets and the retrieval mode is fixed in a certain sub\-dataset/sub\-index. For example, splitting the dataset according to the country ID, and searching the sub\-index of a certain country ID does not need to filter the country ID to improve the retrieval performance. |
|vector_index |index_type |String |Displays the vector index type. The values are as follows:<br><br><br>* HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and realizes fast and efficient search for nearest neighbors, which is suitable for scenarios that require high search efficiency.<br><br><br>The relevant parameters of hnsw include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br><br>* hnsw_hybrid: HNSW algorithm that supports mixed indexing. The mixed indexing algorithm can index both dense and sparse vectors in the dataset at the same time, and return results that take into account the similarity of the two types when retrieving. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>hnsw_hybrid related parameters include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br>hnsw_hybrid the data set indexed must contain sparse_vector types of data, that is, sparse_vector type fields are defined, or pipelines that produce sparse_vector type vectors are bound.<br><br><br>* Flat: brute\-force indexing, searching through all vectors of the entire vector database to calculate and compare the distance with the target vector, the query speed is slow, but flat can provide 100% retrieval recall rate, suitable for less vector candidate sets and 100% retrieval recall rate Scenarios.<br><br><br>The relevant parameters of flat include **Quant, distance**.<br><br><br>* Ivf: Inverted index, use the idea of inverted row to save the vectors under each cluster center, find the nearest centers every time you query the vectors, and search the vectors under these centers respectively. The speed is faster, but the accuracy is slightly lower. It is suitable for medium\-scale data volume, high search efficiency, and second\-precision scenarios.<br><br><br>The relevant parameters of ivf include **Quant, distance**. |
||Distance |String |Displays the distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* IP: The full name is Inner Product, inner product. The algorithm calculates similarity based on the inner product of vectors, that is, the result of multiplying and summing the corresponding elements of two elements. The larger the inner product value, the higher the similarity.<br><br>* L2: Euclidean distance, it calculates the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* Cosine: Cosine similarity, also known as cosine distance, is used to calculate the cosine value of the angle between two high\-dimensional vectors to measure the similarity of the vectors. The smaller the cosine value of the angle between the two vectors, the greater the difference between the two vectors.<br><br><br>When distance = cosine, the vector is normalized by default. |
||Quant |String |The quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, the use of vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* Int 8: Compressing a 4\-byte float into a single byte to gain memory and compute latency results in a small loss of precision, such as a score greater than 1 for cosine distance.<br><br>* Float: full precision, no compression quantization.<br><br>* Fix16: Compress a 4\-byte float into two bytes to gain memory and computational latency, resulting in a small loss of accuracy. By losing a certain search accuracy, improve search performance and save resource costs.<br><br>* Pq: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
||hnsw_m |Number |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* Optional when index_type configured as hnsw. |
||hnsw_cef |Number |The hnsw index parameter, which represents the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional when index_type configured as hnsw. |
||hnsw_sef |Number |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* Optional when index_type configured as hnsw. |
|enum_index |*  |Array |Infer the names of scalar fields that can be used for enumeration retrieval from scalar_index, and non\-float fields can be used for enumeration retrieval. |
|range_index |*  |Array |According to scalar_index infer the scalar field names that can be used for range retrieval, float, int64 fields can be used for range retrieval. |
|scalar_index |field_name |String |Scalar field name. |
||field_type |String |Scalar field type. |
|Status |*  |String |Index state. The value is as follows:<br><br><br>* INIT: Initialized, in build or load.<br><br>* CHANGING: In change, in change build or load<br><br>* READY: It has been launched and can officially provide services. |
|index_cost |cpu_core |Int |The number of CPU cores occupied by the index. |
||mem_gb |String |The memory size occupied by the index. |
|create_time |*  |String |Index creation time. |
|update_time |*  |String |Index update time. |
|update_person |*  |String |Index Updater. |


<span id="84916870"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Get index success |Index details were successfully queried. |
|1000008 |400 |Index not exists |The specified Index does not exist. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Required parameters are missing. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="23592c49"></span>
# Complete example

<span id="731e2227"></span>
## Request message

```Shell

curl -i -X GET \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/info \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test"
}'
```


<span id="16801603"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{
    "code":0,
    "msg":"describe index success",
    "request_id":"021695029537650fd001de666660000000000000000000230da93",
    "data": {
        "collection": "test_name",
        "index": "index_test",
        "status": "ready",
        "index_cost": {
            "mem_gb": "10G",
            "cpu_core": 10  
        }
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
        "update_person": "zhangsan"
    }
}
```


Execution fails to return:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000008,"msg":"index not exist","request_id":"021695029537650fd001de666660000000000000000000230da93"}
```

---
title: "create"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/create1"
---

<span id="cefdba8b"></span>
# Overview

/index/create interface is used to create an index Index for the specified dataset Collection.

Indexing can accelerate the similarity search of vectors. It groups and sorts the original data sources in the vector library according to the specified index algorithm and data structure, improves the efficiency and accuracy of similarity search, and is the core that drives the vector database to filter out candidates in a short time.

<span id="0250c8a0"></span>
# **request interface**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When requesting the OpenAPI interface of the vector database VikingDB, you need to construct a signature for authentication. For detailed OpenAPI signature calling methods, please refer to <a href="https://docs.byteplus.com/en/docs/VikingDB/Preparation">API Signature Call Guide</a>.</div>



|**URI** |/api/index/create |Uniform Resource Identifier |
|---|---|---|
|**request method** |POST |The type of operation requested by the client side on the vector database server |
|**request header** |Content\-Type: application/json |Request message type |
||Authorization: HMAC\-SHA256 \*\*\* |Authentication |


<span id="9a79b893"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |Specifies the name of the Collection to which the index was created.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |*  |String |Yes |*  |Specifies the name of the index created.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|cpu_quota |*  |Int |No |1 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Depending on throughput, regardless of latency, 1 CPU core is about 100QPS.<br><br>* N times the CPU consumption of the number of shardings; if the CPU consumption of the retrieval exceeds the quota, the index will be limited viewership of.<br><br>* Value range: [1,10240]. |
|Description |*  |String |No |" |A custom description of the index. |
|shard_policy |*  |String |No |" |Index sharding type<br><br><br>* The optional value is auto/custom, auto is automatic sharding, and custom is custom sharding.<br><br><br>Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. The query will request index data blocks on different nodes at the same time. Due to the limited capacity of a single node, it is impossible to store all the index data in a single node, so it is necessary to set an appropriate number of index shardings, otherwise it will affect the timeliness of indexing the data. In addition, the number of shardings is related to cost, and the more shardings, the higher the cost. |
|shard_count |*  |Int |No |1 |Custom sharding number.<br><br><br>* shard_count does not take effect when shard_policy is auto.<br><br>* When shard_policy custom, shard_count.<br><br>   * Value range: [1,256].<br><br>   * Default is 1, sharding number estimate reference: data estimate data volume/30 million. |
|partition_by |*  |String |No |" |partition_by is used to divide sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval.<br><br><br>* partition_by field_name corresponding field name, support field type is int64, list< int64 \>, string, list\ < string \>. Partition field value corresponding to field.<br><br>* The recommended number of subindex partitions partition_by partitions should not exceed 1000.<br><br>   * Too many sub\-indexes will cause the index to not be ready or updated<br><br>   * Each sub\-index will occupy at least 100,000 \* dimension \* coefficients and bytes of memory regardless of the amount of data. If the number of sub\-indexes is too large, it will lead to excessive memory consumption and increased billing<br><br>* partition_by parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: It is suitable for scenarios where the data set is divided into multiple sub\-datasets and the retrieval mode is fixed in a certain sub\-dataset/sub\-index. For example, splitting the dataset according to the country ID, and searching the sub\-index of a certain country ID does not need to filter the country ID to improve the retrieval performance. |
|vector_index |index_type |String |Yes |Hnsw |Vector index type. The value is as follows:<br><br><br>* HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and realizes fast and efficient search for nearest neighbors, which is suitable for scenarios that require high search efficiency.<br><br><br>The relevant parameters of hnsw include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br><br>* hnsw_hybrid: HNSW algorithm that supports mixed indexing. The mixed indexing algorithm can index both dense and sparse vectors in the dataset at the same time, and return results that take into account the similarity of the two types when retrieving. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>hnsw_hybrid related parameters include **Quant, distance, hnsw_m, hnsw_cef, hnsw_sef**.<br><br>hnsw_hybrid the data set indexed must contain sparse_vector types of data, that is, sparse_vector type fields are defined, or pipelines that produce sparse_vector type vectors are bound.<br><br><br>* Flat: brute\-force indexing, searching through all vectors of the entire vector database to calculate and compare the distance with the target vector, the query speed is slow, but flat can provide 100% retrieval recall rate, suitable for less vector candidate sets and 100% retrieval recall rate Scenarios.<br><br><br>The relevant parameters of flat include **Quant, distance**.<br><br><br>* Ivf: Inverted index, use the idea of inverted row to save the vectors under each cluster center, find the nearest centers every time you query the vectors, and search the vectors under these centers respectively. The speed is faster, but the accuracy is slightly lower. It is suitable for medium\-scale data volume, high search efficiency, and second\-precision scenarios.<br><br><br>The relevant parameters of ivf include **Quant, distance**. |
||Distance |String |No |IP |Distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* IP: The full name is Inner Product, inner product. The algorithm calculates similarity based on the inner product of vectors, that is, the result of multiplying and summing the corresponding elements of two elements. The larger the inner product value, the higher the similarity.<br><br>* L2: Euclidean distance, it calculates the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* Cosine: Cosine similarity, also known as cosine distance, is used to calculate the cosine value of the angle between two high\-dimensional vectors to measure the similarity of the vectors. The smaller the cosine value of the angle between the two vectors, the greater the difference between the two vectors.<br><br><br>When distance = cosine, the vector is normalized by default.<br><br>When the index algorithm selects IVF, the distance type can be selected as ip, cosine.<br><br>For hnsw_hybrid indexing algorithms, the distance type selection is only valid for dense vectors, and sparse vectors only support inner products. |
||Quant |String |No |See parameter description for details |Quantization method. Quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* Int 8: Compressing a 4\-byte float into a single byte to gain memory and compute latency results in a small loss of precision, such as a score greater than 1 for cosine distance.<br><br>* Float: full precision, no compression quantization.<br><br>* Fix16: Compress a 4\-byte float into two bytes to gain memory and computational latency, resulting in a small loss of accuracy. By losing a certain search accuracy, improve search performance and save resource costs.<br><br>* Pq: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>Int8 is suitable for hnsw, hnsw_hybrid, flat indexing algorithms, and the distance method is ip, consine.<br><br>Float is suitable for hnsw, hnsw_hybrid, flat, diskann indexing algorithms, and the distance methods are ip, l2, consine.<br><br>FIX16 is suitable for hnsw, hnsw_hybrid, flat indexing algorithms, and the distance methods are ip, l2, consine.<br><br>Pq is suitable for diskann and ivf indexing algorithms, and the distance methods are ip, l2, consine. |
||hnsw_m |Number |No |20 |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
||hnsw_cef |Number |No |400 |The hnsw index parameter, which represents the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
||hnsw_sef |Number |No |800 |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* Optional when index_type configured for hnsw and hnsw_hybrid. |
|scalar_index |*  |Array |No |None |List of scalar fields to set the fields that need to be built into a scalar index. Among them, float, int64 fields can be used for range retrieval, and non\-float fields can be used for enumeration retrieval.<br><br><br>* scalar_index defaults to None, meaning all fields are built to a scalar index.<br><br>* scalar_index [] means no scalar index.<br><br>* scalar_index a non\-empty list, the fields in the list are built to a scalar index. |


<span id="596e9f0c"></span>
# **response message**


|**parameter** |**parameter description** |
|---|---|
|Code |Status code |
|Message |Return information |
|request_id |A unique device identifier for each request |


<span id="9f0d6d14"></span>
## **status code description**


|**status code** |**HTTP status code** |**Return information** |**status code description** |
|---|---|---|---|
|0 |200 |Success |Index Index created successfully. |
|1000005 |400 |Collection not exists |The index\-related Collection does not exist. |
|1000007 |400 |Index already Exist |The index name already exists. |
|1000003 |400 |Invalid request:% s |Illegal parameter:<br><br><br>* Required parameters are missing.<br><br>* Index naming does not conform to the specification. |
|1000001 |401 |Unauthorized |The request header lacks authentication information. |
|1000002 |403 |No permission |Insufficient permissions. |


<span id="7cb34767"></span>
# Complete example

<span id="f0c5b352"></span>
## Request message

```Shell

curl -i -X POST \
  -H 'Content-Type: application/json' \
  -H 'Authorization: HMAC-SHA256 ***' \
  https://api-vikingdb.mlp.ap-mya.byteplus.com/api/index/create \
  -d '{
    "collection_name": "test_name",
    "index_name": "index_test"
    "description": "test for index",
    "cpu_quota": 10,
    "partition_by": "country"   //// The field by which partitioning is performed. 
    "vector_index": {
        "index_type": "hnsw",
        "distance": l2,
        "quant": "float"
    },
    "scalar_index": ["city", "date", "score"],
}'
```


<span id="922809ae"></span>
## Response message

Successful execution returns:

```Shell
HTTP/1.1 200 OK
Content-Length: 43
Content-Type: application/json
 
{"code":0,"message":"success","request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```


Execution fails to return:

```Shell
HTTP/1.1 400 OK
Content-Length: 43
Content-Type: application/json
 
{"code":1000005, "message":"collection not exist", "request_id":"021695029736548fd001de66666000000000000000000029aa917"}
```

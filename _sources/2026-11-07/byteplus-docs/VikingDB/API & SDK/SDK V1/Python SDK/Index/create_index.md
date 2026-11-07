---
title: "create_index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_create_index"
---

<span id="b775dfc7"></span>
# Overview

create_index is used to create an index for the specified dataset Collection.

The asynchronous call uses the async_create_index interface, and the parameters remain unchanged.

<span id="87840cc2"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |Specifies the name of the Collection for which to create the index.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |*  |String |Yes |*  |Specifies the name of the index to be created.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|vector_index<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">VectorIndexParams instance.</div><br> |index_type |String |Yes |IndexType. HNSW |Vector index type. The value is as follows:<br><br><br>* IndexType. HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and enables fast and efficient nearest neighbor searches, which is suitable for scenarios that require high search efficiency.<br><br>* IndexType.HNSW_HYBRID: An HNSW algorithm that supports hybrid indexing. The hybrid indexing algorithm can index both dense and sparse vectors in the dataset simultaneously and return retrieval results that combine the similarity scores of both vector types. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>HNSW_HYBRID indexed dataset must contain data of type sparse_vector, that is, a sparse_vector type field is defined, or a pipeline is bound to produce a sparse_vector type vector.<br><br><br>* IndexType. FLAT: This is a brute\-force indexing method that searches through all vectors in the database to calculate their distance to the target vector. Although the query speed is slow, FLAT provides a 100% retrieval recall rate. It is suitable for scenarios with small vector candidate sets that require a perfect recall rate.<br><br>* IndexType. IVF: Inverted index, using the idea of an inverted file to store the vectors belonging to each cluster center, find the nearest centers each time you query the vectors, and search the vectors under these centers respectively. The speed is faster, but the accuracy is slightly lower. It is suitable for medium\-scale datasets that require high search efficiency and can tolerate slightly lower accuracy. |
||Distance |String |No |DistanceType. IP |Distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* DistanceType. IP: The full name is Inner Product, inner product. The algorithm calculates similarity based on the inner product of vectors, that is, the result of multiplying and summing the corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>* DistanceType. L2: Euclidean distance, which computes the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* DistanceType. COSINE: Cosine similarity, also known as cosine distance, is used to calculate the angle cosine value of two high\-dimensional vectors to measure vector similarity. The smaller the angle cosine value, the greater the angle between the two vectors, the greater the difference between the two vectors.<br><br><br>When distance = cosine, the vector is normalized by default.<br><br>For hnsw_hybrid indexing algorithms, the distance type selection is only valid for dense vectors, and sparse vectors only support inner products. |
||Quant |String |No |QuantType. Int8 |Quantization method. Quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* QuantType. Int8: Compressing a 4\-byte float into a single byte to save memory and reduce compute latency results in a small loss of precision, such as a score greater than 1 for cosine distances.<br><br>* QuantType. Float: full precision, no compression quantization.<br><br>* QuantType. Fix16: Compressing a 4\-byte float into two bytes to save memory and reduce computational latency results in a small loss of accuracy. This method improves retrieval performance and saves resources by sacrificing a small amount of retrieval accuracy.<br><br>* QuantType. PQ: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>Int8 is suitable for hnsw, hnsw_hybrid, flat indexing algorithms, and the distance method is ip, cosine.<br><br>Float is suitable for hnsw, hnsw_hybrid, flat, diskann indexing algorithms, and the distance methods are ip, l2, cosine.<br><br>FIX16 is suitable for hnsw, hnsw_hybrid, flat indexing algorithms, and the distance methods are ip, l2, cosine.<br><br>Pq is suitable for diskann and ivf indexing algorithms, and the distance methods are ip, l2, cosine. |
||hnsw_m |Number |No |20 |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* This parameter is optional when index_type is set to HNSW. |
||hnsw_cef |Number |No |400 |An HNSW index parameter that represents the breadth of the search for neighbor nodes when building the graph.<br><br><br>* This parameter is optional when index_type is set to HNSW. |
||hnsw_sef |Number |No |800 |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* This parameter is optional when index_type is set to HNSW. |
|cpu_quota |*  |Int |No |2 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Depending on throughput, regardless of latency, 1 CPU core is about 100QPS.<br><br>* N times the CPU consumption of the number of shardings; if the CPU consumption of the retrieval exceeds the quota, requests to the index will be throttled.<br><br>* Value range: [2,10240]. |
|Description |*  |String |No |" |A custom description of the index. |
|partition_by |*  |String |No |" |partition_by is used to divide sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval.<br><br><br>* The value is the name of the field to partition by. Supported field types are int64, list, string, and list. Partition field value corresponding to field.<br><br>* The recommended number of subindex partitions partition_by partitions should not exceed 1000.<br><br>* If the partition_by parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: It is suitable for scenarios where the data set is divided into multiple sub\-datasets and the retrieval mode is fixed in a certain sub\-dataset/sub\-index. For example, splitting the dataset according to the country ID, and searching the sub\-index of a certain country ID does not need to filter the country ID to improve the retrieval performance. |
|scalar_index |*  |Array |No |None |List of scalar fields.<br><br><br>* scalar_index defaults to None, meaning all fields are built to a scalar index.<br><br>* scalar_index [] means no scalar index.<br><br>* If scalar_index is a non\-empty list, only the fields in the list are included in the scalar index. |
|shard_count |*  |Int |No |*  |Index sharding refers to the fact that in a large\-scale data volume scenario, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and the query load can be distributed to different nodes for concurrent processing. When a node fails, the system can automatically migrate the sharding data on it to other normal nodes to ensure stability, so as to achieve horizontal scaling of data and high\-performance read and write operations.<br><br><br>* Value range: [1,256].<br><br>* The default is 1. To estimate the required number of shards, use the formula: estimated data volume / 30 million. |
|shard_policy |*  |String |No |*  |Index sharding type<br><br><br>* The optional values are ShardType.Auto (automatic sharding) and ShardType.Custom (custom sharding).<br><br><br>Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. The query will request index data blocks on different nodes at the same time. Due to the limited capacity of a single node, it is impossible to store all the index data in a single node, so it is necessary to set an appropriate number of index shardings, otherwise it will negatively affect data indexing performance. In addition, the number of shardings is related to cost, and the more shardings, the higher the cost. |


<span id="07040f42"></span>
# Example

<span id="17861dc9"></span>
## Request parameters

```Python
vector_index = VectorIndexParams(distance=DistanceType.COSINE,index_type=IndexType.HNSW,
                                 quant=QuantType.Float)
res = vikingdb_service.create_index("example","example_index", vector_index, cpu_quota=2,
                                    description="This is an index", partition_by="like", scalar_index=None)


# Asynchronous call
async def create_index():
    vector_index = VectorIndexParams(distance=DistanceType.COSINE, index_type=IndexType.HNSW,quant=QuantType.Float)
    res = await vikingdb_service.async_create_index("async", "async", vector_index, cpu_quota=2, description="This is an index", scalar_index=['price', 'like'], shard_policy=ShardType.Custom, shard_count=10)
asyncio.run(create_index())
       
```


<span id="232972a6"></span>
## Return value

The Python call performs the above task and returns an Index instance. The properties contained in an Index instance are shown in the following table.


|**attribute** |**type** |**explain** |
|---|---|---|
|collection_name |String |Displays the Collection name to which the index belongs. |
|index_name |String |Displays the index name. |
|Description |String |Displays a description of the index. |
|cpu_quota |Int |Displays the CPU quota consumed by online index searches. If the CPU consumed by the search exceeds the quota, requests to the index will be throttled. |
|partition_by |String |Specifies the field name used to partition the index. According to a scalar field, the data set can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes, which can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval. |
|vector_index |VectorIndexParams |Vector index parameter. |
|scalar_index |ArrayList < string \> |Scalar index field list. |
|Stat |String |Index state. The value is as follows:<br><br><br>* Init: Initialization, possibly in build or load.<br><br>* Ready: The index is online and ready to serve requests. |
|shard_count |Int |Index sharding refers to the fact that in a large\-scale data volume scenario, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and the query load can be distributed to different nodes for concurrent processing. When a node fails, the system can automatically migrate the sharding data on it to other normal nodes to ensure stability, so as to achieve horizontal scaling of data and high\-performance read and write operations. |
|create_time |String |Index creation time. |
|update_time |String |Index update time. |
|update_person |String |The user who last updated the index. |
|index_cost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: index size in memory. |

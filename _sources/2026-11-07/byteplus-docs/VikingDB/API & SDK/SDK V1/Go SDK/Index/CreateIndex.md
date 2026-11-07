---
title: "CreateIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_CreateIndex"
---

<span id="151287f7"></span>
# Overview

To accelerate vector similarity searches, you can use the CreateIndex operation to build an index on a specified collection.

This reference details all request parameters for configuring the index, including index types (such as HNSW, FLAT, and IVF), distance metrics, quantization methods, and resource settings like sharding and CPU quotas.

<span id="110660c4"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|---|---|
|collectionName |*  |*  |String |Yes |*  |Specifies the name of the Collection to which the index was created.<br><br><br>* The name must contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |*  |*  |String |Yes |*  |Specifies the name of the index created.<br><br><br>* The name must contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|indexOptions<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">IndexOptions structure.</div><br> |vectorIndex<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">VectorIndexParams structure.</div><br> |IndexType |String |Yes |HNSW |Vector index type. The value is as follows:<br><br><br>* HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. By building a multi\-layer network, HNSW reduces the number of nodes that must be visited during a search. This enables a fast and efficient nearest neighbor search, making it suitable for scenarios that require high search efficiency.<br><br>* HNSW_HYBRID: HNSW algorithm that supports mixed indexing. The mixed indexing algorithm can index both dense and sparse vectors in the dataset at the same time, and return results that take into account the similarity of the two types when retrieving. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>HNSW_HYBRID indexed dataset must contain data of type sparse_vector, that is, a sparse_vector type field is defined, or a pipeline is bound to produce a sparse_vector type vector.<br><br><br>* FLAT: brute\-force indexing, searching through all vectors of the entire vector database to calculate and compare the distance with the target vector, the query speed is slow, but flat can provide 100% retrieval recall rate, suitable for less vector candidate sets and 100% retrieval recall rate Scenarios.<br><br>* IVF: An inverted file index. It saves vectors under each cluster center. When a query is performed, it first finds the nearest cluster centers and then searches only the vectors within those centers. The speed is faster, but the accuracy is slightly lower. It is suitable for scenarios with medium\-scale data volumes that require high search efficiency, where slightly lower accuracy is acceptable. |
|||Distance |String |No |DistanceType. IP |Distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* IP: The full name is Inner Product, inner product. The algorithm calculates similarity based on the inner product of vectors, that is, the result of multiplying and summing the corresponding elements of two elements. The larger the inner product value, the higher the similarity.<br><br>* L2: Euclidean distance, it calculates the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* COSINE: Cosine similarity, also known as cosine distance, is used to calculate the cosine value of the angle between two high\-dimensional vectors to measure the similarity of the vectors. A smaller angle between two vectors indicates a smaller difference between them.<br><br><br>When distance = COSINE, the vector is normalized by default.<br><br>For hnsw_hybrid indexing algorithms, the distance type selection is only valid for dense vectors, and sparse vectors only support inner products. |
|||Quant |String |No |Int8 |Quantization method. Quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* Int8: Compresses a 4\-byte float into a single byte. This reduces memory usage and compute latency, but results in a small loss of precision. For example, a cosine distance score may become greater than 1.<br><br>* Float: full precision, no compression quantization.<br><br>* Fix16: Compressing a 4\-byte float into two bytes to gain memory and computational latency results in a small loss of accuracy. By losing a certain amount of retrieval accuracy, retrieval performance is improved and resource costs are saved.<br><br>* PQ: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
|||HnswM |Number |No |20 |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* Optional configuration when IndexType is configured as HNSW. |
|||HnswCef |Number |No |400 |An HNSW index parameter that specifies the search breadth for neighbor nodes when building the graph.<br><br><br>* Optional configuration when IndexType is configured as HNSW. |
|||HnswSef |Number |No |800 |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* Optional configuration when IndexType is configured as HNSW. |
||cpuQuota |*  |Int |No |2 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Depending on throughput, regardless of latency, 1 CPU core is about 100QPS.<br><br>* N times the CPU consumption of the number of shardings; If retrieval consumption exceeds this quota, the index will be rate\-limited.<br><br>* Value range: [2,10240]. |
||Description |*  |String |No |" |A custom description of the index. |
||PartitionBy |*  |String |No |" |partitionBy is used to divide sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. This enables searching within a specific sub\-index during mixed retrieval, which reduces the need for filtering and improves performance.<br><br><br>* The value of partitionBy must be a field name. Supported field types are int64, list, string, and list.<br><br>* The recommended number of partitions should not exceed 1000.<br><br>* When the partitionBy parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: It is suitable for scenarios where the data set is divided into multiple sub\-datasets and the retrieval mode is fixed in a certain sub\-dataset/sub\-index. For example, splitting the dataset according to the country ID, and searching the sub\-index of a certain country ID does not need to filter the country ID to improve the retrieval performance. |
||scalarIndex |*  |Array |No |None |List of scalar fields.<br><br><br>* scalarIndex defaults to None, which means all fields are built to a scalar index.<br><br>* When scalarIndex is [], it means there is no scalar index.<br><br>* When scalarIndex is a non\-empty list, it means that the fields in the list are built into a scalar index. |
| |shardCount |*  |Int |No |1 |Index sharding refers to the fact that in a large\-scale data volume scenario, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and the query load can be distributed to different nodes for concurrent processing. When a node fails, the system can automatically migrate the sharding data on it to other normal nodes to ensure stability, so as to achieve horizontal expansion of data and high\-performance read and write operations.<br><br><br>* Value range: [1,256].<br><br>* The default is 1. To estimate the required number of shards, use the formula: (estimated total data volume) / 30 million. |
| |shardPolicy |*  |String |No |*  |Index sharding type<br><br><br>* The optional values are `vikingdb.Auto` (automatic sharding) and `vikingdb.Custom` (custom sharding).<br><br><br>Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. The query will request index data blocks on different nodes at the same time. Due to the limited capacity of a single node, it is impossible to store all the index data in a single node, so it is necessary to set an appropriate number of index shardings, otherwise it will affect the timeliness of indexing the data. In addition, the number of shardings is related to cost, and the more shardings, the higher the cost. |


<span id="02854227"></span>
# Example

<span id="df606e2d"></span>
## Request parameters

```Go
vectorIndex := &vikingdb.VectorIndexParams{
    Distance:  vikingdb.COSINE,
    IndexType: vikingdb.HNSW_HYBRID,
}
indexOptions := vikingdb.NewIndexOptions().SetVectorIndex(vectorIndex).SetCpuQuota(2).SetDescription("this is an index").SetPartitionBy("").SetScalarIndex([]string{"price", "like"})
index, err := service.CreateIndex("go", "goIndex", indexOptions)
if err != nil {
    fmt.Println(err)
}
fmt.Println(index)
```


<span id="bcf59d0a"></span>
## Return value

The Go call performs the above task and returns the Index structure address (\* Index). The properties contained in the Index structure are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|CollectionName |String |The name of the collection to which the index belongs. |
|IndexName |String |The name of the index. |
|Description |String |Displays a description of the index. |
|CpuQuota |Int |The CPU quota for online index searches. If the CPU consumption for a search exceeds this quota, the index will be rate\-limited. |
|PartitionBy |String |PartitionBy is used to divide the sub\-index partition, corresponding to the field name. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. This enables searching within a sub\-index, which reduces filtering during mixed retrieval and improves performance. |
|VectorIndex |VectorIndexParams |The vector index parameters. |
|ScalarIndex |List\ < string \> |Scalar index field list. |
|Status |String |Index state. The value is as follows:<br><br><br>* Init: Initialization, possibly in build or load.<br><br>* Ready: It is online and can officially provide services. |
|ShardCount |Int |The number of index shards. |
|CreateTime |String |Index creation time. |
|UpdateTime |String |Index update time. |
|UpdatePerson |String |Index Updater. |
|IndexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: index size in memory. |
|shardPolicy |String |Type of sharding |

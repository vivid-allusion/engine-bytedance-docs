---
title: "createIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_createIndex"
---

<span id="a6ceca4a"></span>
# Overview

To accelerate vector similarity searches within your dataset, you can use the createIndex operation. This API reference explains how to create a vector index for a specified collection by configuring parameters like index type, distance metric, and resource allocation. It provides detailed descriptions of all request parameters and a code example to guide your implementation.

Indexing can accelerate the similarity search of vectors. It groups and sorts the original data sources according to the specified index algorithm and data structure, which improves the efficiency and accuracy of similarity searches. This is the core mechanism that allows the vector database to quickly filter candidates.

For the indexed dataset with only dense vectors (i.e. vector type fields), we call this index a pure dense index; for the indexed dataset with dense vectors and sparse vectors (vector and sparse_vector type fields), we call this index a mixed index.

<span id="9574f2ea"></span>
# **request parameters**

The request parameter is CreateIndexParam, and the parameters included in the CreateIndexParam class are shown in the following table.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the name of the collection for which to create the index.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |*  |String |Yes |*  |Specifies the name of the index to create.<br><br><br>* Only English letters, numbers, underscores _, and begin with English letters, cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|vectorIndex<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">VectorIndexParams instance.</div><br> |indexType |String |Yes |IndexType. HNSW |Vector index type. The value is as follows:<br><br><br>* IndexType. HNSW: The full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, which is a graph\-based index. HNSW reduces the number of nodes that need to be visited during the search process by building a multi\-layer network, and enables a fast and efficient search for nearest neighbors, which is suitable for scenarios that require high search efficiency.<br><br>* IndexType.HNSW_HYBRID: An HNSW algorithm that supports hybrid indexing. The hybrid indexing algorithm can index both dense and sparse vectors in the dataset at the same time, and returns retrieval results that combine the similarity scores of both vector types. Suitable for scenarios that require high search efficiency and need to retrieve both sparse and dense vectors.<br><br><br>A dataset indexed with HNSW_HYBRID must contain data of type sparse_vector, that is, a sparse_vector type field is defined, or a pipeline is bound to produce a sparse_vector type vector.<br><br><br>* IndexType. FLAT: A brute\-force index that searches through all vectors in the database to calculate their distance to the target vector. While query speed is slow, this method provides a 100% retrieval recall rate, making it suitable for scenarios with small candidate sets that require a perfect recall rate.<br><br>* IndexType. IVF: An inverted file index. It groups vectors into clusters and saves them under their respective cluster centers. When queried, it finds the nearest cluster centers and searches only the vectors within those clusters. The speed is faster, but the accuracy is slightly lower. It is suitable for medium\-scale data volume, high search efficiency and second\-order accuracy. |
||Distance |String |No |DistanceType. IP |Distance type, an algorithm that measures the distance between vectors. The values are as follows:<br><br><br>* DistanceType. IP: The full name is Inner Product, inner product. The algorithm calculates similarity based on the inner product of vectors, that is, the result of multiplying and summing the corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>* DistanceType. L2: Euclidean distance, which computes the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* DistanceType. COSINE: Cosine similarity, also known as cosine distance, is used to calculate the angle cosine value of two high\-dimensional vectors to measure vector similarity. A smaller cosine value corresponds to a larger angle between the two vectors, indicating lower similarity.<br><br><br>When distance=DistanceType. COSINE, the vector is normalized by default.<br><br>For HNSW_HYBRID indexing algorithms, the distance type selection is only valid for dense vectors, and sparse vectors only support inner products. |
||Quant |String |No |QuantType. Int8 |Quantization method. Quantization method is the compression method of vectors in the index, which can reduce the complexity of computing the similarity between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce the storage and computing costs of vectors. The values are as follows:<br><br><br>* QuantType. Int8: Compressing a 4\-byte float into a single byte to save memory and reduce compute latency results in a small loss of precision, such as a score greater than 1 for cosine distances.<br><br>* QuantType. Float: full precision, no compression quantization.<br><br>* QuantType. Fix16: Compressing a 4\-byte float into two bytes to save memory and reduce computational latency results in a small loss of accuracy. By losing a certain amount of retrieval accuracy, retrieval performance is improved and resource costs are saved.<br><br>* QuantType. PQ: Convert high\-dimensional vectors to low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
||hnswM |Number |No |20 |The hnsw index parameter indicates the number of neighbor nodes.<br><br><br>* Optional configuration when indexType is configured as IndexType. HNSW. |
||hnswCef |Number |No |400 |The hnsw index parameter, which represents the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when indexType is configured as IndexType. HNSW. |
||hnswSef |Number |No |800 |The hnsw index parameter represents the search breadth of the online search.<br><br><br>* Optional configuration when indexType is configured as IndexType. HNSW. |
|cpuQuota |*  |Int |No |2 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Depending on throughput, regardless of latency, 1 CPU core is about 100QPS.<br><br>* The total CPU consumption is the configured quota multiplied by the number of shards. If CPU consumption during retrieval exceeds this total quota, requests will be throttled.<br><br>* Value range: [2,10240]. |
|Description |*  |String |No |" |A custom description of the index. |
|PartitionBy |*  |String |No |" |The field name used to create sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It enables searching within a specific sub\-index during mixed retrieval and reduces filtering, thereby improving retrieval performance.<br><br><br>* partitionBy corresponds to the field name fieldName, and supports field types of int64, list< int64 \>, string, list\ < string \>. Partition corresponds to the field value of field.<br><br>* The recommended number of partitionBy partitions should not exceed 1000.<br><br>* When the partitionBy parameter is not set, the subindex partition defaults to "default".<br><br>* Applicable scenarios: It is suitable for scenarios where the data set is divided into multiple sub\-datasets and the retrieval mode is fixed in a certain sub\-dataset/sub\-index. For example, splitting the dataset according to the country ID, and searching the sub\-index of a certain country ID does not need to filter the country ID to improve the retrieval performance. |
|scalarIndex |*  |Array |No |None |List of scalar fields.<br><br><br>* scalarIndex defaults to None, which means all fields are built to a scalar index.<br><br>* When scalarIndex is [], it means there is no scalar index.<br><br>* When scalarIndex is a non\-empty list, it means that the fields in the list are built into a scalar index. |
|shardCount |*  |Int |No |*  |Index sharding refers to the fact that in a large\-scale data volume scenario, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and the query load can be distributed to different nodes for concurrent processing. When a node fails, the system can automatically migrate the sharding data on it to other normal nodes to ensure stability, so as to achieve horizontal expansion of data and high\-performance read and write operations.<br><br><br>* Value range: [1,256].<br><br>* The default is 1. To estimate the required number of shards, use the formula: (estimated data volume) / 30 million. |
|shardPolicy |*  |String |No |*  |Index sharding type<br><br><br>* The optional value is ShardType.Auto/ShardType.Custom, auto is automatic sharding, custom is custom sharding.<br><br><br>Index sharding refers to dividing index data into multiple small index data blocks in a large\-scale data volume scenario and distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data. The query will request index data blocks on different nodes at the same time. Because a single node has limited capacity, you must configure an appropriate number of shards to store the entire index. An incorrect number of shards can negatively affect indexing performance. In addition, the number of shards is related to cost; more shards result in higher costs. |


<span id="868d56b5"></span>
# Example

<span id="bd0f3c0e"></span>
## Request parameters

```Java
        VectorIndexParams vectorIndex = new VectorIndexParams()
                                        .setDistance(DistanceType.COSINE)
                                        .setIndexType(IndexType.HNSW_HYBRID)
                                        .setQuant(QuantType.Float)
                                        .build();
        List scalarIndex = new ArrayList<>();
        scalarIndex.add("price");
        scalarIndex.add("aim");
        CreateIndexParam createIndexParam = new CreateIndexParam()
                                        .setCollectionName("javaSDKTest")
                                        .setIndexName("test_index")
                                        .setDescription("this is a test for index")
                                        .setCpuQuoat(5)
                                        .setVectorIndex(vectorIndex)
                                        .setScalarIndex(scalarIndex)
                                        .setPartitionBy("like")
                                        .build();
        Index index = vikingDBService.createIndex(createIndexParam);
        System.out.println(index);
```


<span id="3dc4ed41"></span>
## Return value

The Java call performs the above task and returns an Index instance. The Index instance contains the properties shown in the following table.


|**attribute** |**type** |**explain** |
|---|---|---|
|collectionName |String |The name of the collection to which the index belongs. |
|indexName |String |The name of the index. |
|Description |String |The description of the index. |
|cpuQuota |Int |The CPU quota for index searches. If CPU consumption during a search exceeds this quota, requests will be throttled. |
|PartitionBy |String |The field name used to create sub\-index partitions. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching within a specific sub\-index and reducing filtering during mixed retrieval. |
|vectorIndex |VectorIndexParams |Vector index parameters. |
|scalarIndex |ArrayList < string \> |Scalar index field list. |
|Status |String |Index state. The value is as follows:<br><br><br>* Init: The index is initializing, either being built or loaded.<br><br>* Ready: The index is online and ready to serve requests. |
|shardCount |Int |Sharding number. |
|createTime |String |Index creation time. |
|UpdateTime |String |Index update time. |
|UpdatePerson |String |The user who last updated the index. |
|indexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: index size in memory. |
|shardPolicy |String |Type of sharding |

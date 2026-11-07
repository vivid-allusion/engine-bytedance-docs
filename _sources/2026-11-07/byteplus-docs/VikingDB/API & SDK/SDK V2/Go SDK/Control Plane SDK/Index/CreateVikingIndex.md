---
title: "CreateVikingIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/CreateVikingIndex"
---

The price calculator can output three types of core estimated results based on your data and index configuration: computing resource (CU) usage, storage resource (disk capacity, unit GB), and corresponding cost details.

Usage link: https://console.volcengine.com/vikingdb/region:vikingdb+cn\-beijing/bohr/price\-calculator

CreateVikingdbIndex is used to create an Index for the specified Collection.

Creating an index can accelerate vector similarity search. It groups and sorts the raw data in the vector database according to the specified index algorithm and data structure, improving the efficiency and accuracy of similarity search. It is the core mechanism that enables the vector database to screen candidates in a short time.

For cases where the indexed dataset only contains dense vectors (i.e., vector type fields), we call this a pure dense index; for cases where the indexed dataset contains both dense and sparse vectors (vector and sparse_vector type fields), we call this a hybrid index.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `CreateVikingdbIndex(input)` method through the client instance created by `vikingdb.New(sess)` to initiate an index creation request. The input parameter is of type `vikingdb.CreateVikingdbIndexInput`, which contains the complete configuration information required for index creation.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `CreateVikingdbIndexInput`, and the included parameters are shown in the following table.


|**Parameter** |**Type** |**Required** |**Parameter Description** |
|---|---|---|---|
|ProjectName |string |No |Project name |
|CollectionName |string |One of two |Dataset name |
|ResourceId |string | |Dataset resource ID. The request must specify one of ResourceId and CollectionName. |
|IndexName |string |Yes |Specifies the name of the Index to create.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter, cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index name cannot be duplicated.<br><br>* Under the same account, the number of Index does not exceed 200. |
|Description |string |No |Custom description of the index. |
|ScalarIndex |[]string |No |Scalar field list, used to set the fields that need to be built into the scalar index. |
|ShardPolicy |ShardPolicyEnum |No |Index sharding type<br><br><br>* Optional values are ShardType.Auto/ShardType.Custom, ShardType.Auto is automatic sharding, ShardType.Custom is custom sharding. |
|ShardCount |int |No |Custom shard count. |
|CpuQuota |int |No |CPU quota consumed by index retrieval, in the format of a positive integer. |
|VectorIndex |VectorIndexForCreateVikingdbIndexInput |Yes |See below |



* VectorIndexForCreateVikingdbIndexInput



|**Parameter** |**Type** |**Required** |**Default Value** |**Parameter Description** |
|---|---|---|---|---|
|IndexType |IndexTypeEnum<br><br>Enumeration |Yes |IndexType.HNSW |Vector index type. Values are as follows:<br><br><br>* IndexType.HNSW: Full name is Hierarchical Navigable Small World, a data structure and algorithm for ANN search in high\-dimensional space, based on graph indexing. HNSW reduces the number of nodes that need to be accessed during search by building a multi\-layer network, enabling fast and efficient nearest neighbor search, suitable for scenarios with high search efficiency requirements.<br><br>* IndexType.HNSW_HYBRID: HNSW algorithm that supports hybrid indexes. The hybrid index algorithm can simultaneously index dense and sparse vectors in the dataset, and return results that take into account the similarity of both types during retrieval. Suitable for scenarios with high search efficiency requirements and the need to retrieve both sparse and dense vectors.<br><br>   The dataset for HNSW_HYBRID index must contain sparse_vector type data, i.e., sparse_vector type fields are defined, or a pipeline that can generate sparse_vector type vectors is bound.<br><br>* IndexType.FLAT: Brute\-force index, traverses all vectors in the entire vector database during search to perform distance calculation and comparison with the target vector. The query speed is slow, but flat can provide 100% retrieval recall rate, suitable for scenarios with small vector candidate sets and requiring 100% retrieval recall rate.<br><br>* IndexType.IVF: Inverted index, uses the inverted idea to store vectors under each clustering center. When querying vectors, find the nearest centers and search for vectors under these centers respectively. The speed is fast, but the accuracy is slightly lower. Suitable for medium\-scale data volume, scenarios with high search efficiency requirements and secondary accuracy.<br><br>* IndexType.DISKANN: Disk index algorithm based on Vamana graph, combining Vamana graph with PQ quantization compression scheme to build DiskANN index. The graph index and raw data are stored in SSD, and the compressed index is placed in memory. During retrieval requests, the query vector is compared with cluster centers, and then the corresponding raw data is read from disk for scoring. Suitable for large\-scale data volume, performance\-insensitive scenarios, with lower memory cost and higher recall rate. |
|Distance |DistanceEnum Enumeration |No |DistanceType.IP |Distance type, algorithm for measuring the distance between vectors. Values are as follows:<br><br><br>* DistanceType.IP: Full name is Inner Product, inner product. This algorithm calculates similarity based on the inner product of vectors, i.e., the result of multiplying and summing corresponding elements of two elements. The larger the inner product value, the higher the similarity.<br><br>* DistanceType.L2: Euclidean distance, which calculates the Euclidean space distance of two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>* DistanceType.COSINE: Cosine similarity (Cosine Similarity), also known as Cosine distance (Cosine Distance), used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. The smaller the cosine value of the angle, the larger the angle between the two vectors, indicating a greater difference between the two vectors.<br><br>   When distance=DistanceType.COSINE, vectors are normalized by default.<br><br><br>For HNSW_HYBRID index algorithm, distance type selection only applies to dense vectors, sparse vectors only support inner product. |
|Quant |QuantEnum Enumeration |No |QuantType.Int8 |Quantization method. Quantization method is the compression method of vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce the storage and computing costs of vectors. Values are as follows:<br><br><br>* QuantType.Int8: Compresses 4\-byte float into a single byte to obtain memory and computing latency benefits, causing minor precision loss, for example, cosine distance may have scores greater than 1.<br><br>* QuantType.Float: Full precision, no compression quantization.<br><br>* QuantType.Fix16: Compresses 4\-byte float into two bytes to obtain memory and computing latency benefits, causing minor precision loss. By sacrificing a certain amount of retrieval precision, it improves retrieval performance and saves resource costs.<br><br>* QuantType.PQ: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and improve search efficiency. |
|HnswM |int |No |20 |HNSW index parameter, indicating the number of neighbor nodes.<br><br><br>* Can be configured when indexType is configured as IndexType.HNSW. |
|HnswCef |int |No |400 |HNSW index parameter, indicating the search breadth of neighbor nodes when building the graph.<br><br><br>* Can be configured when indexType is configured as IndexType.HNSW. |
|HnswSef |int |No |800 |HNSW index parameter, indicating the search breadth for online retrieval.<br><br><br>* Can be configured when indexType is configured as IndexType.HNSW. |
|DiskannM |int |No | |DiskANN parameter, indicating the number of neighbor nodes.<br><br><br>* Can be configured when IndexType is configured as IndexType.DISKANN. |
|DiskannCef |int |No | |DiskANN parameter, indicating the search breadth of neighbor nodes when building the graph.<br><br><br>* Can be configured when IndexType is configured as IndexType.DISKANN. |
|PqCodeRatio |float |No | |DiskANN parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it will increase memory usage, range (0.0, 0.25].<br><br><br>* Can be configured when IndexType is configured as IndexType.DISKANN. |
|CacheRatio |float |No | |DiskANN parameter, ratio of cache nodes to raw data. A larger value will improve index performance and increase memory usage. Range [0.0, 0.3).<br><br><br>* Can be configured when IndexType is configured as IndexType.DISKANN. |


<span id="return-parameters"></span>
# Return Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|Message |String |success |Operation result information |


<span id="example"></span>
# Example

```Go
package main

import (
    "fmt"
    "os"

    "github.com/volcengine/volcengine-go-sdk/service/vikingdb"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func main() {
    var (
       accessKey = os.Getenv("VIKINGDB_AK")
       secretKey = os.Getenv("VIKINGDB_SK")
       region    = "ap-southeast-1"
    )

    config := volcengine.NewConfig().
       WithRegion(region).
       WithCredentials(credentials.NewStaticCredentials(accessKey, secretKey, ""))

    sess, err := session.NewSession(config)
    if err != nil {
       panic(err)
    }
    svc := vikingdb.New(sess)

    input := &vikingdb.CreateVikingdbIndexInput{
       CollectionName: volcengine.String("Your Collection Name"),
       IndexName:      volcengine.String("Your Index Name"),
       Description:    volcengine.String("Your Index Description"),
       ProjectName:    volcengine.String("default"),
       VectorIndex: &vikingdb.VectorIndexForCreateVikingdbIndexInput{
          IndexType: volcengine.String(vikingdb.EnumOfIndexTypeForCreateVikingdbIndexInputHnsw),
          Distance:  volcengine.String(vikingdb.EnumOfDistanceForCreateVikingdbIndexInputL2),
          Quant:     volcengine.String(vikingdb.EnumOfQuantForCreateVikingdbIndexInputFloat),
          HnswM:     volcengine.Int32(16),
          HnswCef:   volcengine.Int32(200),
          HnswSef:   volcengine.Int32(200),
       },
       ScalarIndex: volcengine.StringSlice([]string{"title"}),
    }

    output, err := svc.CreateVikingdbIndex(input)
    if err != nil {
       panic(err)
    }
    fmt.Printf("Create index response: %+v\n", output)
}
```

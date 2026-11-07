---
title: "GetVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/GetVikingdbIndex"
---

<span id="overview"></span>
# Overview

GetVikingdbIndex is used to query the details of an Index.

<span id="method-definition"></span>
# Method Definition

The Go SDK uses the client instance created by `vikingdb.New(sess)` to call the `GetVikingdbIndex(input)` method to initiate an index query request. The input parameter type is `vikingdb.GetVikingdbIndexInput`, which contains the parameter information required to query index details.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |string |No |Project name |
|CollectionName |string |One of two required |Collection name |
|ResourceId |string | |Collection resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |string |Yes |Specifies the name of the Index to query.<br><br><br>* Can only use English letters, numbers, and underscores, must start with an English letter, and cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index names must be unique. |


<span id="return-parameters"></span>
# Return Parameters

Go calls execute the above task and return an Index instance. The properties contained in the Index instance are shown in the table below.


|Parameter |First\-level Sub\-parameter |Type |Description |
|---|---|---|---|
|CollectionName | |string |Collection name |
|ProjectName | |string |Project name |
|ResourceId | |string |Resource ID |
|IndexName | |string |Index name |
|CpuQuota | |int |CPU quota consumed for index retrieval. |
|ShardPolicy | |string |Index sharding type, auto for automatic sharding, custom for custom sharding. |
|ShardCount | |int |Index shard count |
|Description | |string |Index description |
|VectorIndex | |VectorIndexForGetVikingdbIndexOutput |Vector index configuration |
| |IndexType |IndexTypeEnum<br><br>Enum |Index type |
| |Distance |DistanceEnum<br><br>Enum |Distance type, the algorithm for measuring the distance between vectors. Values are as follows:<br><br>ip: Full name is Inner Product. This algorithm calculates similarity based on the inner product of vectors, which is the sum of the products of corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance, which calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine Similarity, also known as Cosine Distance. It calculates the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. A smaller cosine value indicates a larger angle between the two vectors, meaning greater difference between the vectors.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When the index algorithm is IVF, the distance type can be ip or cosine.<br><br>For the hnsw_hybrid index algorithm, the distance type selection only applies to dense vectors; sparse vectors only support inner product. |
| |Quant |QuantEnum<br><br>Enum |Quantization method. Quantization is the compression method for vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce vector storage and computation costs. Values are as follows:<br><br><br>* int8: Compresses 4\-byte floats into single bytes to gain benefits in memory and computation latency, with minimal precision loss, such as cosine distance scores exceeding 1.<br><br>* float: Full precision, no compression quantization.<br><br>* fix16: Compresses 4\-byte floats into two bytes to gain benefits in memory and computation latency, with minimal precision loss. By sacrificing some retrieval precision, it improves retrieval performance and saves resource costs.<br><br>* pq: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 applies to hnsw, hnsw_hybrid, flat index algorithms with distance methods ip, cosine.<br><br>float applies to hnsw, hnsw_hybrid, flat, diskann index algorithms with distance methods ip, l2, cosine.<br><br>fix16 applies to hnsw, hnsw_hybrid, flat index algorithms with distance methods ip, l2, cosine.<br><br>pq applies to diskann, ivf index algorithms with distance methods ip, l2, cosine. |
| |HnswM |int |hnsw index parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| |HnswCef |int |hnsw index parameter, indicating the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| |HnswSef |int |hnsw index parameter, indicating the search breadth for online retrieval.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| |DiskannM |int |diskann parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is set to diskann. |
| |DiskannCef |int |diskann parameter, indicating the breadth of searching neighbor nodes when building the graph.<br><br><br>* Optional configuration when index_type is set to diskann. |
| |PqCodeRatio |float |diskann parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it increases memory usage. Range (0.0, 0.25].<br><br><br>* Optional configuration when index_type is set to diskann. |
| |CacheRatio |float |diskann parameter, ratio of cached nodes to original data. A larger value improves index performance and increases memory usage. Range [0.0, 0.3).<br><br><br>* Optional configuration when index_type is set to diskann. |
|ScalarIndex | |[]ScalarIndexForGetVikingdbIndexOutput |Scalar field list<br><br>`json <br> "ScalarIndex": [ <br> { <br> "FieldName": "f_int64_1", <br> "FieldType": "int64", <br> "DefaultValue": 0 <br> } <br> ] <br>` |
| |DefaultValue |interface{} | |
| |Dim |int | |
| |FieldName |string | |
| |FieldType |string | |
|ActualCU | |int |Actual CU usage |


<span id="examples"></span>
# Examples

<span id="request-parameters"></span>
## Request Parameters

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

    // Get index information
    input := &vikingdb.GetVikingdbIndexInput{
       CollectionName: volcengine.String("Your Collection Name"),
       IndexName:      volcengine.String("Your Index Name"),
       ProjectName:    volcengine.String("default"),
    }

    output, err := svc.GetVikingdbIndex(input)
    if err != nil {
       panic(err)
    }
    fmt.Printf("Get index response: %+v\n", output)
}
```

---
title: "ListVikingIndexes"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/ListVikingIndexes"
---

<span id="overview"></span>
# Overview

`ListVikingdbIndex` is used to query the list of indexes associated with a Collection.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `ListVikingdbIndex(input)` method through a client instance created with `vikingdb.New(sess)` to initiate an index list query request. The input parameter is of type `vikingdb.ListVikingdbIndexInput` and contains the parameters required for the query.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter |Type |Required |Description |
|---|---|---|---|
|PageNumber |int |No |Page number for pagination. Starts at 1. |
|PageSize |int |No |Page size for pagination. |
|ProjectName |string |No |Project name, default is default. |
|Filter |FilterForListVikingdbIndexInput |No |Filter conditions, as follows: |



* FilterForListVikingdbIndexInput



|Parameter |Type |Description |
|---|---|---|
|CollectionName |[]string |Collection name |
|IndexNameKeyword |string |Index name |
|Status |[]string |Status |


<span id="response-parameters"></span>
# Response Parameters

Go executes the above operation and returns a list of Index instances. The properties contained in the Index instance are shown in the table below.


|Parameter |First\-level Sub\-parameter |Second\-level Sub\-parameter |Type |Description |
|---|---|---|---|---|
|Indexes | | |[]IndexForListVikingdbIndexOutput |Vector database index details list |
| |CollectionName | |string |Collection name |
| |ProjectName | |string |Project name |
| |ResourceId | |string |Resource ID |
| |IndexName | |string |Index name |
| |Description | |string |Custom description of the index. |
| |VectorIndex | |VectorIndexForListVikingdbIndexOutput |Vector index configuration |
| | |IndexType |IndexTypeEnum<br><br>Enum |Index type |
| | |Distance |DistanceEnum<br><br>Enum |Distance type, the algorithm for measuring the distance between vectors. Values are as follows:<br><br>ip: Full name is Inner Product. This algorithm calculates similarity based on the inner product of vectors, i.e., the result of multiplying and summing corresponding elements of two vectors. The larger the inner product value, the higher the similarity.<br><br>l2: Euclidean distance. It calculates the Euclidean space distance between two vectors. The smaller the Euclidean distance, the higher the similarity.<br><br>cosine: Cosine Similarity, also known as Cosine Distance. Used to calculate the cosine value of the angle between two high\-dimensional vectors to measure vector similarity. A smaller cosine value indicates a larger angle between the two vectors, meaning greater difference between them.<br><br>When distance=cosine, vectors are normalized by default.<br><br>When the index algorithm is IVF, distance types can be ip or cosine.<br><br>For the hnsw_hybrid index algorithm, distance type selection only applies to dense vectors; sparse vectors only support inner product. |
| | |Quant |QuantEnum<br><br>Enum |Quantization method. Quantization is the compression method for vectors in the index, which can reduce the complexity of similarity calculation between vectors. Based on the high\-dimensional and large\-scale characteristics of vectors, vector quantization can effectively reduce vector storage and computing costs. Values are as follows:<br><br><br>* int8: Compresses 4\-byte floats into a single byte to gain benefits in memory and computation latency. May cause minor precision loss, such as cosine distance scores greater than 1.<br><br>* float: Full precision, no compression quantization.<br><br>* fix16: Compresses 4\-byte floats into two bytes to gain benefits in memory and computation latency. May cause minor precision loss. By sacrificing some retrieval precision, it improves retrieval performance and saves resource costs.<br><br>* pq: Converts high\-dimensional vectors into low\-dimensional codebook vectors to reduce memory usage and improve search efficiency.<br><br><br>int8 applies to hnsw, hnsw_hybrid, flat index algorithms with distance methods ip, cosine.<br><br>float applies to hnsw, hnsw_hybrid, flat, diskann index algorithms with distance methods ip, l2, cosine.<br><br>fix16 applies to hnsw, hnsw_hybrid, flat index algorithms with distance methods ip, l2, cosine.<br><br>pq applies to diskann, ivf index algorithms with distance methods ip, l2, cosine. |
| | |HnswM |int |hnsw index parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| | |HnswCef |int |hnsw index parameter, indicating the breadth of searching for neighbor nodes during graph construction.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| | |HnswSef |int |hnsw index parameter, indicating the search breadth for online retrieval.<br><br><br>* Optional configuration when index_type is set to hnsw or hnsw_hybrid. |
| | |DiskannM |int |diskann parameter, indicating the number of neighbor nodes.<br><br><br>* Optional configuration when index_type is set to diskann. |
| | |DiskannCef |int |diskann parameter, indicating the breadth of searching for neighbor nodes during graph construction.<br><br><br>* Optional configuration when index_type is set to diskann. |
| | |PqCodeRatio |float |diskann parameter, size limit for vector dimension encoding. The larger the value, the higher the recall rate, but it increases memory usage. Range (0.0, 0.25].<br><br><br>* Optional configuration when index_type is set to diskann. |
| | |CacheRatio |float |diskann parameter, ratio of cached nodes to original data. A larger value improves index performance and increases memory usage. Range [0.0, 0.3).<br><br><br>* Optional configuration when index_type is set to diskann. |
| |ScalarIndex | |[]ScalarIndexForListVikingdbIndexOutput |Scalar field list |
| |CpuQuota | |int |CPU quota consumed by index retrieval. |
| |ShardPolicy | |string |Index sharding type, auto for automatic sharding, custom for custom sharding. |
| |ShardCount | |int |Number of index shards |
| |ActualCU | |int |Actual CU usage |
|PageSize | | |int |PageSize value from the request, or the default value if not specified in the request. |
|PageNumber | | |int |PageNumber value from the request, or the default value if not specified in the request. |
|TotalCount | | |int |Total number of query results |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

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

    input := &vikingdb.ListVikingdbIndexInput{
       Filter: &vikingdb.FilterForListVikingdbIndexInput{
          CollectionName: volcengine.StringSlice([]string{"Your Collection Name"}),
       },
       ProjectName: volcengine.String("default"),
    }

    output, err := svc.ListVikingdbIndex(input)
    if err != nil {
       panic(err)
    }
    fmt.Printf("List index response: %+v\n", output)
}
```

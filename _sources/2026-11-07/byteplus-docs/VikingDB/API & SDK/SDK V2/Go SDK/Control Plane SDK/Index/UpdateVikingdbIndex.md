---
title: "UpdateVikingdbIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/UpdateVikingdbIndex"
---

<span id="overview"></span>
# Overview

The UpdateVikingdbIndex API is used to modify the description, scalar index, CPU quota, or sharding strategy of an existing index.

<span id="method-definition"></span>
# Method Definition

The Go SDK calls the `UpdateVikingdbIndex(input)` method through a client instance created with `vikingdb.New(sess)` to initiate an index update request. The input parameter is of type `vikingdb.UpdateVikingdbIndexInput` and contains the complete configuration information required for the index update.

<span id="request-parameters"></span>
# **Request Parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ProjectName |string |No |Project name |
|CollectionName |string |One of two |Specifies the Collection name that the modified index belongs to.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter. Cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Collection names cannot be duplicated. |
|ResourceId |string |One of two |Dataset resource ID. The request must specify either ResourceId or CollectionName. |
|IndexName |string |Yes |Specifies the name of the Index to be modified.<br><br><br>* Can only use English letters, numbers, underscores _, and must start with an English letter. Cannot be empty.<br><br>* Length requirement: [1, 128].<br><br>* Index names cannot be duplicated. |
|CpuQuota |int |No |CPU quota consumed by index retrieval, formatted as a positive integer.<br><br><br>* Related to throughput, not related to latency. 1 CPU core is approximately 100 QPS.<br><br>* N shards result in N times CPU consumption. If the CPU consumed by retrieval exceeds the quota, the index will be rate\-limited.<br><br>* Value range: [2, 10240]. |
|Description |string |No |Custom description of the index. |
|ScalarIndex |[]string |No |List of scalar fields.<br><br><br>* scalarIndex defaults to None, indicating all fields are built into the scalar index.<br><br>* When scalarIndex is [], it means no scalar index exists.<br><br>* When scalarIndex is a non\-empty list, it means the fields in the list are built into the scalar index.<br><br><br>If scalar fields are included in the scalar index, they are mainly used for range filtering and enumeration filtering, and will consume additional resources:<br><br><br>* Range filtering: float32, int64<br><br>* Enumeration filtering: int64, string, list, list, bool<br><br><br>If scalar fields are not included in the scalar index, they can still be selected and used as forward index fields and for partial forward index calculations. |
|ShardCount |int |No |Number of shards. Index sharding refers to dividing index data into multiple small index blocks in large\-scale data scenarios, distributing them to different nodes in the same cluster for management. Each node is responsible for storing and processing a portion of the data, allowing query loads to be distributed across different nodes for concurrent processing. When a node fails, the system can automatically migrate shard data from that node to other normal nodes to ensure stability, achieving horizontal data scaling and high\-performance read and write operations.<br><br><br>* Value range: [1, 256].<br><br>* Default is 1. Shard count estimation reference: estimated data volume / 30 million. |


<span id="response-parameters"></span>
# Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|message |String |success |Operation result information |


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

    input := &vikingdb.UpdateVikingdbIndexInput{
       CollectionName: volcengine.String("Your Collection Name"),
       IndexName:      volcengine.String("Your Index Name"),
       ProjectName:    volcengine.String("default"),
       Description:    volcengine.String("Your Index Description"),
       ShardCount:     volcengine.Int32(2),
    }

    output, err := svc.UpdateVikingdbIndex(input)
    if err != nil {
       panic(err)
    }
    fmt.Printf("Update index response: %+v\n", output)
}
```


 &nbsp;

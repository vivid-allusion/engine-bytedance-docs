---
title: "UpdateIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_UpdateIndex"
---

<span id="c2a7c6b3"></span>
# Overview

The UpdateIndex interface allows you to modify the configuration of a specified index. You can use it to update parameters such as the index description, CPU quota, scalar index fields, and shard count.

<span id="e75421c0"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the name of the Collection to which the index was created.<br><br><br>* Must contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |*  |String |Yes |*  |Specifies the name of the index created.<br><br><br>* Must contain only English letters, numbers, and underscores (_). It must begin with an English letter and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|updateIndexOptions |cpuQuota |Int |No |2 |The CPU quota for index retrieval, specified as a positive integer<br><br><br>* As a general estimate where throughput is prioritized over latency, one CPU core can handle approximately 100 QPS<br><br>* N times the CPU consumption of the number of shardings; if the CPU consumption of the retrieval exceeds the quota, requests to the index will be rate\-limited<br><br>* Value range: [2,10240]. |
||Description |String |No |" |A custom description of the index. |
||scalarIndex |Array |No |None |List of scalar fields.<br><br><br>* If `scalarIndex` is not set (defaults to `None`), a scalar index is built for all fields<br><br>* When scalarIndex is [], it means there is no scalar index.<br><br>* When `scalarIndex` is a non\-empty list, a scalar index is built for the specified fields |
| |shardCount |Int |No |1 |Index sharding is the process of dividing index data into smaller blocks (shards) and distributing them across nodes in a cluster. This strategy supports horizontal scaling and high\-performance operations for large datasets. Each node processes a portion of the data, allowing query loads to be distributed for concurrent processing. For high availability, if a node fails, its shards are automatically migrated to other healthy nodes.<br><br><br>* Value range: [1,256].<br><br>* Default is 1, As a guideline for estimating the number of shards, divide the estimated data volume by 30 million |


<span id="46c57616"></span>
# Example

<span id="28763430"></span>
## Request parameters

```Go
params := vikingdb.NewUpdateIndexOptions().SetDescription("go").SetCpuQuota(5).SetScalarIndex([]string{"like", "aim"})
err := service.UpdateIndex("example", "example_index", params)
if err != nil {
    fmt.Println(err)
}
```


<span id="7bd66975"></span>
## Return value

If the operation is successful, the function does not return a value. It returns an error if the operation fails.

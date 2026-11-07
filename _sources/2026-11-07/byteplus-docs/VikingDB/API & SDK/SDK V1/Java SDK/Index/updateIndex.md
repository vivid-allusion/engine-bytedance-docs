---
title: "updateIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_updateIndex"
---

<span id="8418960a"></span>
# Overview

The updateIndex interface is used to update the description, cpuQuota, and scalarIndex of the specified index.

<span id="526dd395"></span>
# **Request parameters**

The request parameter is UpdateIndexParam, and the parameters included in the UpdateIndexParam class are shown in the following table.


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collectionName |*  |String |Yes |*  |Specifies the name of the collection to which the index belongs.<br><br><br>* The name must begin with an English letter, can only contain English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|indexName |*  |String |Yes |*  |Specifies the name of the index.<br><br><br>* The name must begin with an English letter, can only contain English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|cpuQuota |*  |Int |No |2 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Throughput is approximately 100 QPS per CPU core, not accounting for latency.<br><br>* N times the CPU consumption of the number of shardings; if retrieval operations exceed the CPU quota, they will be rate\-limited.<br><br>* Value range: [2,10240]. |
|Description |*  |String |No |" |A custom description of the index. |
|scalarIndex |*  |Array |No |None |List of scalar fields.<br><br><br>* scalarIndex defaults to None, which means all fields are built to a scalar index.<br><br>* When scalarIndex is [], it means there is no scalar index.<br><br>* When scalarIndex is a non\-empty list, it means that the fields in the list are built into a scalar index. |
|shard_count |*  |Int |No |1 |Index sharding is a technique for large\-scale datasets where index data is divided into smaller blocks (shards) and distributed across different nodes in a cluster. Each node is responsible for storing and processing part of the data, allowing query loads to be distributed across nodes for concurrent processing. If a node fails, the system can automatically migrate its shards to healthy nodes to ensure stability. This enables horizontal scaling and high\-performance read/write operations.<br><br><br>* Value range: [1,256].<br><br>* The default is 1. To estimate the required number of shards, use the formula: `estimated data volume / 30 million`. |


<span id="b4ea8a6f"></span>
# Example

<span id="62c9ea7a"></span>
## Request parameters

```Java
List scalar_index = new ArrayList<>();
        scalar_index.add("like");
        UpdateIndexParam parmas = new UpdateIndexParam().setCollectionName("example")
                                        .setIndexName("example_index")
                                        .setCpuQuoat(3)
                                        .setDescription("java test")
                                        .setScalarIndex(scalar_index)
                                        .build();
        vikingDBService.updateIndex(parmas);
```


<span id="9e8c38ed"></span>
## Return value

This operation does not return a value when called from Java.

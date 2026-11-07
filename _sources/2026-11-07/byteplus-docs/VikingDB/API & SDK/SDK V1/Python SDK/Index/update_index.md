---
title: "update_index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_update_index"
---

<span id="478792df"></span>
# Overview

This document describes how to use the update_index interface to modify the configuration of an existing index. You can update parameters such as the index description, CPU quota, and the list of scalar fields.

This document also covers the asynchronous version of this operation, async_update_index.

<span id="c768687d"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|---|
|collection_name |*  |String |Yes |*  |Specifies the name of the collection to which the index belongs.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |*  |String |Yes |*  |Specifies the name of the index.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |
|cpu_quota |*  |Int |No |2 |CPU quota consumed by index retrieval, in the form of a positive integer.<br><br><br>* Depending on throughput, regardless of latency, 1 CPU core is about 100QPS.<br><br>* The total CPU consumption is N times the number of shards. If retrieval requests exceed the CPU quota, they will be throttled.<br><br>* Value range: [2,10240]. |
|Description |*  |String |No |" |A custom description of the index. |
|scalar_index |*  |Array |No |None |List of scalar fields.<br><br><br>* If set to None (the default), a scalar index is built for all fields.<br><br>* An empty list (`[]`) means no scalar index will be created.<br><br>* If scalar_index is a non\-empty list, a scalar index is built only for the fields in the list. |
|shard_count |*  |Int |No |1 |Index sharding refers to the fact that in a large\-scale data volume scenario, index data can be divided into multiple small index blocks and distributed to different nodes in the same cluster for management. Each node is responsible for storing and processing part of the data, and the query load can be distributed to different nodes for concurrent processing. When a node fails, the system automatically migrates its data shards to other healthy nodes to ensure stability, enabling horizontal scaling and high\-performance read/write operations.<br><br><br>* Value range: [1,256].<br><br>* The default is 1. To estimate the required number of shards, use the following guideline: Estimated data volume / 30 million. |


<span id="3328c1cf"></span>
# Example

<span id="67d9e2e5"></span>
## Request parameters

```Python
vikingdb_service.update_index("example", "example_index", description="update index", cpu_quota=4, scalar_index=["aim"])
       
# Asynchronous call
async def update_index():
    await vikingdb_service.async_update_index("async", "async", shard_count=3)                       
asyncio.run(update_index())
```


<span id="cee6afb0"></span>
## Return value

This Python call does not return a value.

---
title: "list_indexes"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_list_indexes"
---

<span id="5c965305"></span>
# Overview

The list_indexes function retrieves a list of all indices associated with a specified collection. This document provides details on its parameters, return values, and includes examples for both synchronous (list_indexes) and asynchronous (async_list_indexes) calls.

The asynchronous call uses the async_list_indexes interface, and the parameters remain unchanged.

<span id="cc7f1711"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* The name must begin with an English letter, contain only English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="b3f61b2a"></span>
# Example

<span id="a8cd2c73"></span>
## Request parameters

```Python
res = vikingdb_service.list_indexes("example")

# Asynchronous call
async def list_index():
    res = await vikingdb_service.async_list_indexes("async")
asyncio.run(list_index())
```


<span id="a00f990f"></span>
## Return value

The Python call performs the above task and returns a list of Index instances. The properties contained in an Index instance are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|collection_name |String |Displays the Collection name to which the index belongs. |
|index_name |String |Displays the index name. |
|Description |String |Displays a description of the index. |
|cpu_quota |Int |Displays the CPU quota consumed by the index during search operations. |
|partition_by |String |Partitions the index based on a specified scalar field. Dividing the dataset into sub\-indexes improves retrieval performance by reducing the search space and the amount of filtering required during hybrid searches. |
|vector_index |VectorIndexParams |Vector index parameters. |
|scalar_index |ArrayList < string \> |Scalar index field list. |
|Stat |String |Index state. The value is as follows:<br><br><br>* INIT: Initializing. The index is being built or loaded.<br><br>* CHANGING: Updating. The index is being rebuilt or reloaded.<br><br>* READY: Ready. The index is available for use. |
|shard_count |Int |Number of shards. |
|create_time |String |Index creation time. |
|update_time |String |Index update time. |
|update_person |String |Last updated by. |
|index_cost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: index size in memory. |
|shard_policy |String |Sharding strategy |

---
title: "get_index"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_get_index"
---

<span id="50759ca7"></span>
# Overview

To retrieve the detailed information for a specific index, you can use the get_index method. This method allows you to check properties like index status, configuration, and resource usage.

For asynchronous operations, an async_get_index method is provided with identical parameters.

<span id="0bfa12ca"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collection_name |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* The name must begin with an English letter, contain only English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |
|index_name |String |Yes |Specify the name of the Index to query.<br><br><br>* The name must begin with an English letter, contain only English letters, numbers, and underscores (_), and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names cannot be repeated. |


<span id="8a0096ca"></span>
# Example

<span id="f6039a7f"></span>
## Request parameters

```Python
res = vikingdb_service.get_index("example", "example_index")

# Asynchronous call
async def get_index():
    res = await vikingdb_service.async_get_index("async", "async")
asyncio.run(get_index())
```


<span id="b099073d"></span>
## Return value

The Python call performs the above task and returns an Index instance. The properties contained in an Index instance are shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|Collection |String |The name of the collection to which the index belongs. |
|Index |String |The index name. |
|Description |String |A description of the index. |
|cpu_quota |Int |Displays the CPU quota consumed by the index for online search. |
|partition_by |String |Divides the index into partitions based on a specified scalar field. This feature improves retrieval performance by building separate sub\-indexes for different data partitions, which reduces filtering during hybrid searches. |
|vector_index |VectorIndexParams |Vector index parameters. |
|scalar_index |ArrayList < string \> |Scalar index field list. |
|Stat |String |Index state. The value is as follows:<br><br><br>* INIT: Initialized, being built or loaded.<br><br>* CHANGING: Changing, being modified, built, or loaded<br><br>* READY: Ready to serve requests. |
|shard_count |Int |Sharding number. |
|create_time |String |Index creation time. |
|update_time |String |Index update time. |
|update_person |String |The user who last updated the index. |
|index_cost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: The index size in memory. |
|shard_policy |String |Sharding strategy |

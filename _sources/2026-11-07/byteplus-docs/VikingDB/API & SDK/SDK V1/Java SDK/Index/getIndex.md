---
title: "getIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_getIndex"
---

<span id="1be819de"></span>
# Overview

To retrieve the details of a specific index, you can use the `getIndex` function. This API reference provides the required parameters, details the structure of the returned `Index` object, and includes a Java code example to help you get started.

<span id="a316f12a"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specify the name of the collection that contains the index.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_).<br><br>* Length requirements: [1,128].<br><br>* Collection names must be unique. |
|indexName |String |Yes |Specify the name of the Index to query.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_).<br><br>* Length requirements: [1,128].<br><br>* Index names must be unique within the collection. |


<span id="e8f9a74b"></span>
# Example

<span id="2e67847c"></span>
## Request parameters

```Java
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


<span id="918ae427"></span>
## Return value

This Java call performs the above task and returns an Index instance. The Index instance contains the properties shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|Collection |String |The name of the collection to which the index belongs. |
|Index |String |Displays the index name. |
|Description |String |Displays a description of the index. |
|cpuQuota |Int |Displays the CPU quota consumed by the index online search. |
|PartitionBy |String |Specifies the scalar field used to partition the dataset. According to a scalar field, the dataset can be divided into different sub\-datasets, and different sub\-datasets can be constructed into different sub\-indexes. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval. |
|vectorIndex |VectorIndexParams |Vector index parameters. |
|scalarIndex |ArrayList < string \> |A list of scalar index fields. |
|Stat |String |Index state. The value is as follows:<br><br><br>* INIT: The index is being initialized, built, or loaded.<br><br>* The index is being modified, which may involve a rebuild or reload.<br><br>* The index is active and can serve queries. |
|shardCount |Int |The number of shards. |
|createTime |String |Index creation time. |
|UpdateTime |String |Index update time. |
|UpdatePerson |String |The user who last updated the index. |
|indexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* The memory footprint of the index (GB). |

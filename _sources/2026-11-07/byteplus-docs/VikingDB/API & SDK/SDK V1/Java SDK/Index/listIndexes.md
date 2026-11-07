---
title: "listIndexes"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_listIndexes"
---

<span id="51891b9c"></span>
# Overview

listIndexes is used to query the list of indices associated with the Dataset Collection.

<span id="3b479c9d"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* Must begin with an English letter and can only contain English letters, numbers, and underscores (_). Cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="c5c785ef"></span>
# Example

<span id="34304c40"></span>
## Request parameters

```Java
List indexes = vikingDBService.listIndexes("javaSDKTest");
```


<span id="2c81d07f"></span>
## Return value

The Java call returns a list of Index instances. An Index instance contains the properties shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|collectionName |String |Displays the Collection name to which the index belongs. |
|indexName |String |Displays the index name. |
|Description |String |Displays a description of the index. |
|cpuQuota |Int |Displays the CPU quota consumed by the index online search. |
|PartitionBy |String |Used to partition the index based on a specified scalar field. Based on a scalar field, the dataset is divided into sub\-datasets, and each sub\-dataset is built into a separate sub\-index. It can improve the retrieval performance by searching in the sub\-index and reducing filtering during mixed retrieval. |
|vectorIndex |VectorIndexParams |Vector index parameters. |
|scalarIndex |ArrayList < string \> |A list of scalar index fields. |
|Stat |String |The state of the index. The value is as follows:<br><br><br>* INIT: Initialized, being built or loaded.<br><br>* CHANGING: The index is being modified.<br><br>* READY: It is ready to serve queries. |
|shardCount |Int |The number of shards. |
|createTime |String |The time when the index was created. |
|UpdateTime |String |The time when the index was last updated. |
|UpdatePerson |String |The user who last updated the index. |
|indexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: Memory usage of the index in GB. |

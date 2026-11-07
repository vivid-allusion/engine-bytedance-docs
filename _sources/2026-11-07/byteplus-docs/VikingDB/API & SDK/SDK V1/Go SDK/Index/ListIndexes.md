---
title: "ListIndexes"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_ListIndexes"
---

<span id="9018af5c"></span>
# Overview

To retrieve detailed information about all indexes within a specific collection, you can use the `ListIndexes` function. This function returns a comprehensive list of index objects, including their names, status, configuration details, and resource consumption metrics.

<span id="cd435b0f"></span>
# **Request parameters**


|**parameter** |**type** |**Required** |**Parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* Must contain only English letters, numbers, and underscores (_), must begin with an English letter, and cannot be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names cannot be repeated. |


<span id="e9ef99b8"></span>
# Example

<span id="612f8c9f"></span>
## Request parameters

```Go
indexes, err := service.ListIndexes("go")
if err != nil {
    fmt.Println(err)
}
for _, index := range indexes {
    fmt.Println(index)
}
```


<span id="eb649415"></span>
## Return value

This function call returns a slice of pointers to Index structs ([]\*Index). The Index struct contains the properties shown in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|CollectionName |String |The name of the Collection to which the index belongs. |
|IndexName |String |The index name. |
|Description |String |A description of the index. |
|CpuQuota |Int |Displays the CPU quota consumed by the index's online search. |
|PartitionBy |String |PartitionBy specifies the scalar field used to partition the data. Based on this field's values, the dataset is divided into sub\-datasets, and a separate sub\-index is built for each. This allows searches to target a specific sub\-index, which reduces filtering during hybrid retrieval and improves performance. |
|VectorIndex |VectorIndexParams |Vector index parameters. |
|ScalarIndex |List\ < string \> |Scalar index field list. |
|Stat |String |Index state. The value is as follows:<br><br><br>* INIT: The index is being initialized, built, or loaded.<br><br>* CHANGING: The index is being modified, rebuilt, or reloaded.<br><br>* READY: The index is active and can serve requests. |
|ShardCount |Int |The number of shards. |
|CreateTime |String |Index creation time. |
|UpdateTime |String |Index update time. |
|UpdatePerson |String |The user who last updated the index. |
|IndexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: index size in memory. |

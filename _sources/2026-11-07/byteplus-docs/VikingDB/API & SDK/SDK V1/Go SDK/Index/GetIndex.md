---
title: "GetIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_GetIndex"
---

<span id="a8a50b53"></span>
# Overview

This API reference provides the details you need to use the GetIndex method. You can call this method to retrieve the complete configuration, status, and resource consumption information for a specific index within a collection.

<span id="4508548b"></span>
# **Request Parameters**


|**parameter** |**Parameter Description** |**Is it required?**  |**parameter description** |
|---|---|---|---|
|collectionName |String |Yes |Specifies the name of the Collection to which you want to query the index.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Collection names must be unique. |
|indexName |String |Yes |Specify the name of the Index to query.<br><br><br>* The name must contain only English letters, numbers, and underscores (_), begin with an English letter, and not be empty.<br><br>* Length requirements: [1,128].<br><br>* Index names must be unique. |


<span id="c5f9220b"></span>
# Example

<span id="ca9523c4"></span>
## Request parameters

```Go
index, err := service.GetIndex("go", "goIndex")
if err != nil {
    fmt.Println(err)
}
```


<span id="0d2463b2"></span>
## Return value

This Go function call retrieves the index details and returns a pointer to an `Index` struct (`*Index`). The properties of the `Index` struct are listed in the following table.


|**attribute** |**type** |**Description** |
|---|---|---|
|Collection |String |The name of the collection that contains the index. |
|Index |String |Displays the index name. |
|Description |String |Displays a description of the index. |
|CpuQuota |Int |The CPU quota for searches performed on this index. |
|PartitionBy |String |The name of the scalar field used for partitioning the index. Partitioning divides the dataset into sub\-datasets based on the values of this field, and a separate sub\-index is built for each. This allows searches to target specific sub\-indexes, which reduces filtering and improves search performance. |
|VectorIndex |VectorIndexParams |Vector index parameter. |
|ScalarIndex |List\ < string \> |Scalar index field list. |
|Stat |String |Index state. The value is as follows:<br><br><br>* INIT: The index is being built or loaded.<br><br>* CHANGING: The index is being updated.<br><br>* READY: The index is ready to serve queries. |
|ShardCount |Int |The number of shards. |
|CreateTime |String |Index creation time. |
|UpdateTime |String |Index update time. |
|UpdatePerson |String |The user who last updated the index. |
|IndexCost |Map |* cpu_core: The number of CPU cores occupied by the index.<br><br>* mem_gb: The size of the index in memory (GB). |

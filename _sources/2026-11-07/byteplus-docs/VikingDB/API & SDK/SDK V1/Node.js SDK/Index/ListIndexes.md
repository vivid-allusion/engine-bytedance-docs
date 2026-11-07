---
title: "ListIndexes"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_ListIndexes"
---

<span id="d98de4c7"></span>
# Overview

To manage and monitor your indexes, you can use the `ListIndexes` operation to retrieve a detailed list of all indexes within a specific collection. The response includes the full configuration, status, and resource consumption for each index, providing a complete overview for administrative tasks.

<span id="ccea96bf"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Dataset name |


<span id="569dee9b"></span>
# Response parameters

```TypeScript
declare class ListIndexesResponse {
  readonly ListIndexes: IndexInfo[];
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    ListIndexes: IndexInfo[],
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="c37eb786"></span>
## IndexInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Dataset name |
|IndexName |`string` |Yes |Index name |
|CpuQuota |`number` |Yes |Index CPU usage |
|Description |`string` |No |Index description |
|ShardPolicy |`ShardPolicy` |Yes |Index sharding strategy |
|ShardCount |`number` |Yes |Number of index shards |
|PartitionBy |`string` |No |Subindex division field |
|Partitions |`string[]` |No |A list of sub\-indices. This field exists only when a partition field is configured. |
|VectorIndex |`VectorIndex` |No |Vector index configuration |
|ScalarIndex |`ScalarFieldInfo` |No |Scalar filter field |
|Stat |`IndexStatus` |Yes |Index state |
|IndexCost |`IndexCost` |Yes |Index resource usage |
|CreateTime |`string` |Yes |Index creation time |
|UpdateTime |`string` |Yes |Index update time |
|UpdatePerson |`string` |Yes |Last updated by |


<span id="bab10be1"></span>
### ShardPolicy

```TypeScript
enum ShardPolicy {
  Custom = "custom",
  Auto = "auto",
}
```


<span id="2f82a89a"></span>
### VectorIndex

```TypeScript
type VectorIndex = 
    | HnswVector
    | HnswHybridVector 
    | FlatVector 
    | DiskannVector 
    | IvfVector
    
type HnswVector = HnswVector1 | HnswVector2
type HnswHybridVector = HnswHybridVector1 | HnswHybridVector2
type FlatVector = FlatVector1 | FlatVector2
```


<span id="29f561a2"></span>
#### HnswVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |Hnsw index parameter, indicating the number of neighbor nodes |
|HnswCef |`number` |No |Hnsw index parameter that specifies the search breadth for neighbor nodes when building the graph |
|HnswSef |`number` |No |Hnsw index parameter that specifies the search breadth for online searches |


<span id="4ab996bd"></span>
#### HnswVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |Hnsw index parameter, indicating the number of neighbor nodes |
|HnswCef |`number` |No |Hnsw index parameter that specifies the search breadth for neighbor nodes when building the graph |
|HnswSef |`number` |No |Hnsw index parameter that specifies the search breadth for online searches |


<span id="b6a75de6"></span>
#### HnswHybridVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="8b1b9f52"></span>
#### HnswHybridVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="156d2df3"></span>
#### FlatVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="8eac2584"></span>
#### FlatVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="339e8245"></span>
#### DiskannVector


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Diskann` |Yes |Index type |
|Distance |`Distance` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Pq` |Yes |Quantization method |
|DiskannM |`number` |No |Diskann parameter, indicating the number of neighbors |
|DiskannCef |`number` |No |Diskann parameter that specifies the search breadth for neighbor nodes when building the graph |
|CacheRatio |`number` |No |Diskann parameter: The ratio of cache nodes to the original data source. |
|PqCodeRatio |`number` |No |Diskann parameter, size limit for vector dimension encoding |


<span id="4c6058d2"></span>
#### IvfVector


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Ivf` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Pq` |Yes |Quantization method |


<span id="c46d83cb"></span>
### ScalarFieldInfo scalar field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |The default value for the field. The type must match the specified FieldType. |


<span id="b56ac3d8"></span>
### IndexStatus

```TypeScript
type IndexStatus = "INIT" | "CHANGING" | "READY";
```


<span id="444bc07b"></span>
### IndexCost


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CpuCore |`number` |Yes |Number of CPU cores used |
|MemoryGb |`string` |Yes |Memory usage |


<span id="44565dc4"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

const response = await service.index.ListIndexes({ 
  CollectionName: 'test_collection_1', 
}) 

console.log(response.ListIndexes) // Output the list of indexes.
```

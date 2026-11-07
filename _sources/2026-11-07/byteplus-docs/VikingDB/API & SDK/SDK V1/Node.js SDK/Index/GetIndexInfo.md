---
title: "GetIndexInfo"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_GetIndexInfo"
---

<span id="8a91a1b8"></span>
# Overview

To retrieve comprehensive details for a specific index, you can call the `GetIndexInfo` API. This API returns the complete configuration and current state of an index, including its vector and scalar field definitions, sharding policy, resource consumption, and operational status.

<span id="de3cd0b8"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|IndexName |`string` |Yes |Index name |


<span id="2f8f1486"></span>
# Response parameters

```TypeScript
declare class GetIndexInfoResponse {
  readonly IndexInfo: IndexInfo;
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    IndexInfo: IndexInfo,
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="dc51fca7"></span>
## IndexInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|IndexName |`string` |Yes |Index name |
|CpuQuota |`number` |Yes |Index CPU usage |
|Description |`string` |No |Index description |
|ShardPolicy |`ShardPolicy` |Yes |Index sharding strategy |
|ShardCount |`number` |Yes |Number of index shards |
|PartitionBy |`string` |No |Partition field |
|Partitions |`string[]` |No |A list of partitions. This field is present only if a partition field is configured. |
|VectorIndex |`VectorIndex` |No |Vector index configuration |
|ScalarIndex |`ScalarFieldInfo` |No |Scalar filter field |
|Stat |`IndexStatus` |Yes |Index status |
|IndexCost |`IndexCost` |Yes |Index resource usage |
|CreateTime |`string` |Yes |Index creation time |
|UpdateTime |`string` |Yes |Index update time |
|UpdatePerson |`string` |Yes |The user who last updated the index |


<span id="33499815"></span>
### ShardPolicy

```TypeScript
enum ShardPolicy {
  Custom = "custom",
  Auto = "auto",
}
```


<span id="8d2508c4"></span>
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


<span id="be1e6f5b"></span>
#### HnswVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |An HNSW parameter that specifies the number of neighboring nodes |
|HnswCef |`number` |No |An HNSW parameter that specifies the search breadth for neighboring nodes when building the graph |
|HnswSef |`number` |No |An HNSW parameter that specifies the search breadth for online searches |


<span id="4487c444"></span>
#### HnswVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |An HNSW parameter that specifies the number of neighboring nodes |
|HnswCef |`number` |No |An HNSW parameter that specifies the search breadth for neighboring nodes when building the graph |
|HnswSef |`number` |No |An HNSW parameter that specifies the search breadth for online searches |


<span id="e608dc38"></span>
#### HnswHybridVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="133be85c"></span>
#### HnswHybridVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="89ead6cd"></span>
#### FlatVector1


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="a5c03e53"></span>
#### FlatVector2


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="b6947f76"></span>
#### DiskannVector


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Diskann` |Yes |Index type |
|Distance |`Distance` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Pq` |Yes |Quantization method |
|DiskannM |`number` |No |A Diskann parameter that specifies the number of neighbors |
|DiskannCef |`number` |No |A Diskann parameter that specifies the search breadth for neighboring nodes when building the graph |
|CacheRatio |`number` |No |A Diskann parameter that specifies the ratio of cached nodes to the original data source |
|PqCodeRatio |`number` |No |A Diskann parameter that specifies the size limit for vector dimension encoding |


<span id="655942ef"></span>
#### IvfVector


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|IndexType |`IndexType.Ivf` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Pq` |Yes |Quantization method |


<span id="e76ba871"></span>
### ScalarFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |The default value for the field. The type must match the `FieldType` parameter. |


<span id="d2ea3ec0"></span>
### IndexStatus

```TypeScript
type IndexStatus = "INIT" | "CHANGING" | "READY";
```


<span id="58063ff5"></span>
### IndexCost


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CpuCore |`number` |Yes |Number of CPU cores |
|MemoryGb |`string` |Yes |Memory usage (GB) |


<span id="f2e19877"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

const response = await service.index.GetIndexInfo({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
}) 

console.log(response.IndexInfo) // Output the index details.
```

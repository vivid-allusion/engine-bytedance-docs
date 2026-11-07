---
title: "CreateIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_CreateIndex"
---

<span id="f701c8c2"></span>
# Overview

The `CreateIndex` API creates a vector index for a specified collection, which is essential for accelerating vector similarity searches. This document provides the request parameters, data types, and code examples you need to configure various index types, such as HNSW, IVF, and DiskANN, to optimize search performance and accuracy.

Indexing can accelerate vector similarity search. An index groups and sorts vectors according to a specified algorithm and data structure. This process improves the efficiency and accuracy of similarity searches, allowing the vector database to quickly filter candidates.

An index on a dataset with only dense vectors (Vector type fields) is called a pure dense index. An index on a dataset with both dense (Vector) and sparse vectors (Sparse_Vector type fields) is called a mixed index.

<span id="73cb50c5"></span>
# Request parameters


|**field name** |**type** |**Required?**  |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|IndexName |`string` |Yes |Index name |
|Description |`string` |No |Index description |
|CpuQuota |`number` |No |Index CPU usage |
|ShardConfig |`ShardConfig` |Yes |Index sharding configuration |
|VectorIndex |`VectorIndex` |No |Vector index configuration |
|PartitionBy |`string` |No |Field for partitioning the index |
|ScalarIndexes |`string[]` |No |Scalar fields to index for filtering |


<span id="017657e9"></span>
## ShardConfig

```TypeScript
type ShardConfig =
  | {
      ShardPolicy: ShardPolicy.Custom;
      ShardCount: number;
    }
  | {
      ShardPolicy: ShardPolicy.Auto;
    };
```


<span id="92857139"></span>
## IndexType

```TypeScript
enum IndexType {
  Hnsw = "hnsw",
  HnswHybrid = "hnsw_hybrid",
  Flat = "flat",
  Ivf = "ivf",
  Diskann = "diskann",
}
```


<span id="4538b9ba"></span>
## Distance

```TypeScript
enum Distance {
  Ip = "ip",
  l2 = "l2",
  Cosine = "cosine",
}
```


<span id="ee9de4ef"></span>
## Quant

```TypeScript
enum Quant {
  Int8 = "int8",
  Float = "float",
  Fix16 = "fix16",
  PQ = "pq",
}
```


<span id="e27e532e"></span>
## VectorIndex

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


<span id="371ec190"></span>
### HnswVector1


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |HNSW parameter that indicates the number of neighbor nodes |
|HnswCef |`number` |No |HNSW parameter that represents the search breadth for neighbor nodes when building the graph |
|HnswSef |`number` |No |HNSW parameter that indicates the search breadth for online searches |


<span id="b5e61fa4"></span>
### HnswVector2


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Hnsw` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |
|HnswM |`number` |No |HNSW parameter that indicates the number of neighbor nodes |
|HnswCef |`number` |No |HNSW parameter that represents the search breadth for neighbor nodes when building the graph |
|HnswSef |`number` |No |HNSW parameter that indicates the search breadth for online searches |


<span id="8b192ef8"></span>
### HnswHybridVector1


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="fdce1283"></span>
### HnswHybridVector2


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.HnswHybrid` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="df6a813e"></span>
### FlatVector1


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Int8`<br><br>`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="3350f134"></span>
### FlatVector2


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Flat` |Yes |Index type |
|Distance |`Distance.l2` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Fix16` |Yes |Quantization method |


<span id="e5768395"></span>
### DiskannVector


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Diskann` |Yes |Index type |
|Distance |`Distance` |Yes |Distance type |
|Quant |`Quant.Float`<br><br>`Quant.Pq` |Yes |Quantization method |
|DiskannM |`number` |No |Diskann parameter that indicates the number of neighbors |
|DiskannCef |`number` |No |Diskann parameter that represents the search breadth for neighbor nodes when building the graph |
|CacheRatio |`number` |No |Diskann parameter, The ratio of cached nodes to the total number of vectors in the data source |
|PqCodeRatio |`number` |No |Diskann parameter that specifies the size limit for vector dimension encoding |


<span id="abe7155e"></span>
### IvfVector


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|IndexType |`IndexType.Ivf` |Yes |Index type |
|Distance |`Distance.Ip`<br><br>`Distance.Cosine` |Yes |Distance type |
|Quant |`Quant.Pq` |Yes |Quantization method |


<span id="742491ed"></span>
# Response parameters

```TypeScript
declare class VikingdbResponse {
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="55cf4744"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace with the initialized service instance. 

await service.index.CreateIndex({
  CollectionName: 'test_collection_1',
  IndexName: 'test_index_1',
  Description: 'Index Description', // optional
  CpuQuota: 2, // optional
  ShardConfig: {
    ShardPolicy: vikingdb.index.ShardPolicy.Custom,
    ShardCount: 10
  }, // Custom sharding
  ShardConfig: {
    ShardPolicy: vikingdb.index.ShardPolicy.Auto,
  }, // Auto sharding
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Hnsw,
    Distance: vikingdb.index.Distance.Ip,
    Quant: vikingdb.index.Quant.Int8,
    HnswM: 10, // optional
    HnswCef: 10, // optional
    HnswSef: 10, // optional
  }, // optional, HnswVector1
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Hnsw,
    Distance: vikingdb.index.Distance.l2,
    Quant: vikingdb.index.Quant.Float,
    HnswM: 10, // optional
    HnswCef: 10, // optional
    HnswSef: 10, // optional
  }, // optional, HnswVector2
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.HnswHybrid,
    Distance: vikingdb.index.Distance.Cosine,
    Quant: vikingdb.index.Quant.Int8,
  }, // optional, HnswHybridVector1
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.HnswHybrid,
    Distance: vikingdb.index.Distance.L2,
    Quant: vikingdb.index.Quant.Float,
  }, // optional, HnswHybridVector2  
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Flat,
    Distance: vikingdb.index.Distance.Ip,
    Quant: vikingdb.index.Quant.Int8,
  }, // optional, FlatVector1    
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Flat,
    Distance: vikingdb.index.Distance.l2,
    Quant: vikingdb.index.Quant.Float,
  }, // optional, FlatVector2
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Diskann,
    Distance: vikingdb.index.Distance.Ip,
    Quant: vikingdb.index.Quant.Pq,
    DiskannM: 10, // optional
    DiskannCef: 10, // optional
    CacheRatio: 10, // optional
    PqCodeRatio: 10, //optional
  }, // optional, DiskannVector  
  VectorIndex: {
    IndexType: vikingdb.index.IndexType.Ivf,
    Distance: vikingdb.index.Distance.Ip,
    Quant: vikingdb.index.Quant.Pq,
  }, // optional, IvfVector  
  PartitionBy: 'Id', // optional
  Scalarindexes: ['Name'], // optinal
})
```

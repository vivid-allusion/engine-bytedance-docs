---
title: "UpdateIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_UpdateIndex"
---

<span id="f0a55001"></span>
# Overview

The UpdateIndex interface allows you to modify the configuration of an existing index. You can use this interface to update properties such as the index description, CPU quota, sharding configuration, and scalar filter fields.

<span id="adcc959f"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Dataset name |
|IndexName |`string` |Yes |Index name |
|Description |`string` |No |Index description |
|CpuQuota |`number` |No |Index CPU usage |
|ShardConfig |`ShardConfig` |No |Index sharding configuration |
|ScalarIndexes |`string[]` |No |Scalar filter field<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently only scalar filter fields are allowed</div><br> |


<span id="14e08f06"></span>
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


<span id="52ebbf66"></span>
## Response parameters

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


<span id="387bc231"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.index.UpdateIndex({
  CollectionName: 'test_collection_1',
  IndexName: 'test_index_1',
  Description: 'Index Description', // optional
  CpuQuota: 2, // optional
  ShardConfig: {
    ShardPolicy: vikingdb.index.ShardPolicy.Custom,
    ShardCount: 10
  }, // optional, custom sharding
  ShardConfig: {
    ShardPolicy: vikingdb.index.ShardPolicy.Auto,
  }, // optional, auto sharding
  Scalarindexes: ['Name'], // optional
})
```

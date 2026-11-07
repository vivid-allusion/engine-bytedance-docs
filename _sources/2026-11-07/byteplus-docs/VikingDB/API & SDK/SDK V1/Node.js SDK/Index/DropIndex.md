---
title: "DropIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_DropIndex"
---

<span id="a9f8183c"></span>
# Overview

The DropIndex operation deletes a specified index from a specified collection.

<span id="578aaf49"></span>
# Request parameters


|**field name** |**type** |**Required** |**explain** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|IndexName |`string` |Yes |Index name |


<span id="a95f1299"></span>
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


<span id="c321b1a6"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.index.DropIndex({
  CollectionName: 'test_collection_1',
  IndexName: 'test_index_1',
})
```

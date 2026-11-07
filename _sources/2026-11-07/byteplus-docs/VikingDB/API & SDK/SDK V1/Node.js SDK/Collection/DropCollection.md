---
title: "DropCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_DropCollection"
---

<span id="171cda29"></span>
# Overview

The DropCollection API is used to permanently delete a dataset Collection. Before calling this API, you must ensure that all associated indexes have been deleted. Please be aware that this operation is irreversible and will result in the complete loss of all data within the specified Collection.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting a collection permanently removes all data in the specified collection. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">To delete a collection, you must first delete all of its associated indexes.</div>



<span id="80b007fb"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The name or alias of the dataset. You must specify one. |


<span id="42a6f80a"></span>
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


<span id="c89e2d15"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.collection.DropCollection({
  CollectionName: 'test_collection_1',
})
```

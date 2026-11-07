---
title: "DeleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_DeleteData"
---

<span id="d38a2a6e"></span>
# Overview

The DeleteData operation deletes data from a specified collection. You can delete single or multiple data entries by primary key, up to a maximum of 100 entries at a time.

<span id="279189b2"></span>
# Request parameters

```TypeScript
type DeleteDataRequest = 
  | DeleteSpecifyDataRequest
  | DeleteAllDataRequest
```


<span id="e7d8d195"></span>
## DeleteSpecifyDataRequest Delete specified data


|**field name** |**type** |**Required?**  |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The name or alias of the collection. You must specify one. |
|PrimaryKeys |`Array` |Yes |The primary key values. The type of each value must match the type defined for the primary key field. |


<span id="8413e541"></span>
## DeleteAllDataRequest Delete all data


|**field name** |**type** |**Required?**  |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The name or alias of the collection. You must specify one. |
|DeleteAll |`true` |Yes |Delete all |


<span id="02949786"></span>
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


<span id="653bf3c4"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.data.DeleteData({
  CollectionName: 'test_collection_1',
  PrimaryKeys: [1, 2]
})

await service.data.DeleteData({
  CollectionAlias: 'test_collection_alias_1',
  DeleteAll: true
})
```

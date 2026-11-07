---
title: "UpsertData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_UpsertData"
---

<span id="dc39babe"></span>
# Overview

UpsertData is used to write data in the specified dataset Collection. The data must be provided as an array, allowing you to insert one or more records at a time, up to a maximum of 100 per call.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Updating some fields is not currently supported. All fields must be updated every time data is written. If a record with the same primary key already exists in the Collection, the existing record is overwritten. Otherwise, a new record is created.</div>


<span id="9ab02c81"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The dataset name or alias. You must specify one. |
|Fields |`Record[]` |Yes |An array of records, where each record is a map. |
|TTL |`number` |No |Expiration time |
|async_upsert |`bool` |No |Specifies whether the request is asynchronous. Asynchronous mode is suitable for large\-scale data writing and can improve performance by up to 10x.<br><br><br>* True: The request is asynchronous.<br><br>* Default: False, indicating a synchronous request. |


<span id="427283cc"></span>
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


<span id="91a9b4a1"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.data.UpsertData({
  CollectionName: 'test_collection_1', 
  Fields: [
    { Id: 1, Name: 'Tom' },
    { Id: 2, Name: 'Jerry' },
  ],
})
```

---
title: "FetchIndexData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_FetchIndexData"
---

<span id="c1f2f13e"></span>
# Overview

Use FetchIndexData to query index data. Use primary key IDs to query one or more data records in the specified Index. You can query up to 100 records at a time.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Index data takes the longest to update after collection data is written/deletedlag 20S, not immediately found in Index.</div>


<span id="78c5cac5"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The name or alias of the collection. |
|PrimaryKeys |`Array` |Yes |An array of primary key values. The type of these values must match the type of the primary key field. |
|Partition |`string \| number` |No |The partition to query. The type of this value must match the type of the partition key field. |
|OutputFields |`string[]` |No |Output fields |


<span id="6b094d45"></span>
# Response parameters

```TypeScript
declare class FetchIndexDataResponse<
  Data extends Record<string, any>,
  PrimaryKey extends GetPrimaryKeys<Data>
> {
  readonly Data: FetchDataInfo<Data, PrimaryKey>[];
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    Data: FetchDataInfo[],
    OriginalRequest: string,
    LogId: string
  );
}
```


```TypeScript
type GetPrimaryKeysextends Record<string, any>> = {
  [K in keyof T]: IsPrimaryKey extends true ? K : never;
}[keyof T];

type FetchDataInfo<
  Data extends Record<string, any>,
  PrimaryKey extends GetPrimaryKeys<Data>
> = Data | { [Key in PrimaryKey]: ScalarFieldType2JsType[Data[PrimaryKey]] };
```


```TypeScript
type IsNever = [T] extends [never] ? true : false;

type IsUnion = IsNever extends true
  ? false
  : T extends B
  ? [B] extends [T]
    ? false
    : true
  : never;
  
enum FieldType {
  Int64 = "int64",
  Float32 = "float32",
  String = "string",
  Boolean = "bool",
  ListString = "list",
  ListInt64 = "list",
/** Dense vector */
  DenseVector = "vector",
/** Sparse vector */
  SparseVector = "sparse_vector",
  Text = "text",
}  
  
interface ScalarFieldType2JsType {
  [FieldType.Int64]: number;
  [FieldType.Float32]: number;
  [FieldType.String]: string;
  [FieldType.Boolean]: boolean;
  [FieldType.ListString]: string[];
  [FieldType.ListInt64]: Array<number>;
}
  
type IsPrimaryKey<
  Data extends Record<string, any>,
  PrimaryKey extends keyof Data
> = IsUnion<PrimaryKey> extends true
  ? false
  : Data[PrimaryKey] extends ScalarFieldType2JsType[PrimaryKeyFieldType]
  ? true
  : false;
```


<span id="efe7f8c2"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

interface Data { 
  Id: number, 
  Name: string 
} 

const response = await service.data.FetchIndexData<Data, 'Id'>({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
  PrimaryKeys: [1, 2], 
  Partition: 3, // optional 
  OutputFields: ['Id', 'Name'], // optional 
}) 

console.log(response.Data) // Output the data queried from the index.
```

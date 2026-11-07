---
title: "FetchCollectionData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_FetchCollectionData"
---

<span id="b2691958"></span>
# Overview

The FetchCollectionData API allows you to query one or more data items from a specified Collection using their primary keys. You can retrieve up to 100 records in a single request

and data is available for query in real\-time immediately after being written or deleted

<span id="099e9735"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The collection name or alias. You must specify one. |
|PrimaryKeys |`Array` |Yes |An array of primary key values. The type of each value must match the type of the collection's primary key field. |


<span id="19ac1a38"></span>
# Response parameters

```TypeScript
declare class FetchCollectionDataResponse<
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


<span id="561bc99a"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

interface Data {
  Id: number,
  Name: string
}

const response = await service.data.FetchCollectionData<Data, 'Id'>({
  CollectionName: 'test_collection_1',
  PrimaryKeys: [1, 2]
})

console.log(response.Data)
```

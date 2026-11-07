---
title: "ListCollections"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_ListCollections"
---

<span id="2f0b1a03"></span>
# Overview

The ListCollections method retrieves a list of all collections within your instance. This document details the method's usage, the complete response structure including the `CollectionInfo` object, and provides a code example to help you integrate this functionality into your application.

<span id="e9242667"></span>
# Request parameters

None

<span id="56460b47"></span>
# Response parameters

```TypeScript
declare class ListCollectionsResponse {
  readonly ListCollections: CollectionInfo[];
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    ListCollections: CollectionInfo[],
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="4c6eeea5"></span>
## CollectionInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|Description |`string` |No |Collection description |
|CollectionAliases |`string[]` |No |List of collection aliases |
|Fields |`FieldInfo[]` |Yes |Collection fields |
|Stat |`Stat` |Yes |Collection status |
|IndexNames |`string[]` |Yes |List of index names in the collection |
|IndexNumber |`number` |Yes |Number of indexes in the collection |
|CreateTime |`string` |Yes |Collection creation time |
|UpdateTime |`string` |Yes |Collection update time |
|UpdatePerson |`string` |Yes |Last updated by |


<span id="c10e413e"></span>
### FieldInfo

```TypeScript
type FieldInfo =
  | ScalarFieldInfo
  | PrimaryKeyFieldInfo
  | DenseVectorFieldInfo
  | SparseVectorFieldInfo
  | TextFieldInfo
  
enum FieldType {
  Int64 = "int64",
  Float32 = "float32",
  String = "string",
  Boolean = "bool",
  ListString = "list",
  ListInt64 = "list",
  
  DenseVector = "vector",
 
  SparseVector = "sparse_vector",
  Text = "text",
}

type PipelineName =
  | "text_split_bge_large_zh"
  | "text_bge_large_zh"
  | "text_split_bge_m3"
  | "text_bge_m3"
  | "text_split_bge_large_and_m3"
  | "text_bge_large_and_m3"
```


<span id="04ffe67b"></span>
#### ScalarFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |Field default value. The type must match the specified FieldType. |


<span id="8335f458"></span>
#### PrimaryKeyFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.String` |Yes |Field type |
|IsPrimary |`true` |Yes |Indicates if this is the primary key. This value must be  true. |


<span id="daf237be"></span>
#### DenseVectorFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.DenseVector` |Yes |Field type |
|Dim |`number` |Yes |Vector dimension, must be a multiple of 4 |


<span id="07255c40"></span>
#### SparseVectorFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.SparseVector` |Yes |Field type |


<span id="28489bbd"></span>
#### TextFieldInfo


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Text` |Yes |Field type |
|PipelineName |`string` |No |The name of the associated pipeline |


<span id="e5224672"></span>
### Stat


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|DataNumber |`number` |Yes |Number of data entries |


<span id="685686ac"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService // Replace with your initialized service instance

const response = await service.collection.ListCollections()
  
console.log(response.ListCollections) // 数据集
```

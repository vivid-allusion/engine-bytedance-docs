---
title: "UpdateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_UpdateCollection"
---

<span id="9f59df4d"></span>
# Overview

The UpdateCollection API is used to modify an existing collection's schema and metadata. You can use this operation to add new fields, update the collection's description, or change its aliases.

Please note that this operation only supports adding new fields; modifying existing fields is not allowed.

<span id="a581b4c7"></span>
# **request parameters**


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|Description |`string` |No |Collection description |
|CollectionAliases |`string[]` |No |Collection alias list |
|Fields |`FieldInfo[]` |Yes |Collection field<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently only incremental updates are supported</div><br><br><br><div data-tips="true" data-tips-type="warning">Adding DenseVectorField, SparseVectorField and TextField with PipelineName is not supported</div><br> |


<span id="54b01177"></span>
## FieldInfo

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


<span id="dc3c0552"></span>
### Scalar field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |The type must match the specified FieldType. |


<span id="fc410aec"></span>
### Primary key field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.String` |Yes |Field type |
|IsPrimary |`true` |Yes |Specifies if this is the primary key. This must be set to true.`true` |


<span id="37f0befe"></span>
### Dense vector field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.DenseVector` |Yes |Field type |
|Dim |`number` |Yes |Vector dimension, requires a multiple of 4 |


<span id="6207c746"></span>
### Sparse vector field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.SparseVector` |Yes |Field type |


<span id="5a0bc93e"></span>
### Text field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Text` |Yes |Field type |
|PipelineName |`string` |No |Associated pipeline name |


<span id="cdf1918f"></span>
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


<span id="00034464"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

await service.collection.UpdateCollection({ 
  CollectionName: 'test_collection_1', 
  Description: 'collection_description', // optional 
  CollectionAliases: ['collection_alias_1', 'collection_alias_2'], // optional 
  Fields: [ 
    { FieldName: 'Id', FieldType: vikingdb.FieldType.Int64, IsPrimary: true }, // primary key 
    { FieldName: 'Name', FieldType: vikingdb.FieldType.String, DefaultValue: 'Hello world'/* optional */ }, // scalar field 
    { FieldName: 'DenseVector', FieldType: vikingdb.FieldType.DenseVector, Dim: 4 }, // dense vector field 
    { FieldName: 'SparseVector', FieldType: vikingdb.FieldType.SparseVector }, // sparse vector field 
    { FieldName: 'Text', FieldType: vikingdb.FieldType.Text, PipelineName: 'text_bge_m3', /* optional */ }, // text field 
  ] // When adding new fields, you must also include all existing fields in the request. 
})
```

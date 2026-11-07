---
title: "CreateCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_CreateCollection"
---

<span id="0e37f382"></span>
# Overview

The CreateCollection API creates a new data collection and defines its schema. You can use this API to configure various fields, such as primary keys, scalar types, and dense or sparse vectors, which prepares the collection for subsequent data ingestion.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Each collection must have a primary key field. After adding a vector field to the <code>Fields</code> array, you cannot add another one, as a collection only supports a single vector field.</div>


* <div data-tips="true" data-tips-type="tip">If you add a <code>Text</code> field with a <code>PipelineName</code>, you cannot also add a <code>Vector</code> field, and only one such <code>Text</code> field is permitted. If you add <code>Text</code> fields without a <code>PipelineName</code>, a <code>Vector</code> field is allowed, and you can add up to 200 of these <code>Text</code> fields.</div>



<span id="240e877f"></span>
# **Request parameters**


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName |`string` |Yes |Data set name |
|Description |`string` |No |Data set description |
|CollectionAliases |`string[]` |No |Dataset alias list |
|Fields |`FieldInfo[]` |Yes |Data set field |


<span id="8f8ae7d7"></span>
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
  /** Dense Vector */
  DenseVector = "vector",
  /** Sparse Vector */
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


<span id="9a912a4b"></span>
### Scalar field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |Field default value. The type must match the specified `FieldType`. |


<span id="e3f33922"></span>
### Primary key field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.String` |Yes |Field type |
|IsPrimary |`true` |Yes |Set to `true` to designate this field as the primary key. If no field is designated as the primary key, one is generated automatically. |


<span id="8888f649"></span>
### Dense vector field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.DenseVector` |Yes |Field type |
|Dim |`number` |Yes |The vector dimension. Must be a multiple of 4. |


<span id="386c404b"></span>
### Sparse vector field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.SparseVector` |Yes |Field type |


<span id="11003851"></span>
### Text field


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Text` |Yes |Field type |
|PipelineName |`string` |No |The name of the pipeline to bind to this field. |


<span id="98d81aa1"></span>
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


<span id="5abcc565"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi'

declare const service: vikingdb.VikingdbService 

await service.collection.CreateCollection({
  CollectionName: 'test_collection_1',
  Description: 'collection_description', // optional
  CollectionAliases: ['collection_alias_1', 'collection_alias_2'], // optional
  Fields: [
    { FieldName: 'Id', FieldType: vikingdb.FieldType.Int64, IsPrimary: true }, 
    { FieldName: 'Name', FieldType: vikingdb.FieldType.String, DefaultValue: 'Hello world'/* optional */ }, 
    { FieldName: 'DenseVector', FieldType: vikingdb.FieldType.DenseVector, Dim: 4 }, 
    { FieldName: 'SparseVector', FieldType: vikingdb.FieldType.SparseVector }, 
    { FieldName: 'Text', FieldType: vikingdb.FieldType.Text, PipelineName: 'text_bge_m3', /* optional */ }, 
  ]
})
```

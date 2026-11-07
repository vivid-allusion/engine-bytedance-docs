---
title: "GetCollectionInfo"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_GetCollectionInfo"
---

<span id="cad82c3b"></span>
# Overview

To retrieve detailed information about a specific collection, you can use the GetCollectionInfo API. This API returns comprehensive data, including the collection's structure, field definitions, associated indexes, and current status.

<span id="93c2efaa"></span>
# Request parameters


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The collection name or alias. You must provide one. |


<span id="0633bae5"></span>
# Response parameters

```TypeScript
declare class ListCollectionsResponse {
  readonly CollectionInfo: CollectionInfo;
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    CollectionInfo: CollectionInfo,
    OriginalRequest: string,
    LogId: string
  );
}
```


<span id="8771b635"></span>
## CollectionInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|CollectionName |`string` |Yes |Collection name |
|Description |`string` |No |Collection description |
|CollectionAliases |`string[]` |No |A list of collection aliases. |
|Fields |`FieldInfo[]` |Yes |Collection fields |
|Stat |`Stat` |Yes |Collection status |
|IndexNames |`string[]` |Yes |A list of index names within the collection. |
|IndexNumber |`number` |Yes |The number of indexes in the collection. |
|CreateTime |`string` |Yes |The creation time of the collection. |
|UpdateTime |`string` |Yes |The last update time of the collection. |
|UpdatePerson |`string` |Yes |The user who last updated the collection. |


<span id="e67c9369"></span>
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


<span id="bd7b1548"></span>
#### ScalarFieldInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.Float32`<br><br>`FieldType.String`<br><br>`FieldType.Boolean`<br><br>`FieldType.ListString`<br><br>`FieldType.ListInt64` |Yes |Field type |
|DefaultValue |`number`<br><br>`string`<br><br>`boolean`<br><br>`string[]`<br><br>`number[]` |No |The default value for the field. The type must match the specified FieldType. |


<span id="a1cc3604"></span>
#### PrimaryKeyFieldInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Int64`<br><br>`FieldType.String` |Yes |Field type |
|IsPrimary |`true` |Yes |Specifies whether the field is the primary key. The value must be true. |


<span id="a2ba2fbb"></span>
#### DenseVectorFieldInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.DenseVector` |Yes |Field type |
|Dim |`number` |Yes |The dimension of the vector, which must be a multiple of 4. |


<span id="2b218244"></span>
#### SparseVectorFieldInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.SparseVector` |Yes |Field type |


<span id="c942963b"></span>
#### TextFieldInfo


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|FieldName |`string` |Yes |Field name |
|FieldType |`FieldType.Text` |Yes |Field type |
|PipelineName |`string` |No |The name of the bound pipeline. |


<span id="28c616dd"></span>
### Stat


|**field name** |**type** |**Required?**  |**explain** |
|---|---|---|---|
|DataNumber |`number` |Yes |The number of data entries. |


<span id="a4907458"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

const response = await service.collection.GetCollectionInfo({ 
  CollectionName: 'test_collection_1', 
}) 

console.log(response.CollectionInfo) // Output the collection details.
```

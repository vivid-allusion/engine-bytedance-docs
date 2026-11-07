---
title: "SearchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_SearchByVector"
---

<span id="26922d4a"></span>
# Overview

The SearchByVector API retrieves the most similar vectors from a collection based on your query vector. It supports both pure vector searches for similarity and hybrid searches that combine vector matching with scalar filtering for more precise, targeted results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After data is written or deleted, there is a lag of up to 20 seconds for the index to update, so changes might not be immediately reflected in search results.</div>


* <div data-tips="true" data-tips-type="tip">If the filter request parameter is configured, the operation performs a mixed search; otherwise, it performs a pure vector search.</div>



<span id="998e479a"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The collection name or alias. You must provide one of them. |
|IndexName |`string` |Yes |Index name |
|Limit |`number` |Yes |The number of results to return. |
|DenseWeight |`number` |No |The weight for dense vectors. This parameter is only valid for mixed indexes (such as hnsw_hybrid). |
|OutputFields |`string[]` |No |The data fields to return. |
|Partition |`string \| number` |No |The name of the partition. The data type of the name must match the partition key's type. |
|Filter |`Filter` |No |Scalar Filtering |
|DenseVectors |`number[][]` |Yes |The dense query vectors. |
|SparseVectors |`Record[]` |No |The sparse query vectors. |


<span id="fbd62b07"></span>
## Filter

```TypeScript
type Filter =
  | MustTypeCondition
  | NumberRangeTypeCondition
  | AreaRangeTypeCondition
  | LogicTypeCondition;
  
enum SearchOperation {
  Must = "must",
  MustNot = "must_not",
  Range = "range",
  RangeOut = "range_out",
  And = "and",
  Or = "or",
}
```


<span id="a0e22474"></span>
### MustTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Must`<br><br>`SearchOperation.MustNot` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|Conditions |`Array` |Yes |The values to match. |


<span id="e48ad025"></span>
### NumberRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOpeartion.RangeOut` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|GreatThen |`number` |No |Greater than |
|LessThen |`number` |No |Less than |
|GreatThenEqual |`number` |No |Greater than or equal to |
|LessThenEqual |`number` |No |Less than or equal to |


<span id="6b3efd8e"></span>
### AreaRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOpeartion.RangeOut` |Yes |Operator |
|FieldNames |`[string, string]` |Yes |The names of the fields for the x and y coordinates. |
|Center |`[number, number]` |Yes |The x and y coordinates of the center point. |
|Radius |`number` |Yes |Radius |


<span id="96ea4874"></span>
### LogicTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.And`<br><br>`SearchOperation.Or` |Yes |Operator |
|Conditions |`Filter[]` |Yes |Subfilter condition |


<span id="0672e816"></span>
# Response parameters

```TypeScript
declare class SearchResponse<Data extends Record<string, any>> {
  readonly Data: SearchData<Data>[][];
  readonly OriginalRequest: string;
  readonly LogId: string;
  constructor(
    Data: SearchData[][],
    OriginalRequest: string,
    LogId: string
  );
}
```


```TypeScript
/** 
 * `score` indicates the ranking of the search result. 
 * 
 * `fields` contains the key-value pairs of the row of data. 
 * 
Other internal fields, such as the primary key field, may also be returned. The key for such a field is its defined name.
 * - the primary key field, where key indicates the defined field name. 
 */ 
interface SearchData<Data extends Record<string, unknown>> { 
  Score: number; 
  Fields?: Data; 
  [key: string]: unknown; 
}
```


<span id="a6c9f372"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

interface Data { 
  Id: number, 
  Name: string 
} 

const response = await service.search.SearchByVector<Data>({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
  DenseVectors: [[1, 2, 3, 4], [2, 3, 4, 5]], 
  SparseVectors: [{ 1: 1, 2: 2, 3: 3, 4: 4}, {2: 2, 3: 3, 4: 4, 5: 5}] // optional 
  Limit: 10, 
  DenseWeight: 0.5, // optional 
  OutputFields: ['Id', 'Name'], // optional 
  Partition: "default", // optional 
  Filter: { 
    Operation: vikingdb.search.SearchOperation.And, 
    Conditions: [ 
      { FieldName: 'Name', Operation: vikingdb.search.SearchOpeartion.Must, Conditions: ['Tom'] }, 
      { FieldName: 'Id', Opeartion: vikingdb.search.SearchOpeartion.Range, GreatThen: 10 } 
    ] 
  }, // optional 
}) 

console.log(response.Data) // Output the retrieved data.
```

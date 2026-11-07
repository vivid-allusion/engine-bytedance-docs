---
title: "SearchByScalar"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_SearchByScalar"
---

<span id="80d4199b"></span>
# Overview

To retrieve data from a vector database by filtering on specific scalar field values, you can use the /index/search API. This document provides a complete reference, including all request parameters, response structures, and a TypeScript code example for implementing scalar retrieval.

Scalar retrieval in vector databases refers to a retrieval method based on scalar values. In vector databases, each vector has one or more associated scalar values. You can perform scalar retrieval by querying these values to find relevant data, such as retrieving documents by author.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After collection data is written or deleted, there is a lag of up to 20 seconds before the index is updated. Therefore, new or deleted data may not be reflected in search results immediately.</div>


<span id="aad39022"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |The name or alias of the collection. |
|IndexName |`string` |Yes |Index name |
|Limit |`number` |Yes |The number of results to return. |
|OutputFields |`string[]` |No |The data fields to return. |
|Partition |`string \| number` |No |The name of the partition. The value's type must match the partition key's type. |
|Filter |`Filter` |No |The scalar filter conditions. |
|ScalarConfig |`ScalarConfig` |No |Scalar configuration |


<span id="58805e79"></span>
## ScalarConfig


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Order |`asc \| desc` |Yes |The sort order. |
|FieldName |String |Yes |The field to sort by. The values in this field must be sortable. |


<span id="3c57e3f0"></span>
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


<span id="463509e4"></span>
### MustTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Must`<br><br>`SearchOperation.MustNot` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|Conditions |`Array` |Yes |The values to match. |


<span id="44905c71"></span>
### NumberRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOperation.RangeOut` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|GreatThen |`number` |No |Greater than |
|LessThen |`number` |No |Less than |
|GreatThenEqual |`number` |No |Greater than or equal to |
|LessThenEqual |`number` |No |Less than or equal to |


<span id="e0f6b236"></span>
### AreaRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOperation.RangeOut` |Yes |Operator |
|FieldNames |`[string, string]` |Yes |The names of the fields for the X and Y coordinates. |
|Center |`[number, number]` |Yes |The X and Y coordinates of the center point. |
|Radius |`number` |Yes |Radius |


<span id="d7a08a6f"></span>
### LogicTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.And`<br><br>`SearchOperation.Or` |Yes |Operator |
|Conditions |`Filter[]` |Yes |The sub\-filter conditions. |


<span id="e360fc68"></span>
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
Other internal fields may also exist, such as the primary key field. The key for this field will be its defined field name.
 * - the primary key field, where key indicates the defined field name. 
 */ 
interface SearchData<Data extends Record<string, unknown>> { 
  Score: number; 
  Fields?: Data; 
  [key: string]: unknown; 
}
```


<span id="f457246c"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

interface Data { 
  Id: number, 
  Name: string 
} 

const response = await service.search.SearchByScalar<Data>({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
  ScalarConfig: { 
    FieldName: 'Id', 
    Order: 'asc', 
  }, // optional 
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

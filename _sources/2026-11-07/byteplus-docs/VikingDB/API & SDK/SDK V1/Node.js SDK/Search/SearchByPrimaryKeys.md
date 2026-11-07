---
title: "SearchByPrimaryKeys"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_SearchByPrimaryKeys"
---

<span id="f6bf69f2"></span>
# Overview

To find data vectors similar to specific items identified by their primary keys, use the SearchByPrimaryKeys function. This function takes a list of primary keys and returns a specified number of vectors that are most similar to the items associated with those keys.

<span id="e6379356"></span>
# Request parameters


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |Specify either the collection name or its alias. |
|IndexName |`string` |Yes |Index name |
|Limit |`number` |Yes |The maximum number of items to return. |
|DenseWeight |`number` |No |Weight |
|OutputFields |`string[]` |No |The data fields to return. |
|Partition |`string \| number` |No |The name of the partition. The value's type must match the type of the partition key. |
|Filter |`Filter` |No |Scalar Filtering |
|PrimaryKeys |`Array` |Yes |An array of primary key values. The type of the values must match the type of the primary key field. |


<span id="e8d65441"></span>
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


<span id="b9bbc59c"></span>
### MustTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Must`<br><br>`SearchOperation.MustNot` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|Conditions |`Array` |Yes |An array of values for the operation. |


<span id="60c79d7e"></span>
### NumberRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOperation.RangeOut` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|GreatThen |`number` |No |Greater than |
|LessThen |`number` |No |Less than |
|GreatThenEqual |`number` |No |Greater than or equal to |
|LessThenEqual |`number` |No |Less than or equal to |


<span id="9c8cd5ae"></span>
### AreaRangeTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOperation.RangeOut` |Yes |Operator |
|FieldNames |`[string, string]` |Yes |Abscissa, ordinate |
|Center |`[number, number]` |Yes |Abscissa, ordinate |
|Radius |`number` |Yes |Radius |


<span id="2351b63d"></span>
### LogicTypeCondition


|**field name** |**type** |**Required** |**Description** |
|---|---|---|---|
|Operation |`SearchOperation.And`<br><br>`SearchOperation.Or` |Yes |Operator |
|Conditions |`Filter[]` |Yes |An array of sub\-filter conditions. |


<span id="76fe7445"></span>
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
/** 
 * - the primary key field, where key indicates the defined field name. 
 */ 
interface SearchData<Data extends Record<string, unknown>> { 
  Score: number; 
  Fields?: Data; 
  [key: string]: unknown; 
}
```


<span id="7eac67c2"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace with your initialized service instance. 

interface Data { 
  Id: number, 
  Name: string 
} 

const response = await service.search.SearchByPrimaryKeys<Data>({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
  PrimaryKeys: [1, 2], 
  Limit: 10, 
  DenseWeight: 0.5, // optional 
  OutputFields: ['Id', 'Name'], // optional 
  Partition: "default", // optional 
  Filter: { 
    Operation: vikingdb.search.SearchOperation.And, 
    Conditions: [ 
      { FieldName: 'Name', Operation: vikingdb.search.SearchOperation.Must, Conditions: ['Tom'] }, 
      { FieldName: 'Id', Opeartion: vikingdb.search.SearchOperation.Range, GreatThen: 10 } 
    ] 
  }, // optional 
}) 

console.log(response.Data) // Output the retrieved data.
```

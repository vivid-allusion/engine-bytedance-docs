---
title: "SearchByText"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_SearchByText"
---

<span id="63f6ffe2"></span>
# Overview

The `SearchByText` API allows you to perform semantic searches on unstructured text data within a specified collection. By providing a text query, you can retrieve the most similar items based on vector distance calculations. This document details the request parameters, response structure, and provides a code example to help you integrate text\-based search for scenarios like duplicate detection, content matching, or Q&A systems.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only unstructured text data is supported.</div>


* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, there is an update lag of up to 20 seconds before the changes are reflected in the index.</div>



<span id="0b182c1c"></span>
# Request parameters


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|CollectionName/CollectionAlias |`string` |Yes |Dataset name or dataset alias, choose one of the two |
|IndexName |`string` |Yes |Index name |
|Limit |`number` |Yes |Number of results to return |
|DenseWeight |`number` |No |Weight |
|OutputFields |`string[]` |No |The data fields to return |
|Partition |`string \| number` |No |The name of the sub\-index. Its type must match the sub\-index's defined type. |
|Filter |`Filter` |No |Scalar Filtering |
|Text |`string` |Yes |Search text |


<span id="d4792bef"></span>
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


<span id="c758da91"></span>
### MustTypeCondition


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|Operation |`SearchOperation.Must`<br><br>`SearchOperation.MustNot` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|Conditions |`Array` |Yes |Condition values |


<span id="31f81530"></span>
### NumberRangeTypeCondition


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOpeartion.RangeOut` |Yes |Operator |
|FieldName |`string` |Yes |Field name |
|GreatThen |`number` |No |Greater than |
|LessThen |`number` |No |Less than |
|GreatThenEqual |`number` |No |Greater than or equal to |
|LessThenEqual |`number` |No |Less than or equal to |


<span id="a176f093"></span>
### AreaRangeTypeCondition


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|Operation |`SearchOperation.Range`<br><br>`SearchOpeartion.RangeOut` |Yes |Operator |
|FieldNames |`[string, string]` |Yes |Abscissa, ordinate |
|Center |`[number, number]` |Yes |Abscissa, ordinate |
|Radius |`number` |Yes |Radius |


<span id="7c74da9e"></span>
### LogicTypeCondition


|**field name** |**type** |**Is it necessary to pass on?**  |**explain** |
|---|---|---|---|
|Operation |`SearchOperation.And`<br><br>`SearchOperation.Or` |Yes |Operator |
|Conditions |`Filter[]` |Yes |Sub\-filter conditions |


<span id="24868deb"></span>
# Response parameters

```TypeScript
declare class SearchResponse> {
  readonly Data: SearchData[][];
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
 * Other internal fields may also exist as extended fields, such as 
 * - the primary key field, where key indicates the defined field name. 
 */ 
interface SearchData<Data extends Record<string, unknown>> { 
  Score: number; 
  Fields?: Data; 
  [key: string]: unknown; 
}
```


<span id="ebcf79e1"></span>
# Reference example

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

interface Data { 
  Id: number, 
  Name: string 
} 

const response = await service.search.SearchByText<Data>({ 
  CollectionName: 'test_collection_1', 
  IndexName: 'test_index_1', 
  Text: 'Some text you want to search', 
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

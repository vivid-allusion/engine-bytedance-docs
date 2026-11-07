---
title: "search_by_id"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_search_by_id"
---

<span id="02627465"></span>
# Overview

To find items in your collection that are similar to a specific item, you can use the search_by_id function. This function takes the primary key ID of a known item and returns a list of the most similar items based on vector distance. This reference provides details on all request parameters, including how to perform hybrid searches using the filter parameter, and includes Python code examples for both synchronous and asynchronous calls.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For mixed indexes using hnsw\-hybrid, search_by_id usage is not supported.</div>


* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, there is an expected 20\-second delay for the index to update. During this time, the data cannot be retrieved from the index.</div>


* <div data-tips="true" data-tips-type="tip">If the <code>filter</code> parameter is configured, the operation performs a mixed search. Otherwise, it performs a pure vector search.</div>


* <div data-tips="true" data-tips-type="tip">For asynchronous calls, use the <code>async_search_by_id</code> method. The parameters are the same.</div>



<span id="1e49859f"></span>
# Prerequisite


* When creating a dataset through the create_collection interface, ensure the `fields` definition includes a vector field.

* When writing data through the upsert_data interface, provide the field name and value for the vector field.

* When you create an index with `create_index`, a vector index must be created.


<span id="23bf69b2"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|ID |Int 64 |Yes |*  |The primary key ID. |
|Filter |Map |No |None |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (`must`, `must_not`, `range`, `range_out`) and two logical operators (`and`, `or`). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For scalar filtered retrieval, `dense_weight` is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |
|output_fields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* If `output_fields` is not provided, all scalar fields are returned, but vector fields are not.<br><br>* If `output_fields` is an empty list, the `fields` field is not returned.<br><br>* output_fields formatting error or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The partition name. Its type must be consistent with the `field_type` of the `partition_by` key, and its value must correspond to a `field_value` of that key.<br><br><br>* If `field_type` is `int64` or `list<int64>`, the partition input type is `int64`.<br><br>* If `field_type` is `string` or `list<string>`, the partition input type is `string` and must match the format `^[a-zA-Z0-9._]+$`. |


<span id="695ab18d"></span>
## Filter expression


|**operator** |**operator description** |**example** |
|---|---|---|
|Must |Effective for the specified field name. The field's value must be in the specified list. |```JSON```<br>```{```<br>```  "op": "must",```<br>```  "field": "region",```<br>```  "conds": ["cn", "sg"]```<br>```}```<br> |
|must_not |Effective for the specified field name. The field's value must not be in the specified list. |```JSON```<br>```{```<br>```  "op": "must_not",```<br>```  "field": "data_type",```<br>```  "conds": [1,2,3]```<br>```}```<br> |
|Range |Effective for the specified field name. The field's value must be within the specified range.<br><br>Use `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), and `lt` (less than) to define a one\-dimensional range.<br><br>In addition, you can use `center` and `radius` to represent the range within a two\-dimensional circle. |```JSON```<br>```// price between [100.0, 500.0)```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br>``````<br>```//price >= 100.0```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br>``````<br>```// Within a circle centered at center with a radius of 50```<br>```{```<br>```  "op": "range",```<br>```  "field": ["pos_x", "pos_y"],```<br>```  "center": [100.0, 123.4],```<br>```  "radius": 50.0```<br>```}```<br> |
|range_out |Effective for the specified field name, the semantics must be outside the specified range. Configure to use`gte`(Greater than or equal to), `gt`(Greater than), `lte`(Less than or equal to), `lt`(Less than), used to delimit the one\-dimensional range. |```JSON```<br>```// Filter products with a price lower than 100 or higher than 500```<br>```{```<br>```  "op": "range_out",```<br>```  "field": "price",```<br>```  "gt": 500.0,```<br>```  "lt": 100.0```<br>```}```<br> |
|And |Logical operator, which intersects multiple conditions for logical query requirements. |```JSON```<br>```{```<br>```  "op": "and",   // Operator name```<br>```  "conds": [     // List of conditions; supports nested logical operators and must/must_not operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1)```<br>```    }```<br>```  ]```<br>```}```<br> |
|Or |Logical operator, for logical query requirements, takes the union of multiple conditions. |```JSON```<br>```{```<br>```  "op": "or",   // Operator name```<br>```  "conds": [    // List of conditions; supports nested logical operators and must/must_not operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...      // Supports combining any number of conditions (>=1)```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="e9c4062d"></span>
# Example

<span id="61bdcc79"></span>
## Request parameters

```Python
# Get the specified index; This method only needs to be called once during program initialization
index = vikingdb_service.get_index("example", "example_index")
```


```Python
res = index.search_by_id("22", limit=2, output_fields=["doc_id", "like", "text_vector"], partition="default")

# Asynchronous call
async def search_by_id():
    index = await vikingdb_service.async_get_index("async", "async")
    res = await index.async_search_by_id("222")
asyncio.run(search_by_id())
```


<span id="c291735e"></span>
## Return value

The method call returns a `List<data>`. The properties contained in the Data instance are shown in the following table.


|**Attribute** |**Description** |
|---|---|
|ID |Primary key id. |
|Fields |A dictionary containing the data for the fields specified in `output_fields`. |
|Score |The similarity score between the query vector and the result vector. |

---
title: "scalar filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_scalar_filtering"
---

You can filter results in a vector database using a scalar filter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Scalar filtering is a general\-purpose search capability that you can use in<strong>Search and Aggregation Statistics</strong>Incoming from the relevant interface<strong>Filter parameters</strong>To enable scalar filtering capabilities.</div>


<span id="417130cc"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Filter |Map |No |None |For filter conditions, see the **Filter expression** section for an explanation.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (must, must_not, range, range_out) and two logical operators (and, or).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The precondition for a filter is that the corresponding field has a scalar index enabled.</div><br> |


<span id="82101e34"></span>
# Filter expression


|**operator** |**operator description** |**example** |
|---|---|---|
|Must |Effective for the specified field name, the semantic is that the value must be in the specified list ([...]), that is, "must in". |```JSON```<br>```{```<br>```  "op": "must",```<br>```  "field": "region",```<br>```  "conds": ["cn", "sg"]```<br>```}```<br> |
|must_not |Effective for the specified field name, the semantic is that the value must not be in the specified list ([...]), that is, "must not in". |```JSON```<br>```{```<br>```  "op": "must_not",```<br>```  "field": "data_type",```<br>```  "conds": [1,2,3]```<br>```}```<br> |
|Range |Effective for the specified field name, the semantic is that the value must be within the specified range.<br><br>Use `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), and `lt` (less than) to define a one\-dimensional range.<br><br>In addition, it supports the use of `center` and `radius` to represent the range within a two\-dimensional circle. |```JSON```<br>```// price in [100.0, 500.0)```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br>``````<br>```// price >= 100.0```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br>``````<br>```// Within a circle centered at 'center' with a radius of 50```<br>```{```<br>```  "op": "range",```<br>```  "field": ["pos_x", "pos_y"],```<br>```  "center": [100.0, 123.4],```<br>```  "radius": 50.0```<br>```}```<br> |
|range_out |Effective for the specified field name, the semantic is that the value must be outside the specified range. Use `gte` (greater than or equal to), `gt` (greater than), `lte` (less than or equal to), and `lt` (less than) to define a one\-dimensional range. |```JSON```<br>```// Filter products with a price lower than 100 or higher than 500```<br>```{```<br>```  "op": "range_out",```<br>```  "field": "price",```<br>```  "gt": 500.0,```<br>```  "lt": 100.0```<br>```}```<br> |
|And |Logical operator that returns the intersection of multiple conditions. |```JSON```<br>```{```<br>```  "op": "and",   // Operator name```<br>```  "conds": [     // List of conditions; supports nested logical operators and must/must_not operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1)```<br>```    }```<br>```  ]```<br>```}```<br> |
|Or |Logical operator that returns the union of multiple conditions. |```JSON```<br>```{```<br>```  "op": "and",   // Operator name```<br>```  "conds": [     // List of conditions; supports nested logical operators and must/must_not operators```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining any number of conditions (>=1)```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="04854d03"></span>
# Example

```Python
# Retrieve the specified index; call once during program initialization, no need to call repeatedly
index = vikingdb_service.get_index("example", "example_index")
```


```Python
agg_result = index.search_agg(agg={'op': 'count', 'field': 'f_string', 'cond': {'gt': 0}}, filter={'op': 'range', 'field': 'f_int64', 'gt': 90})
print(agg_result.agg_op, agg_result.group_by_field, agg_result.agg_result)
```

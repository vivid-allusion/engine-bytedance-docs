---
title: "SearchAgg"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SearchAgg"
---

<span id="09833190"></span>
# Overview

The SearchAgg API performs aggregation statistics on search results from a specified index. You can use this API to group data by a specific scalar field and apply filtering conditions to the aggregated results, which helps you understand data distribution. This document provides the request parameters, code examples, and return value specifications for using the SearchAgg API.

You can specify fields for grouping and add filtering operations to obtain aggregation statistics. These statistics can help you understand data distribution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An index must have at least one scalar index field of type string, int64, or bool.</div>


<span id="321cf71c"></span>
# **request parameters**


|Parameter name |Type |Required |Note |Sub\-parameter |Type |Note |Required |
|---|---|---|---|---|---|---|---|
|Agg |Map |Yes |Aggregation parameter |Op |String |Currently only count is supported. When using the count operator, at least one scalar index field of type string, int64, or bool must be present in the index. |Yes |
|||||Field |String |The name of the field to aggregate. Supported types are string, int64, and bool. The field must be a scalar index field. |No |
|||||Cond |Map |Similar to the SQL HAVING clause. This parameter only takes effect if the 'Field' parameter is also specified. For the 'count' operator, 'gt' is supported, which returns only groups with a count greater than the specified threshold. |No |


<span id="22cfbbda"></span>
# Example

<span id="bf9cc850"></span>
## Request parameters

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchAggOpt := vikingdb.NewSearchAggOptions().
                SetFilter(map[string]interface{}{
                        "op":    "range",
                        "field": "f_int64",
                        "gt":    10,
                }).
                SetAgg(map[string]interface{}{
                        "op":    "count",
                        "field": "f_string",
                        "gt":    0,
                })
aggResult, err := index.SearchAgg(searchAggOpt)
        if err != nil {
                panic(err)
        }
fmt.Println(aggResult.AggOp)
fmt.Println(aggResult.GroupByField)
fmt.Println(aggResult.AggResult)
```


<span id="82283fa0"></span>
## Return value

The Go code example returns an aggregation result object. The fields in this object are described in the following table.


|**attribute** |**explain** |
|---|---|
|agg_op |Operator type |
|group_by_field |The value of the 'field' parameter from the request, which specifies the field used for aggregation. |
|agg_result |The result value of the aggregation process |

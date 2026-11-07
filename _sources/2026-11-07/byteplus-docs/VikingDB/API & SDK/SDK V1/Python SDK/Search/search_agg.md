---
title: "search_agg"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_search_agg"
---

<span id="0da582a0"></span>
# Overview

To analyze your search results and understand data distribution, you can use the search_agg API. This document provides the parameters and code examples for performing aggregation statistics on your index data. You will learn how to group results by a specific field and apply filtering conditions to the final aggregated output.

You can specify fields for grouping and add filtering operations to get aggregation statistics, which helps you understand the data distribution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An index requires at least one scalar index field of type string, int64, or bool.</div>


<span id="0f6ae083"></span>
## **Request parameters**


|Parameter name |Type |Required |Note |Sub\-parameter |Type |Note |Required |
|---|---|---|---|---|---|---|---|
|Agg |Map |Yes |Aggregation parameter |Op |String |Currently only count is supported. When using the count operator, at least one scalar index field of type string, int64, or bool must be present in the index. |Yes |
|||||Field |String |Supported field types are string, int64, and bool. The field must be a scalar index field. |No |
|||||Cond |Map |Similar to the group by having clause in SQL. This parameter only takes effect if the 'field' parameter is also specified. For the count operator, gt is supported, which means that only result items with a count greater than the specified value are returned. |No |


<span id="00d7126f"></span>
# Example

<span id="26a76850"></span>
## Request parameters

```Python
# Get the specified index; only needs to be called during program initialization, no need to call repeatedly
index = vikingdb_service.get_index("example", "example_index")
```


```Python
agg_result = index.search_agg(agg={'op':'count'})
print(agg_result.agg_op, agg_result.group_by_field, agg_result.agg_result)
print("==========")

agg_result = index.search_agg(agg={'op': 'count', 'field': 'f_string', 'cond': {'gt': 0}})
print(agg_result.agg_op, agg_result.group_by_field, agg_result.agg_result)
```


<span id="addd42cb"></span>
## Return value

The Python call returns a Listobject. The properties contained in the Data instance are shown in the following table.


|**Attribute** |**Description** |
|---|---|
|agg_op |Operator type |
|group_by_field |The field specified in the request for aggregation. |
|agg_result |The result value of the aggregation process |

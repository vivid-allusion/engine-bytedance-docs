---
title: "searchAgg"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_searchAgg"
---

<span id="b85cbf7b"></span>
# Overview

The searchAgg operation allows you to perform aggregation statistics on search results from a specified index. You can group data by specific fields and apply filters to obtain targeted statistical results, which helps in understanding data distribution. This reference provides the request parameters, return values, and a code example for using the searchAgg operation.

You can specify fields for grouping and apply filters to generate aggregation statistics. These statistics can help you understand your data distribution.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">An index requires a scalar index field that contains at least one enumeration type (string, int64, or bool).</div>


<span id="494af73e"></span>
## **request parameters**

The request uses a SearchAggParam object. Its parameters are shown in the following table.


|Parameter name |Type |Required |Note |Sub\-parameter |Type |Note |Required |
|---|---|---|---|---|---|---|---|
|Agg |Map |Yes |Aggregation parameter |Op |String |Currently only count is supported. When using the count operator, at least one scalar index field of type string, int64, or bool must be present in the index. |Yes |
|||||Field |String |The name of the field to aggregate. Supported field types are string, int64, and bool. The field must be a scalar index field. |No |
|||||Cond |Map |Similar to the GROUP BY HAVING clause in SQL. This only takes effect if the 'field' parameter is also specified. For the count operator, gt is supported, which means that only result items greater than the threshold are returned. |No |


<span id="87faafc0"></span>
# Example

<span id="9174265d"></span>
## Request parameters

```Python
// Call this method once during program initialization to get the index object. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Python
Map agg = new HashMap<>();
agg.put("op", "count");
agg.put("field", "f_string");
Map filter = new HashMap<>();
filter.put("op", "range");
filter.put("field", "f_int64");
filter.put("gt", 10);
SearchAggResult result = index.searchAgg(new SearchAggParam()
                .setAgg(agg)
                .setFilter(filter)
                .build());
System.out.println(result);
```


<span id="ec3a10d1"></span>
## Return value

A Java call for this task returns a Listobject. The properties contained in the Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|agg_op |Operator type |
|group_by_field |The value of the 'field' parameter from the request, which specifies the field used for aggregation. |
|agg_result |The result value of the aggregation process |

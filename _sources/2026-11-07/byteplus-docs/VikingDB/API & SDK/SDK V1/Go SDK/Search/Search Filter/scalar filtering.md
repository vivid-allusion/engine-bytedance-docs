---
title: "scalar filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_scalar_filtering"
---

You can filter the results in a vector database using a scalar filter.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Scalar filtering is a general\-purpose search capability that you can use in<strong>Search and Aggregation Statistics</strong>Incoming from the relevant interface<strong>Filter parameters</strong>To enable scalar filtering capabilities.</div>


<span id="d4dd2a27"></span>
# Parameter description


|**Parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Filter |Map |No |None |Filter conditions, see the **Filter expression** section below.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (`must`, `must_not`, `range`, `range_out`) and two logical operators (`and`, `or`) for combining conditions.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The precondition for a filter is that the corresponding field has a scalar index enabled.</div><br> |


<span id="7bef19bc"></span>
# Filter expression


|**operator** |**operator description** |**example** |
|---|---|---|
|Must |Applies conditions to the specified field, meaning the field's value must be in the provided list, that is, "must in". |```JSON```<br>```{```<br>```  "op": "must",```<br>```  "field": "region",```<br>```  "conds": ["cn", "sg"]```<br>```}```<br> |
|must_not |Applies conditions to the specified field, meaning the field's value must not be in the provided list, that is, "must not in". |```JSON```<br>```{```<br>```  "op": "must_not",```<br>```  "field": "data_type",```<br>```  "conds": [1,2,3]```<br>```}```<br> |
|Range |Applies conditions to the specified field, meaning the field's value must be within the specified range.<br><br>configure use`gte`(Greater than or equal to), `gt`(Greater than), `lte`(Less than or equal to), `lt`(Less than), used to delimit the one\-dimensional range.<br><br>In addition, it supports the use of `center` and `radius` Represents the range within a two\-dimensional circle. |```JSON```<br>```// price is in the range [100.0, 500.0)```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br>``````<br>```//price >= 100.0```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br>``````<br>```// Within a circle with a radius of 50 centered at 'center'```<br>```{```<br>```  "op": "range",```<br>```  "field": ["pos_x", "pos_y"],```<br>```  "center": [100.0, 123.4],```<br>```  "radius": 50.0```<br>```}```<br> |
|range_out |Effective for the specified field name, the semantics must be outside the specified range. Configure to use`gte`(Greater than or equal to), `gt`(Greater than), `lte`(Less than or equal to), `lt`(Less than), used to delimit the one\-dimensional range. |```JSON```<br>```// Filter for items with a price less than 100 or greater than 500```<br>```{```<br>```  "op": "range_out",```<br>```  "field": "price",```<br>```  "gt": 500.0,```<br>```  "lt": 100.0```<br>```}```<br> |
|And |Logical operator that returns the intersection of multiple conditions. |```JSON```<br>```{```<br>```  "op": "and",   // Operator name```<br>```  "conds": [     // A list of conditions. Supports nested logical operators and must/must_not operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining one or more conditions.```<br>```    }```<br>```  ]```<br>```}```<br> |
|Or |Logical operator that returns the union of multiple conditions. |```JSON```<br>```{```<br>```  "op": "or",   // Operator name```<br>```  "conds": [    // A list of conditions. Supports nested logical operators and must/must_not operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...      // Supports combining one or more conditions.```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="a27dab25"></span>
# Example

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchOption := vikingdb.NewSearchOptions()
.SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5})
res, err := index.Search(vikingdb.VectorOrder{Id: "111"}, searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="8cd45614"></span>
## Return value

The Go call performs the above task and returns `List<dataobject>`. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|Id |Primary key id. |
|Fields |The returned `fields` map, which contains the specific data for the entry. |
|Score |Indicates the degree to which the found vector matches the input vector. |

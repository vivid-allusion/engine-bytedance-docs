---
title: "Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_Search"
---

<span id="e372088b"></span>
# Overview

The Search method allows you to retrieve data from your index using various query types. You can perform a vector similarity search based on a given vector or by a primary key ID, or execute a sorted search based on a scalar field. This method also supports advanced options like filtering, limiting results, and specifying output fields to customize your queries.


* When the request parameter order is configured as the Vector field in the VectorOrder object, it indicates a vector search based on the name of the vector field.

* When the request parameter order is configured as the primary key Id in the vector VectorOrder object, it indicates that the vector is retrieved according to the primary key id.

* When the `order` parameter is configured with `FieldName` and `Order` in a `ScalarOrder` object, it performs a sorted retrieval based on a scalar field. The `filter` parameter can be used to perform a scalar retrieval.


After data is written to or deleted from a collection, updates to the index may take up to 20 seconds. Therefore, new or deleted data cannot be retrieved from the index immediately.

<span id="61546767"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|Order |*  |Map |No |*  |Specify either a `VectorOrder` object or a `ScalarOrder` object. You must choose one.<br><br><br>* For `VectorOrder`, you must specify either the `Vector` or `Id` parameter, but not both.<br><br>   * The name of the vector field. Use this for a `SearchByVector` operation to find vectors similar to the input vector.<br><br>   * The primary key ID. Use this for a `SearchById` operation to find vectors similar to the one identified by the ID.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For mixed indexes using hnsw\-hybrid, search_by_id usage is not supported.</div><br><br><br><br>* For `ScalarOrder`, the `FieldName` and `Order` parameters must be configured together.<br><br>   * FieldName: The name of the scalar field used for sorting.<br><br>   * Order: Sort method, Order. Asc (ascending), Order. Desc (descending). |
|searchOptions |Filter |Map |No |*  |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four query operators (`must`, `must_not`, `range`, `range_out`) and two combination operators (`and`, `or`). |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||outputFields |List\ < string \> |No |*  |A list of scalar or vector fields to return in the response.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When `outputFields` is an empty list, the `Fields` map is not returned in the response.<br><br>* When `outputFields` is formatted incorrectly or a specified field is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
||Partition |String/int |No |"Default" |The name of the sub\-index, the type is consistent with the FieldType of partitionBy, and the field value corresponds to the FieldValue of partitionBy.<br><br><br>* When FieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When `FieldType` is `string` or `list<string>`, the partition input type is `string`, and the value must match the regex `^[a-zA-Z0-9._]+$`. |
||dense_weight |Float |No |0.5 |For filtered retrievals on a mixed index, `dense_weight` is used to control the weight of dense vectors. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |
||sparse_vectors |Map |No |*  |A sparse vector, formatted as a dictionary where the key (string) is the keyword and the value (float) is its weight. |


<span id="b842217a"></span>
## Request parameters

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}).SetDenseWeight(0.5).SetSparseVectors(map[string]interface{}{"hello1": 0.01})
res, err := index.Search(vikingdb.VectorOrder{Id: "111"}, searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}

// or
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}).SetDenseWeight(0.5).SetSparseVectors(map[string]interface{}{"hello1": 0.01})
res, err := index.Search(vikingdb.ScalarOrder{FieldName: "price", Order: vikingdb.Desc}, searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
} 
```


<span id="85c3a580"></span>
## Return value

The Go call returns a slice of pointers to `Data` structs (`[]*Data`). The properties contained in the Data structure are shown in the following table.


|**attribute** |**explain** |
|---|---|
|Id |Primary key id. |
|Fields |A map containing the returned field data. |
|Score |Indicates the degree to which the found vector matches the input vector. |

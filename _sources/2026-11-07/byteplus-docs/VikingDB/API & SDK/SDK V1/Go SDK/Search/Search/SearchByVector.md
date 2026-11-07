---
title: "SearchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SearchByVector"
---

<span id="b20ecd73"></span>
# Overview

The SearchByVector API allows you to perform vector similarity searches. By providing a query vector, you can retrieve a specified number of the most similar vectors from your collection, enabling applications like image search, recommendation systems, and semantic text matching.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After data in a Collection is written or deleted, the index data takes approximately 20s to update, so it cannot be retrieved from the index immediately.</div>


* <div data-tips="true" data-tips-type="tip">When the request parameter filter is configured, it represents a mixed search; when the request parameter filter is not configured, it represents a pure vector search.</div>



<span id="df77e850"></span>
# Prerequisite


* When creating a dataset through the CreateCollection interface, define the fields, ensuring a vector field is included.

* When writing data through the UpsertData interface, the field name and field value of the vector type have been written.

* When creating an index with CreateIndex, a vector index has been created.


<span id="90d341b3"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|Vector |*  |Map |Yes |*  |The name of the vector field used for retrieval. |
|searchOptions |Filter |Map |No |*  |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four types of query operators (must, must_not, range, range_out) and two types of combination operators (and, or). |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||outputFields |List\ < string \> |No |*  |Output fields. Specifies a list of scalar or vector fields to return.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or a specified field is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
||Partition |String/int |No |"Default" |The name of the sub\-index, the type is consistent with the FieldType of partitionBy, and the field value corresponds to the FieldValue of partitionBy.<br><br><br>* When FieldType is int64 or list, the partition input type is int64.<br><br>* When FieldType is string or list, the partition input type is string and must match the format `^[a-zA-Z0-9. _]+$`. |
||dense_weight |Float |No |0.5 |For scalar filtered retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index of the retrieval is a mixed index (HNSW_HYBRID). |
||sparse_vectors |Map |No |*  |Sparse vector, formatted as a dictionary where the key (k) is a string representing the keyword, and the value (v) is a float representing the keyword's weight. |


<span id="4c8d92ee"></span>
# Example

<span id="d04dca69"></span>
## Request parameters

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}).SetDenseWeight(0.5).SetSparseVectors(map[string]interface{}{"hello1": 0.01})
res, err := index.SearchByVector(genRandomVector(12), searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="9adff398"></span>
## Return value

The Go call performs the above task and returns a slice of pointers to Data structs ([]\*Data). The properties contained in the Data structure are shown in the following table.


|**attribute** |**explain** |
|---|---|
|Id |The primary key. |
|Fields |A map containing the returned field data. |
|Score |Indicates how closely the found vector matches the query vector. |

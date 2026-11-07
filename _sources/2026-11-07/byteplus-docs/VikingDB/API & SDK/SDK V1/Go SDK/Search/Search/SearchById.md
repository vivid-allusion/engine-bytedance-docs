---
title: "SearchById"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SearchById"
---

<span id="7baadad0"></span>
# Overview

Use the SearchById API to retrieve vectors based on a specific primary key ID. This reference provides details on how you can refine your search by applying scalar filters for hybrid searches, limiting the number of results, and specifying which fields to return. This allows for flexible and efficient data retrieval tailored to your application's needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, the index update can take up to 20 seconds. The data cannot be retrieved from the index during this period.</div>


* <div data-tips="true" data-tips-type="tip">If the filter parameter is configured, the operation performs a hybrid search. If the filter parameter is not configured, it performs a pure vector search.</div>



<span id="63f494e7"></span>
# Prerequisite


* When creating a collection using the CreateCollection API, you must define fields, including a vector field.

* You have used the UpsertData API to write data, including the name and value for the vector field.

* You have created a vector index using the CreateIndex API.


<span id="7a847dcf"></span>
# **request parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|ID |*  |Int 64 |Yes |*  |Primary key id. |
|searchOptions |Filter |Map |No |*  |Filter conditions, see**scalar filtering**.<br><br><br>* By default, this is empty, which means no filtering is applied.<br><br>* Filter conditions support four types of query operators (must, must_not, range, range_out) and two logical operators for combining them (and, or). |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to include in the search results.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* If outputFields is formatted incorrectly or contains a field that is not in the collection, the API returns an error.<br><br><br>If the index's distance metric is cosine, the returned vectors are normalized. |
||Partition |String/int |No |"Default" |The name of the sub\-index, the type is consistent with the FieldType of partitionBy, and the field value corresponds to the FieldValue of partitionBy.<br><br><br>* When FieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When FieldType is string or list, the partition input type is string and must match the format "^[a\-zA\-Z0\-9._]+$". |
||dense_weight |Float |No |0.5 |For scalar filtered retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. This parameter is valid only when searching a hybrid index. |
||sparse_vectors |Map |No |*  |A sparse vector in dictionary format, where the key (k) is a string representing the keyword, and the value (v) is a float representing the keyword's weight. |


<span id="34403d67"></span>
# Example

<span id="1ed0a91b"></span>
## Request parameters

```Go
// During program initialization, call this operation once to get the specified index object. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchOption := vikingdb.NewSearchOptions().SetFilter(map[string]interface{}{"op": "range", "field": "price", "lt": 3.5}).SetLimit(5).SetOutputFields([]string{"doc_id", "like", "text_vector", "price"}).SetDenseWeight(0.5).SetSparseVectors(map[string]interface{}{"hello1": 0.01})
res, err := index.SearchById("111", searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="1adc9567"></span>
## Return value

The Go SDK call returns a slice of pointers to Data objects ([]\*Data). The properties contained in the Data structure are shown in the following table.


|**attribute** |**explain** |
|---|---|
|Id |Primary key id. |
|Fields |The Fields attribute contains the returned data as a map. |
|Score |The similarity score, indicating how well the result vector matches the query vector. |

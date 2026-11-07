---
title: "SearchByText"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SearchByText"
---

At present, the vector database supports multi\-modal retrieval, allowing you to search for text using text, search for images using text, or search for images using an image. The original SearchByText interface can be migrated to[SearchWithMultiModal](https://www.volcengine.com/docs/84313/1471371)

<span id="9fa04653"></span>
# Overview

The SearchByText API allows you to perform text\-based searches on unstructured data within a vector database. Note: This interface is being phased out. For more powerful multi\-modal retrieval capabilities, including text\-to\-image search, we recommend migrating to the SearchWithMultiModal API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently only unstructured data of text type is supported.</div>


* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, the index update is expected to take 20 seconds. Therefore, changes are not immediately reflected in search results.</div>



<span id="45928347"></span>
# Prerequisites


* You must enable vectorization. This can be done in one of two ways: 1) When creating a collection in the console, select a database type that includes vectorization and configure the vectorization field. 2) When creating a collection with the `CreateCollection` API, set the `vectorize` parameter.

* Data has been written using the UpsertData interface, including a field of type text with its corresponding name and value.

* When you create an index with CreateIndex, an index of type `vector_index` has been created.


<span id="ae13d5cd"></span>
# **Request Parameters**


|**parameter** |**sub\-parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|---|
|TextObject |Text |String |Yes |*  |The input text for the search. |
|searchOptions |Filter |Map |No |*  |Filter conditions, see **Filter expression**Explanation.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions use four query operators (`must`, `must_not`, `range`, `range_out`) and two combination operators (`and`, `or`). |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||outputFields |List\ < string \> |No |*  |A list of scalar or vector fields to return in the results.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
||Partition |String/int |No |"Default" |The name of the sub\-index, the type is the same as the fieldType of partitionBy, and the field value corresponds to the fieldValue of partitionBy.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list, partition input type is string, format requirement `^[a-zA-Z0-9._]+$`. |
||dense_weight |Float |No |0.5 |For mixed retrieval, `dense_weight` is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |


<span id="5161c9fc"></span>
# Example

<span id="1569da03"></span>
## Request Example

```Go
// Call this operation once during program initialization to get a client for the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
searchOption := vikingdb.NewSearchOptions().SetLimit(5).SetOutputFields([]string{"doc_id"}).SetDenseWeight(0.5)
res, err := index.SearchByText(vikingdb.TextObject{Text: "example"}, searchOption)
if err != nil {
    fmt.Println(err)
}
for _, item := range res {
    fmt.Println(item)
}
```


<span id="dd7b3ea0"></span>
## Return value

The Go call performs the above task and returns a slice of pointers to Data structs ([]\*Data). The properties contained in the Data structure are shown in the following table.


|**attribute** |**explain** |
|---|---|
|Id |Primary key id. |
|Fields |A map containing the requested field data, where keys are field names and values are the corresponding field values. |
|Score |The similarity score between the result vector and the query vector. |
|Text |The original text content, returned for unstructured text searches. |

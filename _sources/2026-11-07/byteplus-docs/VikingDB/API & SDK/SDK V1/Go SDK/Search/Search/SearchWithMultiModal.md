---
title: "SearchWithMultiModal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SearchWithMultiModal"
---

<span id="94f8a73b"></span>
# Overview

The SearchWithMultiModal method enables you to retrieve data from a vector database using multiple input types simultaneously. You can perform searches by providing text, an image, or a combination of both. This reference details the necessary request parameters, such as TextObject and ImageObject, and provides a Go SDK code example to guide your implementation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently supports unstructured data of text and image types.</div>


* <div data-tips="true" data-tips-type="tip">After the Collection data is written/deleted, the Index data update time is expected to be 20s, and it cannot be retrieved from the index immediately.</div>



<span id="435b573a"></span>
# Prerequisite


* Configure vectorization for the collection by either: 1) selecting a vectorization\-enabled database type and configuring the vectorization field in the console, or 2) setting the `vectorize` parameter when using the `CreateCollection` interface.

* When writing data through the UpsertData interface, field names and field values of type text or image have been written.

* When creating an index with CreateIndex, a vector index has been created.


<span id="ae13d5cd"></span>
# **Request parameters**


|**parameter** |**sub\-parameter** |**type** |**Required?**  |**default value** |**Parameter description** |
|---|---|---|---|---|---|
|TextObject |Text |String |Select at least one of the text and image parameters |*  |The input text for the retrieval. |
|ImageObject |Image |String |Select at least one of the text and image parameters |*  |The input image for the retrieval currently supports 2 methods:<br><br><br>* Image tos link.`tos://{bucket}/{object_key}`.<br><br>* Base64 string.`base64://{Base64-encoded string}`. |
|searchOptions |Filter |Map |No |*  |Filter conditions, see the **Filter expression** section for details.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four query operators (`must`, `must_not`, `range`, `range_out`) and two combination operators (`and`, `or`). |
||Limit |Int |No |10 |Number of search results, up to 5000. |
||outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to return.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
||Partition |String/int |No |"Default" |The name of the sub\-index, the type is the same as the fieldType of partitionBy, and the field value corresponds to the fieldValue of partitionBy.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list\ < string \>, partition input type is string, format requirement "^[a\-zA\-Z0\-9._]+$". |
||dense_weight |Float |No |0.5 |For mixed retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |


<span id="5161c9fc"></span>
# Example

<span id="1569da03"></span>
## Request parameters

```Go
// Call the related operation once during the initialization of the program to get the specified index. 
index, _ := service.GetIndex("go", "goIndex")
```


```Go
// Create search options and configure parameters such as result limit, text input, and image path. 
searchOpt := vikingdb.NewSearchOptions().SetLimit(5). 
    SetText ("This is a test").  // Set the text input for the query. 
    SetImage("tos://{your_bucket}/{your_object}").  // Set the image path for the query. 
    SetNeedInstruction(false).  // Disable instruction output. 
    SetRetry(true)  // Enable the retry mechanism. 
    
// Execute a multimodal search. 
datas, err := index.SearchWithMultiModal(searchOpt) 
if err != nil{ 
    // Specify the error handling mode. 
    panic(err) 
} 
    
// Display the fields and scores of each search result. 
for _, data := range datas { 
    fmt.Println(data.Fields, data.Score) 
}
```


<span id="dd7b3ea0"></span>
## Return value

The Go call performs the above task and returns a list of Data objects ([] \* Data). The properties contained in the Data structure are shown in the following table.


|**Attribute** |**Explanation** |
|---|---|
|Id |Primary key id. |
|Fields |The fields field in the response contains the specific data as a map. |
|Score |Indicates the similarity score between the found vector and the input vector. |
|Text |The retrieved unstructured text. |

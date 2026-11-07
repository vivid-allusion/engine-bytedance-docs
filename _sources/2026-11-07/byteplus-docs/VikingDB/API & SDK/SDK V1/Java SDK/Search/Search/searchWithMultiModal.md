---
title: "searchWithMultiModal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_searchWithMultiModal"
---

<span id="5f7a91b7"></span>
# Overview

The searchWithMultiModal method allows you to perform multimodal searches within a vector database. This API enables you to retrieve data by providing text, images, or a combination of both as input, supporting powerful cross\-modal query capabilities for text and image data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently supports unstructured data of text and image types.</div>


* <div data-tips="true" data-tips-type="tip">After data in a collection is written or deleted, the index updates with an expected 20\-second delay. Data cannot be retrieved during this period.</div>



<span id="14409adb"></span>
# Prerequisite


* Vectorization must be enabled for the collection, either by selecting a vectorized database type in the console or by setting the vectorize parameter when using the create_collection interface.

* you have written data to fields of type text or image.

* When you create an index with create_index, a vector index (vector_index) is created.


<span id="79d2c8c9"></span>
# **request parameters**

The request parameter is SearchWithMultiModalParam. An instance of SearchWithMultiModalParam contains the parameters shown in the following table.


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|Text |String |Select at least one of the text and image parameters |None |The input text for retrieval. |
|Image |String |Select at least one of the text and image parameters |None |The input image for retrieval currently supports 2 methods:<br><br><br>* A TOS link to the image.`tos://{bucket}/{object_key}`.<br><br>* Base64 string.`base64://{Base64}`. |
|Filter |Map |No |*  |The filter conditions to apply. For more information, see**Scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Specifies filter conditions using query operators (must, must_not, range, range_out) and combination operators (and, or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For mixed retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. This parameter is valid only when searching a mixed index. |
|outputFields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* When outputFields is not specified, all scalar fields are returned, but vector fields are not.<br><br>* When outputFields is an empty list, the response does not include the fields object.<br><br>* When outputFields is formatted incorrectly or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The name of the sub\-index, the type is the same as the fieldType of partitionBy, and the field value corresponds to the fieldValue of partitionBy.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list< string \>, partition input type is string, the format must match the regex "^[a\-zA\-Z0\-9._]+$" |


<span id="a5821432"></span>
# Example

<span id="bc68dbfe"></span>
## Request parameters

```Java
During program initialization, call this operation once to get a reference to the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
// Execute a multimodal search with text and image input. 
List<DataObject> datas = index.searchWithMultiModal(new SearchWithMultiModalParam() 
    .setText("1")  // Set the text input to "1". 
    .setImage("tos://your_bucket/your_object")  // Set the image input to the specified path. 
    .build()); 

// Display the search results. 
System.out.println(datas);
```


<span id="2082ce02"></span>
## Return value

The Java call returns a List. Each DataObject instance contains the following properties shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key ID. |
|Fields |A map containing the requested field data. |
|Score |A score that indicates the similarity between the found vector and the input vector. |
|Text |Returned when the search query includes unstructured text. |

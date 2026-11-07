---
title: "searchByText"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_searchByText"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The vector database supports multi\-modal retrieval, allowing you to perform text\-for\-text, text\-for\-image, and image\-for\-image searches. The original searchByText interface can be migrated to <strong>searchWithMultiModal</strong></div>


<span id="061770e4"></span>
# Overview

To search for unstructured text data within a vector database, you can use the searchByText API. This reference guide details its request parameters, such as Filter and Limit, provides a complete Java code example for implementation, and explains the structure of the returned data. For multi\-modal search capabilities, consider migrating to the searchWithMultiModal interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only text\-type unstructured data is supported.</div>


* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, index updates can take up to 20 seconds. The data is not retrievable during this period.</div>



<span id="9ef5963b"></span>
# Prerequisites


* Either select a vectorized database type and configure the vectorization field when creating the dataset in the console, or configure vectorization for the Collection by setting the vectorize parameter when using the create_collection interface.

* When writing data through the upsert_data interface, you have written text\-type fields and their corresponding values.

* When you create an index with create_index, a vector index is created.


<span id="79d2c8c9"></span>
# **Request Parameters**

The request parameter is SearchByTextParam, and the parameters contained in the SearchByTextParam instance are shown in the following table.


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|Text |String |Yes |*  |The input text for the search. |
|Filter |Map |No |*  |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four query operators (must, must_not, range, range_out) and two logical operators (and, or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For mixed retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |
|outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to return.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The name of the sub\-index, the type is the same as the fieldType of partitionBy, and the field value corresponds to the fieldValue of partitionBy.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list\ < string \>, partition input type is string, format requirement "^[a\-zA\-Z0\-9._]+$".\* n |


<span id="b7ee945b"></span>
# Example

<span id="bc68dbfe"></span>
## Request parameters

```Java
// Call the related operation once during the initialization of the program to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
HashMap filter = new HashMap<>();
filter.put("op", "range");
filter.put("field", "price");
filter.put("lt", 4);
Text text = new Text().setText("this.is test").build();
SearchByTextParam searchByTextParam = new SearchByTextParam()
                                        .setText(text)
                                        .setFilter(filter)
                                        .setDenseWeight(0.5)
                                        .build();
List datas = index.searchByText(searchByTextParam);
```


<span id="2082ce02"></span>
## Return value

The Java method call returns List\ < DataObject \>. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**explain** |
|---|---|
|ID |The primary key (ID) of the data object. |
|Fields |A map containing the returned field data. |
|Score |Indicates how closely the found vector matches the input vector. |
|Text |The original text, which is returned for unstructured text retrievals. |

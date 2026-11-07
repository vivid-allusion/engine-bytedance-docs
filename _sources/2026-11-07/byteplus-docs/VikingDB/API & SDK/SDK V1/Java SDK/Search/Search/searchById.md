---
title: "searchById"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_searchById"
---

<span id="b85cbf7b"></span>
# Overview

The searchById function allows you to find items that are semantically similar to a specific item within your collection. By providing the primary key ID of a source item, this function uses that item's vector as a query to retrieve the most similar vectors from the index.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For hybrid indexes using the hnsw\-hybrid algorithm, id\-based retrieval is temporarily not supported.</div>


* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, there is an expected update delay of approximately 20 seconds, during which the data cannot be retrieved from the index.</div>


* <div data-tips="true" data-tips-type="tip">When the request parameter filter is configured, it represents a mixed search; when the request parameter filter is not configured, it represents a pure vector search.</div>



<span id="38b34783"></span>
# Prerequisite


* When creating a collection using the createCollection interface, define the `fields` parameter to include a vector field.

* When writing data using the upsertData interface, you must provide the name and value for the vector field.

* When creating an index using the createIndex interface, ensure a vector index has been created.


<span id="b7f4dd3a"></span>
# **request parameters**

Request parameters are provided in a SearchByIdParam object, as described in the following table.


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|ID |Int 64 |Yes |*  |Primary key id. |
|Filter |Map |No |*  |Filter conditions, see**scalar filtering**<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (`must`, `must_not`, `range`, `range_out`) and two combination operators (`and`, `or`). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to return.<br><br><br>* If `outputFields` is not specified, all scalar fields are returned, but vector fields are not.<br><br>* If `outputFields` is an empty list, the `fields` attribute is not returned.<br><br>* If `outputFields` is formatted incorrectly or specifies a field that does not exist in the collection, the interface returns an error.<br><br><br>If the index's distance metric is `cosine`, returned vectors are normalized. |
|dense_weight |Float |No |0.5 |For mixed retrieval, `dense_weight` is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. This parameter is valid only for mixed indexes. |
|Partition |String/int |No |"Default" |The name of the sub\-index, the type is consistent with the fieldType of partitionBy, and the field value corresponds to the fieldValue of the partition_by.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When `fieldType` is `string` or `list<string>`, the `partition` input type is `string` and must match the format `^[a-zA-Z0-9._]+$`. |


<span id="15d61dc7"></span>
# Example

<span id="70c88bc3"></span>
## Request parameters

```Java
// Call the related operation once during the initialization of the program to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
List outputField = new ArrayList<>();
outputField.add("doc_id");
outputField.add("price");
outputField.add("text_vector");
HashMap filter = new HashMap<>();
filter.put("op", "range");
filter.put("field", "price");
filter.put("lt", 4);
SearchByIdParam searchByIdParam = new SearchByIdParam()
                                    .setOutputFields(outputField)
                                    .setId("22")
                                    .setPartition("default");
                                    .setFilter(filter)
                                    .setLimit(2)
                                    .build();

List datas = index.searchById(searchByIdParam);
System.out.println(datas);
```


<span id="c064f2d9"></span>
## Return value

A Java call for this operation returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**explain** |
|---|---|
|ID |Primary key id. |
|Fields |The `Fields` attribute contains the returned data as a map. |
|Score |Indicates the degree to which the found vector matches the input vector. |

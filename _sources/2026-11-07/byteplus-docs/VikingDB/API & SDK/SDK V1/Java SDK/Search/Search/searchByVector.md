---
title: "searchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_searchByVector"
---

<span id="22aa1145"></span>
# Overview

Use the searchByVector method to perform powerful vector similarity searches. This method retrieves a specified number of the most similar vectors to a given query vector. You can execute a pure vector search or a hybrid search by combining it with scalar filters for more precise results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After data is written to or deleted from a collection, the index update is expected to take up to 20 seconds. During this period, the data cannot be retrieved from the index.</div>


* <div data-tips="true" data-tips-type="tip">If the filter parameter is configured, the operation performs a mixed search. If the filter parameter is not configured, it performs a pure vector search.</div>



<span id="baa940c3"></span>
# Prerequisite


* When creating a collection using the createCollection interface, you must define the fields to include a vector field.

* When writing data using the upsertData interface, you must provide the field name and value for the vector.

* When creating an index with createIndex, a vector index (vectorIndex) must have been created.


<span id="9fa7995c"></span>
# **request parameters**

The request parameter is SearchByVectorParam, and the parameters contained in the SearchByVectorParam instance are shown in the following table.


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Vector |Map |Yes |*  |The name of the vector field used for retrieval. |
|Filter |Map |No |*  |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four types of query operators (must, must_not, range, range_out) and two combination operators (and, or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For mixed retrieval, dense_weight is used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index (IndexType.HNSW_HYBRID). |
|outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to return.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or contains a field that is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The name of the partition. The type of this parameter must match the fieldType of the partitionBy key, and its value must correspond to a fieldValue of the partitionBy key.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list\ < string \>, partition input type is string, format requirement "^[a\-zA\-Z0\-9._]+$".\*n |


<span id="83870b41"></span>
# Example

<span id="e18f9d9d"></span>
## Request parameters

```Java
// Call this operation once during program initialization to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
List outputField = new ArrayList<>();
outputField.add("doc_id");
outputField.add("like");
outputField.add("text_vector");
HashMap filter = new HashMap<>();
filter.put("op", "range");
filter.put("field", "price");
filter.put("lt", 4);
SearchByVectorParam searchByVectorParam = new SearchByVectorParam()
                                            .setVector(genRandomVector(10))
                                            .setSparseVector({"hello": 0.34, "world": 0.03, "!": 0.11})
                                            .setOutputFields(outputField)
                                            .setLimit(1)
                                            .setFilter(filter)
                                            .setPartition("default")
                                            .setDenseWeight(0.5)
                                            .build();

List datas = index.searchByVector(searchByVectorParam);
System.out.println(datas);
```


<span id="775706fc"></span>
## Return value

A call to this method in Java returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |Primary key id. |
|Fields |A map containing the returned field data. |
|Score |Indicates the degree to which the found vector matches the input vector. |

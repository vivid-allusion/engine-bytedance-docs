---
title: "Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_Search"
---

<span id="bc518c01"></span>
# Overview

To retrieve data from an index, you can use the `search` method. This API reference details the `SearchParam` object and its parameters, such as `VectorOrder`, `ScalarOrder`, and `Filter`, enabling you to perform vector similarity searches, scalar\-based searches, and apply complex filtering conditions.


* When the request parameter configures the vector field in the vector VectorOrder object, it indicates a vector search based on the vector field name.

* When the request parameter configures the primary key id in the vector VectorOrder object, the service searches for vectors similar to the one associated with that ID.

* When the request parameter configures the fieldName and order in the scalar ScalarOrder object, it indicates a scalar sorted search based on the scalar field name. The filter parameter is optional. You can use it to narrow down results for scalar\-based searches.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the Collection data is written/deleted, the Index data update time is expected to be 20s, and it cannot be retrieved immediately in the Index.</div>



<span id="b0b437a2"></span>
# **request parameters**

The request parameter is SearchParam, and the parameters contained in the SearchParam instance are shown in the following table.


|**parameter** |**type** |**Required** |**default value** |**parameter description** |
|---|---|---|---|---|
|VectorOrder |Map |No |*  |For VectorOrder, you must configure either the vector (optionally combined with sparse_vectors) or the ID, but not both.<br><br><br>* Vector: The name of the vector field. Use this for a search_by_vector operation to find similar vectors.<br><br>* sparse_vectors: sparse vectors, only for mixed indexes of search_by_vector.<br><br>* Id: The primary key ID. Use this for a search_by_id operation to find vectors similar to the one associated with this ID.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For hybrid indexes using the hnsw\-hybrid algorithm, id\-based retrieval is temporarily not supported.</div><br> |
|ScalarOrder |Map ||*  |Specify the scalar ScalarOrder object, the fieldName and order parameters must be configured together.<br><br><br>* fieldName: The name of the scalar field used for sorting.<br><br>* Order: Sort method, Order. Asc (ascending), Order. Desc (descending). |
|Filter |Map |No |*  |Filter conditions. For more information, see the scalar filtering documentation.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include must, must_not, range, range_out four types of query operators, including and and or two combinations of query operators. |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For hybrid retrieval, dense_weight is used to control the weight of dense vectors. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |
|outputFields |List\ < string \> |No |*  |Specifies a list of scalar or vector fields to include in the output.<br><br><br>* When outputFields is not passed, all scalar fields are returned, not vector fields.<br><br>* When outputFields is an empty list, the fields field is not returned.<br><br>* When outputFields is formatted incorrectly or a specified field does not exist in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The name of the partition. The data type of this parameter must match the fieldType of the partition key, and its value must correspond to a fieldValue of the partition key.<br><br><br>* When fieldType is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* When fieldType is string, list, partition input type is string, format requirement "^[a\-zA\-Z0\-9._]+$".\* n |


<span id="ffafac3e"></span>
# Example

<span id="c5c8c056"></span>
## Request parameters

```Java
// During program initialization, call this operation once to get a reference to the desired index. 
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
List datas = index.search(new SearchParam()
                                        .setVectorOrder(new VectorOrder().setVector(genRandomVector(12)).setSparseVector({"hello": 0.34, "world": 0.03, "!": 0.11}).build())
                                        .setOutputFields(outputField)
                                        .setFilter(filter)
                                        .setPartition("default");
                                        .setLimit(2)
                                        .build());

System.out.println(datas);

List datas = index.search(new SearchParam()
                                     .setVectorOrder(new VectorOrder().setId("22").build())
                                     .setPartition("default");
                                     .build());

System.out.println(datas);


List datas = index.search(new SearchParam()
                                 .setScalarOrder(new ScalarOrder("price", Order.Asc).build())
                                 .setPartition("default");
                                 .setLimit(2)
                                 .build());
System.out.println(datas);
```


<span id="3bd419e8"></span>
## Return value

The Java call for this operation returns a List. The properties contained in the DataObject instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |Primary key id. |
|Fields |The 'fields' field contains the returned data as a map. |
|Score |Indicates the degree to which the found vector matches the input vector. |

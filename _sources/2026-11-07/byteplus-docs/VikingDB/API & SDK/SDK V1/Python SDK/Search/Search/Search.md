---
title: "Search"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_Search"
---

<span id="0da582a0"></span>
# Overview

The Search API allows you to query an index to retrieve data based on various criteria. This reference explains how to perform vector searches to find items by semantic similarity, scalar searches to sort results by field values, and how to apply filters to refine your query. It provides detailed descriptions of all request parameters, Python code examples for both synchronous and asynchronous calls, and the data structure of the search results.


* When the request parameter order is configured as a vector field in the vector VectorOrder object, it indicates a vector search based on the vector field name.

* When the request parameter order is configured as the primary key id in the vector VectorOrder object, it indicates that the vector is retrieved according to the primary key id.

* When the request parameter order is configured as field_name and order in the scalar ScalarOrder object, it represents a scalar sorted search based on the name of the scalar field. The filter parameter is optionally configured to represent a scalar search.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the Collection data is written/deleted, the Index data update time is expected to be 20s, and it cannot be retrieved immediately in the Index.</div>


* <div data-tips="true" data-tips-type="tip">The asynchronous call uses the async_search interface, and the parameters remain unchanged.</div>



<span id="6263e059"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Order |Map |No |*  |Specify a vector VectorOrder object or a scalar ScalarOrder object, both**Choose one of the two**Configure.<br><br><br>* VectorOrder: both parameter vector and id**Choose one of the two**Configure.<br><br>   * Vector: vector field name, the scene is search_by_vector, according to the vector field name, search for similar vectors.<br><br>   * sparse_vectors: sparse vectors, only for mixed indexes of search_by_vector.<br><br>   * Id: primary key id, the scene is search_by_id, according to the primary key id, search for vectors similar to it.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For mixed indexes using hnsw\-hybrid, search_by_id usage is not supported.</div><br><br><br><br>* ScalarOrder: Parameters field_name and order required**simultaneous configuration**.<br><br>   * field_name: The name of the scalar field used for sorting.<br><br>   * Order: Sort method, Order. Asc (ascending), Order. Desc (descending). |
|Filter |Map |No |None |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include must, must_not, range, range_out four types of query operators, including and and or two combinations of query operators. |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|dense_weight |Float |No |0.5 |For scalar filtered retrieval, dense_weight used to control the weight of dense vectors in the retrieval. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index. |
|output_fields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* output_fields not passed, all scalar fields are returned, not vector fields.<br><br>* output_fields an empty list, the fields field is not returned.<br><br>* output_fields formatting error or the filter field is not a field in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The subindex name, the type is consistent with the field_type of the partition_by, and the field value corresponds to the field_value of the partition_by.<br><br><br>* field_type is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* field_type string, list\ < string \>, partition input type is string, format requirements "^ [a\-zA\-Z0\-9. _ ]+$"\*. n |


<span id="00d7126f"></span>
# Example

<span id="26a76850"></span>
## Request parameters

```Python
# Retrieve the specified index; call once during program initialization, no need to call repeatedly
index = vikingdb_service.get_index("example", "example_index")
```


```Python
def gen_random_vector(dim):
    res = [0, ] * dim
    for i in range(dim):
        res[i] = random.random() - 0.5
    return res
res = index.search(order=VectorOrder(gen_random_vector(10), "1"), limit=2,
                   output_fields=["doc_id", "like", "text_vector"],
                   partition="default", filter={"op": "range", "field": "price", "lt": 3.5})
                   
# Asynchronous call
async def search():
    index = vikingdb_service.get_index("async", "async")
    def gen_random_vector(dim):
        res = [0, ] * dim
        for i in range(dim):
            res[i] = random.random() - 0.5
        return res
    res = index.search(order=VectorOrder(gen_random_vector(10)), limit=2,
                       output_fields=["doc_id", "like", "text_vector"],
                       filter={"op": "range", "field": "price", "lt": 3.5})
    print("-----------search_vector---------")
    for item in res:
        print(item)
        print(item.score)
    print("-----------search_scalar---------")
    res = index.search(order=ScalarOrder("price", Order.Desc), limit=6,
                       output_fields=["price"],
                       filter={"op": "range", "field": "price", "lt": 5})
    for item in res:
        print(item)
        print(item.score)
    print("-----------search_None---------")
    res = index.search(limit=5, output_fields=["doc_id", "like"],
                        ilter={"op": "range", "field": "price", "lt": 3.5})
    for item in res:
         print(item.fields)
         print(item.score)
asyncio.run(search())
```


<span id="addd42cb"></span>
## Return value

The Python call performs the above task and returns List\ < Data \>. The properties contained in the Data instance are shown in the following table.


|**attribute** |**explain** |
|---|---|
|ID |Primary key id. |
|Fields |The fields field in the request return is the specific data, dictionary type. |
|Score |Indicates the degree to which the found vector matches the input vector. |

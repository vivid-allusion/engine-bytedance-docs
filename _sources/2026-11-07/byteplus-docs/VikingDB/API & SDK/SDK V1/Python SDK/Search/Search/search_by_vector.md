---
title: "search_by_vector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_search_by_vector"
---

<span id="ee860520"></span>
# Overview

The search_by_vector method retrieves the most similar vectors from an index based on a given query vector. You can use this method to perform a pure vector search or a hybrid search that combines vector similarity with scalar filtering. For non\-blocking operations, an asynchronous version, async_search_by_vector, is also available.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After data in a Collection is written or deleted, the index takes approximately 20 seconds to update. Data cannot be retrieved from the index during this period.</div>


* <div data-tips="true" data-tips-type="tip">Configuring the filter request parameter performs a mixed search. If the filter parameter is not configured, it performs a pure vector search.</div>


* <div data-tips="true" data-tips-type="tip">For asynchronous calls, use the async_search_by_vector interface. The parameters are the same as for the synchronous version.</div>



<span id="7531bfd0"></span>
# Prerequisite


* When creating a collection using the create_collection interface, ensure the fields definition includes a vector field.

* When writing data using the upsert_data interface, you must provide the field name and value for the vector field.

* When you create an index with create_index, a vector index must be created for the vector field.


<span id="408fb44d"></span>
# **request parameters**


|**parameter** |**type** |**Required** |**Default Value** |**Description** |
|---|---|---|---|---|
|Vector |Map |Yes |*  |Dense vector field for retrieval. |
|sparse_vectors |Map |Spa |*  |The sparse vector used for retrieval. The format is a dictionary, the key (a string) is the keyword and the value (a float) is the weight of the keyword. |
|dense_weight |Float |No |0.5 |For mixed search, dense_weight is used to control the weight of dense vectors in the search. The range is [0.2, 1]. Valid only if the index retrieved is a mixed index (IndexType.HNSW_HYBRID). |
|Filter |Map |No |None |Specifies the filter conditions. For more information, see **scalar filtering.** <br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four query operators (must, must_not, range, range_out) and two combination operators (and, or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|output_fields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* If output_fields is not passed, all scalar fields are returned, but vector fields are not.<br><br>* If output_fields is an empty list, the fields field is not returned.<br><br>* If output_fields has a formatting error or contains a field that is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is the normalized vector. |
|Partition |String/int |No |"Default" |The name of the sub\-index. The type of this value must be consistent with the field_type of the partition_by field, and the value itself must correspond to a field_value of the partition_by field.<br><br><br>* If field_type is int64 or list, the partition input type is int64.<br><br>* field_type string, list, partition input type is string, format requirements "^[a\-zA\-Z0\-9._]+$".\* n |


<span id="4e401273"></span>
# Example

<span id="92d4b8d5"></span>
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
res = index.search_by_vector(gen_random_vector(10), {"hello": 0.34, "world": 0.03, "!": 0.11},limit=2, dense_weight = 0.5, output_fields=["doc_id", "like", "text_vector"], partition="default") # Mixed search

res = index.search_by_vector(gen_random_vector(10),limit=2, output_fields=["doc_id", "like", "text_vector"], partition="default") # Pure dense search

# Asynchronous call
async def search_by_vector():
    def gen_random_vector(dim):
        res = [0, ] * dim
        for i in range(dim):
            res[i] = random.random() - 0.5
        return res
    index = await vikingdb_service.async_get_index("async", "async")
    res = await index.async_search_by_vector(gen_random_vector(10))
asyncio.run(search_by_vector())
```


<span id="75dffce1"></span>
## Return value

The Python call returns a Listobject. The properties contained in the Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key ID. |
|Fields |A dictionary containing the returned field data. |
|Score |The similarity score between the found vector and the input vector. |

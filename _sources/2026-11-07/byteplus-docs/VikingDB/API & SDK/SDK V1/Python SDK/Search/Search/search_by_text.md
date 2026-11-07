---
title: "search_by_text"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_search_by_text"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At present, the vector database has supported multi\-modal retrieval, which can directly search for text, text search images, image search images, etc. The original search_by_text interface can be migrated to <strong>search_with_multi_modal</strong></div>


<span id="7ed283f6"></span>
# Overview

To retrieve unstructured text data from a vector database, you can use the `search_by_text` method. This method allows you to search by providing input text, refine results with filters, and limit the number of returned items. It returns a list of matching data objects. Please note that this interface will be migrated to the more comprehensive `search_with_multi_modal` method, which supports multi\-modal retrieval.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently only unstructured data of text type is supported.</div>


* <div data-tips="true" data-tips-type="tip">After data in a Collection is written or deleted, the index update can take up to 20 seconds. During this period, the data cannot be retrieved from the index.</div>


* <div data-tips="true" data-tips-type="tip">The asynchronous call uses the async_search_by_text interface, and the parameters remain unchanged.</div>



<span id="34d4924b"></span>
# Prerequisite


* Configure vectorization using one of the following methods: 1. From the console, select a database type that supports vectorization and configure the vectorization field when creating the dataset. 2. When using the create_collection interface, configure vectorization for the Collection by setting the vectorize parameter.

* You have written data with text\-type fields and values using the upsert_data interface.

* You have created a vector index using the create_index operation.


<span id="658ffa0c"></span>
# **request parameters**


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Text |String |Yes |*  |The input text to search for. |
|Filter |Map |No |None |Filter conditions, see**scalar filtering**.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (must, must_not, range, and range_out) and two combination operators (and and or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|output_fields |List\ < string \> |No |*  |A list of scalar or vector fields to return.<br><br><br>* If output_fields is not passed, all scalar fields are returned, but vector fields are not.<br><br>* If output_fields is an empty list, the fields field is not returned.<br><br>* If output_fields is formatted incorrectly or contains a field that is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The subindex name, the type is consistent with the field_type of the partition_by, and the field value corresponds to the field_value of the partition_by.<br><br><br>* If field_type is int64 or list, the partition input type is int64.<br><br>* If field_type is string or list, the partition input type is string and must match the format "^[a\-zA\-Z0\-9._]+$".\* n |
|dense_weight |Float |No |0.5 |The weight of the dense vector in a hybrid search, where a value of 1 indicates a pure dense vector search. This parameter is valid only if the index is a hybrid index. The valid range is [0.2, 1].<br><br>Valid only if the index is a mixed index. Range [0.2, 1] |


<span id="8b959441"></span>
# Example

<span id="c50c31db"></span>
## Request parameters

```Python
# Retrieve the specified index. Call this once during program initialization and do not call it repeatedly
index = vikingdb_service.get_index("example_text", "example_index_text")
```


```Python
res = index.search_by_text(Text(text="this is five"), filter={"op": "range", "field": "price", "lt": 4}, limit=3, output_fields=["doc_id", "text", "price", "like"], partition="default")

async def search_by_text():
    index = await vikingdb_service.async_get_index("async", "async")
    res = await index.search_by_text(Text(text="this is five"), filter={"op": "range", "field": "price", "lt": 4}, limit=3, output_fields=["doc_id", "text", "price", "like"], partition= "default")
asyncio.run(search_by_text())
```


<span id="effd0309"></span>
## Return value

The Python call performs the above task and returns List\ < Data \>. The properties contained in the Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |Primary key id. |
|Fields |A dictionary containing the data for the fields specified in the output_fields parameter. |
|Score |Indicates the degree to which the found vector matches the input vector. |

---
title: "search_with_multi_modal"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/pysdk_search_with_multi_modal"
---

<span id="7ed283f6"></span>
# Overview

The search_with_multi_modal API enables multimodal data retrieval from your vector database. This document explains how you can use this API to search with text, images, or a combination of both, and details all relevant parameters like filter, limit, and output_fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently supports unstructured data of text and image types.</div>


* <div data-tips="true" data-tips-type="tip">After data in the Collection is written or deleted, the index takes approximately 20 seconds to update. Data cannot be retrieved from the index immediately.</div>


* <div data-tips="true" data-tips-type="tip">The asynchronous call uses the async_search_with_multi_modal interface, and the parameters remain unchanged.</div>



<span id="34d4924b"></span>
# Prerequisite


* Vectorization is configured for the collection, either by selecting a vectorized database type and configuring the vectorization field in the console, or by setting the vectorize parameter when using the create_collection interface.

* You have written data with text or image fields using the upsert_data interface.

* A vector index has been created using create_index.


<span id="658ffa0c"></span>
# **request parameters**


|**parameter** |**type** |**Required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Text |String |Select at least one of the text and image parameters |None |Retrieved input text. |
|Image |String |Select at least one of the text and image parameters |None |The input image currently supports 2 methods:<br><br><br>* A TOS link to the image.`tos://{bucket}/{object_key}`.<br><br>* A Base64\-encoded string.`base64://{Base64 string}`. |
|Filter |Map |No |None |Filter conditions. For details, see Scalar filtering.<br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions support four types of query operators (must, must_not, range, range_out) and two combination operators (and, or). |
|Limit |Int |No |10 |Number of search results, up to 5000. |
|output_fields |List\ < string \> |No |*  |Filter fields, specifying a list of scalar or vector fields to return.<br><br><br>* If output_fields is not passed, all scalar fields are returned, but vector fields are not.<br><br>* If output_fields is an empty list, the fields field is not returned.<br><br>* If output_fields is formatted incorrectly or contains a field that is not in the collection, the interface returns an error.<br><br><br>If the indexed distance mode is cosine, the vector returned by the vector field is a normalized vector. |
|Partition |String/int |No |"Default" |The name of the sub\-index. Its type must be consistent with the field_type of partition_by, and its value must correspond to the field_value of partition_by.<br><br><br>* field_type is int64 and list\ < int64 \>, the partition input type is int64.<br><br>* field_type string, list\ < string \>, partition input type is string, and must match the format "^[a\-zA\-Z0\-9._]+$".\* n |
|dense_weight |Float |No |0.5 |The weight of dense vectors in a mixed search, where 1 represents a pure dense search and 0 represents a pure literal search.<br><br>Valid only if the index is a mixed index. Range [0.2, 1] |
|need_instruction |Bool |No |Determined by the model default value, the <model_series_name\> models default to true, and other models default to false |For multimodal retrieval scenarios, whether to add instructions before the query when vectorizing the query. |


<span id="8b959441"></span>
# Example

<span id="c50c31db"></span>
## Request parameters

```Python
# Retrieve the specified index; call once during program initialization, no need to call repeatedly
index = vikingdb_service.get_index("example_text", "example_index_text")
```


```Python
datas = index.search_with_multi_modal(
    text="this is a test",  # Text input, representing the query content
    image="tos://{your_bucket}/{your_object}",  # Image input, specifying the image storage location
    limit=5,  # Set the maximum number of returned results to 5
    need_instruction=False
)

# Iterate through and output the search results
for data in datas:
    # Print the ID, field information, and relevance score of each result
    print(data.id, data.fields, data.score)
```


<span id="effd0309"></span>
## Return value

The Python call returns a Listobject. The properties contained in the Data instance are shown in the following table.


|**attribute** |**Description** |
|---|---|
|ID |The primary key ID. |
|Fields |A dictionary containing the returned fields. |
|Score |The relevance score, indicating the similarity between the result vector and the input vector. |

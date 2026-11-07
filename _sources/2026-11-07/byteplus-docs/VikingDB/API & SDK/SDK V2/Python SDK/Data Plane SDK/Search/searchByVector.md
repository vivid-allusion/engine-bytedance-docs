---
title: "searchByVector"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByVector_v2"
---

<span id="overview"></span>
# Overview

`search_by_vector` is used for vector search. Searches for the limit number of vectors closest to the query vector based on distance.


* After Collection data is written/deleted, Index data update takes approximately 20s, so it cannot be immediately retrieved from the Index.

* When the request parameter filter is configured, it indicates hybrid search; when filter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a collection via the create_collection interface, a vector field has been added to the defined fields.

* When writing data via the upsert_data interface, the field names and values of vector type have been written.

* When creating an index via create_index, a vector_index vector index has been created.


Applicable when selecting "Existing vector data" when creating a vector database: when the imported data is vectors, you can input vectors through this interface for search.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByVectorRequest`, with fields shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|dense_vector |List[float] |Yes |Dense vector for search, length must match the index dimension. |
|sparse_vector |Optional[Dict[str, float]] |No |Sparse vector representation (e.g., BOW), used for hybrid search with dense_vector. |
|filter |Optional[Dict[str, Any]] |No |Scalar filter conditions, see **Scalar Filtering** for details<br><br><br>* If not filled, indicates pure vector search.<br><br>* Supports operators like must, must_not, range, range_out, which can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. Returns all scalar fields in the collection when not set.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will error. |
|limit |Optional[int] |No |Limit on number of results returned, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default 0. Large values cause deep pagination performance overhead. |
|partition |Optional[str] |No |Search only the specified partition, default searches all partition data. |
|advance |Optional[SearchAdvance] |No |Advanced parameter collection (post_process_ops, ids_in, etc.), see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082)<br><br>. |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request trace ID. |
|code |Optional[str] |Service return code, Success indicates success. |
|message |Optional[str] |Error or prompt message. |
|api |Optional[str] |Name of the specific API called. |
|result |Optional[SearchResult] |Search result body, structure shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|data |List[SearchItemResult] |List of retrieved results, structure shown below. |
|filter_matched_count |Optional[int] |Total number of documents meeting the filter conditions. |
|total_return_count |Optional[int] |Number of results returned in this request. |
|real_text_query |Optional[str] |Actual query string after potential model correction. |
|token_usage |Dict[str, Any] |Token usage information. |



* SearchItemResult



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key value. |
|fields |Dict[str, Any] |Returned scalar field content. |
|score |Optional[float] |Final similarity score. |
|ann_score |Optional[float] |ANN coarse ranking score. |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

```python
import os

from vikingdb import IAM
from vikingdb.vector import SearchByVectorRequest, VikingVector

auth = IAM(
    ak=os.environ["VIKINGDB_AK"],
    sk=os.environ["VIKINGDB_SK"],
)
client = VikingVector(
    host=os.environ["VIKINGDB_HOST"],
    region=os.environ["VIKINGDB_REGION"],
    auth=auth,
    scheme="https",
)

index_client = client.index(
    collection_name=os.environ["VIKINGDB_COLLECTION"],
    index_name=os.environ["VIKINGDB_INDEX"],
)
request = SearchByVectorRequest(
    dense_vector=[0.5] * 1024,  # replace with real same-dim vector
    limit=5,
    output_fields=["title", "score"],
)
response = index_client.search_by_vector(request)
if response.result:
    for item in response.result.data:
        print(item.id, item.score, item.fields.get("title"))
```

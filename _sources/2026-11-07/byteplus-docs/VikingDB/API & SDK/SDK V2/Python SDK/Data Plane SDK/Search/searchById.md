---
title: "searchById"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchById_v2"
---

<span id="overview"></span>
# Overview

`search_by_id` is used for primary key id retrieval. Based on the primary key id, it searches for the limit number of vectors closest to it.


* For hybrid indexes using the hnsw\-hybrid algorithm, id\-based retrieval is temporarily not supported.

* After Collection data is written/deleted, Index data update takes approximately 20s and cannot be immediately retrieved in the Index.

* When the request parameter filter is configured, it indicates hybrid search; when the filter parameter is not configured, it indicates pure vector search.


<span id="prerequisites"></span>
# Prerequisites


* When creating a dataset through the create_collection interface, the defined fields have added vector fields.

* When writing data through the upsert_data interface, the field names and field values of vector type have been written.

* When creating an index through the create_index interface, a vector_index vector index has been created.


<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByIDRequest`, and its fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|id |Any |Yes |The primary key value to retrieve. |
|filter |Optional[Dict[str, Any]] |No |Scalar filter conditions, see **Scalar Filtering** for details.<br><br><br>* Not filled indicates pure vector search based on id.<br><br>* Supports operators such as must, must_not, range, range_out, and can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. When not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means not returning any scalar fields.<br><br>3. Field names must exist in the collection schema, otherwise the request will report an error. |
|limit |Optional[int] |No |Limit the number of returned items, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default 0, deep pagination performance overhead occurs when too large. |
|partition |Optional[str] |No |Only retrieve the specified partition, default to search all partitions. |
|advance |Optional[SearchAdvance] |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Retrieval Common Parameters](https://docs.byteplus.com/docs/84313/1927082)<br><br>. |


<span id="return-parameters"></span>
# Return Parameters


|Name |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request link ID. |
|code |Optional[str] |Service return code, Success indicates success. |
|message |Optional[str] |Error or prompt information. |
|api |Optional[str] |The specific API name called. |
|result |Optional[SearchResult] |Retrieval result body, structure is shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|data |List[SearchItemResult] |List of recalled results, structure is shown below. |
|filter_matched_count |Optional[int] |Total number of documents that meet the filter conditions. |
|total_return_count |Optional[int] |Number of results returned this time. |
|real_text_query |Optional[str] |The real query string possibly corrected by the model. |
|token_usage |Dict[str, Any] |Token metering information. |



* SearchItemResult



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key value. |
|fields |Dict[str, Any] |Returned scalar field content. |
|score |Optional[float] |Final similarity score. |
|ann_score |Optional[float] |ANN coarse ranking score. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import SearchByIDRequest, VikingVector

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
request = SearchByIDRequest(
    id=1234567890,
    limit=5,
    output_fields=["title", "score"],
)
response = index_client.search_by_id(request)
print(f"request_id={response.request_id}")
if response.result:
    for item in response.result.data:
        print(item.id, item.score, item.fields.get("title"))
```

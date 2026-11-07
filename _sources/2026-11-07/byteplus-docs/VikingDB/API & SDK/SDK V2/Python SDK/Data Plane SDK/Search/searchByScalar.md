---
title: "searchByScalar"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByScalar_v2"
---

<span id="overview"></span>
# Overview

This interface applies to indexes that contain int64/float32 type scalar index fields. Scalar search in a vector database refers to the search method based on scalar values. In a vector database, each vector has one or more scalar values. Scalar search can perform retrieval based on these scalar values to find data relevant to the query. For example, author feature search in document retrieval.

`search_by_scalar` returns results sorted/paginated by scalar field.

<span id="request-parameters"></span>
# Request Parameters

The request parameter is `SearchByScalarRequest`, whose fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|field |str |Yes |Scalar field used for sorting, must be int64/float32 and have a scalar index established. |
|order |Optional[str] |No |Sort direction, values `asc`/`desc`, default `desc`. |
|filter |Optional[Dict[str, Any]] |No |Scalar filter conditions, see **Scalar Filter** for details.<br><br><br>* If not filled, sorting is performed on the full index.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. When not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means returning no scalar fields.<br><br>3. The field name must exist in the collection schema, otherwise the request will throw an error. |
|limit |Optional[int] |No |Limit the number of returned entries, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default 0, deep pagination performance overhead occurs when too large. |
|partition |Optional[str] |No |Only search the specified partition, default searches all partitions. |
| | | | |
|advance |Optional[SearchAdvance] |No |Advanced parameter collection (post_process_ops, ids_in, etc.), see [Common Retrieval Parameters](https://docs.byteplus.com/docs/84313/1927082). |


<span id="return-parameters"></span>
# Return Parameters


|Name |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request chain ID. |
|code |Optional[str] |Service return code, Success indicates success. |
|message |Optional[str] |Error or prompt information. |
|api |Optional[str] |Name of the specific API called. |
|result |Optional[SearchResult] |Main retrieval result, structure shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|data |List[SearchItemResult] |List of retrieved results, structure shown below. |
|filter_matched_count |Optional[int] |Total number of documents that meet the filter conditions. |
|total_return_count |Optional[int] |Number of results returned this time. |
|real_text_query |Optional[str] |Real query string after possible model correction. |
|token_usage |Dict[str, Any] |Token metering information. |



* SearchItemResult



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key value. |
|fields |Dict[str, Any] |Content of the returned scalar fields. |
|score |Optional[float] |Final similarity score. |
|ann_score |Optional[float] |ANN coarse ranking score. |


<span id="example"></span>
# Example

```python
import os

from vikingdb import IAM
from vikingdb.vector import SearchByScalarRequest, VikingVector

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
request = SearchByScalarRequest(
    field="score",
    order="desc",
    limit=10,
    output_fields=["title", "score"],
)
response = index_client.search_by_scalar(request)
if response.result:
    for item in response.result.data:
        print(item.id, item.fields.get("score"))
```

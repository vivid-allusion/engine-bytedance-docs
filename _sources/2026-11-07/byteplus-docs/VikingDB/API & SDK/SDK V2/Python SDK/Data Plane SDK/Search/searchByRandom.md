---
title: "searchByRandom"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByRandom_v2"
---

<span id="overview"></span>
# Overview

Random search is a retrieval method that returns several random records from a dataset without specifying a query. Random search also supports filtering and post\-processing of search results, and can be used for scenarios such as comparing recall effects and data filtering.

`search_by_random` randomly returns a number of records from data that meets the filtering conditions.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByRandomRequest`, and its fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|filter |Optional[Dict[str, Any]] |No |Scalar filtering conditions, see **Scalar Filtering** for details.<br><br><br>* If not filled, random results will be returned from all data in the collection.<br><br>* Supports operators such as must, must_not, range, range_out, which can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. If not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will report an error. |
|limit |Optional[int] |No |Limit the number of returned records, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default 0. |
|partition |Optional[str] |No |Only search the specified partition, search all partitions by default. |
| | | | |
|advance |Optional[SearchAdvance] |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082) for details. |


<span id="response-parameters"></span>
# Response Parameters


|Name |Type |Description |
|---|---|---|
|request_id |Optional[str] |Request chain ID. |
|code |Optional[str] |Service return code, Success indicates success. |
|message |Optional[str] |Error or prompt message. |
|api |Optional[str] |Name of the specific API called. |
|result |Optional[SearchResult] |Search result body, structure shown below. |



* SearchResult



|Name |Type |Description |
|---|---|---|
|data |List[SearchItemResult] |List of recalled results, structure shown below. |
|filter_matched_count |Optional[int] |Total number of documents that meet the filtering conditions. |
|total_return_count |Optional[int] |Number of results returned this time. |
|real_text_query |Optional[str] |Real query string after possible model correction. |
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
import json

from vikingdb import IAM
from vikingdb.vector import SearchByRandomRequest, VikingVector

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
request = SearchByRandomRequest(
    limit=3,
    output_fields=["title"],
)
response = index_client.search_by_random(request)
print(f"request_id={response.request_id}")
# Print complete response JSON
print(response.model_dump_json(indent=2, by_alias=True) if hasattr(response, "model_dump_json") else json.dumps(response.model_dump(by_alias=True, mode="json"), ensure_ascii=False, indent=2, sort_keys=True))
```

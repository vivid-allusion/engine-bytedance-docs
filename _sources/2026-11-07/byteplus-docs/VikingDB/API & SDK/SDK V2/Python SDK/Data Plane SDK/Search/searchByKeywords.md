---
title: "searchByKeywords"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/searchByKeywords_v2"
---

<span id="overview"></span>
# Overview

`search_by_keywords` is used for keyword search, applicable to indexes with text field vectorization configuration (vectorize parameter), and supports searching with multiple keywords.

<span id="request-parameters"></span>
# **Request Parameters**

The request parameter is `SearchByKeywordsRequest`, and its fields are shown in the table below.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|keywords |Optional[List[str]] |Either/or |Tokenization results, list length 1\-10, elements cannot be empty strings. |
|query |Optional[str] |Either/or |Original search string, the SDK will perform tokenization on the server side. At least one of `query` or `keywords` must be provided. |
|case_sensitive |Optional[bool] |No |Whether to be case sensitive, default is False. |
|filter |Optional[Dict[str, Any]] |No |Scalar filtering conditions, see **Scalar Filtering** for details.<br><br><br>* Not filled means no filtering conditions are used.<br><br>* Supports operators such as must, must_not, range, range_out, and can be combined with and / or. |
|output_fields |Optional[List[str]] |No |List of scalar fields to return.<br><br><br>1. When not set, returns all scalar fields in the collection.<br><br>2. Passing an empty list means no scalar fields are returned.<br><br>3. Field names must exist in the collection schema, otherwise the request will report an error. |
|limit |Optional[int] |No |Limit the number of returned items, maximum 5000. |
|offset |Optional[int] |No |Pagination offset, default is 0. Excessively large values may cause deep pagination performance overhead. |
|partition |Optional[str] |No |Only search the specified partition, default searches all partitions. |
|advance |Optional[SearchAdvance] |No |Advanced parameter set (post_process_ops, ids_in, etc.), see [Common Search Parameters](https://docs.byteplus.com/docs/84313/1927082)<br><br>for details. |


<span id="return-parameters"></span>
# Return Parameters


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
|filter_matched_count |Optional[int] |Total number of documents that meet the filtering conditions. |
|total_return_count |Optional[int] |Number of results returned this time. |
|real_text_query |Optional[str] |The actual query string possibly corrected by the model. |
|token_usage |Dict[str, Any] |Token metering information. |



* SearchItemResult



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key value. |
|fields |Dict[str, Any] |Content of returned scalar fields. |
|score |Optional[float] |Final similarity score. |
|ann_score |Optional[float] |ANN coarse ranking score. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import SearchByKeywordsRequest, VikingVector

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
request = SearchByKeywordsRequest(
    keywords=["python"],
    case_sensitive=False,
    limit=5,
    output_fields=["title", "score"],
)
response = index_client.search_by_keywords(request)
if response.result:
    for item in response.result.data:
        print(item.id, item.fields.get("title"))
```

---
title: "fetchDataInIndex"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchDataInIndex_v2"
---

<span id="overview"></span>
# Overview

fetchDataInIndex is used for Index data query. It queries single or multiple data records in a specified Index based on the primary key id, with a maximum of 100 records per query.

After Collection data is written/deleted, there is a synchronization delay for Index data updates, typically around 10 seconds, so the data cannot be queried in the Index immediately.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Remarks |
|---|---|---|---|
|collection_name |str |2选1 |Collection name, choose one with resource_id. |
|resource_id |str | |Collection resource ID. |
|index_name |str |Yes |Index name. |
|ids |List[Any] |Yes |Primary key list for point query, maximum 100 records. |
|partition |Optional[str] |No |Filter index data by partition. |
|output_fields |Optional[List[str]] |No |Controls returned scalar fields:<br><br><br>1. Returns all scalar fields when not provided.<br><br>2. Returns only vectors and id when an empty list is passed.<br><br>3. An error will be thrown directly if the field does not exist or the format is incorrect. |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Response Body Common Parameters Introduction" below). The `result` field type is FetchDataInIndexResult:


* FetchDataInIndexResult



|Name |Type |Description |
|---|---|---|
|items |List[IndexDataItem] |Matched index data. |
|ids_not_exist |List[Any] |Primary keys that were not matched. |



* IndexDataItem



|Name |Type |Description |
|---|---|---|
|id |Any |Data primary key. |
|fields |Dict[str, Any] |Scalar fields. |
|dense_vector |Optional[List[float]] |Persisted dense vector. |
|dense_dim |Optional[int] |Vector dimension. |


<span id="response-body-common-parameters-introduction"></span>
## Response Body Common Parameters Introduction


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID. |
|code |string |Operation status code. `Success` for success, otherwise an error code phrase. |
|message |string |Execution information. `The API call was executed successfully.` on success. |
|result |map |Operation result. If no data needs to be returned, `result = null`. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import FetchDataInIndexRequest, VikingVector

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
request = FetchDataInIndexRequest(
    ids=[4798786918981052481, 8517775955036588997],  # IDs can be obtained from the console or searchByRandom API
    output_fields=["title", "score"],
)
response = index_client.fetch(request)
print(f"request_id={response.request_id}")
if response.result:
    for item in response.result.items:
        print(item.id, item.dense_dim, len(item.dense_vector or []))
```

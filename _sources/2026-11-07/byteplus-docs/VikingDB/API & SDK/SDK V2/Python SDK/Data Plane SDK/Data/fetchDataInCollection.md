---
title: "fetchDataInCollection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/fetchDataInCollection_v2"
---

<span id="overview"></span>
# Overview

Query single or multiple data entries in the specified Collection by primary key, up to 100 entries per query.

Data can be queried in real\-time after writing/deleting data in the Collection.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|collection_name |str |Either one is required |*  |Collection name, either this or resource_id must be provided. |
|resource_id |str | |*  |Collection resource ID. |
|ids |List[Any] |Yes |*  |List of primary keys to query, maximum 100 entries. |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Response Body Common Parameters Introduction" below). The `result` field type is FetchDataInCollectionResult:


* FetchDataInCollectionResult



|Name |Type |Description |
|---|---|---|
|items |List[DataItem] |List of matched data entries, structure shown below. |
|ids_not_exist |List[Any] |List of unmatched primary keys. |



* DataItem



|Name |Type |Description |
|---|---|---|
|id |Any |Primary key of the data. |
|fields |Dict[str, Any] |All scalar fields, key is the field name. |


<span id="response-body-common-parameters-introduction"></span>
## Response Body Common Parameters Introduction


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID. |
|code |string |Operation status code. `Success` on success, otherwise an error code phrase. |
|message |string |Execution information. `The API call was executed successfully.` on success. |
|result |map |Operation result. If no data needs to be returned, `result = null`. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import FetchDataInCollectionRequest, VikingVector

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

collection_client = client.collection(collection_name=os.environ["VIKINGDB_COLLECTION"])
request = FetchDataInCollectionRequest(
    ids=[4798786918981052481, 8517775955036588997], # get ID from console or searchByRandom API
)
response = collection_client.fetch(request)
print(f"request_id={response.request_id}")
if response.result:
    for item in response.result.items:
        print(item.id, item.fields)
```

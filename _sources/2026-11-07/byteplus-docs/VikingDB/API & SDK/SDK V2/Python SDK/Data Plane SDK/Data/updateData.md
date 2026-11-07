---
title: "updateData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/updateData_v2"
---

<span id="overview"></span>
# Overview

updateData is used to update partial fields of existing data, supporting updates for text, scalar fields, and vector fields.

<span id="request-parameters"></span>
# **Request Parameters**


|Name |Type |Description |Required |
|---|---|---|---|
|collection_name |str |Collection name, either this or resource_id must be provided. |Either one is required |
|resource_id |str |Resource ID of the Collection. | |
|data |List[Dict[str, Any]] |List of data to be updated, maximum 100 entries per request. Must include primary key field and fields to be modified. |Yes |
|ttl |int |New time\-to\-live after update, in seconds. |No |
|ignore_unknown_fields |bool |When True, ignores fields not declared in the schema. All fields are validated by default. |No |


<span id="response-parameters"></span>
# Response Parameters

The response body contains common parameters (see "Common Response Body Parameters" below). The `result` field type is UpdateDataResult:


* UpdateDataResult



|Name |Type |Description |
|---|---|---|
|token_usage |Dict[str, Any] |Token usage statistics for this update operation. |


<span id="common-response-body-parameters"></span>
## Common Response Body Parameters


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID. |
|code |string |Operation status code. Returns `Success` on success, otherwise returns an error code phrase. |
|message |string |Execution information. Returns `The API call was executed successfully.` on success. |
|result |map |Operation result. If no data needs to be returned, `result = null`. |


<span id="example"></span>
# Example

<span id="request-parameters"></span>
## Request Parameters

```python
import os

from vikingdb import IAM
from vikingdb.vector import UpdateDataRequest, VikingVector

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

ID = "2532745373549703702"
request = UpdateDataRequest(
    data=[{"__AUTO_ID__": ID, "score": 47.0, "text": "updated"}], # Get ID from console or searchByRandom API
    ignore_unknown_fields=True,
)
response = collection_client.update(request)
print(f"request_id={response.request_id}")
if response.result:
    print(response.result.token_usage)
```

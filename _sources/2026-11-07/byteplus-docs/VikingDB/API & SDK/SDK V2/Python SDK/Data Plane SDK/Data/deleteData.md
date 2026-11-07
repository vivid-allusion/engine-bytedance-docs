---
title: "deleteData"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/deleteData_v2"
---

<span id="overview"></span>
# Overview

deleteData is used to delete data in a specified Collection, deleting single or multiple data entries by primary key. A maximum of 100 data entries can be deleted in a single request.

<span id="request-parameters"></span>
# **Request Parameters**


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|collection_name |str |Either/or |Collection name, either this or resource_id must be provided. |
|resource_id |str | |Resource ID corresponding to the Collection. |
|ids |List[Any] |Either/or |List of primary keys to delete (int or str), maximum 100 entries. An invalid request will fail entirely. |
|delete_all |Optional[bool] | |Corresponds to API field `del_all`. When set to True, all data in the Collection will be deleted (there may be a short delay in index synchronization). |


<span id="response-parameters"></span>
# Response Parameters

This interface only returns common parameters, and `result` is always `null` (see "Common Response Body Parameters" below for details).

<span id="common-response-body-parameters"></span>
## Common Response Body Parameters


|Parameter Name |Type |Description |
|---|---|---|
|request_id |string |Request ID. |
|code |string |Operation status code. Returns `Success` on success, or an error code phrase otherwise. |
|message |string |Execution information. Returns `The API call was executed successfully.` on success. |
|result |map |Operation result. For this interface, `result` is always `null`. |


<span id="example"></span>
# Example

<span id="request-example"></span>
## Request Example

```python
import os

from vikingdb import IAM
from vikingdb.vector import DeleteDataRequest, VikingVector

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
request = DeleteDataRequest(ids=[2532745373549703702])
response = collection_client.delete(request)
print(f"request_id={response.request_id}")
```

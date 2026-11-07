---
title: "DeleteMemoryCollection - Deletes memory"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteMemoryCollection_-_Deletes_memory"
---

You can call this operation to delete a memory.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: DeleteMemoryCollection`

The action that you want to perform. Value: DeleteMemoryCollection.



**Version ** <span data-label="purple">string   </span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**MemoryId ** <span data-label="purple">string   </span>`Sample value: mem-17616225****`

Memory ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-17616225****`

Memory ID.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: mem-294775****`

ID of the imported memory.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Type of the imported memory. Value:


* VIKINGDB_MEMORY: Viking LTM.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Memory status. Value:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Deleted.

* Error: Error.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteMemoryCollection&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "MemoryId": "mem-1761138****"
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DeleteMemoryCollection",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MemoryId": "mem-1761138****",
    "ProviderCollectionId": "mem-294775****",
    "ProviderType": "VIKINGDB_MEMORY",
    "Status": "Deleting"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MemoryId |The required parameter MemoryId is not supplied. |The parameter MemoryId cannot be empty. |

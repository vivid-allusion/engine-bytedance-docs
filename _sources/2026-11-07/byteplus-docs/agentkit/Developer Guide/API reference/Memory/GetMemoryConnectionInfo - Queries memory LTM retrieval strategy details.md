---
title: "GetMemoryConnectionInfo - Queries memory LTM retrieval strategy details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetMemoryConnectionInfo_-_Queries_memory_LTM_retrieval_strategy_details"
---

You can call this API to query the LTM extraction strategy details of a memory.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: GetMemoryConnectionInfo`

The action that you want to perform. Value: GetMemoryConnectionInfo.



**Version ** <span data-label="purple">string   </span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**MemoryId ** <span data-label="purple">string   </span>`Sample value: viking-176113869****`

Memory ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ConnectionInfos ** <span data-label="purple">object[] </span>`Sample value: --`

Information about the LTM extraction strategies.


**AddrType ** <span data-label="purple">string </span>`Sample value: PUBLIC`

Network address type. Value:


* PUBLIC: Public network.



**AuthKey ** <span data-label="purple">string </span>`Sample value: key-123`

The authentication key.



**AuthType ** <span data-label="purple">string </span>`Sample value: APIKEY`

Authentication type. Value:


* BEARER_TOKEN: Use the value in AuthKey as the Bearer token.

* APIKEY: Use the value in AuthKey as the Authorization header.

* AK_SK: Use the standardized signature value of your BytePlus AK/SK as the Authorization header.



**BaseUrl ** <span data-label="purple">string </span>`Sample value: https://base.url`

The base URL address of the memory platform.



**ExpireAt ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Expiration time of the authentication information.



**Status ** <span data-label="purple">string </span>`Sample value: AVAILABLE`

Connection status. Value:


* AVAILABLE: Connected.

* CREATING: Connecting.

* UNAVAILABLE: Connection failed.




**Managed ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the memory is managed by the AgentKit platform. Value: 


* true: Indicates that the memory is created by the AgentKit platform. When the memory is deleted, the corresponding platform resources are also deleted.

* false: Indicates that the memory is imported from the provider platform. When the memory is deleted, the corresponding platform resources are retained.



**MemoryId ** <span data-label="purple">string </span>`Sample value: viking-176113869****`

Memory ID.



**Message ** <span data-label="purple">string </span>`Sample value: No ready endpoints.`

Status message, containing additional status information or error description.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: viking-176113869****`

ID of the imported memory.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Memory type. Value:


* VIKINGDB_MEMORY: Viking LTM.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Memory status. Value:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: Error.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetMemoryConnectionInfo&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "MemoryId": "mem-17611386****"
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetMemoryConnectionInfo",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MemoryId": "viking-176113869****",
    "ProviderCollectionId": "viking-176113869****",
    "ProviderType": "VIKINGDB_MEMORY",
    "Status": "Ready",
    "ConnectionInfos": [
      {
        "BaseUrl": "https://base.url",
        "AuthType": "APIKEY",
        "AuthKey": "api-key",
        "ExpireAt": ""
      }
    ],
    "Managed": "true",
    "Message": "Collection is ready for use"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MemoryId |The required parameter MemoryId is not supplied. |The MemoryId parameter cannot be left empty. |

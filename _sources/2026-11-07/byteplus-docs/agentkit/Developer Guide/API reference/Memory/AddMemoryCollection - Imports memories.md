---
title: "AddMemoryCollection - Imports memories"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AddMemoryCollection_-_Imports_memories"
---

You can call this operation to import memories.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|S9HCmC">必选</span> `Sample value: AddMemoryCollection`

The action that you want to perform. Value: AddMemoryCollection.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|FxBgQU">必选</span> ` Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ClientToken**<span data-label="purple"> string</span>` Optional Sample value: 333339fe****`

The ClientToken is used to ensure request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Collections.N.ProviderCollectionId ** <span data-label="purple">string[] </span><span data-api-tag="require|JMiehX">必选</span> `Sample value: m-123`

ID of the memory to be imported.


* Parameter \- N: indicates the serial number of the memory.

* Separate multiple field names with ampersands (&).


Value:


* Viking: Enter ResourceId.



**Collections.N.Description ** <span data-label="purple">string[]</span>` Optional Sample value: knmemory-test`

Description of the memory to be imported.


* Parameter \- N: indicates the serial number of the memory.

* Up to 200 characters are allowed. If not specified, it is left empty by default.

* Separate multiple field names with ampersands (&).



**Collections.N.Name ** <span data-label="purple">string[] </span>`Optional Sample value: my_collection`

Name of the memory to be imported.


* Parameter \- N: indicates the serial number of the memory.

* Separate multiple field names with ampersands (&).


Value:


* Viking: Enter CollectionName.



**Collections.N.ProjectName**<span data-label="purple"> string[] </span>`Optional Sample value: default`

Name of the associated project.


* Parameter \- N: indicates the serial number of the memory.

* Separate multiple field names with ampersands (&).



**Collections.N.ProviderType ** <span data-label="purple">string[] </span>`Optional Sample value: VIKINGDB_MEMORY`

Type of the memory to be imported.


* Parameter \- N: indicates the serial number of the memory.

* Separate multiple field names with ampersands (&).

* Value:

   * VIKINGDB_MEMORY: Viking LTM.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Collections ** <span data-label="purple">object[] </span>`Sample value: --`

Information of the imported memory.


**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-17616225****`

Memory ID.



**Message ** <span data-label="purple">string </span>`Sample value: The collection is not ready.`

Detailed information of the current status, as a supplement to the release status. For example, the cause of a startup failure.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: mem-294775****`

ID of the imported memory.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Type of the imported memory platform.



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
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=AddMemoryCollection&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "Collections": [
      {
        "ProviderType": "VIKINGDB_MEMORY",
        "ProviderCollectionId":"mem-294775****"
      }
    ]
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "AddMemoryCollection",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Collections": [
      {
        "MemoryId": " mem-1761138****",
        "ProviderCollectionId": "mem-294775****",
        "ProviderType": "VIKINGDB_MEMORY",
        "Status": "Ready",
        "Message": ""
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name is invalid. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |InvalidProviderCollectionId.Malformed |The specified ProviderCollectionId is malformed. |The specified ProviderCollectionId is invalid. |
|400 |InvalidRegion.Malformed |The specified Region is malformed. |The specified Region is invalid. |
|400 |LimitExceeded.MaximumCollections |The number of specified Collections exceeds the maximum limit. |The specified Collections exceed the upper limit. |
|400 |MissingParameter.Collections |The required parameter Collections is not supplied. |The parameter Collections cannot be empty. |
|400 |MissingParameter.ProviderCollectionId |The required parameter ProviderCollectionId is not supplied. |The parameter ProviderCollectionId cannot be empty. |

---
title: "GetMemoryCollection - Queries memory details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetMemoryCollection_-_Queries_memory_details"
---

You can call this operation to query memory details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|khlDgT">必选</span> `Sample value: GetMemoryCollection`

The action that you want to perform. Value: GetMemoryCollection.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|QR7DGy">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MemoryId ** <span data-label="purple">string </span><span data-api-tag="require|vOan9m">必选</span> `Sample value: mem-17616225****`

Memory ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

List of associated runtimes.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye9tu7****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: runtime-01`

Runtime name.




**CreateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Creation time of the memory.



**Description ** <span data-label="purple">string </span>`Sample value: memory-test`

Memory description.



**LastUpdateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Update time of the memory.



**LongTermConfiguration ** <span data-label="purple">object </span>`Example value: --`

Information about the LTM extraction strategies.


**Strategies ** <span data-label="purple">object[] </span>`Sample value: --`

List of LTM extraction strategies.


**CustomExtractionInstructions ** <span data-label="purple">string </span>`Sample value: Summarize facts.`

The system prompt for a custom strategy.



**Name ** <span data-label="purple">string </span>`Sample value: s_1`

Name of the LTM extraction strategy.



**Type ** <span data-label="purple">string </span>`Sample value: Summary`

Type of the LTM extraction strategy. Value:


* Summary: Session summary (session level).

* Semantic: Semantic memory (user level).

* UserPreference: User preference (user level).





**Managed ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the memory is managed by the AgentKit platform. Value: 


* true: Indicates that the memory is created by the AgentKit platform. When the memory is deleted, the corresponding platform resources are also deleted.

* false: Indicates that the memory is imported from the provider platform. When the memory is deleted, the corresponding platform resources are retained.



**MemoryId ** <span data-label="purple">string </span>`Sample value: mem-17616225****`

Memory ID.



**Name ** <span data-label="purple">string </span>`Sample value: my_collection`

Memory name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the project associated with the memory.



**ProviderCollectionId ** <span data-label="purple">string </span>`Sample value: mem-294775****`

Viking memory ID.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_MEMORY`

Memory type. Value:


* VIKINGDB_MEMORY: Viking LTM.



**Region ** <span data-label="purple">string </span>`Sample value: ap-southeast-1`

Region of the memory.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Memory status. Value:


* Creating: Being created.

* CreateFailed: Creation failed.

* Ready: Available for use.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: An error occurred.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

Memory tags.


**Type ** <span data-label="purple">string </span>`Sample value: custom`

Tag type.


* system: system tag

* custom: user tag



**Key ** <span data-label="purple">string </span>`Sample value: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Sample value: v1`

The tag value.




**Trn ** <span data-label="purple">string </span>`Sample value: trn:agentkit:ap-southeast-1:210000:memory:mem-****`

TRN of the memory.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetMemoryCollection&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  "MemoryId": "mem-1761138****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetMemoryCollection",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MemoryId": "mem-1761138****",
    "Name": "my_collection",
    "Description": "memory-test",
    "Trn": "trn:appo:memory:ap-southeast-1:123456:memory/mem-1761138****",
    "ProviderCollectionId": "mem-294775****",
    "ProviderType": "VIKINGDB_MEMORY",
    "Status": "Ready",
    "LongTermConfiguration": {
      "Strategies": [
        {
          "Type": "Summary",
          "CustomExtractionInstructions": "Extract key information from conversation",
          "Name": "agentkit_semantic_v1"
        }
      ]
    },
    "LastUpdateTime": "2025-09-16T10:05:00Z",
    "Managed": "true",
    "CreateTime": "2025-09-16T10:00:00Z"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MemoryId |The required parameter MemoryId is not supplied. |The parameter MemoryId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |

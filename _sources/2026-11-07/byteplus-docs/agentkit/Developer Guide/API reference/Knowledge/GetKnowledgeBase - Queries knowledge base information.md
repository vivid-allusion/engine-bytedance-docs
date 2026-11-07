---
title: "GetKnowledgeBase - Queries knowledge base information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetKnowledgeBase_-_Queries_knowledge_base_information"
---

You can call this operation to query knowledge base information.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: GetKnowledgeBase`

The action that you want to perform. Value: GetKnowledgeBase.



**Version ** <span data-label="purple">string   </span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**KnowledgeId ** <span data-label="purple">string   </span>`Sample value: kb-4yds45****`

Knowledge base ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AssociatedRuntimes ** <span data-label="purple">object[] </span>`Sample value: --`

List of associated runtimes.


**Id ** <span data-label="purple">string </span>`Sample value: r-ye9tu7****`

ID of the runtime.



**Name ** <span data-label="purple">string </span>`Sample value: runtime-01`

Runtime name.




**CreateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Creation time of the knowledge base.



**Description ** <span data-label="purple">string </span>`Sample value: sample description.`

Description of the knowledge base.



**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-4yds45****`

Knowledge base ID.



**LastUpdateTime ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Update time of the knowledge base.



**Name ** <span data-label="purple">string </span>`Sample value: my_knowledge`

Knowledge base name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The project associated with the runtime.



**ProviderKnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

ID of the imported knowledge base.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_KNOWLEDGE`

Type of the knowledge base platform. Value:


* VIKINGDB_KNOWLEDGE: Viking knowledge base



**Region ** <span data-label="purple">string </span>`Sample value: cn-beijing`

Region of the knowledge base.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Knowledge base status. Value:


* Ready: Available for use

* Deleted: Resource expired

* Error: Abnormal status



**Trn ** <span data-label="purple">string </span>`Sample value: trn:agentkit:cn-beijing:210000:knowledge:kb-****`

A unique resource ID within BytePlus.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetKnowledgeBase&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  "PageNumber": 1
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetKnowledgeBase",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AssociatedRuntimes": {
      "Id": "r-ye9tu7****",
      "Name": "runtime-01"
    }
    "CreateTime": "2025-09-16T10:00:00Z",
    "Description": "",
    "KnowledgeId": "kb-4yds45****",
    "LastUpdateTime": "2025-09-16T10:05:00Z",
    "Name": "my_knowledge",
    "ProjectName": "default",
    "ProviderKnowledgeId": "kb-travel-001",
    "ProviderType": "VIKINGDB_KNOWLEDGE",
    "Region": "cn-beijing",
    "Name": "my_knowledge",
    "Trn": "trn:agentkit:cn-beijing:210000:knowledge:kb-****",
    "Status": "Ready"
    }
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.KnowledgeId |The required parameter KnowledgeId is not supplied. |The parameter KnowledgeId cannot be empty. |

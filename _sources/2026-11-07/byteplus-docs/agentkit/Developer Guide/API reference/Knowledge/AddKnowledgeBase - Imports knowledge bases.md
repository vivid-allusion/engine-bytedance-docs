---
title: "AddKnowledgeBase - Imports knowledge bases"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AddKnowledgeBase_-_Imports_knowledge_bases"
---

You can call this API to import a knowledge base. For operation instructions and precautions, refer to the [Import knowledge base](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases#AXRPmjaf).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|1gMvMo">必选</span> `Sample value: AddKnowledgeBase`

The action that you want to perform. Value: AddKnowledgeBase.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|oHATrZ">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 23fa21A8823nfasd7f****`

The ClientToken is used to ensure the request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**KnowledgeBases.N.Name ** <span data-label="purple">string[] </span><span data-api-tag="require|DZBFmN">必选</span> `Sample value: knowledge_viking`

Name of the knowledge base to be imported.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* Separate multiple field names with ampersands (&).

* Value:

   * For a Viking knowledge base, CollectionName is required.



**KnowledgeBases.N.ProviderKnowledgeId ** <span data-label="purple">string[] </span><span data-api-tag="require|0GPLMX">必选</span> `Sample value: kb-ye7s2g****`

ID of the knowledge base to be imported.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* Separate multiple field names with ampersands (&).

* Value:

   * For a Viking knowledge base, use ResourceId.



**KnowledgeBases.N.ProviderType ** <span data-label="purple">string[] </span><span data-api-tag="require|fiEPIo">必选</span> `Sample value: VIKINGDB_KNOWLEDGE`

The type of knowledge base platform to be imported.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* Separate multiple field names with ampersands (&).

* Value:

   * VIKINGDB_KNOWLEDGE: Viking knowledge base



**KnowledgeBases.N.Description**<span data-label="purple"> string[] </span>`Optional Sample value: knowledge-test`

Description of the knowledge base to be imported.


* Parameter \- N: Indicates the serial number of the knowledge base. Value range: 1–10.

* If left blank, the parameter defaults to an empty value.

* Separate multiple field names with ampersands (&).



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

Name of the project associated with the knowledge base. If not specified, the default value is "default".



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**KnowledgeBases ** <span data-label="purple">object[] </span>`Sample value: --`

Knowledge base information.


**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-4yds45****`

Knowledge base ID.



**Message ** <span data-label="purple">string </span>`Sample value: The knowledgebase is not ready.`

Message about knowledge base status, containing additional status information or error description.



**ProviderKnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

ID of the imported knowledge base.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_KNOWLEDGE`

The type of the imported knowledge base platform.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Knowledge base status. Value:


* Importing: Importing.

* ImportFailed: Import failed.

* Ready: Succeeded.

* Deleting: Being deleted.

* DeleteFailed: Deletion failed.

* Deleted: Resource expired.

* Error: Error.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=AddKnowledgeBase&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "KnowledgeBases":[
      {
        "ProviderType": "VIKINGDB_KNOWLEDGE",
        "Name": "name1",
        "ProviderKnowledgeId": "kb-ye7s2g****"
      }
    ],
    "ClientToken": "abc123def456"
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "AddKnowledgeBase",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "KnowledgeBases": [
      {
        "KnowledgeId": "kb-4yds45***",
        "ProviderKnowledgeId": "kb-ye7s2g****",
        "ProviderType": "VIKINGDB_KNOWLEDGE",
        "Status": "Ready",
        "Message": "Knowledge base is ready"
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
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified description is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name is invalid. |
|400 |LimitExceeded.MaximumKnowledgeBases |The number of specified KnowledgeBases exceeds the maximum limit. |The specified KnowledgeBases exceeds the upper limit. |
|400 |LimitExceeded.MinimumKnowledgeBases |The number of specified KnowledgeBases exceeds the minimum limit. |The specified KnowledgeBases exceeds the lower limit. |
|400 |MissingParameter.KnowledgeBases |The required parameter KnowledgeBases is not supplied. |The parameter KnowledgeBases cannot be empty. |
|400 |MissingParameter.Name |The required parameter Name is not supplied. |Name cannot be empty. |
|400 |MissingParameter.ProviderKnowledgeId |The required parameter ProviderKnowledgeId is not supplied. |The parameter ProviderKnowledgeId cannot be empty. |
|400 |InvalidParameter.UnsupportedProviderType |The specified provider type is not supported. |The specified provider type is not supported. |

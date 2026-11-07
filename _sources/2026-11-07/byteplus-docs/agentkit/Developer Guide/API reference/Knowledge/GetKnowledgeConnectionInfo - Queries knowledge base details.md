---
title: "GetKnowledgeConnectionInfo - Queries knowledge base details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetKnowledgeConnectionInfo_-_Queries_knowledge_details"
---

You can call this API to query knowledge base details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span>`Sample value: GetKnowledgeConnectionInfo`

The action that you want to perform. Value: GetKnowledgeConnectionInfo.



**Version ** <span data-label="purple">string   </span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**KnowledgeId ** <span data-label="purple">string   </span>`Sample value: kb-4yds45****`

Knowledge base ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ConnectionInfos ** <span data-label="purple">object[] </span>`Sample value: --`

Connection information of the knowledge base.


**AddrType ** <span data-label="purple">string </span>`Sample value: PUBLIC`

Network address type. Value:


* PUBLIC: Public network.



**AuthKey ** <span data-label="purple">string </span>`Sample value: my-key`

The key used for authentication.



**AuthType ** <span data-label="purple">string </span>`Sample value: BEARER_TOKEN`

Authentication type. Value:


* BEARER_TOKEN: Use the value in AuthKey as the Bearer token.

* APIKEY: Use the value in AuthKey as the Authorization header.

* AK_SK: Use the standardized signature value of your BytePlus AK/SK as the Authorization header.



**BaseUrl ** <span data-label="purple">string </span>`Sample value: https://base.url`

The base URL address of the knowledge base platform.



**ExpireAt ** <span data-label="purple">string </span>`Sample value: 2025-09-17T10:00:00+8:00`

Expiration time of the authentication information.



**ExtraConfig ** <span data-label="purple">string </span>`Sample value: {}`

Additional platform\-specific configuration. (JSON format)



**Region ** <span data-label="purple">string </span>`Sample value: cn-beijing`

Service region.



**Status ** <span data-label="purple">string </span>`Sample value: VAILABLE`

Connection status. Value:


* AVAILABLE: Available.

* CREATING: Creating.

* UNAVAILABLE: Unavailable.




**KnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-4yds45****`

Knowledge base ID.



**Message ** <span data-label="purple">string </span>`Sample value: No ready endpoints.`

Status message, containing additional status information or error description.



**Name ** <span data-label="purple">string </span>`Sample value: my_collection`

Knowledge base name.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

Name of the project associated with the imported knowledge base.



**ProviderKnowledgeId ** <span data-label="purple">string </span>`Sample value: kb-ye7s2g****`

ID of the project associated with the imported knowledge base.



**ProviderType ** <span data-label="purple">string </span>`Sample value: VIKINGDB_KNOWLEDGE`

The platform type of the imported knowledge base platform. Value:


* VIKINGDB_KNOWLEDGE: Viking knowledge base.



**Status ** <span data-label="purple">string </span>`Sample value: Ready`

Knowledge base status. Value:


* Importing: Importing.

* ImportFailed: Importing failed.

* Ready: Succeeded.

* Deleting: It is being deleted.

* DeleteFailed: Deletion failed.

* Deleted: It is deleted.

* Error: Exception occurs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetKnowledgeConnectionInfo&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
  {
    "KnowledgeId": "kb-4yds45****"
  }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "GetKnowledgeConnectionInfo",
    "Version": "2025-10-10",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "KnowledgeId": "kb-4yds45****",
    "ProviderKnowledgeId": "kb-ye7s2g****",
    "ProviderType": "VIKINGDB_KNOWLEDGE",
    "Status": "Ready",
    "ConnectionInfos": [
      {
        "BaseUrl": "https://viking****.volces.com",
        "Region": "cn-beijing",
        "AuthType": "BEARER_TOKEN",
        "AuthKey": "ak-abc123d****",
        "ExpireAt": "2025-09-17T10:00:00Z",
        "ExtraConfig": "{\"endpoint\":\"https://custom.endpoint.com\"}"
      }
    ],
    "Message": "Knowledge base is ready for use",
    "ProjectName": "default",
    "Name": "my_travel_knowledge"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.KnowledgeId |The required parameter KnowledgeId is not supplied. |The parameter KnowledgeId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

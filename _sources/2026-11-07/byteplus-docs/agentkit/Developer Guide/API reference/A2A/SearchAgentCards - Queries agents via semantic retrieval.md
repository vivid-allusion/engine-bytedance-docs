---
title: "SearchAgentCards - Queries agents via semantic retrieval"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/SearchAgentCards_-_Queries_agents_via_intent_recognition"
---

Query A2A agents in an A2A agent space via semantic retrieval.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|a3uWyY">必选</span> `Sample value: SearchAgentCards`

The operation that you want to perform. Value: SearchAgentCards.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|9zy9HR">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**SpaceId ** <span data-label="purple">string </span><span data-api-tag="require|ZXldEd">必选</span> `Sample value: as-yeglyhjytc3srhse****`

The space of the A2A agents.



**Prompt ** <span data-label="purple">string </span><span data-api-tag="require|z5bW9O">必选</span> `Sample value: write a book`

The prompt used to search for target A2A agents in the A2A agent space.



**TopK ** <span data-label="purple">integer </span><span data-api-tag="require|fubddt">必选</span> `Sample value: 10`

Limits the number of agents returned and only returns the top K results with the highest match scores.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 6`

The total number of returned A2A agents.



**AgentCards ** <span data-label="purple">string </span>`Sample value: --`

The JSON text of the A2A agents.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=SearchAgentCards&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T124821Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "SpaceId": "as-yeglyhjytc3srhse****",
  "Prompt": "write a book",
  "TopK": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260309204825168158121125B****",
    "Action": "SearchAgentCards",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 6,
    "AgentCards": "--"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

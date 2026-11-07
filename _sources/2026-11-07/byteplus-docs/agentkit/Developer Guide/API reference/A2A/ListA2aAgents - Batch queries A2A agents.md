---
title: "ListA2aAgents - Batch queries A2A agents"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListA2aAgents_-_Batch_queries_A2A_agents"
---

Batch query A2A agents.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|GAYUWM">必选</span> `Sample value: ListA2aAgents`

The operation that you want to perform. Value: ListA2aAgents.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|FV13rx">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



**Filter ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The agent filter.


**Id ** <span data-label="purple">string </span>`Optional` `Sample value: a-yeh4hhuscg30lppp****`

The ID of the A2A agent.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: Agent`

The name of the A2A agent.



**Version ** <span data-label="purple">string </span>`Optional` `Sample value: 1.0.0`

The version of the A2A agent.



**Skill ** <span data-label="purple">string </span>`Optional` `Sample value: chat`

The Skills of the A2A agent.



**Source ** <span data-label="purple">string[] </span>`Optional` `Sample value: ["Runtime"]`

The registration source of the A2A agent.


* Runtime: The A2A agent in the agent runtime is registered to an A2A agent space via the agent runtime address.

* Standard: The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.




**SpaceId ** <span data-label="purple">string </span><span data-api-tag="require|JwHbEE">必选</span> `Sample value: as-yeglyhjytc3srhse****`

The ID of the A2A agent space.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the project associated with the A2A agent.



**TagFilters ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tag filters.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|aziC6G">必选</span> `Sample value: key1`

The key of the tag.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|yqInN0">必选</span> `Sample value: value1`

The value of the tag.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of A2A agents that meet the conditions.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The details of the agents.


**Id ** <span data-label="purple">string </span>`Sample value: a-yeh6nxnpxcy63nqw****`

The ID of the A2A agent.



**Name ** <span data-label="purple">string </span>`Sample value: agent`

The name of the A2A agent.



**Source ** <span data-label="purple">string </span>`Sample value: Runtime`

The registration source of the A2A agent.


* Runtime: The A2A agent in the agent runtime is registered to an A2A agent space via the agent runtime address.

* Standard: The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.



**DefaultVersion ** <span data-label="purple">string </span>`Sample value: 1.0.0`

The version number of the default version of the A2A agent.



**Host ** <span data-label="purple">string </span>`Sample value: https://sd6khs4kjd57adbvg****.apigateway-ap-southeast-1.volceapi.com`

The domain name of the A2A agent.



**Capabilities ** <span data-label="purple">string[] </span>`Sample value: ["Streaming"]`

The capabilities of the A2A agent.



**Skills ** <span data-label="purple">string[] </span>`Sample value: ["model"]`

The Skills of the A2A agent.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 177219****`

The creation time of the A2A agent.



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 177224****`

The update time of the A2A agent.



**Status ** <span data-label="purple">string </span>`Sample value: running`

The status of the A2A agent.


* running: Registration succeeded.

* failed: Registration failed.



**Reason ** <span data-label="purple">string </span>`Sample value: --`

The error information.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=ListA2aAgents&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T121910Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "PageNumber": 1,
  "PageSize": 10,
  "Filter": {
    "Id": "a-yeh4hhuscg30lppp****",
    "Name": "Agent",
    "Version": "1.0.0",
    "Skill": "chat",
    "Source": [
      "["Runtime"]"
    ]
  },
  "SpaceId": "as-yeglyhjytc3srhse****",
  "ProjectName": "default",
  "TagFilters": [
    {
      "Key": "key1",
      "Values": [
        "value1"
      ]
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260309201925086076184153ED****",
    "Action": "ListA2aAgents",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 1,
    "Items": [
      {
        "Id": "a-yeh6nxnpxcy63nqw****",
        "Name": "agent",
        "Source": "Runtime",
        "DefaultVersion": "1.0.0",
        "Host": "https://sd6khs4kjd57adbvg****.apigateway-ap-southeast-1.volceapi.com",
        "Capabilities": [
          "["Streaming"]"
        ],
        "Skills": [
          "["model"]"
        ],
        "CreateTimeStamp": "177219****",
        "UpdateTimeStamp": "177224****",
        "Status": "running",
        "Reason": "--"
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
|403 |AccessDenied |You are not authorized to perform this action. |You do not have permission to perform this operation. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

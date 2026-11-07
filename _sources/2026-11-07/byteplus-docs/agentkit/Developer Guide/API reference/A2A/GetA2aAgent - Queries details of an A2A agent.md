---
title: "GetA2aAgent - Queries details of an A2A agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetA2aAgent_-_Queries_details_of_an_A2A_agent"
---

Query details of an A2A agent.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mu5XuH">必选</span> `Sample value: GetA2aAgent`

The operation that you want to perform. Value: GetA2aAgent.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|aMXbu6">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span>`Optional` `Sample value: a-yeh4hhuscg30lppp****`

The ID of the A2A agent.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: agent`

The name of the A2A agent.



**SpaceId ** <span data-label="purple">string </span><span data-api-tag="require|4HA8UX">必选</span> `Sample value: as-yegj2ehvk0y0puxl****`

The ID of the A2A agent space.



**RuntimeId ** <span data-label="purple">string </span>`Optional` `Sample value: r-yehe28rh8g9d1og9****`

The ID of the A2A agent runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: a-yeh4hhuscg30lppp****`

The ID of the A2A agent.



**Source ** <span data-label="purple">string </span>`Sample value: Runtime`

The registration source of the A2A agent.


* Runtime: The A2A agent in the agent runtime is registered to an A2A agent space via the agent runtime address.

* Standard: The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.



**A2aSpaceId ** <span data-label="purple">string </span>`Sample value: as-yeglyhjytc3srhse****`

The ID of the A2A agent space.



**AgentCard ** <span data-label="purple">string </span>`Sample value: ei6****`

The ID of the AgentCard.



**RuntimeConfig ** <span data-label="purple">object </span>`Sample value: -`

The configuration of the agent runtime.


**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-yeh6nlafwgo2eybt****`

The ID of the A2A agent runtime.



**NetworkType ** <span data-label="purple">string </span>`Sample value: private`

After an agent runtime is selected, its service address is automatically populated. You can select either a public or private address based on your needs.


* private: Select this address if only internal private network communication is required. Private network connectivity is free of charge.

* public: This address is required for accessing cloud resources over the Internet.




**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The project name of the agent runtime.



**Tags ** <span data-label="purple">object </span>`Sample value: -`

The tag.


**Key ** <span data-label="purple">string </span>`Sample value: key1`

The key of the tag.



**Value ** <span data-label="purple">string </span>`Sample value: value1`

The value of the tag.




**DefaultVersion ** <span data-label="purple">string </span>`Sample value: 1.0.0`

The version number of the default version of the A2A agent.



**Status ** <span data-label="purple">string </span>`Sample value: running`

The status of the A2A agent.


* running: Registration succeeded.

* failed: Registration failed.



**StandardConfig ** <span data-label="purple">object </span>`Sample value: -`

The external import configuration.


**ImportType ** <span data-label="purple">string </span>`Sample value: json`

This parameter is supported when "Source" is set to "Standard". The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.


* json: The A2A agent is registered to an A2A agent space by importing a JSON file that complies with the A2A protocol specifications. A valid JSON file must be prepared in advance. Details regarding field definitions, value ranges, and validation rules can be found in the [official A2A protocol documentation](https://a2a-protocol.org/latest/specification/#441-agentcard). A sample JSON file is provided in [Sample A2A agent JSON file](https://docs.byteplus.com/en/docs/agentkit/Sample_A2A_agent_JSON_file).

* url: The A2A agent is registered to an A2A agent space using the AgentCard address of the A2A agent. The AgentCard address must be obtained in advance.



**AgentCardUrl ** <span data-label="purple">string </span>`Sample value: http://api.example.com/a2a/v1`

The AgentCard address for registering the A2A agent. This parameter is required when "ImportType" is set to `url`.




**Name ** <span data-label="purple">string </span>`Sample value: agent`

The name of the A2A agent.



**OriginalAgentCard ** <span data-label="purple">string </span>`Sample value: 1.0.0`

The original AgentCard version.



**Reason ** <span data-label="purple">string </span>`Sample value: -`

The error information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=GetA2aAgent&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T122933Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "a-yeh4hhuscg30lppp****",
  "Name": "agent",
  "SpaceId": "as-yegj2ehvk0y0puxl****",
  "RuntimeId": "r-yehe28rh8g9d1og9****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202603092029411811701761568F****",
    "Action": "GetA2aAgent",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "a-yeh4hhuscg30lppp****",
    "Source": "Runtime",
    "A2aSpaceId": "as-yeglyhjytc3srhse****",
    "AgentCard": "ei6****",
    "RuntimeConfig": {
      "RuntimeId": "r-yeh6nlafwgo2eybt****",
      "NetworkType": "private"
    },
    "ProjectName": "default",
    "Tags": {
      "Key": "key1",
      "Value": "value1"
    },
    "DefaultVersion": "1.0.0",
    "Status": "running",
    "StandardConfig": {
      "ImportType": "json",
      "AgentCardUrl": "http://api.example.com/a2a/v1"
    },
    "EnableProxy": true,
    "Name": "agent",
    "OriginalAgentCard": "1.0.0",
      }
    },
    "Reason": "-"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is invalid. |The request parameter value is invalid. Verify the parameter value and try again. |
|403 |AccessDenied |You are not authorized to perform this action. |You do not have permission to perform this operation. |
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

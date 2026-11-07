---
title: "UpdateA2aAgent - Updates an A2A agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateA2aAgent_-_Updates_an_A2A_agent"
---

Update an A2A agent.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|eodC7Z">必选</span> `Sample value: UpdateA2aAgent`

The operation that you want to perform. Value: UpdateA2aAgent.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|imbkOQ">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|LuPSqi">必选</span> `Sample value: a-yegj2ehvk0y0puxl****`

The ID of the A2A agent.



**Source ** <span data-label="purple">string </span><span data-api-tag="require|kfMJZe">必选</span> `Sample value: Runtime`

The registration source of the A2A agent.


* Runtime: The A2A agent in the agent runtime is registered to an A2A agent space via the agent runtime address.

* Standard: The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.



**A2aSpaceId ** <span data-label="purple">string </span><span data-api-tag="require|YgBUQK">必选</span> `Sample value: as-yeglyhjytc3srhse****`

The ID of the A2A agent space.



**AgentCard ** <span data-label="purple">string </span>`Optional` `Sample value: ei6****`

The JSON text of the AgentCard. This parameter is required when "Source" is set to "Standard" and you want to register an A2A agent via a JSON file.



**RuntimeConfig ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The configuration information of the agent runtime associated with the A2A agent to be registered. This parameter is required when "Source" is set to "Runtime".


**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|FIEQ5P">必选</span> `Sample value: r-yeh6nlafwgo2eybt****`

The ID of the runtime.



**NetworkType ** <span data-label="purple">string </span><span data-api-tag="require|r8VV9g">必选</span> `Sample value: private`

After an agent runtime is selected, its service address is automatically populated. You can select either a public or private address based on your needs.


* private: Select this address if only internal private network communication is required. Private network connectivity is free of charge.

* public: This address is required for accessing cloud resources over the Internet.




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the project associated with the A2A agent.



**Tags ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tag of the A2A agent.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|ER9d0l">必选</span> `Sample value: key1`

The key of the tag.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|iBnmJP">必选</span> `Sample value: value1`

The value of the tag.




**SetDefaultVersion ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to set as the default version. By default, the agent calls the default version of the A2A agent. A2A agents support version lifecycle management, allowing you to create, view, and delete different versions to meet agent iteration and compatibility requirements.


* true: Set as the default version.

* false: Do not set as the default version.



**StandardConfig ** <span data-label="purple">object </span>`Optional` `Sample value: --`

The configuration for importing the A2A agent from external sources. This parameter is required when "Source" is set to "Runtime".


**ImportType ** <span data-label="purple">string </span><span data-api-tag="require|hYUrAL">必选</span> `Sample value: json`

This parameter is supported when "Source" is set to "Standard". The A2A agent is registered to an A2A agent space by importing a JSON file or AgentCard address.


* json: The A2A agent is registered to an A2A agent space by importing a JSON file that complies with the A2A protocol specifications. A valid JSON file must be prepared in advance. Details regarding field definitions, value ranges, and validation rules can be found in the [official A2A protocol documentation](https://a2a-protocol.org/latest/specification/#441-agentcard). A sample JSON file is provided in [Sample A2A agent JSON file](https://docs.byteplus.com/en/docs/agentkit/Sample_A2A_agent_JSON_file).

* url: The A2A agent is registered to an A2A agent space using the AgentCard address of the A2A agent. The AgentCard address must be obtained in advance.



**AgentCardUrl ** <span data-label="purple">string </span>`Optional` `Sample value: http://api.example.com/a2a/v1`

The AgentCard address for registering the A2A agent. This parameter is required when "ImportType" is set to `url`.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=UpdateA2aAgent&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T122557Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "Id": "a-yegj2ehvk0y0puxl****",
  "Source": "Runtime",
  "A2aSpaceId": "as-yeglyhjytc3srhse****",
  "AgentCard": "ei6****",
  "RuntimeConfig": {
    "RuntimeId": "r-yeh6nlafwgo2eybt****",
    "NetworkType": "private"
  },
  "ProjectName": "default",
  "Tags": [
    {
      "Key": "key1",
      "Value": "value1"
    }
  ],
  "SetDefaultVersion": true,
  "StandardConfig": {
    "ImportType": "json",
    "AgentCardUrl": "http://api.example.com/a2a/v1"
  }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2026030920260219814616804541****",
    "Action": "UpdateA2aAgent",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|403 |AccessDenied |You are not authorized to perform this action. |You do not have permission to perform this operation. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

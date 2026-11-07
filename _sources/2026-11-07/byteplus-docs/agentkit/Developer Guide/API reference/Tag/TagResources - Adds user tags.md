---
title: "TagResources - Adds user tags"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/TagResources_-_Adds_user_tags"
---

You can call this operation to add user tags for one or more resources.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string  </span><span data-api-tag="require|ZVJiCq">必选</span>`Sample value: TagResources`

The action that you want to perform. Value: TagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|Rh9hCm">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|9Q50an">必选</span> `Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

Resource ID.


* Parameter \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate multiple resources with ampersands (&).



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|gweiHx">必选</span> `Sample value: memory`

The resource type. Valid values:


* runtime: Agent runtime.

* tool: Toolset.

* memory: Memory.

* mcpservice: MCP service.

* mcptoolset: MCP toolset.



**Tags.N.Key ** <span data-label="purple">string[]  </span><span data-api-tag="require|igSMT8">必选</span>`Sample value: Tags.1.Key=k1`

The tag key of the user tag to be added to the resource.


* Parameter \- N: Indicates the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands ( & ).


Naming rules:


* It cannot start with `volc:` or` sys:` in any case form.

> Tags that start with `volc:` or `sys:` are reserved for the system. You cannot create tags starting with them.


* It can contain only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



**Tags.N.Value**<span data-label="purple"> string[] </span>`Optional` `Sample value: Tags.1.Value=v1`

The tag value of the tag associated with the resource.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It can be empty. Length limit: 0\-256 characters.



**Tags.N.Type**<span data-label="purple"> string[] </span>`Optional Sample value: custom`

Tag type.


* system: System tag.

* custom: User tag.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=TagResources&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "ResourceType": "sRywhOzLUe"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162502098132110105524B2F",
    "Action": "TagResources",
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
|400 |MissingParameter.Key |The required parameter Key is not supplied. |The parameter Key cannot be empty.  |
|400 |MissingParameter.ResourceIds |Resource Ids cannot be empty. |The ResourceIds cannot be empty. |
|400 |MissingParameter.ResourceType |The required parameter ResourceType is not supplied. |The parameter ResourceType cannot be empty. |
|400 |MissingParameter.Tags |The required parameter Tags is not supplied. |The parameter Tags cannot be empty. |
|400 |MissingParameter.Value |The required parameter Value is not supplied. |The parameter Value cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The resource does not exist. |
|500 |InternalError |An internal error has occurred. |Internal error. |

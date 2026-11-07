---
title: "UntagResources - Deletes user tags"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UntagResources_-_Deletes_user_tags"
---

You can call this operation to delete user tags for one or more resources.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span><span data-api-tag="require|h8t4C7">必选</span>`Sample value: UntagResources`

The action that you want to perform. Value: UntagResources.



**Version ** <span data-label="purple">string   </span><span data-api-tag="require|tdvz6I">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ResourceIds.N ** <span data-label="purple">string[]   </span><span data-api-tag="require|U6sYXN">必选</span>`Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

The resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate multiple resources with ampersands ( & ).



**ResourceType ** <span data-label="purple">string   </span><span data-api-tag="require|sAxDGO">必选</span>`Sample value: runtime`

The resource type. Valid values:


* runtime: Agent runtime.

* tool: Toolset.

* memory: Memory.

* mcpservice: MCP service.

* mcptoolset: MCP toolset.



**TagKeys.N ** <span data-label="purple">string[] </span>`Optional Sample value: TagKeys.1=k1`

The tag key of the user tag to be deleted from the resource.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or` sys:` in any case form.

> Tag keys that start with `volc:` or `sys:` are reserved for the system. You cannot create tags starting with them.


* It can contain only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* It must be 1 to 128 characters in length.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UntagResources&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "ResourceType": "runtime"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162658193149250187EE6098",
    "Action": "UntagResources",
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
|400 |MissingParameter.ResourceIds |Resource Ids cannot be empty. |The resource ID cannot be empty. |
|400 |MissingParameter.ResourceType |The required parameter ResourceType is not supplied. |The ResourceType parameter cannot be left empty. |

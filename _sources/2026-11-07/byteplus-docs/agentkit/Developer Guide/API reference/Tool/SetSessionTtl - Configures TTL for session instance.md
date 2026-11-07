---
title: "SetSessionTtl - Configures TTL for session instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/SetSessionTtl_-_Configures_TTL_for_session_instance"
---

You can call this operation to configure TTL (Time to Live) for a session instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|du0wUn">必选</span> `Sample value: SetSessionTtl`

The action that you want to perform. Value: SetSessionTtl.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|UnwheF">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**SessionId ** <span data-label="purple">string </span><span data-api-tag="require|C6jcgZ">必选</span> `Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|xWrI17">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



**Ttl ** <span data-label="purple">integer </span><span data-api-tag="require|YzIRac">必选</span> `Sample value: 1800`

TTL of the session instance, that is, the validity period during which the tool, in a single "user\-tool interactive session", retains the user status and operation context without loss. After the session expires, you simply log in again or restart the operation.


* Unit: second.

* Value range: 60–86400.

* Default value: 1800.



**TtlUnit ** <span data-label="purple">string </span>`Optional Sample value: second`

The unit for TTL. Value:


* minute: minute.

* second (default): second.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ExpireAt ** <span data-label="purple">string </span>`Sample value: 2006-01-02T15:04:05Z07:00`

Expiration time of the session.



**SessionId ** <span data-label="purple">string </span>`Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**ToolId ** <span data-label="purple">string </span>`Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=SetSessionTtl&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx",
    "SessionId": "s-ye6xzwchkwoaroxxxxxx",
    "Ttl": 1800
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027144356FBC64212879D5D3A****",
    "Action": "SetSessionTtl",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "SessionId": "s-ye7sfdm2o0c1kdto****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.SessionId |The required parameter SessionId is not supplied. |SessionId cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |ToolId cannot be empty. |
|400 |MissingParameter.Ttl |The required parameter Ttl is not supplied. |The parameter Ttl cannot be empty. |
|400 |InvalidParameter.Ttl |The specified parameter Ttl is invalid. |The parameter Ttl cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

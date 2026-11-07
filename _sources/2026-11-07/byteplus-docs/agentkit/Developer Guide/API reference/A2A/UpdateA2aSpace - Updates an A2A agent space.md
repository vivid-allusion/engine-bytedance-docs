---
title: "UpdateA2aSpace - Updates an A2A agent space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateA2aSpace_-_Updates_an_A2A_agent_space"
---

Update an A2A agent space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|vTb9Se">必选</span> `Sample value: UpdateA2aSpace`

The operation that you want to perform. Value: UpdateA2aSpace.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|X5tK9S">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|y0h6J6">必选</span> `Sample value: as-yeglyhjytc3srhs****`

The ID of the A2A agent space.



**Name ** <span data-label="purple">string </span>`Optional` `Sample value: space`

The name of the A2A agent space.



**IntentEnabled ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether semantic retrieval is enabled for the A2A agent space. By default, it is not enabled. After you enable semantic retrieval for an A2A agent space, when an agent calls the A2A agent space, the A2A agent space can parse the calling intent and return the agent with the highest matching degree in the A2A agent space.


* true: Enabled.

* false: Disabled.



**Tags ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tag of the A2A agent.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|NQSXdI">必选</span> `Sample value: Key1`

The key of the A2A agent.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|luWppK">必选</span> `Sample value: Value1`

The value of the A2A agent.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=UpdateA2aSpace&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T120808Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "as-yeglyhjytc3srhs****",
  "Name": "space",
  "IntentEnabled": true,
  "Tags": [
    {
      "Key": "Key1",
      "Value": "Value1"
    }
  ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202603092008161662111252542C****",
    "Action": "UpdateA2aSpace",
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
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

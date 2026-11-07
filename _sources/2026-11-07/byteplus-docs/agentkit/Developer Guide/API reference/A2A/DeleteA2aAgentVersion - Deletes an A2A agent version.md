---
title: "DeleteA2aAgentVersion - Deletes an A2A agent version"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteA2aAgentVersion_-_Deletes_an_A2A_agent_version"
---

Delete an A2A agent version.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|mlHoQR">必选</span> `Sample value: DeleteA2aAgentVersion`

The operation that you want to perform. Value: DeleteA2aAgentVersion.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|kIz6O4">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|uRewyt">必选</span> `Sample value: a-yeh6nxnpxcy63nqw****`

The ID of the A2A agent.



**AgentVersion ** <span data-label="purple">string </span><span data-api-tag="require|6JP510">必选</span> `Sample value: 1.0.0`

The version of the A2A agent.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=DeleteA2aAgentVersion&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T120435Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "a-yeh6nxnpxcy63nqw****",
  "AgentVersion": "1.0.0"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202603092004410602450830568D****",
    "Action": "DeleteA2aAgentVersion",
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
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

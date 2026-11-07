---
title: "GetA2aAgentVersion - Queries version details of an A2A agent"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetA2aAgentVersion_-_Queries_version_details_of_an_A2A_agent"
---

Query version details of an A2A agent.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|OFYkOM">必选</span> `Sample value: GetA2aAgentVersion`

The operation that you want to perform. Value: GetA2aAgentVersion.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|pXxKgs">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|kOtNs2">必选</span> `Sample value: a-yeh6nxnpxcy63nqw****`

The ID of the A2A agent.



**AgentVersion ** <span data-label="purple">string </span><span data-api-tag="require|HVek4w">必选</span> `Sample value: 1.0.0`

The version of the A2A agent.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AgentCard ** <span data-label="purple">string </span>`Sample value: a-yeh6nxnpxcy63nqw****`

The name of the A2A agent.



**Status ** <span data-label="purple">string </span>`Sample value: running`

The status of the A2A agent.


* running: Successful registration.

* failed: Registration failed.



**ErrorMessage ** <span data-label="purple">string </span>`Sample value: --`

The error message.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=GetA2aAgentVersion&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T123414Z
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
    "RequestId": "20260309203420162016039100FA****",
    "Action": "GetA2aAgentVersion",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AgentCard": "a-yeh6nxnpxcy63nqw****",
    "Status": "running",
    "ErrorMessage": "--"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

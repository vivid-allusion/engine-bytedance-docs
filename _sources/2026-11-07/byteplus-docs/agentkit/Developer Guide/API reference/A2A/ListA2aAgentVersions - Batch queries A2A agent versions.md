---
title: "ListA2aAgentVersions - Batch queries A2A agent versions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListA2aAgentVersions_-_Batch_queries_A2A_agent_versions"
---

Batch query A2A agent versions.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|6HaqXz">必选</span> `Sample value: ListA2aAgentVersions`

The operation that you want to perform. Value: ListA2aAgentVersions.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|2Ku3ol">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|J8rTAd">必选</span> `Sample value: a-yeh6nxnpxcy63nqw****`

The ID of the A2A agent.



**PageNumber ** <span data-label="purple">integer </span>`Optional Sample value: 1`

The current page number.


* Starting value: 1.

* Default value: 1.



**PageSize**<span data-label="purple"> integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Value range: 1–100.

* Default value: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of A2A agents.



**Items ** <span data-label="purple">object[] </span>`Sample value: --`

The version of the A2A agent.


**Version ** <span data-label="purple">string </span>`Sample value: 1.0.0`

The version of the A2A agent.



**CreateTimeStamp ** <span data-label="purple">string </span>`Sample value: 177219****`

The creation time of the A2A agent.



**UpdateTimeStamp ** <span data-label="purple">string </span>`Sample value: 177224****`

The update time of the A2A agent.



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
POST /?Action=ListA2aAgentVersions&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T123231Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "a-yeh6nxnpxcy63nqw****",
  "PageNumber": 1,
  "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260309203227055237193215BE****",
    "Action": "ListA2aAgentVersions",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TotalCount": 1,
    "Items": [
      {
        "Version": "1.0.0",
        "CreateTimeStamp": "177219****",
        "UpdateTimeStamp": "177224****",
        "Status": "running",
        "ErrorMessage": "-"
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
|404 |ResourceNotFound |The specified resource cannot be found. |The corresponding resource cannot be found. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

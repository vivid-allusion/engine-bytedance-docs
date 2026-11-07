---
title: "GetA2aSpace - Queries details of an A2A agent space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetA2aSpace_-_Queries_details_of_an_A2A_agent_space"
---

Query details of an A2A agent space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zykWj4">必选</span> `Sample value: GetA2aSpace`

The operation that you want to perform. Value: GetA2aSpace.



 **Version ** <span data-label="purple">string </span><span data-api-tag="require|zc76Nu">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|g1K5Qv">必选</span> `Sample value: as-yeglyhjytc3srhse****`

The instance ID of the A2A agent space.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: as-yeglyhjytc3srhse****`

The instance ID of the A2A agent space.



**Name ** <span data-label="purple">string </span>`Sample value: space`

The name of the A2A agent space.



**IntentEnabled ** <span data-label="purple">boolean </span>`Sample value: true`

Whether semantic retrieval is enabled for the A2A agent space. After semantic retrieval is enabled, the agent with the highest matching degree in the space is returned based on the natural language of the calling intent.


* true: Enabled.

* false: Disabled.



**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The name of the project associated with the A2A agent space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag of the A2A agent space.


**Key ** <span data-label="purple">string </span>`Sample value: Key1`

The key of the tag.



**Value ** <span data-label="purple">string </span>`Sample value: Value1`

The value of the tag.




**IsDefault ** <span data-label="purple">boolean </span>`Sample value: false`

Whether it is specified as the default A2A agent space. When you register an A2A agent, if no A2A agent space is specified, the agent is registered to the default A2A agent space.


* true: Specified as the default space.

* false: Not specified as the default space.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=GetA2aSpace&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T121250Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "as-yeglyhjytc3srhse****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2026030920125301921010312839****",
    "Action": "GetA2aSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "as-yeglyhjytc3srhse****",
    "Name": "space",
    "IntentEnabled": true,
    "ProjectName": "default",
    "Tags": [
      {
        "Key": "Key1",
        "Value": "Value1"
      }
    ],
    "IsDefault": true
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

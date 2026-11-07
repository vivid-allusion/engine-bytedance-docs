---
title: "CreateA2aSpace - Creates an A2A agent space"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/CreateA2aSpace_-_Creates_an_A2A_agent_space"
---

Create an A2A agent space.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|CMwsSb">必选</span> `Sample value: CreateA2aSpace`

The operation that you want to perform. Value: CreateA2aSpace.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VIwbDc">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**Name ** <span data-label="purple">string </span><span data-api-tag="require|ycZvza">必选</span> `Sample value: space`

The name of the A2A agent space.



**IntentEnabled ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether semantic retrieval is enabled for the A2A agent space. By default, semantic retrieval is not enabled. After you enable semantic retrieval for an A2A agent space, when an agent calls the A2A agent space, the space can parse the calling intent and return the best\-matching agent in the A2A agent space.


* true: Enabled.

* false: Disabled.



**Tags ** <span data-label="purple">object[] </span>`Optional` `Sample value: --`

The tag of the A2A agent.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|BmlImF">必选</span> `Sample value: Key1`

The key of the A2A agent tag.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|XPs8F8">必选</span> `Sample value: Value1`

The value of the A2A agent tag.




**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: default`

The name of the associated project.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Id ** <span data-label="purple">string </span>`Sample value: as-yeglyhjytc3srhse****`

The ID of the A2A agent space.



**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag of the A2A agent.


**Key ** <span data-label="purple">string </span>`Sample value: Key1`

The key of the A2A agent tag.



**Value ** <span data-label="purple">string </span>`Sample value: Value1`

The value of the A2A agent tag.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST /?Action=CreateA2aSpace&Version=2025-10-30 HTTP/1.1
Host: agentkit.ap-southeast-1.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260309T120634Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260309/ap-southeast-1/agentkit/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Name": "space",
  "IntentEnabled": true,
  "Tags": [
    {
      "Key": "Key1",
      "Value": "Value1"
    }
  ],
  "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202603091945422371672520079C****",
    "Action": "CreateA2aSpace",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "as-yeglyhjytc3srhse****",
    "Tags": [
      {
        "Key": "Key1",
        "Value": "Value1"
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
|400 |InvalidParameter |The specified parameter %s is invalid. |The request parameter value is invalid. Verify the parameter value and try again. |
|403 |AccessDenied |You are not authorized to perform this action. |You do not have permission to perform this operation. |
|500 |InternalError |The request has failed due to an unknown error. |Internal error. |

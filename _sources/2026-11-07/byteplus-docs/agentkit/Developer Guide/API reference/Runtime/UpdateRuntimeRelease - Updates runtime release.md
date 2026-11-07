---
title: "UpdateRuntimeRelease - Updates runtime release"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Update_runtime_release_-_Updates_runtime_release"
---

You can call this operation to update the runtime release (update release traffic percentage).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ilASts">必选</span> `Sample value: UpdateRuntimeRelease`

The action that you want to perform. Value: UpdateRuntimeRelease.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|PSgIjE">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|yZEwLe">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



**TargetTrafficWeight ** <span data-label="purple">integer </span><span data-api-tag="require|QFcOOq">必选</span> `Sample value: 100`

The target traffic percentage for the release.


* Value range: 1\-100.

* If the value is 100: Full release.

* If the value is less than 100: Grey release.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RuntimeId ** <span data-label="purple">string </span>`Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateRuntimeRelease&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye7agye1a8cr38iu****",
    "TargetTrafficWeight": 100
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateRuntimeRelease",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Id": "r-ye7agye1a8cr38iu****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |
|400 |MissingParameter.TargetTrafficWeight |The required parameter TargetTrafficWeight is not supplied. |The TargetTrafficWeight parameter cannot be empty. |

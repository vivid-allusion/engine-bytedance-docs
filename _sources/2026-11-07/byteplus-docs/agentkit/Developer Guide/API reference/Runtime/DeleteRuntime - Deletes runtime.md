---
title: "DeleteRuntime - Deletes runtime"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteRuntime_-_Deletes_runtime"
---

You can call this operation to delete a runtime.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Z4nCCi">必选</span> `Sample value: DeleteRuntime`

The action that you want to perform. Value: DeleteRuntime.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|h4L88l">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 23fa21A8823nfasd7f****`

The ClientToken is used to ensure the request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|8Crmsh">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RuntimeId ** <span data-label="purple">string </span>`Example value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com?Action=DeleteRuntime&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "RuntimeId": "r-ye6hflyl1c598vs****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DeleteRuntime",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "RuntimeId": " r-3thhlu***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The RuntimeId parameter cannot be empty. |

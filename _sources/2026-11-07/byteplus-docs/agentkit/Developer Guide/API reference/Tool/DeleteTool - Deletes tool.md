---
title: "DeleteTool - Deletes tool"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteTool_-_Deletes_tool"
---

You can call this operation to delete a sandbox tool. When you delete a sandbox tool, the associated sessions are automatically reclaimed. This operation is irreversible. Please proceed with caution.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|xdrolT">必选</span> `Sample value: DeleteTool`

The action that you want to perform. Value: DeleteTool.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VQ7oJq">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API operation times out or an internal server error occurs. Values:

Not more than 64 ASCII characters.



**ToolId ** <span data-label="purple">string </span>`Optional Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ToolId ** <span data-label="purple">string </span>`Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteTool&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-ye6xzwchkwoaroxxxxxx"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DeleteTool",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ToolId": "t-ye7hr4n01soarome****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).

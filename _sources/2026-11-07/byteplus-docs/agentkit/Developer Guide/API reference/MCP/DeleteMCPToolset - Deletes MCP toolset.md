---
title: "DeleteMCPToolset - Deletes MCP toolset"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteMCPToolset_-_Deletes_MCP_toolset"
---

You can call this operation to delete an MCP toolset.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

If an MCP toolset is no longer used by any agent, workflow, or external caller, or if you plan to recreate a toolset of the same type with a new configuration, you can delete the toolset.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

**A deleted MCP toolset cannot be recovered. ** Proceed with caution. If any agent or caller still depends on the toolset, deleting it will immediately cause call failures.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|sJFVCT">必选</span> `Sample value: DeleteMCPToolset`

The action that you want to perform. Value: DeleteMCPToolset.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|bWeX5y">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MCPToolsetId ** <span data-label="purple">string  </span><span data-api-tag="require|uzW21x">必选</span>`Sample value: mt-ye7f6gd7nktv3gi6c***`

MCP toolset ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-ye7f6gd7nktv3gi6c***`

MCP toolset ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteMCPToolset&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPToolsetId":"mt-ye7d4hlbswq7oi5c****"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DeleteMCPToolset",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPToolsetId": "mt-ye7f6gd7nktv3gi6c***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPToolsetId |The required parameter MCPToolsetId is not supplied. |The parameter MCPToolsetId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |

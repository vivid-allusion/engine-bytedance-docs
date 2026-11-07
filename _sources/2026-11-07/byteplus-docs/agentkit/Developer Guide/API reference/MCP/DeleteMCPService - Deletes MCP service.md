---
title: "DeleteMCPService - Deletes MCP service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/DeleteMCPService_-_Deletes_MCP_service"
---

You can call this operation to delete an MCP service.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

If an MCP service is no longer in use, you can delete it.


* An MCP service created for testing has been verified and no longer needs to be retained.

* A service has been migrated to a new MCP service instance, and the old service can be retired.

* An MCP service created by mistake needs to be cleaned up.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

A deleted MCP service cannot be recovered. After deletion, agents, IDEs, CLIs, or external systems that depend on the service will no longer be able to call the associated tools. Before proceeding, confirm that all callers have switched away from the service or stopped using it.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string</span><span data-api-tag="require|lmBO3Z">必选</span>  `Sample value: DeleteMCPService`

The action that you want to perform. Value: DeleteMCPService.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|7lXo47">必选</span>` Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MCPServiceId ** <span data-label="purple">string </span><span data-api-tag="require|aQDd2Z">必选</span> `Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=DeleteMCPService&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPServiceId":"m-ye7f6gd7nktv3gi6c***"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DeleteMCPService",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPServiceId": " m-ye7f6gd7nktv3gi6c***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPServiceId |The required parameter MCPServiceId is not supplied. |The parameter MCPServiceId cannot be empty. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The operation on this resource is not allowed. |

---
title: "UpdateMCPTools - Modifies API information associated with an MCP service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/UpdateMCPTools_-_Modifies_API_information_associated_with_an_MCP_service"
---

Modify API information associated with an MCP service.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

You can modify the API information only when the access method for the MCP service is "HTTP to MCP". To query the access method, call the [GetMCPService](https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details) operation and check the value of the ProtocolType parameter in the response.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|QkKoMj">必选</span> `Sample value: UpdateMCPTools`

The action that you want to perform. Value: UpdateMCPTools.



**Version**<span data-label="purple"> string</span> <span data-api-tag="require|wR6knX">必选</span>`Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**MCPServiceId ** <span data-label="purple">string</span><span data-api-tag="require|dhkz5Y">必选</span>  `Sample value: m-ye7f6gd7nktv3gi6c***`

MCP service ID.



**MCPToolsetId ** <span data-label="purple">string </span><span data-api-tag="require|B24R4v">必选</span> `Sample value: mt-ye7f6gd7nktv3gi6c***`

MCP toolset ID.



**Tools ** <span data-label="purple">string</span><span data-api-tag="require|bprGpT">必选</span>  `Sample value: --`

Add API information in Swagger format. [How do I upload a valid Swagger file?](https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples)



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f4f7gu8q7oi5cu***`

MCP service ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=UpdateMCPTools&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPServiceId": "m-xasxa***",
    "Tools": ""
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "UpdateMCPTools",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPServiceId |The required parameter MCPServiceId is not supplied. |The parameter MCPServiceId cannot be empty. |
|400 |MissingParameter.MCPToolsetId |The required parameter MCPToolsetId is not supplied. |The parameter MCPToolsetId cannot be empty. |
|400 |MissingParameter.Tools |The required parameter Tools is not supplied. |The parameter Tools cannot be empty. |

---
title: "ListMCPToolsetTools - Queries tools in an MCP toolset"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsetTools_-_Queries_tools_in_an_MCP_toolset"
---

Query tools in an MCP toolset.

<span id="UwaaRMZV"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://www.volcengine.com/docs/6369/67268).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5UTAO2">必选</span> `Sample value: ListMCPToolsetTools`

The action that you want to perform. Value: ListMCPToolsetTools.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|j6wO11">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**MCPToolsetId ** <span data-label="purple">string </span><span data-api-tag="require|dt2i4M">必选</span> `Sample value: m-ye7f6gd7nktv3gi6c***`

MCP toolset service ID.



&nbsp;

<span id="wrdnqEHK"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://www.volcengine.com/docs/6369/80336).



**MCPService ** <span data-label="purple">object[] </span>`Sample value: --`

MCP toolset details.


**IsAllTool ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to return all tools.



**MCPServiceId ** <span data-label="purple">string </span>`Sample value: m-ye7f6gd7nktv3gi6c****`

MCP service ID.



**MCPTools ** <span data-label="purple">object[] </span>`Sample value: -`

Tool tags.


**Description ** <span data-label="purple">string </span>`Sample value: add comments`

Description of the MCP service tool.



**Name ** <span data-label="purple">string </span>`Sample value: add-comments`

Name of the MCP tool.



**Tags ** <span data-label="purple">string[] </span>`Sample value: Version1`

Tool tags.




**Name ** <span data-label="purple">string </span>`Sample value: add-comments`

Name of the MCP tool.




**MCPToolsetId ** <span data-label="purple">string </span>`Sample value: mt-yefjsz5s0054ppxu****`

MCP toolset ID.



&nbsp;

<span id="qPEBWeI9"></span>
## Sample request

```JSON
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListMCPToolsetTools&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "MCPToolsetId":"mt-ye7d4hlbswq7oi5c****"
}

```


<span id="BEUJQxjC"></span>
## Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20260212221805CB3871ABF16839****",
    "Action": "ListMCPToolsetTools",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MCPToolsetId": "mt-yefjsz5s0054ppxu****",
    "MCPService": [
      {
        "MCPServiceId": "m-yefgecdo8wntl8dn****",
        "Name": "mcp_service_test_liutao",
        "IsAllTool": true,
        "MCPTools": [
          {
            "Name": "update-doc",
            "Description": "Update the doc.",
            "Tags": [
              "22"
            ]
          }
        ]
      }
    ]
  }
}
```


<span id="btfvAQk0"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://www.volcengine.com/docs/86681/1913777).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.MCPToolsetId |The required parameter MCPToolsetId is not supplied. |The parameter MCPToolsetId cannot be empty. |

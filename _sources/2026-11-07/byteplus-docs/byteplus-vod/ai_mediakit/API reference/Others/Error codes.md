---
title: "Error codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-error-codes"
---

When an AI MediaKit API request fails, this guide helps you diagnose and resolve the issue. It explains the structure of the JSON error response and provides a detailed list of common error codes, their meanings, and recommended solutions to help you quickly fix your integration.

```JSON
{
  "code": "InvalidParameter",
  "message": "tool(unknown-tool) not found",
  "request_id": "1742012d******************"
}
```



* `code`: A machine\-readable code that identifies the error type.

* `message`: A detailed, human\-readable description of the error.

* `request_id`: The unique identifier for this request. Please provide this ID when you need technical support.


<span id="dd4d822a"></span>
## Error codes


|Error code |Description |Solution |
|---|---|---|
|`MissingParameter` |A required parameter is missing from the request. For example, the `message` field might contain `tool name is required`. |Please check the API documentation to ensure that your request includes all required parameters (such as `tool-name`) and that the parameter names are spelled correctly. |
|`InvalidParameter` |A parameter value in the request is invalid or incorrectly formatted. |Carefully read the `message` field in the error response, as it will specify which parameter is causing the issue and why.<br><br><br>* **Example 1**: `invalid empty request body...` indicates that the request body is empty. Please ensure your request body is formatted as JSON and that the `Content-Type` header is set to `application/json`.<br><br>* **Example 2**: `...enum: unknown does not equal any of: [standard professional]` indicates that you have provided an unsupported value for a parameter (e.g., `tool_version`). Please correct the value based on the list of available options provided in the `message`. |
|`InvalidParameter` |The requested resource does not exist. For example, the `message` field might contain `tool(some-tool) not found`. |The tool name or task ID you requested may not exist or may be misspelled. Please check the parameter value and refer to the API documentation for a list of available tools. |
|`InternalServiceError` |An unexpected internal error occurred on the server. | |

---
title: "GetSessionLogs - Views tool session logs"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetSessionLogs_-_Views_tool_session_logs"
---

You can call this operation to view tool session logs.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|oa5ZBQ">必选</span> `Sample value: GetSessionLogs`

The action that you want to perform. Value: GetSessionLogs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|E23n9T">必选</span> `Sample value: 2025-10-30`

The API version. Value: 2025\-10\-30.



**Limit ** <span data-label="purple">integer </span>`Optional` `Sample value: 1000`

The limit on the number of log lines.


* Parameter \- N: Specifies the latest N log lines to be returned.

* If this parameter is not passed in, all logs are returned.



**SessionId ** <span data-label="purple">string </span><span data-api-tag="require|H4uf0Q">必选</span> `Sample value: s-3tigy72q3u3vj0x2****`

Session ID.



**ToolId ** <span data-label="purple">string </span><span data-api-tag="require|WzC6VE">必选</span> `Sample value: t-3tigy72q3u3vj0x2****`

Tool ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Logs ** <span data-label="purple">string </span>`Sample value: 2025-11-23T17:11:12.902769436+08:00 [FaaS System] starting user function at port 80802025-11-23T17:11:12.902934949+08:00 [FaaS System] run user command: ulimit -n ${BYTEFAAS_FUNC_ULIMIT:-2048} && /opt/gem/run.sh`

Instance logs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetSessionLogs&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-3tigy72q3u3vj0x2****",
    "SessionId": "s-3tigy72q3u3vj0x2****",
    "Limit": 1000
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202511231712426C9C75D44DC92BEC157C",
    "Action": "GetSessionLogs",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Logs": "2025-11-23T17:11:12.902769436+08:00 [FaaS System] starting user function at port 8080\n2025-11-23T17:11:12.902934949+08:00 [FaaS System] run user command: ulimit -n ${BYTEFAAS_FUNC_ULIMIT:-2048} && /opt/gem/run.sh"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.SessionId |The required parameter SessionId is not supplied. |The parameter SessionId cannot be empty. |
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The parameter ToolId cannot be empty. |

---
title: "GetRuntimeInstanceLogs - Queries runtime logs"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/GetRuntimeInstanceLogs_-_Queries_runtime_logs"
---

Query runtime logs.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|yvOhHi">必选</span> `Sample value: GetRuntimeInstanceLogs`

The action that you want to perform. Value: GetRuntimeInstanceLogs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|UdCPeA">必选</span> `Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|DE8j7T">必选</span> `Sample value: 1jsq6bcn-630g8l8****`

The instance name.



**Limit ** <span data-label="purple">integer </span>`Optional` `Sample value: 1000`

The number of latest log lines to query.


* Valid range: 0\-1000.

* If you do not specify this parameter, the latest 1,000 log lines are displayed.



**RuntimeId ** <span data-label="purple">string </span><span data-api-tag="require|9jX4xO">必选</span> `Sample value: r-ye7agye1a8cr38iu****`

ID of the runtime.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Logs ** <span data-label="purple">string </span>`Sample value: 2026-01-13T15:01:07.180067320+08:00 WARNING:(ast) sonic only supports go1.17~1.23, but your environment....`

The log text information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=GetRuntimeInstanceLogs&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "InstanceName":"1jsq6bcn-630g8l8****",
    "RuntimeId":"r-ye7agye1a8cr38iu****",
    "Limit":1000
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260113151804CDD****",
    "Action": "GetRuntimeInstanceLogs",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Logs": "2026-01-13T15:01:07.180067320+08:00 WARNING:(ast) sonic only supports go1.17~1.23, but your environment...."
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.InstanceName |The required parameter InstanceName is not supplied. |The instance name cannot be empty. |
|400 |MissingParameter.RuntimeId |The required parameter RuntimeId is not supplied. |The parameter RuntimeId cannot be empty. |

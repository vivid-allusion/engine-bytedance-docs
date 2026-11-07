---
title: "AsyncExecCommand - Asynchronously executes a Shell command in a tool"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AsyncExecCommand_-_Asynchronously_executes_a_Shell_command_in_a_tool"
---

Asynchronously execute a Shell command in a sandbox tool instance. This applies to time\-consuming background tasks or tasks that do not require waiting for real\-time results, such as compilation, script execution, data processing, and other similar operations.

<span id="Fk0w8ncO"></span>
## Instruction

This operation is called asynchronously. It returns only the task creation status and does not directly return the command execution result. You can use the task ID returned by this operation to query the command execution result through the [ViewAsyncCommand](https://docs.byteplus.com/en/docs/agentkit/ViewAsyncCommand_-_Queries_the_execution_result_of_an_asynchronous_command) operation.

<span id="c1mc1VbI"></span>
## Usage notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you call this operation, the <a href="https://docs.byteplus.com/en/docs/agentkit/Service_address?lang=zh">service address</a> is different from that of other operations. Use the region\-specific service address <code>https://agentkit.ap-southeast-1.bytepluses.com</code>.</div>


<span id="RLHtzxxy"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|**Parameter​**  |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ToolId |String |Yes |t\-yebi0bt\*\*\*\* |Tool ID. |
|Command |String |Yes |ls \-la / |The Shell command to execute. The command content must comply with the syntax of the target operating system. |
|UserSessionId |String |No |session\-1 |Specify the user session information of the execution request. This parameter is used to track and manage multiple consecutive requests from the same user. The system will attempt to route the session to the same sandbox instance.<br><br><br>* When you specify both the parameter and its value, the system executes the request based on the session information provided. If a session matching that information does not exist, the system creates a new session.<br><br>* If you specify the parameter but do not provide a value for it, a new session will be created.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If both <code>SessionId</code> and <code>UserSessionId</code> are not specified, a new <code>UserSessionId</code> will be created by default.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend that you use UserSessionId to associate multiple requests from the same user. This way, the sandbox instance can be reused and unnecessary cold start overhead can be avoided.</div><br> |
|SessionId |String |No |s\-yecrzeybt\*\*\*\* |Specify the session ID of the execution request, which is used to route the request to the specified sandbox instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If both <code>SessionId </code>and <code>UserSessionId</code> are not specified, a new value of the parameter <code>UserSessionId </code>will be created by default.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend that you use UserSessionId to associate multiple requests from the same user. This way, the sandbox instance can be reused and unnecessary cold start overhead can be avoided.</div><br> |
|TaskId |String |No |task\-e8a4g\*\*\*\* |The custom task ID. This parameter is used to uniquely identify an asynchronous execution.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this parameter is not passed in, a new <code>TaskId</code> is created by default.</div><br> |
|ExecDir |String |No |/home/gem |The starting directory where the command is executed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this parameter is not specified, the default working directory of the sandbox environment is used (for example, <code>/</code> or <code>/home/work</code>).</div><br> |
|Ttl |Integer |No |1,800 |TTL of the session instance, that is, the validity period during which the tool, in a single "user\-tool interactive session", retains the user status and operation context without loss.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">After the session expires, you simply log in again or restart the operation.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If there are no requests within the specified time, the instance will be automatically destroyed.</div><br><br><br>* Unit: second.<br><br>* Value range: 60–86400.<br><br>* Default value: 1800. |


<span id="0z7xnhwR"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|**Parameter​**  |**Instance type** |**Sample value** |**Description** |
|---|---|---|---|
|ToolId |String |t\-yebi0bt\*\*\*\* |The ID of the tool for command execution. |
|UserSessionId |String |session\-1 |The user session information of the execution request. |
|SessionId |String |s\-yecrbt\*\*\*\* |The session ID for the execution request. |
|TaskId |String |task\-e8a4g\*\*\*\* |The task ID for this asynchronous execution, which can be used for subsequent queries. |
|Status |String |Running |The initial status of the task. The status is typically "Running", indicating that the command has been submitted for execution. |
|Command |String |ls \-la / |The Shell command to execute. |
|ExecDir |String |/home/gem |The starting directory where the command is executed. |


<span id="8wJdH6el"></span>
## Sample request

```JSON
POST https://agentkit.ap-southeast-1.bytepluses.com?Action=AsyncExecCommand&Version=2025-10-30 HTTP/1.1
Content-Type: application/json

{
    "ToolId": "t-yebi0bt****",
    "UserSessionId": "session-1",
    "Command": "sleep 5 && echo 'Hello, World!'",
    "ExecDir": "/home/gem"
}
```


<span id="Jzxolgfl"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240122163000010225****",
        "Action": "AsyncExecCommand",
        "Version": "2025-10-30",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ToolId": "t-yebi0bt****",
        "UserSessionId": "session-1",
        "SessionId": "s-yecrbt****",
        "TaskId": "task-e8a4g****",
        "Status": "Running",
        "Command": "sleep 5 && echo 'Hello, World!'",
        "ExecDir": "/home/gem"
    }
}
```


<span id="NgLqv6Qp"></span>
## Error codes


|HttpCode |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ToolId |The required parameter ToolId is not supplied. |The required ToolId parameter is missing in the request. Check and provide it. |
|400 |MissingParameter.Command |The required parameter Command is not supplied. |The required Command parameter is missing in the request. Check and provide it. |



---

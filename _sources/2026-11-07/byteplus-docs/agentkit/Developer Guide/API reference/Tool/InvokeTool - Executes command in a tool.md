---
title: "InvokeTool - Executes command in a tool"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/InvokeTool_-_Executes_command_in_a_tool"
---

Call the InvokeTool operation to execute a command in a sandbox tool instance.

<span id="nIKM14Cp"></span>
## Instruction

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you call InvokeTool, <a href="https://docs.byteplus.com/en/docs/agentkit/Service_address">the service address</a> differs from that of other APIs. Use <code>https://agentkit.ap-southeast-1.bytepluses.com</code> based on the region.</div>


<span id="mkNDi57c"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters). 


|**Parameter​**  |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |InvokeTool |The action that you want to perform. Value: InvokeTool. |
|ToolId |String |Yes |t\-yebi04gb28o2eybt\*\*\*\* |Tool ID. |
|OperationType<br><br> |String |Yes<br><br> |RunCode |Operation type.<br><br><br>* Value: RunCode. This indicates using code to execute commands, which specifies the sandbox instance interface to be called, such as `/v1/jupyter/execute`. |
|OperationPayload<br><br> |String |Yes |{ "code": "print('helloworld')", "timeout": 30, "kernel_name": "python3"} |Specifies the request parameters for the sandbox instance interface. Values:<br><br><br>* code: The Python code that you want to execute.<br><br>* timeout: The timeout duration for the code execution.<br><br>* kernel_name: The kernel name, such as python3, python3.11, python3.12. The default value is python3. |
|SessionId |String |No |s\-yecrzqygw0o2eybt\*\*\*\* |Specifies the session ID for the request execution. If you specify the parameter but do not provide a value for it, a new session will be created.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Because a <code>SessionId</code> becomes unavailable when the tool's lifecycle ends, we recommend prioritizing the use of a <code>UserSessionId</code> for your requests.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If both <code>SessionId </code>and <code>UserSessionId</code> are not specified, a new value of the parameter <code>UserSessionId </code>will be created by default.</div><br> |
|UserSessionId |String |No |session\-1 |Specifies the user session information for request execution. By configuring this parameter, you can direct requests to run within specific session instances for context isolation.<br><br><br>* When you specify both the parameter and its value, the system executes the request based on the session information provided. If a session matching that information does not exist, the system creates a new session.<br><br>* If you specify the parameter but do not provide a value for it, a new session will be created.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If both <code>SessionId</code> and <code>UserSessionId</code> are not specified, a new <code>UserSessionId</code> will be created by default.</div><br> |
|Ttl |Integer |No |1,800 |TTL of the session instance, that is, the validity period during which the tool, in a single "user\-tool interactive session", retains the user status and operation context without loss. After the session expires, you simply log in again or restart the operation.<br><br><br>* Unit: second.<br><br>* Value range: 60–86400.<br><br>* Default value: 1800. |


<span id="r7bxWhvI"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|**Parameter​**  |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ToolId |String |tool\-3tigy72q3u3vj0x2\*\*\*\* |Tool ID. |
|UserSessionId |String |session\-1 |User session information. |
|SessionId<br><br> |String |s\-yecrzqygw0o2eybt\*\*\*\* |Session ID. |
|Endpoint |String |https://sd5acdbuo20h0ng5g\*\*\*\*.apigateway\-\*\*\*\*.volceapi.com/?faasInstanceName=vefaas\-\*\*\*\* |Domain name of the tool.<br><br> |
|InternalEndpoint |String |https://sd5acdbuo20h0ng5g\*\*\*\*.apigateway\-\*\*\*\*.volceapi\-inner.com/?faasInstanceName=vefaas\-\*\*\*\* |Internal access domain name for the tool. |
|Result |String |{<br><br> "success": true,<br><br> "message": "Code executed successfully",<br><br> "data": {<br><br> "kernel_name": "python3",<br><br> "session_id": "",<br><br> "status": "ok",<br><br> "execution_count": 1,<br><br> "outputs": [<br><br> {<br><br> "output_type": "stream",<br><br> "name": "stdout",<br><br> "text": "helloworld",<br><br> "data": null,<br><br> "metadata": {},<br><br> "execution_count": null,<br><br> "ename": null,<br><br> "evalue": null,<br><br> "traceback": null<br><br> }<br><br> ],<br><br> "code": "print('helloworld')",<br><br> "msg_id": ""<br><br> }<br><br>} |The execution results in the tool. |


<span id="r7bxWhvI"></span>
## Sample request

```JSON
POST https://agentkit.ap-southeast-1.bytepluses.com?Action=InvokeTool&Version=2025-10-30 HTTP/1.1
Content-Type: application/json
{
    "ToolId": "t-yebi04gb28o2eybt****",
    "UserSessionId": "session-1",
    "OperationType": "RunCode",
    "OperationPayload": "{\"code\": \"print('helloworld')\",\"timeout\": 30,\"kernel_name\": \"python3\"}"
}
```


<span id="or8la5Ln"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "02176751173569200000000000000000000ffffac10029*******",
        "Action": "InvokeTool",
        "Version": "2025-10-30",
        "Service": "agentkit",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ToolId": "t-yebi04gb28o2eybt****",
        "UserSessionId": "session-1",
        "SessionId": "s-yecrzqygw0o2eybt****",
        "Endpoint": "https://sd5acdbuo20h0ng5g****.apigateway-****.volceapi.com/?faasInstanceName=vefaas-****",
        "InternalEndpoint": "",
        "Result": "{\n  \"success\": true,\n  \"message\": \"Code executed successfully\",\n  \"data\": {\n    \"kernel_name\": \"python3\",\n    \"session_id\": \"****\",\n    \"status\": \"ok\",\n    \"execution_count\": 1,\n    \"outputs\": [\n      {\n        \"output_type\": \"stream\",\n        \"name\": \"stdout\",\n        \"text\": \"helloworld\\n\",\n        \"data\": null,\n        \"metadata\": {},\n        \"execution_count\": null,\n        \"ename\": null,\n        \"evalue\": null,\n        \"traceback\": null\n      }\n    ],\n    \"code\": \"print('helloworld')\",\n    \"msg_id\": \"****\"\n  }\n}"
    }
}
```


<span id="jCceUlnG"></span>
## Error codes

To learn more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).

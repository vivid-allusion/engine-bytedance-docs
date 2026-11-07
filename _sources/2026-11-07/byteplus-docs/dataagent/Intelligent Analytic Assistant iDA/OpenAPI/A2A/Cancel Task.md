---
title: "Cancel Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Cancel_Task"
---

<span id="93cae33a"></span>
## A2A cancelTask

<span id="824bc6d1"></span>
### Request description

It is used to cancel an ongoing task.


* The caller can only cancel tasks that he owns.



|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/` |
|`method` |`CancelTask` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


&nbsp;

<span id="882c4898"></span>
### Request parameters

> The original text does not provide a separate parameter table. The following are the **JSON\-RPC 2.0** request structure parameters organized according to the request description and examples.


<span id="92801152"></span>
#### Top\-level parameters (JSON\-RPC)


|Parameter name |Type |Is it required? |Explain |
|---|---|---|---|
|`jsonrpc` |string |Yes |Fixed as `"2.0"` |
|`id` |string |number |Yes |
|`method` |string |Yes |Fixed as `"CancelTask"` |
|`params` |object |Yes |Business parameter objects, see table below |


<span id="eb888d8e"></span>
#### Params parameter


|Parameter name |Type |Is it required? |Explain |
|---|---|---|---|
|`task.id` |string |No (choose one of three) |Task ID (choose one of `taskId`and `id`). |
|`taskId` |string |No (choose one of three) |Task ID (choose one of `task.id`and `id`). |
|`id` |string |No (choose one of three) |Task ID (choose one of `task.id`and `taskId`). |
|`contextId` |string |No |Session/Context ID. Additional verification tasks and session attribution are passed in. |


&nbsp;

<span id="c3e0b017"></span>
### Request example

Standard Curl Example:

```Plain
curl -X POST \
  "https://\${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/" \
  -H "Authorization: Bearer \${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"jsonrpc":"2.0","id":5,"method":"CancelTask","params":{"task":{"id":"9105"}}}' \
  --silent | jq
```


<span id="66303c02"></span>
### Return parameters


|Field path |Type |Explain |
|---|---|---|
|`jsonrpc` |string |JSON\-RPC protocol version, fixed to `"2.0"`. |
|`id` |number |Request ID, corresponding to the `id`in the request body. |
|`result` |object |Business results after a successful request. |
|`result.success` |boolean |Whether the operation was successful. `True`indicates that the cancellation request was successfully received. |
|`result.message` |string |Additional information, usually empty string on success. |


<span id="4a30fa7a"></span>
#### Back to example

```Plain
{
  "jsonrpc": "2.0",
  "id": 5,
  "result": {
    "success": true,
    "message": ""
  }
}
```


&nbsp;

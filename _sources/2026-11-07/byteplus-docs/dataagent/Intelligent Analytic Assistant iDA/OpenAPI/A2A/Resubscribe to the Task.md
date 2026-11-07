---
title: "Resubscribe to the Task"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Resubscribe_to_the_Task"
---

<span id="3a300d9f"></span>
## A2A Re\-subscribeToTask

<span id="20716f85"></span>
### Request description

It is used for scenarios such as network reconnection and page recovery. After the call is successful, the server level will first return the current **snapshot (snapshot)**  of the task, and then continue to push `statusUpdate`, `artifactUpdate`and other events through **SSE (Server\-Sent Events)** .


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/` |
|`method` |`SubscribeToTask` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |
|return form |`Text/event-stream`(SSE, continuous streaming return) |


<span id="211f3601"></span>
### Request parameters

> The original text does not provide a separate parameter table. The following are the **JSON\-RPC 2.0** request structure parameters organized according to the request description and examples.


<span id="44f7fa14"></span>
#### Top\-level parameters (JSON\-RPC)


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`jsonrpc` |string |Yes |Fixed as `"2.0"` |
|`id` |string |number |Yes |
|`method` |string |Yes |Fixed as `"SubscribeToTask"` |
|`params` |object |Yes |Business parameter objects, see table below |


<span id="4949c0c1"></span>
#### Params parameter

TaskId, id and task.id are obtained in the return result of [Start Streaming Q & A](https://docs.byteplus.com/docs/dataagent/Start_Streaming_Q_A) sse.


|Parameter name |Type |Is it required? |Description |
|---|---|---|---|
|`taskId` |string |No (choose one of three) |Task ID (choose one of `id`and `task.id`) |
|`id` |string |No (choose one of three) |Task ID (choose one of `taskId`and `task.id`) |
|`task.id` |string |No (choose one of three) |Task ID (choose one of `taskId`and `id`) |
|`contextId` |string |No |Session/Context ID. Additional verification of task and session attribution is passed in |


<span id="a39664a5"></span>
### Request example

Standard Curl Example:

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"jsonrpc":"2.0","id":2,"method":"SubscribeToTask","params":{"taskId":"7103"}}'
```


<span id="861af5e4"></span>
### Return parameters

`Content-Type: text/event-stream`. Each SSE data is a JSON\-RPC result envelope with the same event structure as `SendStreamingMessage`; `data: [DONE]`is returned at the end of the stream.

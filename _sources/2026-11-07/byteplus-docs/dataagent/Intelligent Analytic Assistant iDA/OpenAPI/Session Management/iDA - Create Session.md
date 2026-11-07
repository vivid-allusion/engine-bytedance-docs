---
title: "iDA - Create Session"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Create_Session"
---

<span id="460c0f03"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/createSession` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


Before calling the A2A interface, create a session with `createSession`and convert the returned `data.sessionInfo.id`**to string** as the `contextId`of the A2A request. When you need to restore pages or query session details, you can call `sessionInfo`to get session, message, and task information.

**Authentication:**  `Both createSession`and `sessionInfo`interfaces support existing OpenAPI **JWT authentication** or **x\-token signature authentication** .


* JWT call: use `Authorization: Bearer ${JWT_TOKEN}`

* When the request body is JSON: set `Content-Type: application/json`


<span id="a9955730"></span>
### Request parameters


|Parameter name |Type |Is it required? |Explain |
|---|---|---|---|
|agentId |integer |Yes |Agent ID. Used to specify the target agent to create the session. |
|name |string |No |Session name (used to present/distinguish the session). |
|source |string |No |Invoke source identifier. Example: `OpenAPI`. |
|version |string |No |Call version ID. Example: `v5`. |


<span id="cfb8697f"></span>
### Request example

Standard cURL example:

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/createSession" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"agentId":430,"name":"OpenAPI 数据问答","source":"openapi","version":"v5"}' \
  --silent | jq
```


<span id="1ab317de"></span>
### Return parameters

**Returns successfully:**  `data.sessionInfo`returns new session information. The current implementation stably gets the `id`and `name`; subsequent A2A calls use the `id`(converted to string) as the `contextId`.


|Field path |Type |Explain |
|---|---|---|
|code |string |Return code. Success example: `llm/ok`. |
|msg |object |Returns information (possibly an empty object). |
|data |object |Return data. |
|data.sessionInfo |object |The newly created session information. |
|data.sessionInfo.id |integer |Session ID. Subsequent A2A calls need to convert it to a string as a `contextId`. |
|data.sessionInfo.name |string |Session name. |


Successful return example:

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "sessionInfo": {
      "id": 14468,
      "name": "OpenAPI Data Q&A"
    }
  },
  "msg": {}
}
```

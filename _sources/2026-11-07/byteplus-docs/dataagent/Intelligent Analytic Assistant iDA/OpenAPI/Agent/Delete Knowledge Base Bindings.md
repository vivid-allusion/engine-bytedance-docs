---
title: "Delete Knowledge Base Bindings"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Delete_Knowledge_Base_Bindings"
---

<span id="2927edc0"></span>
## Delete Knowledge Base Bindings

Unbind the binding relationship between the specified agent and the knowledge base. A single request can unbind multiple binding relationships in batches.

<span id="dc24efdd"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/removeKnowledgeBase` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|Content\-Type |`application/json` |


<span id="9effef16"></span>
### Request parameters


|Location |Parameter |Type |Is it required? |Sample value |Explain |
|---|---|---|---|---|---|
|ROOT |agentId |Number |Yes |`61` |Agent ID |
|ROOT |knowledgeBaseIds |Number[] |Yes |`[45]` |**List of knowledge base binding relationship IDs** (Note: it is a binding relationship ID, not a knowledge base ID). It cannot be empty, otherwise it will report missing parameters. |


> Tip: You can get the binding relationship ID (that is, return the `id`field in items) through the "View Agent Binding Knowledge" interface.


<span id="5f64848c"></span>
### Request example

```Plain
curl -sS -X POST "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/removeKnowledgeBase" -H "Authorization: Bearer ${JWT_TOKEN}" -H "Content-Type: application/json" --data-raw '{"agentId":279,"knowledgeBaseIds":[25]}' | jq
```


<span id="b15c9d39"></span>
### Return parameters


|Location |Parameter |Type |Sample value |
|---|---|---|---|
|code |String |`llm/ok` |request status code |
|data |Object |See example |Return data |
|data.success |Number[] |`[45]` |List of successfully unbound binding relationship IDs |
|data.failed |Array |`[]` |List of unbinding failures (the structure is subject to the actual return) |
|data.message |String |`"Untied successfully"` |Operation prompt information |
|msg |Object |`{}` |Additional information (if applicable) |


<span id="7208b8be"></span>
### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "errorMsg": null,
    "extra": null,
    "failed": [],
    "message": "Unbind success",
    "success": [
      25
    ]
  },
  "msg": {}
}
```

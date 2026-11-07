---
title: "Agent Binding Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Agent_Binding_Knowledge_Base"
---

<span id="c9219868"></span>
## Agent binding knowledge base bindKnowledgeBase

<span id="6082149e"></span>
### Request description

Used to bind a **knowledge engine knowledge base** to a specified agent.


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/bindKnowledgeBase` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


<span id="eb208f1c"></span>
### Request parameters


|Location |Parameter |Type |Is it required? |Sample value |Parameter transfer description |
|---|---|---|---|---|---|
|Body |`agentId` |number |Yes |`61` |Agent ID. |
|Body |`appId` |number |No |`1` |Project ID (knowledge engine project), as the knowledge base ownership tenant.<br><br>Data source reference[IDA - Acquisition Knowledge Base Project](https://docs.byteplus.com/docs/dataagent/118671) |
|Body |`knowledgeEngineBaseIds` |number[] |No |`[182]` |List of Knowledge Engine Knowledge Base IDs.<br><br>Data source reference[IDA - Get the list of knowledge bases under the project](https://docs.byteplus.com/docs/dataagent/118675) |


> Description: When the `knowledgeEngineBaseIds`is an empty array or not passed, the interface behavior (whether to empty the binding/do not change) is subject to the actual implementation.


<span id="4e5479ba"></span>
### Request example

Standard Curl Example:

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/bindKnowledgeBase" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --data-raw '{"agentId":279,"appId":1,"knowledgeEngineBaseIds":[182]}' \
  --silent | jq
```


<span id="6989cd12"></span>
#### Return parameters

<span id="6efaf777"></span>
## data field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.success` |array |`[...]` |Brief result list of successfully bound knowledge bases. |
|`data.failed` |array |`[]` |Brief result list of knowledge bases that failed to bind. |
|`data.errorMsg` |array |`[]` |List of error messages (often used to summarize error messages). |
|`data.message` |string |`""` |Overall prompt information. |
|`data.extra` |object |`{...}` |Extended information about the binding process (including more complete knowledge base details and classification results). |


<span id="96e30e06"></span>
### data.success [] field (summary results)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.success[].id` |integer |`55` |Knowledge Base ID. |
|`data.success[].name` |string |`XXX knowledge base` |Knowledge base name. |
|`data.success[].success` |boolean |`true` |Whether the binding is successful. |
|`data.success[].errorMsg` |string |null |`null` |


<span id="85f93d1e"></span>
### data.extra field (extended result)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.extra.successKnowledgeBaseList` |array |`[...]` |A complete list of successfully bound knowledge bases. |
|`data.extra.failedKnowledgeBaseList` |array |`[]` |A complete list of knowledge bases that failed to bind. |
|`data.extra.duplicatedKnowledgeBaseList` |array |`[]` |List of rebound repositories (e.g. request contains bound repositories). |


<span id="31fed0da"></span>
### successKnowledgeBaseList [] field (full Knowledge Base information)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`...[].id` |integer |`55` |Knowledge Base ID. |
|`...[].name` |string |`XXX knowledge base` |Knowledge base name. |
|`...[].description` |string |`XXXX's testing knowledge base` |Knowledge base description. |
|`...[].tenantId` |integer |`1` |The tenant ID to which the knowledge base belongs. |
|`...[].createdBy` |string |`admin` |Founder. |
|`...[].createDate` |string |`2026-07-18 13:35:37` |Creation time (string). |
|`...[].createTime` |integer |`1784352937887` |Create timestamp in milliseconds. |
|`...[].updateDate` |string |`2026-07-23 15:44:24` |Update time (string). |
|`...[].updateTime` |integer |`1784792664203` |Update timestamp in milliseconds. |
|`...[].status` |string |`1` |Knowledge base status (enumeration meaning is subject to product\-side definition). |
|`...[].permission` |string |`team` |The scope of knowledge base permissions (the meaning of enumeration is subject to the definition on the product side). |
|`...[].actions` |array |`["read","write","create"]` |The set of operations that the current user can perform on the knowledge base. |
|`...[].approvalRequired` |boolean |`false` |Whether the operation requires approval. |
|`...[].category` |string |`general` |Knowledge base classification. |
|`...[].contentType` |string |`general` |Type of content. |
|`...[].type` |string |`vision` |Knowledge base type. |
|`...[].language` |string |`English` |Knowledge base language. |
|`...[].docNum` |integer |`6` |Number of documents. |
|`...[].chunkNum` |integer |`5` |Number of slices. |
|`...[].tokenNum` |integer |`0` |Number of Tokens. |
|`...[].defaultDocId` |integer |`262` |Default document ID. |
|`...[].parserId` |string |`verag_1_55_kg` |Resolver ID. |
|`...[].parserConfig` |object |`{...}` |Parser configuration. |
|`...[].similarityThreshold` |number |`0.2` |similarity threshold. |
|`...[].vectorSimilarityWeight` |number |`0.3` |Vector similarity weight. |
|`...[].scheduleConfig` |object |`{...}` |Scheduling configuration. |
|`...[].autoLabels` |array |`[]` |Automatic label list. |
|`...[].avatar` |string |null |`null` |
|`...[].llmId` |string |null |`null` |
|`...[].embdId` |string |`""` |Embedding model ID; empty string in the example. |
|`...[].retrievalAppCount` |integer |null |`null` |
|`...[].subjectId` |integer |`0` |Subject ID. |


<span id="c204649d"></span>
### parserConfig field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`...[].parserConfig.pages` |array |`[[1,1000000]]` |Parse the page range. |
|`...[].parserConfig.ragEngine` |string |`sophon` |RAG engine logo. |


<span id="fafd6b36"></span>
### scheduleConfig field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`...[].scheduleConfig.scheduleType` |integer |`0` |Scheduling type. |
|`...[].scheduleConfig.bdbTaskId` |integer |`-1` |BDB task ID; `-1`usually means unbound task. |
|`...[].scheduleConfig.frequency` |string |null |`null` |
|`...[].scheduleConfig.dayOfWeek` |string |null |`null` |
|`...[].scheduleConfig.dayOfMonth` |string |null |`null` |
|`...[].scheduleConfig.timeSetting` |string |null |`null` |


<span id="8fa125d6"></span>
### Result judgment and description


|Project |Explain |
|---|---|
|Binding success determination |`Code = llm/ok`and `data.success [] .success = true`, indicating that the corresponding knowledge base binding is successful. |
|Success List (Brief) |`Data.success is`used to quickly see which knowledge base bindings are successful. |
|Success list (detailed) |`Data.extra. successKnowledgeBaseList`Returns complete information about the successful binding of the knowledge base. |
|failure list |`Data.failed`and `data.extra failedKnowledgeBaseList`are empty to indicate no failures. |
|duplicate list |`Data.extra duplicatedKnowledgeBaseList`is empty to indicate no duplicate bindings. |


<span id="6cee7249"></span>
#### Response example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "errorMsg": [],
    "extra": {
      "duplicatedKnowledgeBaseList": [],
      "failedKnowledgeBaseList": [],
      "successKnowledgeBaseList": [
        {
          "actions": [
            "read",
            "write",
            "create"
          ],
          "approvalRequired": false,
          "autoLabels": [],
          "avatar": null,
          "category": "general",
          "chunkNum": 5,
          "contentType": "general",
          "createDate": "2026-07-18 13:35:37",
          "createTime": 1784352937887,
          "createdBy": "admin",
          "defaultDocId": 262,
          "description": "xxx's test knowledge base",
          "docNum": 6,
          "embdId": "",
          "id": 55,
          "language": "English",
          "llmId": null,
          "name": "xxx's knowledge base",
          "parserConfig": {
            "pages": [
              [
                1,
                1000000
              ]
            ],
            "ragEngine": "sophon"
          },
          "parserId": "verag_1_55_kg",
          "permission": "team",
          "retrievalAppCount": null,
          "scheduleConfig": {
            "bdbTaskId": -1,
            "dayOfMonth": null,
            "dayOfWeek": null,
            "frequency": null,
            "scheduleType": 0,
            "timeSetting": null
          },
          "similarityThreshold": 0.2,
          "status": "1",
          "subjectId": 0,
          "tenantId": 1,
          "tokenNum": 0,
          "type": "vision",
          "updateDate": "2026-07-23 15:44:24",
          "updateTime": 1784792664203,
          "vectorSimilarityWeight": 0.3
        }
      ]
    },
    "failed": [],
    "message": "",
    "success": [
      {
        "errorMsg": null,
        "id": 55,
        "name": "xxx's knowledge base",
        "success": true
      }
    ]
  },
  "msg": {}
}
```


&nbsp;

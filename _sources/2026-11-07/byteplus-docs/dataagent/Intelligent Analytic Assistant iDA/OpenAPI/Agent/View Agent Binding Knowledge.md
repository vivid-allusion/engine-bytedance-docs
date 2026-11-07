---
title: "View Agent Binding Knowledge"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/View_Agent_Binding_Knowledge"
---

<span id="7f71befe"></span>
## View knowledge bindings

Query the list of knowledge bases bound to the specified agent (paged back).

<span id="e24cffda"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/knowledgeBaseList` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|Content\-Type |`application/json` |


<span id="d4979ab3"></span>
### Request parameters


|Location |Parameter |Type |Is it required? |Sample value |Explain |
|---|---|---|---|---|---|
|ROOT |agentId |Number |Yes |`61` |Agent ID |
|ROOT |page |Number |No |`1` |Page number, default `1` |
|ROOT |pageSize |Number |No |`10` |Number of pages, default `5` |


<span id="9dce8318"></span>
### Request example

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/knowledgeBaseList" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --data-raw '{"agentId":279,"page":1,"pageSize":10}' \
  --silent | jq
```


<span id="9bff555b"></span>
### Return parameters

<span id="10e337f8"></span>
## Back to content parsing


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`JSONIFY_PRETTYPRINT_REGULAR` |boolean |`false` |JSON output format control markup (usually without business\-side processing). |
|`code` |string |`llm/ok` |Request result code. `Lm/ok`indicates that the request was successful. |
|`msg` |object |`{}` |Hint object; the example is an empty object. |
|`data` |object |`{...}` |Agent has bound the results of the paging list of the knowledge base. |


<span id="d3006812"></span>
### data field (paging information)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.isSuccess` |boolean |`true` |The query was successful. |
|`data.errorMsg` |string |`""` |Error message; usually empty string on success. |
|`data.items` |array |`[...]` |List of knowledge base bindings for the current page. |
|`data.page` |integer |`1` |The current page number (starting from 1). |
|`data.pageSize` |integer |`10` |Number of pages per page. |
|`data.total` |integer |`2` |Total number of records (total number of binding relationships). |
|`data.totalPages` |integer |`1` |Total number of pages. |
|`data.hasNextPage` |boolean |`false` |Is there a next page? |


<span id="5b9ec7b0"></span>
### data.items[] field (binding record)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.items[].id` |integer |`25` |Binding relationship record ID. |
|`data.items[].agentId` |integer |`279` |Agent ID。 |
|`data.items[].appId` |integer |`1` |App ID. |
|`data.items[].orgId` |integer |`1` |Organization/tenant ID. |
|`data.items[].knowledgeEngineBaseId` |string |`55` |Knowledge Base ID. |
|`data.items[].knowledgeEngineBaseName` |string |`openAPi test` |Knowledge base name. |
|`data.items[].knowledgeBase` |object |`{...}` |Knowledge base details (complete information). |
|`data.items[].knowledgeBaseStatus` |object |`{...}` |Knowledge base status information. |
|`data.items[].isDefault` |boolean |`false` |Is it the default knowledge base? |
|`data.items[].priority` |integer |`0` |Binding priority. |
|`data.items[].status` |integer |`1` |Binding relationship status (enumeration meaning is subject to product\-side definition). |
|`data.items[].deleted` |boolean |`false` |Whether it has been deleted. |
|`data.items[].metaInfo` |object |`{}` |Binding relationship extension information; the example is an empty object. |
|`data.items[].creator` |string |`admin` |Binding relationship creator. |
|`data.items[].updator` |string |`admin` |The binding relationship was recently updated. |
|`data.items[].createdAt` |string |`2026-08-14 10:08:23` |Binding relationship creation time. |
|`data.items[].updatedAt` |string |`2026-08-14 10:08:23` |Binding relationship update time. |


<span id="704a316e"></span>
### data.items[].knowledgeBaseStatus field (knowledge base status)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.items[].knowledgeBaseStatus.code` |string |`1` |Knowledge base status code (the meaning of enumeration is subject to the definition on the product side). |
|`data.items[].knowledgeBaseStatus.message` |string |`VALID` |Knowledge base status description; `VALID`indicates that the knowledge base is valid. |


<span id="63ae8c3e"></span>
### data.items[].knowledgeBase field (knowledge base details)


|Field path |Type |Sample value |explain |
|---|---|---|---|
|`data.items[].knowledgeBase.id` |integer |`55` |Knowledge Base ID. |
|`data.items[].knowledgeBase.name` |string |`openAPi test` |Knowledge base name. |
|`data.items[].knowledgeBase.description` |string |`openAPi test` |Knowledge base description. |
|`data.items[].knowledgeBase.tenantId` |integer |`1` |The tenant ID to which the knowledge base belongs. |
|`data.items[].knowledgeBase.createdBy` |string |`admin` |Knowledge base creator. |
|`data.items[].knowledgeBase.createDate` |string |`2026-07-18 13:35:37` |Creation time (string). |
|`data.items[].knowledgeBase.createTime` |integer |`1784352937887` |Create timestamp in milliseconds. |
|`data.items[].knowledgeBase.updateDate` |string |`2026-07-23 15:44:24` |Update time (string). |
|`data.items[].knowledgeBase.updateTime` |integer |`1784792664203` |Update timestamp in milliseconds. |
|`data.items[].knowledgeBase.status` |string |`1` |Knowledge base status (enumeration meaning is subject to product\-side definition). |
|`data.items[].knowledgeBase.permission` |string |`team` |Knowledge base permission scope. |
|`data.items[].knowledgeBase.actions` |array |`["read","write","create"]` |The set of operations that the current user can perform on the knowledge base. |
|`data.items[].knowledgeBase.approvalRequired` |boolean |`false` |Whether the operation requires approval. |
|`data.items[].knowledgeBase.category` |string |`general` |Knowledge base classification. |
|`data.items[].knowledgeBase.contentType` |string |`general` |Type of content. |
|`data.items[].knowledgeBase.type` |string |`vision` |Knowledge base type. |
|`data.items[].knowledgeBase.language` |string |`English` |Knowledge base language. |
|`data.items[].knowledgeBase.docNum` |integer |`6` / `1` |Number of documents. |
|`data.items[].knowledgeBase.chunkNum` |integer |`5` / `0` |Number of slices. |
|`data.items[].knowledgeBase.tokenNum` |integer |`0` |Number of Tokens. |
|`data.items[].knowledgeBase.defaultDocId` |integer |`269` |Default document ID. |
|`data.items[].knowledgeBase.parserId` |string |`verag_1_55_kg` |Resolver ID. |
|`data.items[].knowledgeBase.parserConfig` |object |`{...}` |Parser configuration. |
|`data.items[].knowledgeBase.scheduleConfig` |object |`{...}` |Scheduling configuration. |
|`data.items[].knowledgeBase.similarityThreshold` |number |`0.2` |similarity threshold. |
|`data.items[].knowledgeBase.vectorSimilarityWeight` |number |`0.3` |Vector similarity weight. |
|`data.items[].knowledgeBase.autoLabels` |array |`[]` |Automatic label list. |
|`data.items[].knowledgeBase.avatar` |string |null |`null` |
|`data.items[].knowledgeBase.llmId` |string |null |`null` |
|`data.items[].knowledgeBase.embdId` |string |`""` |Embedding model ID; empty string in the example. |
|`data.items[].knowledgeBase.retrievalAppCount` |integer |null |`null` |
|`data.items[].knowledgeBase.subjectId` |integer |`0` |Subject ID. |


<span id="97256983"></span>
### parserConfig field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.items[].knowledgeBase.parserConfig.pages` |array |`[[1,1000000]]` |Parse the page range. |
|`data.items[].knowledgeBase.parserConfig.ragEngine` |string |`sophon` |RAG engine logo. |


<span id="4c2cb93f"></span>
### scheduleConfig field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.items[].knowledgeBase.scheduleConfig.scheduleType` |integer |`0` |Scheduling type. |
|`data.items[].knowledgeBase.scheduleConfig.bdbTaskId` |integer |`-1` |BDB task ID; `-1`usually means unbound task. |
|`data.items[].knowledgeBase.scheduleConfig.frequency` |string |null |`null` |
|`data.items[].knowledgeBase.scheduleConfig.dayOfWeek` |string |null |`null` |
|`data.items[].knowledgeBase.scheduleConfig.dayOfMonth` |string |null |`null` |
|`data.items[].knowledgeBase.scheduleConfig.timeSetting` |string |null |`null` |


&nbsp;


|Project |Explain |
|---|---|
|query success determination |`Code = llm/ok`and `data.isSuccess = true`, indicating that the query was successful. |
|number of bindings |`data.total = 1`, indicating that the Agent currently binds 1 knowledge base relationship record. |
|paging status |`Page = 1`, `pageSize = 10`, `totalPages = 1`, `hasNextPage = false`, indicating that all data has been returned. |
|Knowledge Base Status |`KnowgeBaseStatus.message = VALID`means the knowledge base is valid; both records in the example are `VALIDs`. |


<span id="e67dfdfc"></span>
### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "errorMsg": "",
    "hasNextPage": false,
    "isSuccess": true,
    "items": [
      {
        "agentId": 279,
        "appId": 1,
        "createdAt": "2026-08-12 11:45:43",
        "creator": "admin",
        "deleted": false,
        "id": 25,
        "isDefault": false,
        "knowledgeBase": {
          "actions": [
            "read",
            "write",
            "create"
          ],
          "approvalRequired": false,
          "autoLabels": [],
          "avatar": null,
          "category": "general",
          "chunkNum": 0,
          "contentType": "general",
          "createDate": "2026-08-12 11:39:38",
          "createTime": 1786505978938,
          "createdBy": "admin",
          "defaultDocId": 269,
          "description": "openAPi test",
          "docNum": 1,
          "embdId": "",
          "id": 56,
          "language": "English",
          "llmId": null,
          "name": "openAPi test",
          "parserConfig": {
            "pages": [
              [
                1,
                1000000
              ]
            ],
            "ragEngine": "sophon"
          },
          "parserId": "verag_1_56_kg",
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
          "updateDate": "2026-08-12 11:39:56",
          "updateTime": 1786505996952,
          "vectorSimilarityWeight": 0.3
        },
        "knowledgeBaseStatus": {
          "code": "1",
          "message": "VALID"
        },
        "knowledgeEngineBaseId": "56",
        "knowledgeEngineBaseName": "openAPi test",
        "metaInfo": {},
        "orgId": 1,
        "priority": 0,
        "status": 1,
        "updatedAt": "2026-08-14 10:32:34",
        "updator": "admin"
      }
    ],
    "page": 1,
    "pageSize": 10,
    "total": 1,
    "totalPages": 1
  },
  "msg": {}
}
```

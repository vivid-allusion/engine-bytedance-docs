---
title: "iDA - Get List of Knowledge Bases Under the Project"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Get_List_of_Knowledge_Bases_Under_the_Project"
---

POST dataAgent/llm/openApi/v2/deepresearch/knowledgeEngineBaseList

<span id="2c955aeb"></span>
### Interface description

Get the knowledge base list of the specified item (tenant/app) under the knowledge engine and return it by pagination.

Return only the knowledge base that the user has permission to

<span id="9d83b221"></span>
### Request parameters (JSON Body)


|Field |Type |Required |Default value |Explain |
|---|---|---|---|---|
|`appId` |int/string |Yes |*  |Project (tenant) ID; if you need to be accurate to the knowledge base under a certain project, you need to pass it |
|`page` |int |Yes |`1` |Current page number, starting from 1 |
|`pageSize` |int |Yes |`5` |number of pages per page |
|`kw` |string |No |*  |Fuzzy search keywords, matching knowledge base names |


<span id="b3618538"></span>
### Return parameters

Returns the standard page structure `PaginationInfo`:


|Field |Type |Explain |
|---|---|---|
|`data.page` |int |current page number |
|`data.pageSize` |int |number of pages per page |
|`data.total` |int |total number of articles |
|`data.totalPages` |int |total number of pages |
|`data.hasNextPage` |bool |Is there a next page? |
|`data.isSuccess` |bool |Was it successful? |
|`data.errorMsg` |string |Error message (success is empty) |
|`data.items` |Array |Knowledge base list, passthrough fields ( `id`, `name`, `category`, `tenantId`, etc.) |


<span id="e89a69a7"></span>
### Call example

Example A: Paged query (without keywords)

```Bash
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/knowledgeEngineBaseList" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Content-Type: application/json' \
  --data-raw '{"page":1,"pageSize":200,"appId":1}' \
  --silent | jq
```


Example B: fuzzy search with keywords

```Bash
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/knowledgeEngineBaseList" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Accept: application/json, text/plain, */*' \

  -H 'Content-Type: application/json' \
  --data-raw '{"page":1,"pageSize":200,"appId":1,"kw":"存量"}' \
  --silent | jq
```


Response (real example, excerpt):

```JSON
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "msg": {},
  "data": {
    "errorMsg": "",
    "hasNextPage": false,
    "isSuccess": true,
    "page": 1,
    "pageSize": 200,
    "total": 6,
    "totalPages": 1,
    "items": [
      {
        "id": 104,
        "name": "Existing knowledge migration-10004",
        "description": "Existing knowledge migration",
        "category": "general",
        "contentType": "general",
        "type": "normal",
        "status": "1",
        "tenantId": 1,
        "subjectId": 0,
        "createdBy": "admin",
        "createDate": "2026-06-04 15:04:41",
        "createTime": 1780556681025,
        "updateDate": "2026-06-04 15:04:41",
        "updateTime": 1780556681114,
        "docNum": 3,
        "chunkNum": 152,
        "tokenNum": 0,
        "defaultDocId": 571,
        "language": "English",
        "embdId": "",
        "llmId": null,
        "avatar": null,
        "actions": ["read", "write"],
        "autoLabels": [],
        "permission": "team",
        "parserId": "verag_1_189_kg",
        "parserConfig": {
          "pages": [[1, 1000000]],
          "ragEngine": "sophon"
        },
        "scheduleConfig": {
          "bdbTaskId": -1,
          "dayOfMonth": null,
          "dayOfWeek": null,
          "frequency": null,
          "scheduleType": 0,
          "timeSetting": null
        },
        "similarityThreshold": 0.2,
        "vectorSimilarityWeight": 0.3
      },
      {
        "id": 188,
        "name": "Existing knowledge migration-4",
        "description": "Existing knowledge migration",
        "docNum": 1,
        "chunkNum": 76,
        "defaultDocId": 569,
        "tenantId": 1,
        "createdBy": "admin",
        "createDate": "2026-06-03 18:43:09",
        "updateDate": "2026-06-03 18:43:10",
        "actions": ["read", "write"],
        "permission": "team",
        "parserId": "verag_1_188_kg",
        "parserConfig": {"pages": [[1, 1000000]], "ragEngine": "sophon"},
        "scheduleConfig": {"bdbTaskId": -1, "scheduleType": 0},
        "similarityThreshold": 0.2,
        "vectorSimilarityWeight": 0.3
      }
    ]
  }
}
```

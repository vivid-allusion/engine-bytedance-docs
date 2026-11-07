---
title: "iDA - Get a List of Documents Under the Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Get_a_List_of_Documents_Under_the_Knowledge_Base"
---

POST /dataAgent/llm/openApi/v2/deepresearch/getKnowledgeBaseDocuments

<span id="8606ca45"></span>
## Interface description

Query the list of documents under the knowledge base.

<span id="2e298189"></span>
### Request parameters (JSON Body)


|Field |Type |Required |Default value |Explain |
|---|---|---|---|---|
|`agentId` |int |Yes |*  |Agent ID |
|`appId` |int |Yes |*  |Project (tenant) ID |
|getKnowledgeBaseDocuments |int |Yes |*  |Knowledge engine side knowledge base ID, need to cooperate with `appId`use |
|`kw` |string |No |*  |Document name fuzzy search |
|`page` |int |No |`1` |current page number |
|`pageSize` |int |No |`5` |number of pages per page |


<span id="e847cd8b"></span>
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
|`data.errorMsg` |string |error message |
|`data.items` |array |Document list, common fields `id`, `name`, `kbId`, `size`, `type`, `status`, `progress`, `progressMsg`, `chunkNum`, `tokenNum`, `parserId`, `parserConfig`, `labels`, `location`, `createDate`, `updateDate`, etc |


<span id="5255733e"></span>
### Call example

Imported parameter

```Bash
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/deepresearch/getKnowledgeBaseDocuments" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'Accept-Language: zh-CN,zh;q=0.9' \
  -H 'App-Id: 1' \
  -H 'Content-Language: zh-CN' \
  -H 'Content-Type: application/json' \
  --data-raw '{"page":1,"pageSize":200,"agentId":2,"appId":1,"knowledgeEngineBaseId":189}' \
  --silent | jq
```


Response:

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
    "total": 4,
    "totalPages": 1,
    "items": [
      {
        "id": 1001,
        "name": "xxx品牌知识库.docx",
        "kbId": 100,
        "type": "WORD",
        "status": "1",
        "size": 180000,
        "chunkNum": 5,
        "tokenNum": 0,
        "progress": 1,
        "progressMsg": "FINISHED",
        "processDuation": 0.68,
        "sourceType": "sophon",
        "parserId": "xxxx",
        "parserConfig": {
          "chunkSettings": {
            "chunkType": "default",
            "genAtomicQuestion": false,
            "maxSegmentLength": 1024,
            "mergeSmallChunks": false,
            "removeSpaces": true,
            "removeUrlsPics": true,
            "separator": "\n",
            "smallChunkTokenThreshold": 100
          },
          "completenessCheck": false,
          "imageExtraction": true,
          "sensitiveWordCheck": false,
          "sophonSubDocChunk": {"xxxx": 5},
          "spellCheck": false,
          "tableExtraction": false
        },
        "location": "/storage/rag/tenant-id/file-uuid-1.docx",
        "downloadable": true,
        "isEnabled": true,
        "folderId": 0,
        "labels": [],
        "autoDeleteOnExpire": false,
        "validDate": "永久有效", // permanent validity
        "createdBy": "user_001",
        "createDate": "2026-06-06 10:00:00",
        "createTime": 1700000000000,
        "updateDate": "2026-06-06 10:00:30",
        "updateTime": 1700000030000,
        "run": "3",
        "subDocs": [],
        "contentCategory": []
      },
      {
        "id": 1002,
        "name": "knowledge_base_sample.csv",
        "kbId": 100,
        "type": "CSV",
        "status": "1",
        "size": 6000,
        "chunkNum": 64,
        "tokenNum": 0,
        "progress": 1,
        "progressMsg": "FINISHED",
        "sourceType": "sophon",
        "parserId": "xxxx",
        "labels": [
          {
            "labelId": 11,
            "labelName": "da_knowledge_type",
            "labelType": "multiple_value_text",
            "labelValueBuilder": "manual",
            "labelValues": [
              {
                "id": 34,
                "labelValueBuilder": "manual",
                "value": "BUSINESS_KNOWLEDGE",
                "valueUsage": 0
              }
            ],
            "createDate": "2026-06-06 10:00:00",
            "createTime": 1700000000000,
            "updateDate": "2026-06-06 10:00:00",
            "updateTime": 1700000000000
          }
        ],
        "location": "/storage/rag/tenant-id/file-uuid-2.csv",
        "downloadable": true,
        "isEnabled": true,
        "folderId": 0,
        "validDate": "永久有效", // permanent validity
        "createdBy": "user_001",
        "createDate": "2026-06-02 10:00:00",
        "updateDate": "2026-06-02 10:00:10"
      },
      {
        "id": 1003,
        "name": "财务分析框架模板.pdf",
        "kbId": 100,
        "type": "PDF",
        "size": 700000,
        "chunkNum": 12,
        "progress": 1,
        "progressMsg": "FINISHED",
        "parserId": "xxxx",
        "labels": [
          {
            "labelId": 11,
            "labelName": "da_knowledge_type",
            "labelValues": [
              {
                "id": 35,
                "value": "ANALYSIS_TEMPLATE",
                "labelValueBuilder": "manual"
              }
            ]
          }
        ],
        "location": "/storage/rag/tenant-id/file-uuid-3.pdf",
        "createDate": "2026-06-02 10:00:00",
        "updateDate": "2026-06-02 10:00:30"
      },
      {
        "id": 1004,
        "name": "eval_details_sample.txt",
        "kbId": 100,
        "type": "TXT",
        "size": 56000,
        "chunkNum": 76,
        "progress": 1,
        "progressMsg": "FINISHED",
        "parserId": "xxxx",
        "location": "/storage/rag/tenant-id/file-uuid-4.txt",
        "createDate": "2026-06-02 10:00:00",
        "updateDate": "2026-06-02 10:00:10"
      }
    ]
  }
}
```

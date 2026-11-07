---
title: "iDA - Get List of Prompt Templates"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Get_List_of_Prompt_Templates"
---

<span id="IXIYRkjGXi"></span>
### Request description


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates?agentId=80&isPublic=1&offset=0&limit=30` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


<span id="iSRsdxm1oZ"></span>
### Request parameters


|Parameter |Type |Required |Default value |Explain |
|---|---|---|---|---|
|`agentId` |int |Yes |*  |Agent ID |
|`isPublic` |int |No |*  |Public status: `1`public, `0`private |
|`isOwner` |int/bool |No |*  |When passing `1`, only the template created by the current `x-user`is returned |
|`query` / `q` |string |No |*  |A fuzzy search by template name, description, or scene name |
|`mode` |string |No |*  |`knowledge_qa`or `deep_research` |
|`myCollected` / `isCollected` |int/bool |No |`0` |When passing `1`, only the templates of the current user's collection are returned |
|`isTopPick` |int/bool |No |`0` |Return to the selected template when passing `1` |
|`orderBy` |string |No |`collected_cnt` |Optional: `collected_cnt`, `used_cnt`, `most_recent`, `like_cnt`, `share_cnt` |
|`limit` |int |No |`20` |Number of pages; maximum is `100` |
|`offset` |int |No |`0` |Paging offset with a minimum value of `0` |
|`include` |string |No |`stats,myFlags` |Response extended field, comma separated; `stats`returns count, `myFlags`returns current user likes/favorites status, `none`means none is returned |


<span id="cIkoNpIS7F"></span>
### Request example

Standard Curl Example:

```bash
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates?agentId=80&isPublic=1&offset=0&limit=30" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --silent | jq
```


<span id="dcBAqdROs6"></span>
### Return parameters

&nbsp;


|Field |Type |Explain |
|---|---|---|
|`code` |string |Business code, success is `llm/ok` |
|`data.items` |array |template list |
|`data.total` |int |Total number of eligible templates |
|`data.limit` |int |Number of pages per page |
|`data.offset` |int |current paging offset |
|`data.hasMore` |bool |Is there a next page? |
|`msg` |object |error message container |


<span id="a4c8e50b"></span>
### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "hasMore": false,
    "items": [
      {
        "agentId": 279,
        "collectedCnt": 0,
        "conversationOptions": {
          "enableAeolusAssetSearch": false,
          "enableHiveDataSearch": false,
          "enableLarkQA": false,
          "enableWebSearch": true,
          "enabledMcpServers": [],
          "templateSkills": []
        },
        "ctime": "2026-08-12T13:57:21",
        "data": "请评估活动策划方案：{{e7f79b80-871a-4c39-af89-1e6b06931668}}",
        "description": "对活动策划方案进行全面评估和优化",
        "id": 186,
        "isOfficial": false,
        "isPinned": false,
        "isPublic": 1,
        "isRecommend": 0,
        "likeCnt": 0,
        "me": {
          "collected": false,
          "liked": false
        },
        "mode": "knowledge_qa",
        "mtime": "2026-08-12T13:57:21",
        "name": "活动策划",
        "owner": "admin",
        "previewImageList": [],
        "scene": [
          "PLANNING",
          "DOCUMENT_COMPOSITION"
        ],
        "shareCnt": 0,
        "status": 1,
        "templateAvailableSkills": [],
        "templateVariables": [
          {
            "creator": "admin",
            "ctime": "2026-08-12T13:57:21",
            "defaultValue": {},
            "description": "支持 Word、PDF、Markdown 文件",
            "id": 549,
            "mtime": "2026-08-12T13:57:21",
            "name": "活动策划方案",
            "required": 1,
            "sortOrder": 0,
            "status": 1,
            "templateId": 186,
            "updatedBy": "admin",
            "valueType": "file",
            "varId": "e7f79b80-871a-4c39-af89-1e6b06931668"
          }
        ],
        "updatedBy": "admin",
        "usedCnt": 0
      }
    ],
    "limit": 30,
    "offset": 0,
    "total": 1
  },
  "msg": {}
}
```

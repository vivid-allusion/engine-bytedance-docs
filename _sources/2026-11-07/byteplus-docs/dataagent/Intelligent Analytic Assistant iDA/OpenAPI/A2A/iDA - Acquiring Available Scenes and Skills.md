---
title: "iDA - Acquiring Available Scenes and Skills"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Acquiring_Available_Scenes_and_Skills"
---

<span id="jRJZNQ14Ej"></span>
### Acquire Available Scenes and Skills

Before initiating the A2A OpenAPI Q & A, you can call this interface to query the configured scenarios and skills of the specified agent. Returns a tree structure: `category = group`represents the scene grouping, and `category = scene`represents the specific scene that can be used for Q & A.

<span id="2561dfce"></span>
### Request description


|Project |Content |
|---|---|
|request method |`GET` |
|request address |https://{domain}/dataAgent/llm/openApi/v2/a2a/skills |
|Authentication method |`Authorization: Bearer <JWT>` |
|default language |`Content-Language: zh-CN`(optional) |


> Authentication method: OpenAPI Token, using `Authorization: Bearer < JWT >`request header.


<span id="f1550d33"></span>
### Request parameters


|Location |Parameter |Type |Is it required? |Description |
|---|---|---|---|---|
|Query |`agent_id` |int |Yes |Agent ID |
|Query |`include_disabled` |bool |No |Whether to return a disabled node, the default is `false`. The node where `isEnabled = true`should be selected when answering questions. |
|Header |`Content-Language` |string |No |Returns content language, such as `zh-CN`; default `zh-CN`. |


<span id="12a5f463"></span>
### Request example

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/a2a/skills?agentId=11&page=1&pageSize=100" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --silent | jq
```


<span id="9c5df553"></span>
### How to determine scenes and skills


1. Recursively traverse `data.scenes [] .children`, selecting the node with `category = scene`and `isEnabled = true`.

2. Use the `id`of the scene node as A2A `message.metadata.sceneId`. For example, the following "data quickly find" id = 3291, then pass in `sceneId:`3291.

3. To explicitly preload skills, select the entry `enable = true`from the `skills`of the scene and `code`as A2A `message.metadata.skill`. Generally, only the `sceneId`can be passed, and the corresponding skill is loaded by the scene binding relationship; only when a single skill needs to be forcibly specified can the `skill`be passed.


**Note:**  `skill`must use skill code, such as asset\-query\-after\-search; do not pass the scene name (such as "Data Quickly Find"), skill display name `displayName`, scene alias `scene-5`or numeric `skillId`.

<span id="ad9aa325"></span>
### A2A parameter example

```Plain
{
  "message": {
    "metadata": {
      "sceneId": 3291,
      "skill": "asset-query-after-search"
    }
  }
}
```


<span id="6adb62f2"></span>
### Return parameters

Response (real example, excerpt):

```Plain
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "scenes": [
            {
                "builtinSceneCode": "group_search",
                "category": "group",
                "children": [
                    {
                        "builtinSceneCode": "data_find",
                        "category": "scene",
                        "children": [],
                        "config": {
                            "webSearchEnabled": true
                        },
                        "fromBuiltinScene": "data_find",
                        "icon": "",
                        "id": 3291,
                        "isEnabled": true,
                        "isOfficial": true,
                        "modelType": "text",
                        "name": "数据速找",
                        "nameEn": "find data",
                        "order": 2,
                        "parentId": 3285,
                        "placeholder": "",
                        "recommendedQuestions": [
                            {
                                "id": 11736,
                                "question": "「xxx」数据在哪个数据集可以查看到？",
                                "questionEn": "where can i view the “xxx” data – which  dataset contains it?",
                                "resource": {
                                    "datasetList": [],
                                    "fileList": [],
                                    "larkFileList": [],
                                    "reportList": []
                                },
                                "sceneId": 3291
                            },
                            {
                                "id": 11737,
                                "question": "「xxx」指标是什么意思？在什么数据集能查到？",
                                "questionEn": "what does the “xxx” metric mean, and in which dataset can i query it?",
                                "resource": {
                                    "datasetList": [],
                                    "fileList": [],
                                    "larkFileList": [],
                                    "reportList": []
                                },
                                "sceneId": 3291
                            }
                        ],
                        "skills": [
                            {
                                "code": "asset-query-after-search",
                                "displayName": "资产搜索的后续查数策略",
                                "displayNameEn": "",
                                "enable": true,
                                "icon": "",
                                "isBuiltIn": true,
                                "name": "asset-query-after-search",
                                "skillId": 1,
                                "supportCheck": false
                            },
                            {
                                "code": "query_aeolus_report",
                                "displayName": "DataWind图表查询",
                                "displayNameEn": "",
                                "enable": true,
                                "icon": "",
                                "isBuiltIn": true,
                                "name": "query_aeolus_report",
                                "skillId": 12,
                                "supportCheck": true
                            },
                            {
                                "code": "resource-statistics",
                                "displayName": "DataWind资源统计",
                                "displayNameEn": "",
                                "enable": true,
                                "icon": "",
                                "isBuiltIn": true,
                                "name": "resource-statistics",
                                "skillId": 14,
                                "supportCheck": false
                            }
                        ]
                    }
                ],
                "config": {
                    "webSearchEnabled": true
                },
                "fromBuiltinScene": "group_search",
                "icon": "assetssearch",
                "id": 3285,
                "isEnabled": true,
                "isOfficial": true,
                "modelType": "text",
                "name": "知识检索",
                "nameEn": "search",
                "order": 1,
                "parentId": null,
                "placeholder": "",
                "recommendedQuestions": [],
                "skills": []
            }
        ]
    },
    "msg": {}
}
```

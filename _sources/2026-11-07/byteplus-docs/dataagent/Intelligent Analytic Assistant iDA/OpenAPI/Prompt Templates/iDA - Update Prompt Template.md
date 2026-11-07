---
title: "iDA - Update Prompt Template"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Update_Prompt_Template"
---

<span id="2964e1da"></span>
## Update prompt word template

Used to update the cue word template for the specified `templateId`. The calling user must be the template owner or the agent administrator.

<span id="14c66c86"></span>
### Request description


|Project |Content |
|---|---|
|request method |`PUT` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates/{templateId}` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


\*\* Update rules: \*\* Except for the path parameter `templateId`, the remaining fields are passed in on demand; the unpassed fields remain unchanged.

<span id="2f124d03"></span>
### Path parameter


|Parameter |Type |Required |Explain |
|---|---|---|---|
|`templateId` |int / string |Yes |Cue word template ID |


<span id="361ba2be"></span>
### Request parameters (Body, `application/json`)


|Parameter |Type |Required |Explain |
|---|---|---|---|
|`name` |string |No |Template name, up to 255 characters |
|`description` |string |No |template description |
|`scene` |array |No |List of business scenarios |
|`sceneName` |object / string / array |No |Scene display name |
|`isPublic` |int |No |`1`public, `0`private |
|`data` |string |No |prompt word template body |
|`mode` |string / array |No |Template mode: `knowledge_qa`or `deep_research` |
|`conversationOptions` |object |No |session capability configuration |
|`templateVariables` |array |No |List of template variables ( **full synchronization semantics**, see note below) |
|`isRecommend` |int |No |Agent administrator privileges are required to modify the recommendation status |


<span id="7184a366"></span>
### Request example

Standard Curl Example:

```Plain
curl -X PUT \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates/186" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  --header 'Content-Type: application/json' \
  --data-raw '{"name":"活动策划","description":"更新后的模板描述","isPublic":1}' \
  --silent | jq
```


Supplementary examples (including business authentication headers and variable updates):

```Plain
curl -X PUT \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates/74" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --data-raw '{
    "name": "活动策划",
    "description": "对活动策划方案进行全面评估和优化",
    "scene": ["PLANNING", "DOCUMENT_COMPOSITION"],
    "isPublic": 1,
    "data": "请评估活动策划方案：{{e7f79b80-871a-4c39-af89-1e6b06931668}}",
    "mode": "knowledge_qa",
    "conversationOptions": {
      "enableLarkQA": false,
      "enableWebSearch": true,
      "enableAeolusAssetSearch": false,
      "enableHiveDataSearch": false,
      "enabledMcpServers": [],
      "templateSkills": []
    },
    "templateVariables": [
      {
        "id": 133,
        "varId": "e7f79b80-871a-4c39-af89-1e6b06931668",
        "name": "活动策划方案",
        "description": "支持 Word、PDF、Markdown 文件",
        "required": 1,
        "valueType": "file",
        "defaultValue": {}
      }
    ]
  }' \
  --silent | jq
```


<span id="9a86574a"></span>
### Notes (important)


1. **Do not use the entire template object returned by a page GET directly as an update Body.** 


For example `collectedCnt`, `likeCnt`, `shareCnt`, `usedCnt`, `me`, `owner`, `status`, `ctime`, `mtime`, etc. are response or system fields that should be removed from the request, otherwise it may cause verification failure or update exceptions.


2. **When not modifying variables: omit the** **`templateVariables`field entirely.** 


After omission, the variables in the database remain unchanged.


3.  **"Full synchronization" semantics when passing in** **`templateVariables`** **:** 

   * Variables carrying `id`: Updated in\- `situ by id`.

   * Variables without `id`: new.

   * Variables that are original but not included this time: will be disabled (no longer enabled as variables in the current template).

4. `TemplateVariables [*] .varId`and `templateVariables [*] .name`**are required** .

5. `TemplateVariables [*] .defaultValue`**must be an object** (e.g. `{}`), not string/array/ `null`.

6. In the same request, the variable name ( `templateVariables [*] .name`) cannot be repeated.


<span id="8d5a5f46"></span>
### Return parameters


|Field path |Type |Explain |
|---|---|---|
|`code` |string |Request result code, "llm/ok" indicates that the update was successful. |
|`msg` |object |Hint message object; null means no additional hints. |
|`data` |object |Updated template details object. |
|`data.id` |integer |Template ID (from URL path `/promptTemplates/186`). |
|`data.agentId` |integer |Template Owner Agent ID. |
|`data.name` |string |Template name (imported parameter `name`for this update). |
|`data.description` |string |Template description (this update imported parameter `description`). |
|`data.scene` |array |List of suitable scenarios for the template. |
|`data.isPublic` |integer |Whether it is public: `1`public, `0`non\-public (this update imported parameter `isPublic`). |
|`data.owner` |string |Template creator. |
|`data.updatedBy` |string |The most recent update person is usually the account corresponding to the current caller. |
|`data.data` |string |Template body content (this field is not updated in this request, and is returned as the current stock value). |
|`data.conversationOptions` |object |A collection of configuration items to use when initiating a conversation. |
|`data.status` |integer |Template status: `1`Normal (other values are subject to server level definition). |
|`data.mode` |string |Template applicable mode. |
|`data.isRecommend` |integer |Recommended: `0`Not recommended. |
|`data.isPinned` |boolean |Whether to stick to the top. |
|`data.isOfficial` |boolean |Is it an official template? |
|`data.previewImageList` |array |Template preview diagram list. |
|`data.templateAvailableSkills` |array |List of available skills for the template. |
|`data.templateVariables` |array |List of template variables. |
|`data.ctime` |string |Template creation time. |
|`data.mtime` |string |Template update time (the time after this update). |


<span id="0402732b"></span>
### data.conversationOptions


|Field path |Type |Current value |Explain |
|---|---|---|---|
|`data.conversationOptions.enableAeolusAssetSearch` |boolean |`false` |Whether to enable Aeolus asset search. |
|`data.conversationOptions.enableHiveDataSearch` |boolean |`false` |Whether to enable Hive data search. |
|`data.conversationOptions.enableLarkQA` |boolean |`false` |Whether to enable Lark Q & A. |
|`data.conversationOptions.enableWebSearch` |boolean |`true` |Whether to enable Web search. |
|`data.conversationOptions.enabledMcpServers` |array |`[]` |List of enabled MCP Servers. |
|`data.conversationOptions.templateSkills` |array |`[]` |Template binding skill list. |


<span id="bedec8fb"></span>
### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "agentId": 279,
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
    "description": "更新后的模板描述",
    "id": 186,
    "isOfficial": false,
    "isPinned": false,
    "isPublic": 1,
    "isRecommend": 0,
    "mode": "knowledge_qa",
    "mtime": "2026-08-12T14:31:57",
    "name": "活动策划",
    "owner": "admin",
    "previewImageList": [],
    "scene": [
      "PLANNING",
      "DOCUMENT_COMPOSITION"
    ],
    "status": 1,
    "templateAvailableSkills": [],
    "templateVariables": [],
    "updatedBy": "admin"
  },
  "msg": {}
}
```

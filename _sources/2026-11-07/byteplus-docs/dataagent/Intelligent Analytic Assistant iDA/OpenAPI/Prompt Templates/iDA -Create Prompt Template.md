---
title: "iDA -Create Prompt Template"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-Create_Prompt_Template"
---

<span id="550777a5"></span>
### Request description


|Project |Content |
|---|---|
|request method |`POST` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


<span id="cf024d4a"></span>
### Request Parameters


|Parameter |Type |Required |Explain |
|---|---|---|---|
|`agentId` |int |Yes |Agent ID; the calling user must be a member of the agent |
|`name` |string |Yes |Template name, up to 255 characters |
|`description` |string |Yes |Template description, not nullable |
|`scene` |array |Yes |List of business scenarios, such as `["PLANNING", "DOCUMENT_COMPOSITION"]` |
|`isPublic` |int |Yes |Public status: `1`public, `0`private |
|`data` |string |Yes |Tip template body, not nullable; variables are referenced `with {{varId}}` |
|`mode` |string/array |Yes |`knowledge_qa`or `deep_research` |
|`sceneName` |object/string/array |No |Scene display name, such as `{"cn": ["scheme planning"]}` |
|`conversationOptions` |object |No |Session capability configuration; internal fields are preserved as\-is |
|`templateVariables` |array |No |List of template variables, see "Template Variable Description" for field constraints |
|`isRecommend` |int |No |Recommended or not; setting to `1`requires agent administrator privileges |


<span id="4f5dcc32"></span>
## Template variable description


|Field |Type |Required |Explain |
|---|---|---|---|
|`id` |int |When updating an existing variable |Variable record ID; not passed when creating new variables |
|`varId` |string |Yes |The variable identifier corresponding to `{{varId}}`in the template body |
|`name` |string |Yes |Variable names cannot be repeated within the same request |
|`description` |string |No |variable description |
|`required` |int |No |`1`Required, `0`Optional |
|`valueType` |string |No |`String`or `file`, default `string` |
|`defaultValue` |object |No |Default object, such as `{"text": "today"}`or `{}` |


<span id="59f9349d"></span>
### Request example

```Plain
curl -X POST \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/promptTemplates" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --data-raw '{
  "agentId": 279,
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


<span id="7e94240f"></span>
### Return parameters


|Field path |Type |Explain |
|---|---|---|
|`code` |string |Request result code, success is `llm/ok`. |
|`msg` |object |Hint information container; usually empty object on success. |
|`data` |object |Template details after successful creation. |


<span id="0ca4828c"></span>
### Data field


|Field path |Type |Explain |
|---|---|---|
|`data.id` |integer |Template ID. |
|`data.agentId` |integer |Template Owner Agent ID. |
|`data.name` |string |Template name. |
|`data.description` |string |Template description. |
|`data.scene` |array |The template applies to a list of scenarios, such as `PLANNING`, `DOCUMENT_COMPOSITION`. |
|`data.isPublic` |integer |Public: `1`public, `0`private/not public. |
|`data.owner` |string |Template creator mailbox prefix. |
|`data.updatedBy` |string |Recently updated person mailbox prefix. |
|`data.data` |string |Template body content; variables take place as `{{varId}}`. |
|`data.conversationOptions` |object |The configuration item to use when initiating a conversation. |
|`data.status` |integer |Template status, `1`means normally available. |
|`data.mode` |string |Templates apply patterns such as `knowledge_qa`. |
|`data.isRecommend` |integer |Recommended: `1`Recommended, `0`Not Recommended. |
|`data.isPinned` |boolean |Whether to stick to the top. |
|`data.isOfficial` |boolean |Is it an official template? |
|`data.previewImageList` |array |Template preview URL list; up to one is supported when created. Returns an empty array when no preview image is passed. |
|`data.templateAvailableSkills` |array |A list of available skills for the template; creating an interface usually returns an empty array unless explicitly passed in by the service tier. |
|`data.templateVariables` |array |List of template variables. |
|`data.ctime` |string |Creation time, ISO format. |
|`data.mtime` |string |Update time, ISO format. |


<span id="b229e7f2"></span>
### Data.conversationOptions field

> `ConversationOptions`will be saved as an object as the request body is when created, and will not force a non\-existent key to be filled.



|Field path |Type |Explain |
|---|---|---|
|`data.conversationOptions.enableAeolusAssetSearch` |boolean |Whether to enable Aeolus asset search. |
|`data.conversationOptions.enableHiveDataSearch` |boolean |Whether to enable Hive data search. |
|`data.conversationOptions.enableLarkQA` |boolean |Whether to enable Lark Q & A. |
|`data.conversationOptions.enableWebSearch` |boolean |Whether to enable Web search. |
|`data.conversationOptions.enabledMcpServers` |array |List of enabled MCP Servers. |
|`data.conversationOptions.templateSkills` |array |List of skills bound to the template. |


<span id="18393bce"></span>
### data.templateVariables[] field


|Field path |Type |Explain |
|---|---|---|
|`data.templateVariables[].id` |integer |Template variable record ID. |
|`data.templateVariables[].templateId` |integer |Owned template ID. |
|`data.templateVariables[].varId` |string |Variable unique identifier; referenced by `{{varId}}`in template body. |
|`data.templateVariables[].name` |string |Variable names, such as `event planning scenarios`. |
|`data.templateVariables[].description` |string |Variable descriptions, such as supported file types. |
|`data.templateVariables[].required` |integer |Required: `1`required, `0`not required. |
|`data.templateVariables[].valueType` |string |Variable value types, such as `file`, `string`. |
|`data.templateVariables[].defaultValue` |object |Default object; empty when there is no default. |
|`data.templateVariables[].sortOrder` |integer |Variable sort value, the smaller the value, the higher. |
|`data.templateVariables[].creator` |string |Variable creator mailbox prefix. |
|`data.templateVariables[].updatedBy` |string |Variable most recently updated person mailbox prefix. |
|`data.templateVariables[].status` |integer |Variable status, `1`indicates normal availability. |
|`data.templateVariables[].ctime` |string |Variable creation time, ISO format. |
|`data.templateVariables[].mtime` |string |Variable update time, ISO format. |


<span id="28e4ed69"></span>
### Field post script


|Field |Explain |
|---|---|
|`data.data` |The template body is a plain string; the ID in the variable placeholder should correspond to `templateVariables [] .varId`. |
|`data.scene` |It is saved as a JSON string when warehoused and parsed as an array when returned. |
|`data.mode` |Saved with bittag when warehousing, converted to schema name string when returning. |


<span id="4683c4ef"></span>
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
    "description": "对活动策划方案进行全面评估和优化",
    "id": 186,
    "isOfficial": false,
    "isPinned": false,
    "isPublic": 1,
    "isRecommend": 0,
    "mode": "knowledge_qa",
    "mtime": "2026-08-12T13:57:21",
    "name": "活动策划",
    "owner": "admin",
    "previewImageList": [],
    "scene": [
      "PLANNING",
      "DOCUMENT_COMPOSITION"
    ],
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
    "updatedBy": "admin"
  },
  "msg": {}
}
```

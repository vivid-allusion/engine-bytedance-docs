---
title: "iDA - Get Session Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Get_Session_Details"
---

<span id="yFGB2pGMg8"></span>
## Acquire session information

Get session basic information based on `sessionId`; optionally return message list and task history (in DeepResearch/A2A scenario).

<span id="SYwCT1Vh9u"></span>
### Request description


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/sessionInfo` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


<span id="J8hURLPPqo"></span>
### Request parameters (Query)


|Parameter name |Type |Required |Default value |Example |Explain |
|---|---|---|---|---|---|
|`sessionId` |integer |Yes |*  |14468 |Session ID. |
|`needMsg` |boolean |No |`false` |`true` |Whether to return a list of session messages. `False`when `data.messageList`is an empty array. |
|`maxMsgCount` |integer |No |*  |`20` |The maximum number of messages returned. Effective only when `needMsg = true`. |


> Description: If the session is of DeepResearch/A2A type, the response may contain `data.tasks`as the task history; other session types may return an empty array. While the task is still executing, the interface updates the session state (such as `latestTaskStatus`) with the latest task status.


<span id="CaZ5Pd89Tw"></span>
### Request example

Standard Curl Example:

```bash
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/sessionInfo?sessionId=14468&needMsg=true&maxMsgCount=20" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H 'Content-Type: application/json' \
  --silent | jq
```


HTTP example:

```text
GET https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/sessionInfo?sessionId=8350&needMsg=true&maxMsgCount=20
```


<span id="UBqqF0wQN6"></span>
### Return parameters


|Parameter name |Type |Explain |
|---|---|---|
|`code` |string |Request result code, success is `llm/ok`. |
|`msg` |object |Hint message, usually an empty object on success. |
|`data` |object |Business data. |
|`data.messageList` |array |List of session messages; empty array when `needMsg = false`. |
|`data.tasks` |array |Session\-associated task list (DeepResearch/A2A session may return); empty array when no task. |
|`data.sessionInfo` |object |Conversation details. |
|`data.sessionInfo.id` |integer |Session ID. |
|`data.sessionInfo.name` |string |Session name. |
|`data.sessionInfo.emailPrefix` |string |Session creator mailbox prefix. |
|`data.sessionInfo.dataSetId` |integer |null |
|`data.sessionInfo.sessionType` |string |Session type, such as `normal`. |
|`data.sessionInfo.scene` |string |Conversation scenarios, such as `data_set`. |
|`data.sessionInfo.version` |string |Session context version, such as `v5`. |
|`data.sessionInfo.createTime` |string |Session creation time. |
|`data.sessionInfo.lastActiveTime` |string |The last active time of the session. |
|`data.sessionInfo.serverTime` |string |Server level current time. |
|`data.sessionInfo.isExpired` |boolean |Whether the session has expired. |
|`data.sessionInfo.isKnowledgeQA` |boolean |Whether it is a knowledge Q & A session. |
|`data.sessionInfo.isMixed` |boolean |Whether it is a mixed session. |
|`data.sessionInfo.isBackendCreated` |boolean |Is it created by the backend? |
|`data.sessionInfo.submittedViaInternalA2a` |boolean |Whether to submit through internal A2A. |
|`data.sessionInfo.restrictMode` |integer |Session Restriction Mode. |
|`data.sessionInfo.latestTaskStatus` |string |null |
|`data.sessionInfo.fileList` |array |Session upload file list. |
|`data.sessionInfo.linkEmbed` |array |session\-associated linked resources. |
|`data.sessionInfo.mcpServers` |array |List of session enabled MCP Servers. |
|`data.sessionInfo.customTag` |array |Session custom tags. |
|`data.sessionInfo.extraInfo` |object |Session extension information. |
|`data.sessionInfo.generalAgentInfo` |object |Universal Agent Extension Information. |
|`data.sessionInfo.reportId` |integer |null |
|`data.sessionInfo.storageId` |string |null |
|`data.sessionInfo.queryHistoryId` |integer |null |
|`data.sessionInfo.relatedQueryId` |integer |null |
|`data.sessionInfo.relatedQueryQuestion` |string |null |
|`data.sessionInfo.relatedQueryDataSetId` |integer |null |
|`data.sessionInfo.relatedQueryDataSetIdList` |array |null |
|`data.sessionInfo.originReportStorageId` |string |null |
|`data.sessionInfo.originDataPreviewMode` |string |null |
|`data.sessionInfo.xPageUrl` |string |null |
|`data.sessionInfo.agentInfo` |object |Session Owner Agent information. |
|`data.sessionInfo.agentInfo.id` |integer |Agent ID。 |
|`data.sessionInfo.agentInfo.name` |string |Agent name. |
|`data.sessionInfo.agentInfo.description` |string |Agent description. |
|`data.sessionInfo.agentInfo.detail` |object |null |
|`data.sessionInfo.agentInfo.avatar` |string |Agent avatar ID. |
|`data.sessionInfo.agentInfo.agentType` |string |Agent type, such as `Expert`. |
|`data.sessionInfo.agentInfo.agentMode` |string |Agent current schema, such as `knowledgeQA`. |
|`data.sessionInfo.agentInfo.creatorPrefix` |string |Agent creator mailbox prefix. |
|`data.sessionInfo.agentInfo.privilegeType` |string |Permission types, such as `agent`. |
|`data.sessionInfo.agentInfo.modelTypeStandardName` |string |Model type standard name. |
|`data.sessionInfo.agentInfo.isAgentAdmin` |boolean |Is the current user an agent administrator? |
|`data.sessionInfo.agentInfo.isDeepResearchOpen` |boolean |Whether to enable in\-depth research capabilities. |
|`data.sessionInfo.agentInfo.isDeepResearchQueryOpen` |boolean |Whether to open the in\-depth research fetch link. |
|`data.sessionInfo.agentInfo.isInsightReportOpen` |boolean |Whether to enable insight reporting capabilities. |
|`data.sessionInfo.agentInfo.isSmartQueryOpen` |boolean |Whether to turn on the intelligent number asking ability. |
|`data.sessionInfo.agentInfo.isKnowledgeQASeen` |boolean |Whether to demonstrate knowledge answering ability. |
|`data.sessionInfo.agentInfo.isSkillMarketPlaceEnable` |boolean |Whether to open the skills market. |
|`data.sessionInfo.agentInfo.uploadSkillOnSessionEnable` |boolean |Is it allowed to upload skills within the session? |
|`data.sessionInfo.agentInfo.deepResearchUploadSkillOnSessionEnable` |boolean |Examine in depth whether skills are allowed to be uploaded within a session. |
|`data.sessionInfo.agentInfo.isBuiltinPPTTemplateSelectionEnable` |boolean |Whether to enable the built\-in PPT template selection. |
|`data.sessionInfo.agentInfo.enableMultiReport` |boolean |Whether to enable multi\-reporting capability. |
|`data.sessionInfo.agentInfo.multiReportNums` |integer |Maximum number of multiple reports. |
|`data.sessionInfo.agentInfo.supportKnowledgeEngine` |boolean |Whether to support the knowledge engine. |
|`data.sessionInfo.agentInfo.knowledgeEngines` |object |The knowledge engine configuration used by the different modes. |
|`data.sessionInfo.agentInfo.knowledgeEngines.knowledgeQA` |string |The knowledge engine used by knowledge Q & A. |
|`data.sessionInfo.agentInfo.knowledgeEngines.deepresearch` |string |Deep research uses a knowledge engine. |
|`data.sessionInfo.agentInfo.config` |object |Agent configuration. |
|`data.sessionInfo.agentInfo.config.isNewAgent` |boolean |Whether to configure for the new version of Agent. |
|`data.sessionInfo.agentInfo.config.dateCalcSw` |boolean |Whether to turn on the date calculation switch. |
|`data.sessionInfo.agentInfo.config.defaultKnowledgeBaseId` |integer |Default Knowledge Base ID. |
|`data.sessionInfo.agentInfo.config.defaultKnowledgeTenantId` |integer |Default knowledge base tenant ID. |
|`data.sessionInfo.agentInfo.config.defaultKnowledgeBaseInitd` |boolean |Is the default knowledge base initialized? |
|`data.sessionInfo.agentInfo.config.useKnowledgeEngineKb` |boolean |Whether to use the knowledge engine knowledge base. |
|`data.sessionInfo.agentInfo.config.knowledgeEnginePriority` |string |Knowledge engine priority, such as `user`. |
|`data.sessionInfo.agentInfo.config.isInsightReportOpen` |boolean |Configuration layer insight report switch. |
|`data.sessionInfo.agentInfo.config.visibleAgentModes` |array |Visible list of Agent modes. |
|`data.sessionInfo.agentInfo.config.oncallEntrance` |string |Oncall entry URL. |
|`data.sessionInfo.agentInfo.config.knowledgeQa` |object |Knowledge Q & A configuration. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.scene` |object |Knowledge Q & A scenario configuration. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools` |object |Knowledge Q & A can be configured with tools. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.python.enabled` |boolean |Whether to enable Python tools. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.sql.enabled` |boolean |Whether to enable SQL tools. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.webSearch.enabled` |boolean |Whether to enable the Web search tool. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.queryAeolusReport.enabled` |boolean |Whether to enable the Aeolus report query tool. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.queryHiveTableInfo.enabled` |boolean |Whether to enable the Hive table information query tool. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.search.knowledgeBase.enabled` |boolean |Whether to enable Knowledge Base Search. |
|`data.sessionInfo.agentInfo.config.knowledgeQa.tools.search.aeolusAsset.enabled` |boolean |Whether to enable Aeolus asset search. |


<span id="heN7A0IKfh"></span>
### Back to example

```json
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "messageList": [],
    "sessionInfo": {
      "agentInfo": {
        "agentMode": "knowledgeQA",
        "agentType": "Expert",
        "avatar": "system3",
        "config": {
          "dateCalcSw": true,
          "defaultKnowledgeBaseId": 118,
          "defaultKnowledgeBaseInitd": true,
          "defaultKnowledgeTenantId": 8000000000001,
          "isInsightReportOpen": false,
          "isNewAgent": true,
          "knowledgeEnginePriority": "user",
          "knowledgeQa": {
            "scene": {},
            "tools": {
              "python": {
                "enabled": true
              },
              "queryAeolusReport": {
                "enabled": true
              },
              "queryHiveTableInfo": {
                "enabled": true
              },
              "search": {
                "aeolusAsset": {
                  "enabled": false
                },
                "knowledgeBase": {
                  "enabled": true
                }
              },
              "sql": {
                "enabled": true
              },
              "webSearch": {
                "enabled": true
              }
            }
          },
          "oncallEntrance": "https://cloud.bytedance.net/oncall/chats/user/index?lang=zh-CN&open_in_browser=true&x-resource-account=public&x-bc-region-id=bytedance&tenantId=28603&step=self-solve",
          "useKnowledgeEngineKb": true,
          "visibleAgentModes": []
        },
        "creatorPrefix": "admin",
        "deepResearchUploadSkillOnSessionEnable": false,
        "description": "openApi test",
        "detail": null,
        "enableMultiReport": false,
        "id": 430,
        "isAgentAdmin": true,
        "isBuiltinPPTTemplateSelectionEnable": false,
        "isDeepResearchOpen": true,
        "isDeepResearchQueryOpen": true,
        "isInsightReportOpen": true,
        "isKnowledgeQASeen": true,
        "isSkillMarketPlaceEnable": true,
        "isSmartQueryOpen": true,
        "knowledgeEngines": {
          "deepresearch": "knowledgeBase",
          "knowledgeQA": "knowledgeBase"
        },
        "modelTypeStandardName": "GPT model",
        "multiReportNums": 1,
        "name": "openApi",
        "privilegeType": "agent",
        "supportKnowledgeEngine": true,
        "uploadSkillOnSessionEnable": true
      },
      "createTime": "2026-08-11 16:41:55",
      "customTag": [],
      "dataSetId": null,
      "emailPrefix": "admin",
      "extraInfo": {},
      "fileList": [],
      "generalAgentInfo": {},
      "id": 14468,
      "isBackendCreated": false,
      "isExpired": false,
      "isKnowledgeQA": false,
      "isMixed": false,
      "lastActiveTime": "2026-08-11 16:41:55",
      "latestTaskStatus": null,
      "linkEmbed": [],
      "mcpServers": [],
      "name": "OpenAPI Data Q&A",
      "originDataPreviewMode": null,
      "originReportStorageId": null,
      "queryHistoryId": null,
      "relatedQueryDataSetId": null,
      "relatedQueryDataSetIdList": null,
      "relatedQueryId": null,
      "relatedQueryQuestion": null,
      "reportId": null,
      "restrictMode": 0,
      "scene": "data_set",
      "serverTime": "2026-08-12 10:01:27",
      "sessionType": "normal",
      "storageId": null,
      "submittedViaInternalA2a": false,
      "version": "v5",
      "xPageUrl": null
    },
    "tasks": []
  },
  "msg": {}
}
```

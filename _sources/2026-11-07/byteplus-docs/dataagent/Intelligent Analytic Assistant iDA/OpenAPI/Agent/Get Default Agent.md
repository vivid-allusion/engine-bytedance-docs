---
title: "Get Default Agent"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_Default_Agent"
---

<span id="0400ebdf"></span>
## Get the default agent getDefaultAgent

<span id="4afd3ad8"></span>
### Request description

Used to obtain the **default agent** information available to the current tenant/current user (including agent basic information, capability switches and some configurations).


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getDefaultAgent` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


<span id="abe13003"></span>
### Request parameters

No imported parameters.

<span id="d96ff252"></span>
### Request example

Standard Curl Example:

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getDefaultAgent" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --silent | jq
```


<span id="08ae2fa6"></span>
### Return parameters

<span id="ec8b10fc"></span>
### Top\-level field


|Field path |Type |Explain |
|---|---|---|
|`JSONIFY_PRETTYPRINT_REGULAR` |boolean |JSON output configuration tag, usually `false`. |
|`code` |string |Request result code. Success is `llm/ok`. |
|`msg` |object |Prompt message. Usually an empty object when successful. |
|`data` |object |Default Agent query results. |


<span id="0e5c1498"></span>
### Data field


|Field path |Type |Explain |
|---|---|---|
|`data.agentInfo` |object |null |
|`data.isVolcSearchOpen` |boolean |Volcano search switch marker. The example returns `true`(whether it is fixed or not depends on the actual implementation). |


<span id="b87469f6"></span>
### data.agentInfo field


|Field path |Type |Explain |
|---|---|---|
|`data.agentInfo.id` |integer |Agent ID. |
|`data.agentInfo.name` |string |Agent name. |
|`data.agentInfo.avatar` |string |Agent avatar ID (or avatar URL, subject to actual return). |
|`data.agentInfo.description` |string |null |
|`data.agentInfo.detail` |string |null |
|`data.agentInfo.agentType` |string |Agent type, such as `General`, `Expert`. |
|`data.agentInfo.agentMode` |string |null |
|`data.agentInfo.isAgentAdmin` |boolean |Is the current user an administrator for the agent? |
|`data.agentInfo.modelTypeStandardName` |string |Model type standard name. |
|`data.agentInfo.isDeepResearchOpen` |boolean |Whether to enable in\-depth research capabilities. |
|`data.agentInfo.isInsightReportOpen` |boolean |Whether to enable insight reporting capabilities. |
|`data.agentInfo.isDeepResearchQueryOpen` |boolean |Whether to open the in\-depth research fetch link. |
|`data.agentInfo.isSmartQueryOpen` |boolean |Whether to turn on the intelligent number asking ability. |
|`data.agentInfo.analysisParams` |boolean |Whether to enable the ability to analyze parameters. |
|`data.agentInfo.concurrentMultiRoundSw` |boolean |Whether to turn on the concurrent multi\-wheel switch. |
|`data.agentInfo.simpleAnalyzeSw` |boolean |Whether to turn on the Simple Analysis switch. |
|`data.agentInfo.config` |object |Agent configuration (larger structure, subject to actual return). |
|`data.agentInfo.isKnowledgeQASeen` |boolean |Whether the knowledge answering ability is displayed to the current user (field semantics are subject to the actual situation). |
|`data.agentInfo.isKnowledgeQAOpen` |boolean |string |
|`data.agentInfo.isPersonal` |boolean |Whether it is a Personal Agent. |
|`data.agentInfo.isMultiModalOpen` |boolean |Whether to enable multimodal capabilities. |
|`data.agentInfo.isFeedbackEnabled` |boolean |Whether to enable feedback capabilities. |
|`data.agentInfo.uploadSkillOnSessionEnable` |boolean |Is it allowed to upload skills within the session? |
|`data.agentInfo.deepResearchUploadSkillOnSessionEnable` |boolean |Examine in depth whether skills are allowed to be uploaded within a session. |
|`data.agentInfo.isSkillMarketPlaceEnable` |boolean |Whether to open the skills market. |
|`data.agentInfo.isBuiltinPPTTemplateSelectionEnable` |boolean |Whether to enable the built\-in PPT template selection (whether the field is returned is subject to the actual situation). |
|`data.agentInfo.supportKnowledgeEngine` |boolean |Whether to support the knowledge engine. |
|`data.agentInfo.knowledgeEngines` |object |The knowledge engine configuration used by the different modes. |
|`data.agentInfo.knowledgeEngines.knowledgeQA` |string |The knowledge engine used by knowledge Q & A. |
|`data.agentInfo.knowledgeEngines.deepresearch` |string |Deep research uses a knowledge engine. |


<span id="1617bb2f"></span>
### Back to example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "agentInfo": {
      "agentMode": "knowledgeQA",
      "agentType": "Expert",
      "analysisParams": true,
      "avatar": "system13",
      "concurrentMultiRoundSw": false,
      "config": {
        "dateCalcSw": true,
        "isNewAgent": false,
        "knowledgeQa": {
          "tools": {
            "python": {
              "enabled": true
            },
            "queryAeolusReport": {
              "enabled": true
            },
            "search": {
              "acrosite": {
                "enabled": false
              },
              "aeolusAsset": {
                "enabled": true
              },
              "coral": {
                "enabled": true
              },
              "knowledgeBase": {
                "enabled": true
              },
              "lark": {
                "enabled": true
              },
              "oncall": {
                "enabled": false
              }
            },
            "sql": {
              "enabled": true
            }
          }
        },
        "oncallEntrance": "xxxxx",
        "visibleAgentModes": []
      },
      "deepResearchUploadSkillOnSessionEnable": false,
      "description": "Q&A freely on knowledge and assets of space",
      "detail": "",
      "enableMultiReport": true,
      "id": 305,
      "isAgentAdmin": true,
      "isBuiltinPPTTemplateSelectionEnable": false,
      "isDeepResearchOpen": true,
      "isDeepResearchQueryOpen": true,
      "isFeedbackEnabled": false,
      "isInsightReportOpen": true,
      "isKnowledgeQAOpen": true,
      "isKnowledgeQASeen": true,
      "isMultiModalOpen": true,
      "isPersonal": true,
      "isSkillMarketPlaceEnable": true,
      "isSmartQueryOpen": true,
      "knowledgeEngines": {
        "deepresearch": "knowledgeBase",
        "knowledgeQA": "knowledgeBase"
      },
      "modelTypeStandardName": "XXX model",
      "multiReportNums": 5,
      "name": " wangbingya's knowledge space ",
      "simpleAnalyzeSw": true,
      "supportKnowledgeEngine": true,
      "uploadSkillOnSessionEnable": true
    },
    "isVolcSearchOpen": true
  },
  "msg": {}
}
```

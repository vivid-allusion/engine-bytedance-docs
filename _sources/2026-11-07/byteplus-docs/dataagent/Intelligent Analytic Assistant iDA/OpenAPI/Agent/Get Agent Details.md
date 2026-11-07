---
title: "Get Agent Details"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Get_Agent_Details"
---

<span id="5ea5c57d"></span>
## Get agent details getAgentInfo

<span id="659d9369"></span>
### Request description

It is used to obtain the detailed information of the specified agent according to the `agentId`(including the basic information of the agent, the ability switch and some configurations).


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getAgentInfo?agentId=11` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


<span id="f53e0186"></span>
### Request parameters


|Location |Parameter |Type |Is it required? |Sample value |Parameter transfer description |
|---|---|---|---|---|---|
|Query |`agentId` |number |Yes |298 |Target agent ID. |


<span id="c5da9da8"></span>
### Request example

Standard Curl Example:

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getAgentInfo?agentId=298" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --silent | jq
```


<span id="b0d6c5fd"></span>
### Return parameters


|Field path |Type |Explain |
|---|---|---|
|`JSONIFY_PRETTYPRINT_REGULAR` |boolean |JSON output configuration tags (server level internal fields). |
|`code` |string |Business return code. Example: `llm/ok`indicates success (subject to actual enumeration). |
|`data` |object |Agent detail data. |
|`msg` |object |Message extension field (possibly an empty object). |


<span id="c28d0c44"></span>
#### Data field (agent object)


|Field path |Type |Explain |
|---|---|---|
|`data.id` |integer |Agent ID. |
|`data.name` |string |Agent name. |
|`data.description` |string |null |
|`data.detail` |string |null |
|`data.avatar` |string |Agent avatar ID or URL (subject to actual return). |
|`data.agentType` |string |Agent type (example: `General`). |
|`data.agentMode` |string |null |
|`data.creatorPrefix` |string |Creator account ID (such as email prefix). |
|`data.privilegeType` |string |Permission type identifier (example: `agent`; meaning is actual). |
|`data.isAgentAdmin` |boolean |Whether the current user is the administrator of the agent. |
|`data.supportKnowledgeEngine` |boolean |Whether to support knowledge engine capabilities. |
|`data.knowledgeEngines` |object |Knowledge Engine Configuration Mapping for Different Patterns. |
|`data.knowledgeEngines.knowledgeQA` |string |The knowledge engine used by the Q & A pattern (example: `knowledgeBase`). |
|`data.knowledgeEngines.deepresearch` |string |The knowledge engine used by the deep research mode (example: `knowledgeBase`). |
|`data.modelTypeStandardName` |string |Model type standard name (example: `GPT model`). |
|`data.uploadSkillOnSessionEnable` |boolean |Whether skills are allowed to be uploaded within the session (subject to the actual meaning). |
|`data.deepResearchUploadSkillOnSessionEnable` |boolean |In\-depth research on whether skills are allowed to be uploaded within the session (subject to actual meaning). |
|`data.isDeepResearchOpen` |boolean |Whether to enable in\-depth research capabilities. |
|`data.isDeepResearchQueryOpen` |boolean |Whether to open the in\-depth research access link (subject to the actual meaning). |
|`data.isInsightReportOpen` |boolean |Whether to enable insight reporting capabilities. |
|`data.isSmartQueryOpen` |boolean |Whether to turn on the intelligent number asking ability. |
|`data.isKnowledgeQASeen` |boolean |Whether the knowledge answering ability is displayed (the field semantics are subject to the actual situation). |
|`data.isSkillMarketPlaceEnable` |boolean |Whether to activate the skills market ability. |
|`data.enableMultiReport` |boolean |Whether to support multiple reporting capabilities. |
|`data.multiReportNums` |integer |Maximum number of multiple reports. |
|`data.config` |object |Agent configuration object (larger structure, subject to actual return). |


<span id="6ca02cdd"></span>
#### Data.config field (excerpt)


|Field path |Type |Explain |
|---|---|---|
|`data.config.isNewAgent` |boolean |Whether it is a new version of the agent. |
|`data.config.isInsightReportOpen` |boolean |Configuration\-level insight reporting switch (may exist at the same time as `data.isInsightReportOpen`, the meaning is subject to the actual situation). |
|`data.config.visibleAgentModes` |array |List of visible/switchable modes. |
|`data.config.knowledgeQa` |object |Question Answering Mode Configuration (excerpt). |
|`data.config.knowledgeQa.tools.search.aeolusAsset.enabled` |boolean |Whether to enable Aeolus asset search. |


<span id="ddc314fa"></span>
#### Response example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "agentMode": "insightReport",
    "agentType": "General",
    "avatar": "systemGeneral",
    "config": {
      "isInsightReportOpen": false,
      "isNewAgent": true,
      "knowledgeQa": {
        "tools": {
          "search": {
            "aeolusAsset": {
              "enabled": false
            }
          }
        }
      },
      "visibleAgentModes": []
    },
    "creatorPrefix": "admin",
    "deepResearchUploadSkillOnSessionEnable": false,
    "description": "New methods of AI-driven data analysis allow data to speak and collaborate automatically.",
    "detail": "### In-depth Research: Let large models become your data insight assistant ... (For details of Agents, see rich text. Omitted here.)",
    "enableMultiReport": true,
    "id": 11,
    "isAgentAdmin": false,
    "isDeepResearchOpen": false,
    "isDeepResearchQueryOpen": true,
    "isInsightReportOpen": true,
    "isKnowledgeQASeen": true,
    "isSkillMarketPlaceEnable": true,
    "isSmartQueryOpen": false,
    "knowledgeEngines": {
      "deepresearch": "knowledgeBase",
      "knowledgeQA": "knowledgeBase"
    },
    "modelTypeStandardName": "XXX model",
    "multiReportNums": 5,
    "name": "iDA",
    "privilegeType": "agent",
    "supportKnowledgeEngine": true,
    "uploadSkillOnSessionEnable": true
  },
  "msg": {}
}
```

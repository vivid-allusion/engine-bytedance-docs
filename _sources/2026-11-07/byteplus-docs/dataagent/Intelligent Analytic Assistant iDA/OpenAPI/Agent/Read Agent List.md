---
title: "Read Agent List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Read_Agent_List"
---

<span id="7b6d775c"></span>
## Read the agent list getAgentList

<span id="3b6bb343"></span>
### Request description

Used to obtain a list of agents available under the current tenant, with support for keyword search and pagination.


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getAgentList?page=1&pageSize=10` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |
|content type |`Content-Type: application/json` |


<span id="967ddce4"></span>
### Request parameters

> Parameters are passed through QueryString.



|Location |Parameter |Type |Is it required? |Sample value |Explain |
|---|---|---|---|---|---|
|Query |`kw` |string |No |`Aeolus` |Query keywords for fuzzy matching by fields such as name. |
|Query |`page` |number |No |`1` |Page number. `1`represents the first page, the default is `1`. |
|Query |pageSize |number |No |`10` |Number of entries per page. Default `16`. |


<span id="7b96026d"></span>
### Request example

With paging parameters:

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getAgentList?page=1&pageSize=1" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --silent | jq
```


Do not pass page parameters (use default values):

```Plain
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/getAgentList" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --silent | jq
```


<span id="a2bf25bf"></span>
### Return parameters


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`JSONIFY_PRETTYPRINT_REGULAR` |boolean |`false` |JSON output configuration tags (server level internal fields). |
|`code` |string |`llm/ok` |Request result code. The example indicates that the request was successful. |
|`msg` |object |`{}` |Prompt message object, possibly empty. |
|`data` |object |*  |Agent list paging results. |


<span id="677f7378"></span>
#### Data field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.list` |array |*  |List of Agents for the current page. |
|`data.total` |integer |`229` |The total number of Agents that meet the query criteria. |


<span id="b5b05d21"></span>
#### Data.list [] field (Agent object)


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.list[]` |object |*  |Single Agent object. |
|`data.list[].id` |integer |`298` |Agent ID。 |
|`data.list[].name` |string |`Data Agent` |Agent name. |
|`data.list[].pcName` |string |`Data Agent` |PC\-side display name. |
|`data.list[].description` |string |`A new approach to AI-driven data analytics that allows data to speak and collaborate automatically.` |Agent description. |
|`data.list[].pcDescription` |string |`A new approach to AI-driven data analytics that allows data to speak and collaborate automatically.` |PC\-side display description. |
|`data.list[].avatar` |string |`systemGeneral` |Agent avatar ID (or avatar URL, depending on the actual return). |
|`data.list[].pcAvatar` |string |`systemGeneral` |PC\-side avatar ID (or avatar URL, depending on the actual return). |
|`data.list[].agentType` |string |`General` |Agent type. Example is the Universal Agent. |
|`data.list[].agentMode` |string |`knowledgeQA` |Agent default/current mode. |
|`data.list[].status` |integer |`1` |Agent status. In the example, `1`usually means available (subject to the actual enumeration). |
|`data.list[].creatorPrefix` |string |`admin` |Creator account prefix (such as email prefix). |
|`data.list[].creatorName` |string |`administrator` |Creator display name. |
|`data.list[].creatorAvatar` |string |null |`null` |
|`data.list[].isAdmin` |boolean |`true` |Is the current user an administrator for the agent? |
|`data.list[].isPersonal` |boolean |`false` |Whether it is a Personal Agent. |
|`data.list[].ctime` |string |`2026-08-06 11:49:49` |Creation time. |
|`data.list[].mtime` |string |`2026-08-11 22:04:57` |Update time. |
|`data.list[].config` |object |*  |Agent configuration (many fields, subject to actual return). |
|`data.list[].analysisParams` |boolean |`true` |Whether to enable the ability to analyze parameters. |
|`data.list[].simpleAnalyzeSw` |boolean |`true` |Whether to turn on the Simple Analysis switch. |
|`data.list[].concurrentMultiRoundSw` |boolean |`false` |Whether to turn on the concurrent multi\-wheel switch. |


<span id="7da61190"></span>
#### Data.list [] .config field


|Field path |Type |Sample value |Explain |
|---|---|---|---|
|`data.list[].config.isInsightReportOpen` |boolean |`false` |Whether to enable insight reporting configuration. |
|`data.list[].config.isNewAgent` |boolean |`false` |Is it a new version of Agent? |


<span id="68285d8e"></span>
#### Paging instructions (corresponding to request parameters)


|Field |Sample value |Explain |
|---|---|---|
|`page` |`1` |Request page number (from request parameter `page`). |
|`pageSize` |`1` |Per page size (from the request parameter `pageSize`). |
|`data.list.length` |`1` |The actual number of items returned on the current page. |
|`data.total` |`229` |The total number of items that meet the conditions. |


<span id="cd78c282"></span>
### Response example

```Plain
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "list": [
      {
        "agentMode": "knowledgeQA",
        "agentType": "General",
        "analysisParams": true,
        "avatar": "systemGeneral",
        "concurrentMultiRoundSw": false,
        "config": {
          "isInsightReportOpen": false,
          "isNewAgent": false
        },
        "creatorAvatar": null,
        "creatorName": "管理员", //manager
        "creatorPrefix": "admin",
        "ctime": "2026-08-06 11:49:49",
        "description": "New methods of AI-driven data analysis allow data to speak and collaborate automatically.",
        "id": 298,
        "isAdmin": true,
        "isPersonal": false,
        "mtime": "2026-08-11 22:04:57",
        "name": "Data Agent",
        "pcAvatar": "systemGeneral",
        "pcDescription": "New methods of AI-driven data analysis allow data to speak and collaborate automatically.",
        "pcName": "Data Agent",
        "simpleAnalyzeSw": true,
        "status": 1
      }
    ],
    "total": 229
  },
  "msg": {}
}
```


&nbsp;

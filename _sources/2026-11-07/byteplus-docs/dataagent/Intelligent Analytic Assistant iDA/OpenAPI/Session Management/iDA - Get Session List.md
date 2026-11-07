---
title: "iDA - Get Session List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA_-_Get_Session_List"
---

<span id="wlhXKyxcKM"></span>
## Request description


|Project |Content |
|---|---|
|request method |`GET` |
|request address |`https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/sessionList?appId=1&agentId=11&limit=30&before=2629` |
|default authentication |`Authorization: Bearer ${JWT_TOKEN}` |


In addition to A2A initiating data Q & A, the OpenAPI side also provides a session list query interface for paging and pulling the current user's historical session by Agent/Application dimension. The authentication method is consistent with other OpenAPI interfaces, using JWT.

Authentication method: `jwtToken`authentication.

<span id="Jm16Dkklp6"></span>
## Request parameters


|Parameter name |Type |Is it required? |Explain |
|---|---|---|---|
|agentId |int |No |Agent ID, filter sessions by the specified agent |
|appId |int |No |App ID |
|limit |int |No |The number of returns on a single page, the default is 20. |
|before |int |No |Paging cursor, return the data before the session ID, the first page can not be passed or passed \-1 |
|fuzzySearch |string |No |By session name fuzzy search |
|sessionType |int |No |session type |
|startDate |string |No |Start date filter, format `YYYY-MM-DD` |
|customTag |string |No |custom label filtering |
|source |string |No |source identification |
|isMixed |bool |No |Whether to mix sessions |
|isKnowledgeQA |bool |No |Knowledge Q & A session |
|isNewAgent |bool |No |Is it a new version of Agent? |


<span id="qk1iyJGslg"></span>
## Request example

```bash
curl -X GET \
  "https://${IDA_DOMAIN}/dataAgent/llm/openApi/v2/signed/agent/sessionList?appId=1&agentId=430&limit=30" \
  -H "Authorization: Bearer ${JWT_TOKEN}" \
  -H "Content-Type: application/json" \
  --silent | jq
```


<span id="UdrMLyORrt"></span>
## Return parameters


|Parameter name |Type |Explain |
|---|---|---|
|code |string |Status code, "llm/ok" indicates success |
|msg |object |prompt message |
|data.sessionList |array |conversation list |
|data.sessionList[].id |int |Session ID |
|data.sessionList[].name |string |session name |
|data.sessionList[].emailPrefix |string |The mailbox prefix of the session owner |
|data.sessionList[].dataSetId |int |Linked Data Set ID |
|data.sessionList[].isExpired |bool |Has the session expired? |
|data.sessionList[].sessionType |int |session type |
|data.sessionList[].latestTaskStatus |string |Last task status |
|data.sessionList[].isMixed |bool |Whether to mix sessions |
|data.sessionList[].createTime |string |Creation time, format `YYYY-MM-DD HH: MM: SS` |
|data.sessionList[].lastActiveTime |string |Last active time |
|data.sessionList[].serverTime |string |Server level current time |
|data.sessionList[].agentInfo |object |Agent information (returned when the session is associated with a valid agent, otherwise the `agentId`field is returned) |
|data.sessionList[].isKnowledgeQA |bool |Knowledge Q & A session |
|data.sessionList[].customTag |array |custom tag list |


<span id="nNx2ozA8Gs"></span>
## Back to example

```json
{
  "JSONIFY_PRETTYPRINT_REGULAR": false,
  "code": "llm/ok",
  "data": {
    "sessionList": [
      {
        "agentInfo": {
          "agentType": "Expert",
          "avatar": "system3",
          "creatorPrefix": "admin",
          "description": "openApi test",
          "detail": null,
          "id": 430,
          "isNewAgent": true,
          "isPersonal": false,
          "mtime": "2026-08-11 11:29:17",
          "name": "openApi",
          "privilegeType": "agent"
        },
        "createTime": "2026-08-11 11:46:04",
        "customTag": [],
        "dataSetId": null,
        "emailPrefix": "admin",
        "id": 14442,
        "isExpired": true,
        "isKnowledgeQA": true,
        "isMixed": false,
        "lastActiveTime": "2026-08-11 11:51:07",
        "latestTaskStatus": "completed",
        "name": "Analyze the recent sales situation of e-commerce platforms",
        "serverTime": "2026-08-11 16:13:47",
        "sessionType": "deep_research"
      }
    ]
  },
  "msg": {}
}
```

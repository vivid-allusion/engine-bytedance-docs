---
title: "Retrieve Session Information"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Retrieve_Session_Information"
---

<span id="33e6f63c"></span>
# **Request description**


* Request method: GET

* Request URL: `/dataAgent/llm/openApi/v2/signed/agent/sessionInfo?sessionId={sessionId}`


<span id="f8fc26a9"></span>
# **Request parameters**


|Parameter |Type |Required or not |Example value |Description |
|---|---|---|---|---|
|sessionId |int |Yes |12886164 |Session ID. The session ID is returned in the sessionInfo result when a session is created. For details, see [Create a Session](https://docs.byteplus.com/docs/dataagent/Create_a_Session). |


<span id="5106a3cc"></span>
# **Response parameters**


|Parameter |Type |Description |
|---|---|---|
|messageList |array |Session history information. The current series of APIs does not support multi\-turn conversations. This field always returns an empty array. When multi\-turn conversations are supported in the future, historical session messages will be returned. |
|sessionInfo |object |Session information, including parameters such as agentInfo. For details, see the detailed parameter description below. |
|sessionInfo.agentInfo |object |Agent information associated with the session. For details, see the detailed parameter description below. |
|sessionInfo.agentInfo.agentType |string |Agent type<br><br><br>* Expert: Expert agent, that is, a custom agent you create yourself.<br><br>* General: General agent.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a comparison between general agents and custom agents, see <a href="https://docs.byteplus.com/docs/dataagent/Description_of_Agent_Types_General_and_Custom_Agents">Description of Agent Types: General and Custom Agents</a>.</div><br> |
|sessionInfo.agentInfo.avatar |string |Agent icon URL or abbreviation |
|sessionInfo.agentInfo.description |string |Agent description. |
|sessionInfo.agentInfo.id |int |Agent ID. |
|sessionInfo.agentInfo.isAgentAdmin |boolean |Whether the current user is the agent administrator. |
|sessionInfo.agentInfo.isDeepResearchOpen |boolean |Whether deep research is enabled for the agent. |
|sessionInfo.agentInfo.isDeepResearchQueryOpen |boolean |Whether this is the new intelligent query link. All current intelligent queries use the new link. You do not need to pay attention to this parameter. |
|sessionInfo.agentInfo.isInsightReportOpen |boolean |Whether deep research insight reports are enabled. |
|sessionInfo.agentInfo.name |string |Agent name. |
|sessionInfo.createTime |string |Session creation time, in yyyy\-MM\-dd HH:mm:ss format. |
|sessionInfo.dataSetId |int |Dataset bound to the session. |
|sessionInfo.emailPrefix |string |Session creator. |
|sessionInfo.id |int |Session ID. |
|sessionInfo.isExpired |boolean |Whether the session has expired. A session is considered expired if more than 24 hours have passed since its creation. |
|sessionInfo.lastActiveTime |string |Latest session activity time, in yyyy\-MM\-dd HH:mm:ss format. |
|sessionInfo.name |string |Session name. |
|sessionInfo.sessionType |string |Session type:<br><br><br>* normal Intelligent query<br><br>* deep_research Deep research |
|sessionInfo.reportId |int |DataWind visualization chart ID associated with the session result. |


<span id="fe5956f1"></span>
# Response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "messageList": [],
        "sessionInfo": {
            "agentInfo": {
                "agentType": "Expert",
                "avatar": "system4",
                "description": "1",
                "id": 24384,
                "isAgentAdmin": true,
                "isDeepResearchOpen": true,
                "isDeepResearchQueryOpen": true,
                "isInsightReportOpen": false,
                "modelTypeStandardName": "***model",
                "name": "Agent Name"
            },
            "createTime": "2025-10-24 16:03:54",
            "dataSetId": null,
            "emailPrefix": "admin",
            "fileList": [],
            "id": 12886164,
            "isExpired": false,
            "isMixed": false,
            "lastActiveTime": "2025-10-24 16:03:54",
            "latestTaskStatus": null,
            "name": "new session",
            "reportId": null,
            "restrictMode": 0,
            "scene": "data_set",
            "serverTime": "2025-10-24 16:03:54",
            "sessionType": "normal",
            "storageId": null
        }
    },
    "msg": {}
}
```

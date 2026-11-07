---
title: "Create a Session"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Create_a_Session"
---

<span id="c5981f2c"></span>
# **Request description**


* Request method: POST

* Request URL: `/dataAgent/llm/openApi/v2/signed/agent/createSession`

* Content\-Type：application/json


<span id="66f29296"></span>
# **Request parameters**

The body parameters are as follows.


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|agentId |int |Yes |123 |Agent ID. For information on how to obtain the agent ID, see [agentId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#6c63d736). |
|appId |int |Yes |123\*\*4 |DataWind project ID. If you do not use a scenario with joint deployment with DataWind, you can enter `0`. |
|sessionType |string |No (default is normal) |normal |Type of session to be created. Supported enumeration values:<br><br><br>* normal: Intelligent Q&A<br><br>* deep_research: Deep analysis |


<span id="4702d0a2"></span>
# **Response parameters**

The data in the response mainly contains parameters related to the created session (sessionInfo). Detailed parameter descriptions are as follows.


|Parameter |Type |Example value |Description |
|---|---|---|---|
|sessionInfo.emailPrefix |string |admin |The account name of the session creator, that is, the BytePlus account ID. |
|sessionInfo.id |int |12886164 |The ID of the created session (session id). You can record the session ID, which is required for subsequent interfaces such as retrieving session information and obtaining conversation results. |
|sessionInfo.lastActiveTime |string |2025\-10\-24 16:03:54 |The latest active time of the session. Date format: yyyy\-MM\-dd HH:mm:ss |
|sessionInfo.name |string |New session |Session name. The default is "New session" when first created. To modify the session name, call updateSession. |


<span id="e33fe648"></span>
# Response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "sessionInfo": {
            "createTime": "2025-10-24 16:03:54",
            "emailPrefix": "admin",
            "id": 12886164,  // Session ID, the most important field. You can record it for use in interfaces such as retrieving session information and other interfaces.
            "isExpired": false,
            "lastActiveTime": "2025-10-24 16:03:54",
            "name": "new session"
        }
    },
    "msg": {}
}
```

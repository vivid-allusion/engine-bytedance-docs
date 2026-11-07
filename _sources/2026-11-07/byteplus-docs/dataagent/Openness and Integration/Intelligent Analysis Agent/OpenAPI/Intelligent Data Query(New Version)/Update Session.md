---
title: "Update Session"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Update_Session"
---

<span id="93d2d538"></span>
# **Request description**


* Request method: POST

* Request URL: `/dataAgent/llm/openApi/v2/signed/agent/updateSession`

* Content\-Type：application/json


<span id="f192eafa"></span>
# **Request parameters**

The body parameters are as follows.


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|agentId |int |Yes |555327 |Agent ID. For information on how to obtain the agent ID, see [agentId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#6c63d736). |
|appId |int |Yes |17368 |DataWind project ID. If there is no scenario where DataWind is used in joint deployment, you can enter `0`. |
|sessionId |int |Yes |11469472 |Session ID. The session ID will be returned in sessionInfo when creating a session. For details, see [Create a Session](https://docs.byteplus.com/docs/dataagent/Create_a_Session). |
|payload |object |No |See the request example below |Identifies the request source. The default is openapi. |
|payload.name |string |No |See the request example below |Session name. Only the first 128 characters are retained. |


<span id="dc9f77d8"></span>
# Request example

```JSON
{
    "appId": 555327,
    "agentId": 17368,
    "sessionId": 11469472,
    "payload": {
        "name": "Grouping and analyzing the usage of the large model yesterday by first level scenario for each scene UV"
    }
}
```


<span id="5859e7f7"></span>
# **Response parameters**

The data in the response mainly contains parameters related to the created session (sessionInfo). Detailed parameter descriptions are as follows.


|Parameter |Type |Example value |Description |
|---|---|---|---|
|sessionInfo.createTime |string |2025\-09\-04 13:51:10 |Session creation time. Date format: yyyy\-MM\-dd HH:mm:ss |
|sessionInfo.emailPrefix |string |admin |The account name of the session creator, that is, the BytePlus account ID. |
|sessionInfo.id |int |12886164 |The created session ID (session id). You can record the session ID. Subsequent interfaces for obtaining session information, retrieving conversation results, and so on require the session ID. |
|sessionInfo.isExpired |boolean |false |Whether the session is expired. A session is considered expired if more than 24 hours have passed since creation. |
|sessionInfo.lastActiveTime |string |2025\-10\-24 16:03:54 |The latest active time of the session. Date format: yyyy\-MM\-dd HH:mm:ss |
|sessionInfo.name |string |New session |Session name. |


<span id="f16e4e33"></span>
# Response example

```JSON
{
    "JSONIFY_PRETTYPRINT_REGULAR": false,
    "code": "llm/ok",
    "data": {
        "sessionInfo": {
            "createTime": "2025-09-04 13:51:10",
            "emailPrefix": "admin",
            "id": 11469472,
            "isExpired": false,
            "lastActiveTime": "2025-09-04 13:51:10",
            "name": "Grouping and analyzing the usage of the large model yesterday by first level scenario for each scene UV"
        }
    }
}
```

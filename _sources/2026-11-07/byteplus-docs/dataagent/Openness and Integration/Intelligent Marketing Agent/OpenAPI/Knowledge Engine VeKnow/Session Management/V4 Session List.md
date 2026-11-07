---
title: "V4 Session List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/v4-session-list"
---

Call this interface to page and pull the current user's V4 intelligent Q & A session, support filtering by keywords, and keep source compatibility parameters.

# Interface description

* Interface name: list_conversations_v4_conversation_v4_conversations_get

* Interface address:/conversation/v4/conversations

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|page |Number |No |paging page number |
|page_size |Number |No |entries per page |
|keywords |String |No |keyword |
|source |String |No |data source |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |business status code |
|msg |String |No |business status description |
|data |\- |No |interface returns data |

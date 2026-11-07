---
title: "V4 Session Message List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/v4-session-message-list"
---

Call this interface to page and pull the chat history and final results in the specified V4 Q & A session.

# Interface description

* Interface name: list_message_v4_conversation_v4_list_message_get

* Interface address:/conversation/v4/list/message

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |String |Yes |Session ID |
|page_number |Number |No |paging page number |
|page_size |Number |No |entries per page |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |business status code |
|msg |String |No |business status description |
|data |\- |No |interface returns data |

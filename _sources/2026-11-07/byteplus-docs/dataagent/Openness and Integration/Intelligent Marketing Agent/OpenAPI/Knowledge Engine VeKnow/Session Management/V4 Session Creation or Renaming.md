---
title: "V4 Session Creation or Renaming"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/v4-session-creation-or-renaming"
---

Call this interface to create a V4 Q&A session, or rename an existing session according to the session ID.

# Interface description

* Interface name: set_conversation_v4_conversation_v4_set_post

* Interface address:/conversation/v4/set

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |String |No |Session ID to rename; creates a new session for empty time. |
|id |String |No |conversation_id compatible alias. |
|title |String |No |Session title. |
|name |String |No |Compatible aliases for the title. |
|metadata |Object |No |Extended information passed through when creating a session. |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |business status code |
|msg |String |No |business status description |
|data |Object |No |Session information created or renamed; may be empty in case of business failure. See the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |String |No |Session ID |
|id |String |No |id |
|title |String |No |conversation title |
|name |String |No |session name |

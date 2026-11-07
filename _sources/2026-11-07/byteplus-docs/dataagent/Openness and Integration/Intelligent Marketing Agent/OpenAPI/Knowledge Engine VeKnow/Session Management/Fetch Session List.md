---
title: "Fetch Session List"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/fetch-session-list"
---

Call this interface to page query all session records under the specified conversation, and support filtering by source type.

# Interface description

* Interface name: list_conversation_conversation_list_get

* Interface address: /conversation/list

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|dialog_id |Number |Yes |Conversation ID |
|source |String |No |source type |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |No |Session list data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|id |Number |Yes |Session ID |
|dialog_id |Number |Yes |Conversation ID |
|name |String |Yes |session name |
|message |Array |No |message list |
|reference |Array |No |Reference list, two\-dimensional array format, array elements are objects, that is, Object [] [] |
|config |Object |No |Session configuration response, see the **config** table below for details |
|rag_setting |Object |No |Retrieve Application RAG Settings |

## config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|knowledge_scope |Object |No |Scope of knowledge, see **knowledge_scope** table below |
|attach_files |Array |No |See the **attach_files** table below for a list of annexes |
|web_search |Boolean |No |Whether to open online search |
|deep_thinking |Boolean |No |Whether to start deep thinking |

## knowledge_scope

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |Scope mode:<br><br><br>* scoped<br><br>* global |
|kb_ids |Array |No |Knowledge Base ID List |
|graph_ids |Array |No |graph ID list |

## attach_files

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_type |String |No |file type |
|id |Number |No |Document ID |
|file_name |String |No |Document name |

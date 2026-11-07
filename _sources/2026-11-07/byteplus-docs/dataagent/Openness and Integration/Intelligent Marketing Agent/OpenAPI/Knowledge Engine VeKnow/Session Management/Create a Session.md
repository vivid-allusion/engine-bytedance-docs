---
title: "Create a Session"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/create-a-session"
---

Calling this interface creates a new conversation session to record the interaction history between the user and the AI application.

# Interface description

* Interface name: set_conversation_conversation_set_post

* Interface address: /conversation/set

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |Number |No |session identifier |
|dialog_id |Number |No |conversation identifier |
|name |String |No |session name |
|id |Number |No |Session ID (alias) |
|title |String |No |conversation title |
|message |Array |No |message list |
|reference |Array |No |Reference list, two\-dimensional array format, array elements are objects, that is, Object [] [] |
|source |String |No |Source:<br><br><br>* dialog<br><br>* retrieval |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code:<br><br>0 = success<br><br>Non\-zero = failure |
|msg |String |No |When the code is not 0, an error message is returned |
|message |String |No |error message |
|data |Object |Yes |Session data, see the **data** table below for details |

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

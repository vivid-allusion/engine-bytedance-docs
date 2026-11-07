---
title: "Fetch Chat Content in Session"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/fetch-chat-content-in-session"
---

Call this interface page to get the history of chat messages in the specified session, in chronological order.

# Interface description

* Interface name: list_message_conversation_list_message_get

* Interface address:/conversation/list/message

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |Number |Yes |Session ID |
|page_number |Number |No |page number |
|page_size |Number |No |page size |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code:<br><br>0 = success<br><br>Non\-zero = failure |
|msg |String |No |When the code is not 0, an error message is returned |
|message |String |No |error message |
|data |Object |Yes |Paging session messages, see the **data** table below |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|total |Number |Yes |total |
|page |Number |Yes |page number |
|page_size |Number |Yes |number of pages per page |
|items |Array |Yes |List of messages, see the **items** table below |

## **items**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|id |Number |Yes |Message ID |
|prompt |String |No |cue word |
|role |String |Yes |Message role:<br><br><br>* user<br><br>* assistant<br><br>* system |
|content |String |Yes |content |
|reasoning_content |String |No |inference content |
|references |Array |No |List of references, see the **references** table below |
|feedback |Object |No |Feedback, please see the **feedback** form below |
|content_type |String |No |content type |
|chat_id |String |No |Chat ID |
|conversation_id |String |No |Session ID |
|message_type |String |No |message type |

## references

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|type |String |No |Message reference type:<br><br><br>* file<br><br>* doc<br><br>* online<br><br>* quote |
|item |Object |No |Reference content, different message return parameters are different, please refer to the following **item** table for details |

## **item**

### Situation 1: Document message references

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|resource_key |String |No |resource key |
|resource_name |String |No |resource name |
|resource_type |String |No |resource type |

### Situation 2: Referenced message references

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |Chunk ID ID |
|chunk_id |String |Yes |Chunk logo |
|content_with_weight |String |Yes |Weighted Chunk Content |
|doc_id |String |Yes |Document ID |
|doc_name |String |Yes |Document name |
|kb_id |String |No |Knowledge Base ID |
|image_url |String |No |image URL |
|url |String |No |reference URL |
|extra |Object |No |Additional information |

### Situation 3: Online message citation

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|site_name |String |No |site name |
|summary |String |No |abstract |
|publish_time |String |No |release time |
|title |String |No |title |
|url |String |No |reference link |
|logo_url |String |No |Logo link |
|mobile_url |String |No |Mobile end link |
|cover_image |Object |No |Cover image, see **cover_image** table below |

### cover_image

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |No |Cover image link |
|width |Number |No |width |
|height |Number |No |height |

## **feedback**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|contents |Array |No |Feedback content list, see the **contents** table below for details |
|thumb_up |Boolean |No |Do you like it? |

## contents

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|type |String |Yes |Feedback type:<br><br><br>* system<br><br>* custom |
|content |String |Yes |feedback content |

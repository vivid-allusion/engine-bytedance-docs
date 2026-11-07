---
title: "V4 Smart Q&A"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/v4-smart-q-a"
---

Call this interface to initiate V4 intelligent Q & A, support enterprise knowledge, personal knowledge, ontology semantics, Knowledge Graph, attachments, networked search and deep thinking, and return results in SSE streaming.

# Interface description

* Interface name: chat_v4_conversation_v4_chat_post

* Interface address:/conversation/v4/chat

* Request method: POST

# Request parameters

Object type request body, including parameter description as shown in the following table.

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|conversation_id |String |No |Session ID; automatically created when empty. |
|chat_id |String |No |This round of chat ID; automatically generated when empty. |
|regenerate_from_chat_id |String |No |The original chat ID associated with the regeneration. |
|qa_kb_ids |Array |No |List of QA Knowledge Base IDs that are merged into knowledge_scope and passed to master\-control. |
|qa_doc_ids |Array |No |List of QA document IDs that are merged into knowledge_scope and passed to master\-control. |
|qa_folder_ids |Array |No |List of QA folder IDs that are merged into knowledge_scope and passed to master\-control. |
|term_kb_ids |Array |No |The list of term knowledge base IDs that are merged into knowledge_scope and passed to master\-control. |
|term_doc_ids |Array |No |A list of term document IDs that are merged into knowledge_scope and passed to master\-control. |
|term_folder_ids |Array |No |List of term folder IDs that are merged into knowledge_scope and passed to master\-control. |
|graph_ids |Array |No |Compatibility field; for new requests, pass in the Knowledge Graph ID knowledge_graph_scope. |
|ontology_ids |Array < Number \> or<br><br>Array |No |Compatibility field; pass in string ontology ID via ontology_scope for new requests. |
|metadata |Object |No |Runtime extension parameters. |
|stream |Enum<br><br>Boolean |No |Compatibility field; the current interface is always streamed back in SSE. |
|messages |Array |Yes |Message list; currently only the last message is consumed, and its role must be user, text content cannot be empty. See the **messages** table below for details |

## messages

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|role |String |Yes |Message role; requires the role of the last message to be user<br><br><br>* system<br><br>* user<br><br>* assistant |
|message_type |String |No |Message type; intelligent Q & A request using question |
|content_type |String |No |Message content type; text means plain text, mixed means contains multiple capability items |
|content |String or Object |Yes |Text questions, or mixed content objects containing items. |

# Response parameters

The response is of type Object.

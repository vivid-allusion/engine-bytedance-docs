---
title: "Get the Sublist of Personal Knowledge Base Resources"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/get-the-sublist-of-personal-knowledge-base-resources"
---

Call this interface to query the resource sub\-list of Token binding user personal knowledge base: the root layer returns the knowledge base list, and returns the folder and document of the same layer after specifying the parent resource.

# Interface description

* Interface name: get_resource_children_knowledge_spaces_resources_children_get

* Interface address:/knowledge\-spaces/resources/children

* Request method: GET

# Request parameters

## Query

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|parent_resource_id |Number |No |Parent resource ID; passed in pairs with parent_resource_type |
|parent_resource_type |String |No |Parent resource type; query space root node when ID and type are omitted<br><br><br>* LIBRARY<br><br>* FOLDER<br><br>* DOCUMENT |
|cursor |String |No |Previous page next_cursor; Home page is not passed on |
|page |Number |No |Page numbers; takes effect when cursor is empty |
|page_size |Number |No |Number of pages, default 50 |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Error |No |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|items |Array |No |Current level of resources. See the **items** table below for details |
|next_cursor |Number |No |Next page cursor |

## items

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|resource_id |Number |Yes |Resource ID; document resource equals document_id |
|resource_type |String |Yes |The node type of the sidebar resource tree; LIBRARY is the virtual root node of each class library under the space.<br><br><br>* LIBRARY<br><br>* FOLDER<br><br>* DOCUMENT |
|library_type |String |No |The type of first\-level knowledge base that space can mount must be consistent with knowledge_space_kb_ref kb_type.<br><br><br>* KNOWLEDGE_BASE<br><br>* LLM_WIKI<br><br>* ONTOLOGY<br><br>* GRAPH |
|name |String |Yes |display name |
|status |String |Yes |The visible processing state before resource consumption is not equivalent to the complete state of the underlying parsing task.<br><br><br>* READY<br><br>* PROCESSING<br><br>* FAILED |
|has_children |Boolean |Yes |Can it continue to expand? |
|capabilities |Array |Yes |executable action |

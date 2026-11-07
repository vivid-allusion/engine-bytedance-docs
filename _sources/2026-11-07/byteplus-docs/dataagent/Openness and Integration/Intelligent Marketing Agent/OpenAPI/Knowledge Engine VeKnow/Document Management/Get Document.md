---
title: "Get Document"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/get-document"
---

Call this interface to obtain the document content in the knowledge base (such as downloading files) through the document ID.

# Interface description

* Interface name: get_document_get__doc_id__get

* Interface address:/document/get/

* Request method: GET

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number |Yes |Document ID |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Object |No |Document data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|id |Number |Yes |Document ID |
|thumbnail |String |No |Thumbnail Base64 string |
|kb_id |Number |Yes |Knowledge Base ID |
|parser_id |String |Yes |Default parser ID |
|parser_config |Object |No |parse configuration |
|source_type |String |Yes |document source |
|type |String |Yes |file extension |
|created_by |String |Yes |founder |
|name |String |Yes |file name |
|display_name |String |No |document display name |
|location |String |No |File storage location |
|size |Number |No |size |
|token_num |Number |Yes |Number of Tokens |
|chunk_num |Number |Yes |number of slices |
|character_count |Number |No |Total number of characters in the document |
|avg_character_count |Number |No |segmented average characters |
|progress |Number |Yes |progress |
|progress_msg |String |No |process message |
|task_progress_raw |String |No |Sophon raw taskProgress aggregate JSON string |
|process_begin_at |String |No |Processing start time |
|process_duation |Number |Yes |processing time |
|run |String |No |Operating status: 1 running, 2 canceled |
|status |String |No |Document Status: 0 obsolete, 1 valid |
|valid_date |String |No |Effective Date |
|auto_delete_on_expire |Boolean |No |Is it automatically deleted after expiration? |
|labels |Array |No |Label information, see the **labels** table below |
|category |String |No |classification |
|sha256 |String |No |SHA256 Abstract |
|retrieval_count |Number |No |number of searches |
|versions |Array |No |version list |
|folder_id |Number |No |Folder ID |
|url |String |No |File URL |
|downloadable |Boolean |No |Can it be downloaded? |
|content_category |Array |No |List of content category names, see below for details<br><br>**content_category** table |
|quality_result |Number |No |Quality test results |
|spell_check_count |Number |No |number of typos detected |
|completeness_check_count |Number |No |number of integrity tests |
|sensitive_word_check_count |Number |No |number of sensitive words detected |
|is_enabled |Boolean |No |Whether to enable |
|prep_task_id |Number |No |Preprocessing Task ID |
|chunk_settings_type |String |No |The conversion slice configuration category used by the current document |
|prep_file_path |String |No |Prep file path |
|actions |Array |No |The current user's valid permissions to the document |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|create_time |Number |No |Create timestamp |
|create_date |String |No |creation time |
|update_time |Number |No |Update timestamp |
|update_date |String |No |update time |
|label_id |Number |Yes |Tag ID |
|label_name |String |No |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_values |Array |No |List of label values, see **label_values** table below |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |
|prompt_version |String |No |Cue word version |
|label_usage |Number |No |tag usage |

## label_values

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |tag value ID |
|value |String |No |label value |
|value_usage |Number |No |tag value usage |
|label_value_builder |String |No |Label Value Builder<br><br><br>* manual<br><br>* chat_model |

## content_category

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |Yes |Category ID |
|name |String |No |Category name |

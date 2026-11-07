---
title: "Add Document Version"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/add-document-version"
---

Call this interface to submit a single file that has been uploaded as a new version of the target document; target_doc_id required.

# Interface description

* Interface name: create_document_entry_version_document_version_create_post

* Interface address:/document/version/create

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|kb_ids |Array |Yes |Knowledge Base ID List |
|file_ids |Array |No |file identifier |
|file_parse_type_overrides |Array |No |File parsing type override; import scope can be inferred from match.file_ids/source_keys when file_ids/object_keys is not explicitly provided. See **file_parse_type_overrides** table below for details |
|embd_id |String |No |Embedded Model Identifier |
|source_type |String |No |parsing model source type |
|chunk_settings |Object |No |Unified slice configuration. For details, please see [chunk_settings](https://docs.byteplus.com/docs/dataagent/edit-document-configuration#0941fe1e). |
|quality_settings |Object |No |Unified quality inspection configuration. For details, please refer to [quality_settings](https://docs.byteplus.com/docs/dataagent/edit-document-configuration#302ace2c). |
|parser_config |AnyOf |No |Parse configuration, support LarkParserConfig/ReportifyConfig/SophonParserConfig three structures. For details, please see [config](https://docs.byteplus.com/docs/dataagent/edit-document-configuration#98a2f9f4). |
|skip_duplicate |Boolean |No |Whether to skip duplicate files |
|feishu_config |Array |No |Lark configuration. For details, please see [feishu_config](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base#edfd36dd). |
|dingtalk_config |Array |No |DingTalk configuration. For details, please see [feishu_config](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base#edfd36dd). |
|wecom_config |Array |No |WeCom document configuration. See **wecom_config** table below for details |
|schedule_config |Object |No |Scheduling configuration. For details, please see [schedule_config](https://docs.byteplus.com/docs/dataagent/create-knowledge-bases#d3e763f7). |
|object_keys |Array |No |Object Storage Key |
|template_id |String |No |Parse template identifiers that will overwrite parser_config |
|apply_type |Number |No |Application Type |
|access_key |String |No |Access key (soon to be deprecated) |
|secret_key |String |No |Secret key (soon to be obsolete) |
|oss_config |Object |No |OSS configuration. See **oss_config** table below for details |
|media_platform_config |Object |No |Media platform configuration. See **media_platform_config** table below for details |
|public_url_config |Object |Yes |Expose the link import configuration. See **public_url_config** table below for details |
|datasource_code |String |No |Data source code |
|folder_id |Number |No |Import destination folder ID |
|target_doc_id |Number |No |Destination document ID for version import |
|version_policy |String |No |The persistent version mode when creating a new document, the new version is added by default; the target document configuration is not overwritten when target_doc_id exists<br><br><br>* ADD_VERSION<br><br>* OVERWRITE_VERSION |
|version_rule_type |String |No |Version number rules persisted when creating a new document; target document configuration is not overwritten when target_doc_id or source_unique_id hits an existing document<br><br><br>* CUSTOM<br><br>* DAY<br><br>* WEEK<br><br>* MONTH<br><br>* QUARTER<br><br>* YEAR |
|version_rule_config |Object |No |Configuration of version number rules for new documents; support prefix and timezone, default V and Asia/Shanghai |
|version_date |Number |No |Business version date, Unix millisecond timestamp; current time is used when version import is not passed |
|source_unique_id |String |No |Prep/API source document unique identity; automatically import according to its version policy when an existing document is hit in the knowledge base |
|source_identity_type |String |No |Upstream uniquely identifies the source type to which it belongs; use datasource_code when not passed |
|datasource_meta_id |Number |No |Data source metadata ID |
|data_connection_id |Number |No |Data Connection ID |
|name |String |No |Document name |
|rds_config |Object |No |RDS configuration |
|vecdp_config |Object |No |VecDP configuration |
|labels |Array<Array\> |No |List of document tags, the outer list corresponds to multiple documents, and the inner list corresponds to the tags of a single document. See the **labels** below for details |
|label_ids |Array |No |Batch setting of document labels (for frontend use). See **label_ids** table below for details |
|extras |Array |No |additional data |
|extra |Object |No |Version group extra parameters for passing additional parameters to Sophon |
|ocr_model |String |No |It has been abandoned. Use switch_config: switch_doc_parser_vlm_ocr to control the ocr backend |
|prompt_locale |String |No |The locale of the cue word parsed by Sophon VLM, such as zh\-CN or en\-US. |
|spell_check |Boolean |No |Whether to enable spell check |
|completeness_check |Boolean |No |Deprecated: Please use quality_settings. \* completeness_check |
|sensitive_word_check |Boolean |No |Deprecated: Please use quality_settings. \* sensitive_word_check |
|duplicate_doc_check |Boolean |No |Deprecated: Please use quality_settings. \* duplicate_doc_check |
|video_parser_config |Object |No |Video parsing configuration. For details, please see [video_parser_config](https://docs.byteplus.com/docs/dataagent/edit-document-configuration#1c231ffd). |

## file_parse_type_overrides

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|match |Object |Yes |Slice configuration matching criteria. See the **match** table below for details |
|parse_type |String |Yes |File parsing type<br><br><br>* text<br><br>* doc<br><br>* other<br><br>* pdf<br><br>* ppt<br><br>* image<br><br>* table |

## match

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_id |Number |No |local file ID |
|file_ids |Array |No |List of local file IDs |
|source_key |String |No |Object storage source file key |
|source_keys |Array |No |Object storage source file key list |

## **wecom_config**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_url |String |Yes |WeCom documentation URL |
|doc_token |String |No |Document token (show value only) |
|name |String |No |Document name (display values only) |
|doc_type |String |No |Document type (only displaying values) |
|type |Number |No |WeCom document type |
|endpoint_fingerprint |String |No |MCP endpoint fingerprint (show value only) |

## oss_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|access_key |String |No |access key |
|secret_key |String |No |key |
|region |String |No |region |
|bucket |String |No |bucket name |
|directory |Array |No |directory listing |
|endpoint |String |No |access address |
|type |String |No |type |

## media_platform_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|access_key |String |No |access key |
|secret_key |String |No |key |

## public_url_config

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|urls |Array |Yes |Publish a list of links (elements are {url, file_id} binding structures, also compatible with pure URL strings), URLs must start with http://or https://. See the **urls** table below for details |
|recursive_links |Boolean |No |Whether to crawl a layer of inner chain recursively (only HTML takes effect) |
|auto_update |Boolean |No |Whether to turn on automatic updates |
|schedule_config |Object |No |scheduling configuration |
|directory |String |No |Directory ID (UUID), used to reuse verification results or locate the same batch |

## urls

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |Yes |Public links must start with http://or https:// |
|file_id |Number |No |Bound uploaded file ID (/public_url/html mode = upload |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_name |String |Yes |label name |
|label_type |String |Yes |document tag type<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_value |Array |Yes |list of label values |

## label_ids

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_id |Number |Yes |Tag ID |
|label_value_ids |Array |No |Label value ID list |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Array |No |Data, see the **data** table below for details |

## data

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|id |Number |No |identifier |
|file_id |Number |No |File ID |
|document_id |Number |No |Document ID |
|running_state |String |No |running state |
|version_id |Number |No |Version Record ID |
|run_required |Boolean |No |Do you need to call the document run interface? |
|document_name |String |No |Document name |
|duplicate_docs_names |Array |No |duplicate document name |
|is_all_duplicate |Boolean |No |Is it all repeated? |

---
title: "File Associate with Knowledge Base"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/file-associate-with-knowledge-base"
---

Call this interface to associate the uploaded file to the specified knowledge base and configure the parsing parameters. Before calling the current interface, it should call [Upload File](https://docs.byteplus.com/docs/dataagent/upload-file) first; after completing the current interface, the relevant tasks are only submitted, not yet officially executed, and must continue to call [Start Parsing the Document](https://docs.byteplus.com/docs/dataagent/start-parsing-the-document) before they really start to execute.

# Interface description

* Interface name: convert_file2document_convert_post

* Interface address: /file2document/convert

* Request method: POST

# Request parameters

> **说明**

* > The request body is in JSON format. The minimum request only needs to pass in the target knowledge base ID and the file ID to be imported; if you need to set the resolution policy for different file types, you can pass in `chunk_settings`, `quality_settings`and `file_parse_type_overrides`.

* > It is recommended that new access parties use `chunk_settings` and `quality_settings`organization resolution configurations uniformly; legacy fields are only used for historical compatibility.

* > Top\-level old fields `completeness_check`, `sensitive_word_check`, `duplicate_doc_check`are reserved for compatibility purposes only. New access uniformly into the `quality_settings`.

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|kb_ids |Array |Yes |Knowledge Base ID List |
|file_ids |Array |Required conditions |file identifier |
|file_parse_type_overrides |Array |No |File parsing type override; import scope can be inferred from match.file_ids/source_keys when file_ids/object_keys is not explicitly provided. For more information, please see [parse type override](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base#4a0de738). |
|embd_id |String |No |Embedded Model Identifier |
|source_type |String |No |parsing model source type |
|chunk_settings |Object |No |Unified slice configuration. For configuration details, see [chunk_settings configuration](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base#16071ea6). |
|quality_settings |Object |No |Unified quality inspection configuration. For configuration details, see [quality_settings configuration](https://docs.byteplus.com/docs/dataagent/file-associate-with-knowledge-base#960eaade). |
|parser_config |Object |No |Parse configuration, support LarkParserConfig/ReportifyConfig/SophonParserConfig three structures, see the following **parser_config** table for details |
|feishu_config |Array |No |Lark configuration, see **feishu_config** table below |
|schedule_config |Object |No |Scheduling configuration, see **schedule_config** table below |
|object_keys |Array |Required conditions |The object stores a list of source file keys under the import scene. When not explicitly passed in, can be derived from `file_parse_type_overrides. Match. source_key`or `file_parse_type_overrides. Match. source_keys`. |
|template_id |String |No |Parse template identifiers that will overwrite parser_config |
|apply_type |Number |No |Application Type |
|access_key |String |No |Access key (soon to be deprecated) |
|secret_key |String |No |Secret key (soon to be obsolete) |
|oss_config |Object |No |OSS configuration |
|media_platform_config |Object |No |media platform configuration |
|public_url_config |Object |Yes |Public Link Import Configuration |
|datasource_code |String |Object storage scenario Required |Data source type identification, such as the `object_storage`used when importing an object store. |
|folder_id |Number |No |Import destination folder ID |
|datasource_meta_id |Number |Object storage scenario Required |Data source meta information ID. |
|data_connection_id |Number |No |Data Connection ID |
|name |String |"" |Document name |
|rds_config |Object |No |RDS configuration |
|vecdp_config |Object |No |VecDP configuration |
|labels |Array |No |Document label list, the outer list corresponds to multiple documents, and the inner list corresponds to the label of a single document |
|label_ids |Array |No |Batch setting of document labels, label ID collection |
|extras |Array |No |additional data |
|extra |Object |No |Version group extra parameters for passing additional parameters to Sophon |
|ocr_model |String |No |It has been abandoned. Use switch_config: switch_doc_parser_vlm_ocr to control the ocr backend |
|prompt_locale |String |No |The locale of the cue word parsed by Sophon VLM, such as zh\-CN or en\-US. |
|spell_check |Boolean |No |Whether to enable spell check |
|completeness_check |Boolean |No |Deprecated: Please use quality_settings. \* completeness_check |
|sensitive_word_check |Boolean |No |Deprecated: Please use quality_settings. \* sensitive_word_check |
|duplicate_doc_check |Boolean |No |Deprecated: Please use quality_settings. \* duplicate_doc_check |
|video_parser_config |Object |No |Video analysis configuration, see the **video_parser_config** table below for details |

## Minimum Available Request Example

```JSON
{
  "kb_ids": [123],
  "file_ids": [1001]
}
```

## Parse type override

`file_parse_type_overrides`Used to logically resolve types by file declaration. It only decides which type of parsing configuration the file should read and does not directly override the specific slice parameters; the specific parameters remain in the `chunk_settings`and `file_overrides`of the corresponding type.

### Matching rule

|**Field** |**Applicable scenario** |**Description** |
|---|---|---|
|match.file_id |local upload |Matches individual file IDs. |
|match.file_ids |local upload |Match multiple file IDs in batches. |
|match.source_key |Object Store Import |Matches a single source file key. |
|match.source_keys |Object Store Import |Batch match multiple source file keys. |

`parse_type`optional values: `text`, `doc`, `other`, `pdf`, `ppt`, `image`, `table`. Where `doc`is handled as `text`.

```JSON
{
  "file_parse_type_overrides": [
    {
      "match": {
        "file_ids": [1002, 1003]
      },
      "parse_type": "ppt"
    }
  ],
  "chunk_settings": {
    "ppt": {
      "max_segment_length": 800,
      "exclude_master_content": true
    }
  }
}
```

## chunk_settings configuration

`chunk_settings`Grouped by file type to control slicing, parsing, and import extraction parameters for different types of files. Fields use `snake_case`uniformly.

### 1. File type grouping

|**Group** |**Applicable documents** |**Description** |
|---|---|---|
|`text`/`doc` |.Doc, .docx, .txt, .md, etc |Common documentation; `doc`is a compatibility alias. |
|`other` |.HTML, .json, etc |Other document types. |
|`pdf` |.pdf |PDF file. |
|`ppt` |.ppt、.pptx |PowerPoint. |
|`image` |image file |Picture understanding and OCR configuration. |
|`audio` |.mp3、.wav |Audio transcription configuration. |
|`video` |.mp4、.mov、.avi |Video understanding, audio transcription, and audio\-video fusion configuration. |
|`table` |.xls、.xlsx、.csv |Automatic table segmentation or custom segmentation configuration. |

### 2. General Documents, Other Documents, and PDF Configuration

|**Field name** |**Type** |**Description** |
|---|---|---|
|`mode` |String |Slicing mode. Optional values: `default`, `custom`, `model_summary`, `context_aware`. |
|`max_segment_length` |Integer |The maximum length of each slice segment, defaults to 1024. |
|`custom_separator` |String |Custom delimiter that takes effect only when `mode = custom`. |
|`associate_chunk_title` |Boolean |Whether to associate a header when customizing a segment only takes effect when `mode = custom`. |
|`merge_small_chunks` |Boolean |When customizing segments, whether successive small segments are automatically merged. |
|`small_chunk_token_threshold` |Integer |Small segmentation threshold, unit token. |
|`extract_images` |Boolean |Whether to extract images from the document, the default is true. |
|`image_understand` |Boolean |Whether to intelligently understand the extracted pictures, the default is false. |
|`image_understand_max_tokens` |Integer |The maximum number of output tokens allowed to be generated when the image is intelligently understood. |
|`extract_tables` |Boolean |Whether to extract a table from a document, the default is false. |

### 3. PPT, picture, audio and video configuration

|**Type** |**Field** |**Description** |
|---|---|---|
|`ppt` |`mode`、`max_segment_length`、`exclude_master_content`、`exclude_header_footer` |PPT only supports automatic segmentation, allowing you to configure slice lengths, remove master noise, and remove headers and footers. |
|`image` |`mode`、`image_understand`、`image_ocr`、`max_segment_length` |Control image comprehension, OCR, and slice length. |
|`audio` |`mode`、`asr_model` |When importing audio files, you must provide `asr_model`. |
|`video` |`mode`、`fuse_video_asr`、`asr_model`、`video_model`、`fuse_model` |When importing video files, you must provide `asr_model`, `video_model`and `fuse_model`. |

> **注意**

> If the imported audio file is missing `chunk_settings.audio. asr_model`, or the imported video file is missing `chunk_settings.video. asr_model`, `video_model`, `fuse_model`, the request will fail during the entry verification phase.

### 4. Table configuration

Table files support automatic segmentation and custom segmentation. It is recommended to organize the configuration at the following level: `table`represents the table default policy, `table. file_overrides []`hits a specific file, `file_overrides [] .sheets []`specifies sheet, `sheets [] .columns []`specifies column configuration.

|Scene |Configuration method |Description |
|---|---|---|
|Automatic segmentation |`mode=auto` |The system completes sheet and header recognition. Model identification or rule configuration can be specified by `parse_strategy`. |
|Model automatic recognition header |`parse_strategy=model_auto_header` |Headers are identified by the model. |
|rule configuration |`parse_strategy = rule`, and configure `header_row`, `data_start_row` |Identifies the header and data start rows by the specified line number, starting at 1. |
|custom segmentation |`file_overrides [] .mode = custom`, and configure `sheets`, see the following **sheets field table** |Separately configure sharding rules and column configurations for one or more sheets of a table file. |

#### Sheets field

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|`sheet_name` |String |Required conditions |Sheet name; pass at least one with `sheet_id`. |
|`sheet_id` |String |Required conditions |Sheet ID; pass at least one with `sheet_name`. |
|`header_row` |Integer |No |The header of the current sheet, starting at 1. |
|`data_start_row` |Integer |No |The starting row of the current sheet, starting at 1. |
|`columns` |List |No |Column configuration for the current sheet. See the **columns field** table below for details. |

#### Columns field

|**Field name** |**Type** |**Description** |
|---|---|---|
|`source_name` |String |Original list name. |
|`target_name` |String |The imported column alias. Use `source_name`when not transmitted. |
|`enabled` |Boolean |Whether to enable the column to participate in the recall, the default is true. |
|`data_type` |String |Column data type. Optional values: `STRING`, `INT`, `DOUBLE`, `DATE`, `DATETIME`, `ARRAY`, `LINK`. Default `STRING`when not passed. |
|`description` |String |Column description. |

## quality_settings configuration

`quality_settings` Responsible for managing quality inspection and duplicate document validation policies, grouped by file type with the same type name as `chunk_settings`. The current `quality_settings` does not support `file_overrides`.

|**Field name** |**Type** |**Description** |
|---|---|---|
|`spell_check` |Boolean |Whether to enable typo detection. |
|`completeness_check` |Boolean |Whether to enable integrity detection. |
|`sensitive_word_check` |Boolean |Whether to turn on sensitive word detection. |
|`duplicate_doc_check` |Boolean |Whether to enable duplicate document validation. This configuration will take effect before import, and only the files with the switch turned on under the current hit file type will be checked. |

```JSON
{
  "quality_settings": {
    "text": {
      "completeness_check": true,
      "sensitive_word_check": false,
      "duplicate_doc_check": true
    },
    "ppt": {
      "completeness_check": false,
      "sensitive_word_check": true,
      "duplicate_doc_check": false
    }
  }
}
```

## Configure the effective rules

When a request contains multiple files, the system resolves the configuration file by file. A high\-priority configuration overrides a low\-priority configuration with the same name.

|**Priority** |**Configuration source** |**Description** |
|---|---|---|
|1 |`file_parse_type_overrides` |Determine whether the current file overwrites the default parsing type; if it misses, continue to read the configuration according to the default file type. |
|2 |`file_overrides` |Within the final hit file type grouping, look for an overwrite that hit the current file. |
|3 |type\-level global configuration |Use global configurations for file types such as `text`, `pdf`, `audio`, `video`, `table`. |
|4 |`parser_config` |History\-compatible configuration, fallback only if no relevant fields are defined in the new configuration. |
|5 |System Default |When none of the above configurations are provided, the system default values are used. |

## Verification and limit

|**Rule** |**Description** |
|---|---|
|Table schema mutual exclusion |`Mode = auto`does not allow `sheets`to be configured at the same level; `mode = custom`must configure `sheets`at the same level. |
|Automatic segmentation rule configuration |`Mode = auto`allows configuration of `header_row`and `data_start_row`only if `parse_strategy = rule`. |
|custom segmentation limit |`Mode = custom`does not allow configuring `parse_strategy`, nor does it allow configuring `header_row`or `data_start_row`at the same level. |
|CSV limit |CSV files have no sheet concept and are not suitable for multi\-sheet configuration. |
|Required audio model |You must provide `chunk_settings.audio asr_model`when importing audio files. |
|video required model |You must provide `chunk_settings.video. asr_model`, `chunk_settings.video. video_model`and `chunk_settings.video. fuse_model`when importing video files. |

## parser_config

### **Situation 1: Lark parsing configuration**

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|auto_keywords |Number |Yes |automatic keyword count |
|auto_questions |Number |Yes |number of automated questions |
|strategy |Number |Yes |Slicing strategy |
|chunk_size |Number |Yes |Maximum slice length |
|detect_pdf_table |Boolean |No |Whether to recognize PDF forms |
|detect_pdf_img |Boolean |No |Whether to recognize PDF images |
|page_size_limit |Number |No |page size limit |
|merge_small_chunks |Boolean |No |Whether to merge small slices |
|pdf_with_ocr |Boolean |No |Whether to enable PDF OCR |
|doctree_with_outline |Boolean |No |Whether to output a document tree with an outline |
|custom_splitter |String |No |Custom Splitter |
|to_md |Boolean |No |Whether to convert to Markdown |
|md_collapsed |Boolean |No |Markdown whether to fold |
|tos_bucket_name |String |No |TOS Bucket Name |
|tos_access_key |String |No |TOS access key |
|detect_header |Boolean |No |Excel parsing whether to enable table recognition |
|file_trans_timeout |Number |No |Timeout setting for converting images in pptx/ppt parsing |
|slides_full_page_as_image |Boolean |No |In PPT files, use full\-page images instead of small images<br><br>In PPT files, use full\-page images instead of small images |
|open_access_token |String |No |Lark open API access_token |
|lark_doc_user_id |String |No |Cloud Document/Bitable/Lark Form User ID Required for Inter\-Domain Gateway Authentication |
|chunk_with_vlm |Boolean |No |Whether to use VLM capabilities, including chapter understanding, image understanding, etc |
|expected_level |Number |No |Chapter Expected Maximum Level |
|deduplicate |Boolean |No |Whether to automatically deduplicate |
|spell_check |Boolean |No |Whether to turn on typo detection |
|completeness_check |Boolean |No |Whether to turn on integrity detection |
|sensitive_word_check |Boolean |No |Whether to turn on sensitive word detection |
|enable_llm_tag |Boolean |No |Whether to turn on unstructured marking |
|tableExtraction |Boolean |No |Table extraction switch |
|imageExtraction |Boolean |No |Picture extraction switch |

### **Situation 2: Report analysis configuration**

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|delimiter |String |No |separator |
|deduplicate |Boolean |No |Whether to automatically deduplicate |
|enable_llm_tag |Boolean |No |Whether to turn on unstructured marking |

### **Situation 3:**  Sophon **parsing configuration**

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|imageExtraction |Boolean |No |Picture extraction switch |
|tableExtraction |Boolean |No |Table extraction switch |
|chunkType |String |No |Type of sharding strategy |
|genAtomicQuestion |Boolean |No |Does it generate an atomic problem? |
|maxSegmentLength |Number |No |Sharding maximum number of characters |
|maxToken |Number |No |Deprecated: Compatible with old fields, current local upload interpreted by characters |
|removeSpaces |Boolean |No |whitespace removal |
|removeUrlsPics |Boolean |No |Remove image URL |
|separator |String |No |separator |
|customSeparator |String |No |custom separator |
|mergeSmallChunks |Boolean |No |Whether to merge consecutive small segments |
|smallChunkTokenThreshold |Number |No |Small segmentation threshold, unit token |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|visionPagesPerChunk |Number |No |Number of pages per process in Vision model |
|spell_check |Boolean |No |Whether to turn on typo detection |
|completeness_check |Boolean |No |Whether to turn on integrity detection |
|sensitive_word_check |Boolean |No |Whether to turn on sensitive word detection |
|enable_llm_tag |Boolean |No |Whether to turn on unstructured marking |
|deduplicate |Boolean |No |Whether to automatically deduplicate |

## feishu_config

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|user_id |String |No |Lark User ID |
|name |String |No |Document name |
|doc_type |String |No |document content type |
|source |String |No |document import source |
|url |String |No |Document URL |
|token |String |Yes |Lark document import token |
|sheets |Array |No |Lark table settings, see **sheets** below for details |
|callback_url |String |No |Callback URL after Lark document import is complete |

### sheets

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|sheet_title |String |No |Lark sheet name |
|sheet_id |String |No |Lark sheet ID |

## schedule_config

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|schedule_type |Number |No |Scheduling type: 0\-no update, 1\-regular update |
|frequency |String |No |scheduling frequency |
|time_setting |String |No |time setting |
|day_of_week |Array |No |day of the week |
|day_of_month |Array |No |What day of each month? |
|bdb_task_id |Number |No |Task ID |

## video_parser_config

|**Field name** |**Type** |**Is it required?**  |**Description** |
|---|---|---|---|
|fuse_video_asr |Boolean |No |Whether to use audio & video fusion parsing |
|asr_model |String or Object |No |ASR model, see section **asr_model** above |
|video_model |String or Object |No |Video model, see section **video_model** above |
|fuse_model |String or Object |No |Fusion model, see section **fuse_model** above |

### asr_model

* **Situation 1:**  String type, non\-mandatory, ASR model

* **Situation 2:**  Object type, required, ASR model endpoint

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|host |String |No |service address |
|api_key |String |No |interface key |
|access_token |String |Yes |access token |
|app_id |String |Yes |App ID |
|resourceId |String |Yes |Resource ID |
|endpoint_id |String |No |endpoint ID |
|temperature |Number |No |Sampling temperature |
|top_p |Number |No |Kernel Sampling Probability Top P |
|model_id |Number |No |Model ID |

* **Situation 3:**  Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

### video_model

* **Situation 1:**  String type, non\-mandatory, video model

* **Situation 2:**  Object type, required, model endpoint

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |Yes |model access address |
|model_name |String |Yes |Model name |
|api_key |String |Yes |interface key |

* **Situation 3:**  Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

### fuse_model

* **Situation 1:**  String type, non\-mandatory, video model

* **Situation 2:**  Object type, required, model endpoint

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |Yes |model access address |
|model_name |String |Yes |Model name |
|api_key |String |Yes |interface key |

* **Situation 3:**  Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

# Response parameters

> **说明**

> The interface returns a unified JSON structure. The caller should preferentially judge whether the request is successful according to the `code: code = 0`indicates success, and non\-0 indicates failure.

|**Parameter name** |**Parameter type** |**Parameter description** |
|---|---|---|
|code |Integer |Response code. `0`indicates success and non\- `0`indicates failure. |
|msg |string |Response message. Success is usually `success`, failure returns the cause of the error. |
|data |List |Returns a list of import results on success; `null`on failure. See the **data** table below for details. |

## data

|**Parameter name** |**Parameter type** |**Parameter description** |
|---|---|---|
|data[].id |Integer |File and document association record ID. |
|data[].file_id |Integer |The source file ID for this import. |
|data[].document_id |Integer |The document ID generated after the import. This ID can be used for subsequent queries, management, or re\-segmentation. |
|data[].running_state |String |Parse the running state of the task, which can be empty. This field is used to display the status of asynchronous processing, and the actual document status query result shall prevail if it is not returned. |

# Request example

```JSON
{
  "kb_ids": [123],
  "file_parse_type_overrides": [
    {
      "match": {
        "file_ids": [1001]
      },
      "parse_type": "text"
    },
    {
      "match": {
        "file_ids": [1002]
      },
      "parse_type": "ppt"
    },
    {
      "match": {
        "file_ids": [1004]
      },
      "parse_type": "table"
    }
  ],
  "chunk_settings": {
    "text": {
      "mode": "custom",
      "max_segment_length": 1200,
      "custom_separator": "\\n---\\n",
      "associate_chunk_title": true,
      "merge_small_chunks": true,
      "small_chunk_token_threshold": 128,
      "extract_images": true,
      "image_understand": true,
      "image_understand_max_tokens": 1024,
      "extract_tables": true
    },
    "ppt": {
      "max_segment_length": 800,
      "exclude_master_content": true,
      "exclude_header_footer": true
    },
    "table": {
      "mode": "auto",
      "parse_strategy": "model_auto_header",
      "file_overrides": [
        {
          "match": {
            "file_id": 1004
          },
          "mode": "custom",
          "sheets": [
            {
              "sheet_name": "汇总", //in total
              "header_row": 2,
              "data_start_row": 3,
              "columns": [
                {
                  "source_name": "城市", //city
                  "target_name": "city",
                  "enabled": true,
                  "data_type": "STRING",
                  "description": "城市列" //city column
                },
                {
                  "source_name": "金额", //amount
                  "target_name": "amount",
                  "enabled": true,
                  "data_type": "DOUBLE",
                  "description": "金额列"
                }
              ]
            }
          ]
        }
      ]
    }
  },
  "quality_settings": {
    "text": {
      "completeness_check": true,
      "sensitive_word_check": false,
      "duplicate_doc_check": true
    },
    "ppt": {
      "completeness_check": false,
      "sensitive_word_check": true,
      "duplicate_doc_check": false
    }
  }
}
```

# Response example

## Successful response example

```JSON
{
  "code": 0,
  "msg": "success",
  "data": [
    {
      "id": 9001,
      "file_id": 1001,
      "document_id": 2001,
      "running_state": null
    }
  ]
}
```

## Failure response example

```JSON
{
  "code": 500,
  "msg": "kb_ids can not be null",
  "data": null
}
```

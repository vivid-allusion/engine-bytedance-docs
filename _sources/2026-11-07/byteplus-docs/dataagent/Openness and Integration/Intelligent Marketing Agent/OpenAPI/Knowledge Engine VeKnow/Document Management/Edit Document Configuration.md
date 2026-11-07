---
title: "Edit Document Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/edit-document-configuration"
---

Call this interface to edit the specific document parsing configuration in the knowledge base, and submit subsequent execution tasks. After calling the current interface, the relevant task is only submitted and has not been officially executed, and must continue to call [Start Parsing the Document](https://docs.byteplus.com/docs/dataagent/start-parsing-the-document) before it will actually start execution.

# Interface description

* Interface name: change_parser_document_change_parser_post

* Interface address:/document/change_parser

* Request method: POST

# Request parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|doc_id |Number or Array < Number \> |Yes |Document ID, supports passing in a single ID, and also supports passing in multiple IDs in digital form |
|parser_id |String |Yes |New parser ID |
|source_type |String |No |parsing model source type |
|config |Object |No |Parsing configuration, supports a variety of, including: Lark parsing configuration, report parsing configuration, Sophon parsing configuration, see the following **config** section for details |
|chunk_settings |Object |No |Unified slice configuration, see **chunk_settings** table below |
|file_parse_type_overrides |Array |No |List of document parsing types, see **file_parse_type_overrides** table below |
|quality_settings |Object |No |Unified quality inspection configuration, see **quality_settings** table below |
|labels |Array |No |List of document labels, see the **labels** table below |
|template_id |String |No |Parser template ID that will overwrite parser_config |
|video_parser_config |Object |No |Video analysis configuration, see the **video_parser_config** table below for details |

## config

### Situation 1: Lark parsing configuration

|Parameter name |Type |Is it necessary to pass on? |Description |
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
|slides_full_page_as_image |Boolean |No |In PPT files, use full\-page images instead of small images |
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

### Situation 2: Report analysis configuration

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|delimiter |String |No |separator |
|deduplicate |Boolean |No |Whether to automatically deduplicate |
|enable_llm_tag |Boolean |No |Whether to turn on unstructured marking |

### Situation 3: Sophon parsing configuration

|Parameter name |Type |Is it necessary to pass on? |Description |
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

## chunk_settings

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|text |Object |No |Text document type slice configuration, see the **test/other/pdf** table below for details |
|other |Object |No |For additional document type slice configurations, see the **test/other/pdf** table below |
|pdf |Object |No |PDF document type slice configuration, see the **test/other/pdf** table below for details |
|ppt |Object |No |PPT type slice configuration, see the **ppt** table below for details |
|image |Object |No |Image type slice configuration, see the **image** table below for details |
|table |Object |No |Table type slice configuration, see **table** below for details |
|audio |Object |No |Audio type slice configuration, see the **audio** table below for details |
|video |Object |No |Video type slice configuration, see the **video** table below for details |

## test/other/pdf

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |Slicing mode:<br><br><br>* default<br><br>* auto<br><br>* custom<br><br>* model_summary<br><br>* context_aware |
|max_segment_length |Number |No |maximum number of segmented characters |
|custom_separator |String |No |custom separator |
|associate_chunk_title |Boolean |No |Whether to associate a title when customizing a segment |
|merge_small_chunks |Boolean |No |Whether to automatically merge consecutive small segments when customizing segments |
|small_chunk_token_threshold |Number |No |Small segmentation threshold, unit token |
|extract_images |Boolean |No |Whether to extract the picture, it is turned on by default. |
|image_understand |Boolean |No |Whether to enable image VLM post\-processing after OCR does not affect the main parsing pipeline |
|image_understand_max_tokens |Number |No |Image depth understanding of the largest tokens |
|image_ocr |Boolean |No |Has the picture been OCR? |
|extract_tables |Boolean |No |Whether to extract the form |
|exclude_header_footer |Boolean |No |Whether to filter headers and footers |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|visionPagesPerChunk |Number |No |Number of pages per process in vision model mode |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** table below |

### file_overrides

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |Slicing mode:<br><br><br>* default<br><br>* auto<br><br>* custom<br><br>* model_summary<br><br>* context_aware |
|max_segment_length |Number |No |maximum number of segmented characters |
|custom_separator |String |No |custom separator |
|associate_chunk_title |Boolean |No |Whether to associate a title when customizing a segment |
|merge_small_chunks |Boolean |No |Whether to automatically merge consecutive small segments when customizing segments |
|small_chunk_token_threshold |Number |No |Small segmentation threshold, unit token |
|extract_images |Boolean |No |Whether to extract the picture, it is turned on by default. |
|image_understand |Boolean |No |Whether to enable image VLM post\-processing after OCR does not affect the main parsing pipeline |
|image_understand_max_tokens |Number |No |Image depth understanding of the largest tokens |
|image_ocr |Boolean |No |Has the picture been OCR? |
|extract_tables |Boolean |No |Whether to extract the form |
|exclude_header_footer |Boolean |No |Whether to filter headers and footers |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|visionPagesPerChunk |Number |No |Number of pages per process in vision model mode |
|match |Object |No |Slicing configuration matching conditions, see the **match** table below for details |
|file_id |Number |No |Deprecated: Please use file_id |

### match

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|file_id |Number |No |local file ID |
|file_ids |Array |No |List of local file IDs |
|source_key |String |No |Object storage source file key |
|source_keys |Array |No |Object storage source file key list |

## ppt

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |PPT only supports default segmentation |
|max_segment_length |Number |No |maximum number of segmented characters |
|exclude_master_content |Boolean |No |Whether to filter PPT master noise |
|exclude_header_footer |Boolean |No |Whether to filter headers and footers |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** table below |

### **file_overrides**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |PPT only supports default segmentation |
|max_segment_length |Number |No |maximum number of segmented characters |
|exclude_master_content |Boolean |No |Whether to filter PPT master noise |
|exclude_header_footer |Boolean |No |Whether to filter headers and footers |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |
|file_id |Number |No |Deprecated: Please use file_id |

## image

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |The picture only supports default segmentation and is compatible with auto.<br><br><br>* default<br><br>* auto |
|max_segment_length |Number |No |maximum number of segmented characters |
|image_understand |Boolean |No |Whether to enable image VLM post\-processing after OCR does not affect the main parsing pipeline |
|image_understand_max_tokens |Number |No |Image depth understanding of the largest tokens |
|image_ocr |Boolean |No |Has the picture been OCR? |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** table below |

### **file_overrides**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |The picture only supports default segmentation and is compatible with auto.<br><br><br>* default<br><br>* auto |
|max_segment_length |Number |No |maximum number of segmented characters |
|image_understand |Boolean |No |Whether to enable image VLM post\-processing after OCR does not affect the main parsing pipeline |
|image_understand_max_tokens |Number |No |Image depth understanding of the largest tokens |
|image_ocr |Boolean |No |Has the picture been OCR? |
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |
|file_id |Number |No |Deprecated: Please use file_id |

## table

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |Table slicing mode:<br><br><br>* auto<br><br>* custom |
|max_segment_length |Number |No |maximum number of segmented characters |
|parse_strategy |String |No |Automatic table parsing strategy:<br><br><br>* model_auto_header<br><br>* rule |
|header_row |Number |No |The row of the table header under the rule configuration, 1 starts counting |
|data_start_row |Number |No |The starting line of data under the rule configuration, 1 starts counting |
|sheets |Array |No |Excel multi\-sheet configuration under custom segmentation, see **sheets** below |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** table below |

### **sheets**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|sheet_name |String |No |Sheet name |
|sheet_id |String |No |Sheet ID |
|header_row |Number |No |Header row, 1 starts counting |
|data_start_row |Number |No |Data start row, 1 starts counting |
|columns |Array |No |The column configuration of the current sheet, see the **columns** table below for details |

### columns

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|source_name |String |No |original listing |
|target_name |String |No |Imported column names |
|enabled |Boolean |No |Whether to enable the column to participate in the recall |
|data_type |String |No |Table column data type:<br><br><br>* STRING<br><br>* INT<br><br>* DOUBLE<br><br>* DATE<br><br>* DATETIME<br><br>* ARRAY<br><br>* LINK |
|description |String |No |column description |

### **file_overrides**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|mode |String |No |Table slicing mode:<br><br><br>* auto<br><br>* custom |
|max_segment_length |Number |No |maximum number of segmented characters |
|parse_strategy |String |No |Automatic table parsing strategy:<br><br><br>* model_auto_header<br><br>* rule |
|header_row |Number |No |The row of the table header under the rule configuration, 1 starts counting |
|data_start_row |Number |No |The starting line of data under the rule configuration, 1 starts counting |
|sheets |Array |No |Excel multi\-sheet configuration under custom segmentation, see **sheets** table above for details |
|pipelineTypeEnum |String |No |Parsing methods, such as VISION_MODEL |
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |
|file_id |Number |No |Deprecated: Please use file_id |

## audio

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|asr_model |String or Object |No |ASR model, see **asr_model** section below |
|mode |String |No |Audio only supports default resolution mode |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** section below |

### asr_model

* **Situation 1** : String type, non\-mandatory, ASR model

* **Situation 2** : Object type, required, ASR model endpoint

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

* **Situation 3** : Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

### **file_overrides**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|asr_model |String or Object |No |ASR model, see section **asr_model** above |
|mode |String |No |Audio only supports default resolution mode |
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |
|file_id |Number |No |Deprecated: Please use file_id |

## video

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|fuse_video_asr |Boolean |No |Whether to use audio & video fusion parsing |
|asr_model |String or Object |No |ASR model, see section **asr_model** above |
|video_model |String or Object |No |Video model, see **video_model** section below |
|fuse_model |String or Object |No |Fusion model, see **fuse_model** section below |
|mode |String |No |Video only supports default resolution mode |
|file_overrides |Array |No |Override slice configurations according to matching conditions for the current type, see **file_overrides** section below |

### video_model

* **Situation 1** : String type, non\-mandatory, video model

* **Situation 2** : Object type, required, model endpoint

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |Yes |model access address |
|model_name |String |Yes |Model name |
|api_key |String |Yes |interface key |

* **Situation 3** : Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

### fuse_model

* **Situation 1** : String type, non\-mandatory, video model

* **Situation 2** : Object type, required, model endpoint

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|url |String |Yes |model access address |
|model_name |String |Yes |Model name |
|api_key |String |Yes |interface key |

* **Situation 3** : Object type, required, model index

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|operator_key |String |Yes |operator identifier |
|model_id |Number |Yes |Model ID |

### **file_overrides**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|fuse_video_asr |Boolean |No |Whether to use audio & video fusion parsing |
|asr_model |String or Object |No |ASR model, see section **asr_model** above |
|video_model |String or Object |No |Video model, see section **video_model** above |
|fuse_model |String or Object |No |Fusion model, see section **fuse_model** above |
|mode |String |No |Video only supports default resolution mode |
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |
|file_id |Number |No |Deprecated: Please use file_id |

## file_parse_type_overrides

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|match |Object |No |Slicing configuration matching conditions, see the **match** table above for details |

## quality_settings

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|text |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|other |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|pdf |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|ppt |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|image |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|table |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|audio |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |
|video |Object |No |Quality inspection configuration, please refer to the following **quality inspection configuration parameter** table for details |

### Quality inspection configuration parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|spell_check |Boolean |No |Whether to turn on typo detection |
|completeness_check |Boolean |No |Whether to turn on integrity detection |
|sensitive_word_check |Boolean |No |Whether to turn on sensitive word detection |
|duplicate_doc_check |Boolean |No |Whether to enable duplicate document detection |

## labels

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|label_name |String |Yes |label name |
|label_type |String |Yes |Document label type:<br><br><br>* multiple_value_text<br><br>* single_value_text |
|label_value |Array |Yes |list of label values |

## **video_parser_config**

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|fuse_video_asr |Boolean |No |Whether to use audio & video fusion parsing |
|asr_model |String or Object |No |ASR model, see table **asr_model** above for details |
|video_model |String or Object |No |Video model, see table **video_model** above for details |
|fuse_model |String or Object |No |Fusion model, see table **fuse_model** above for details |

# Response parameters

|Parameter name |Type |Is it necessary to pass on? |Description |
|---|---|---|---|
|code |Number |Yes |Response code: 0 = success, non\-0 = failure |
|msg |String |No |Code is not 0, error message is returned |
|message |String |No |error message |
|data |Boolea |No |Edit successfully returns true |

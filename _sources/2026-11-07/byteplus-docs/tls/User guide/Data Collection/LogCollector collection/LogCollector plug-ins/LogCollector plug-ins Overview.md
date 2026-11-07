---
title: "LogCollector plug-ins Overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/plug-ins_Overview"
---

If complex and unstructured business logs cannot be parsed using common log collection modes like JSON, you can use LogCollector plug\-ins to process the collected logs.

<span id="功能概述"></span>
## Feature overview

LogCollector offers various text log collection modes including the delimiter\-based mode, JSON mode, and full regex\-based mode. In addition, LogCollector supports multiple advanced configurations such as log filtering. This way, it can meet the requirements for log collection and processing in most typical scenarios. Assume that you are in specific complex scenarios such as in scenarios where business log structures are complex, logs contain both JSON data and delimiters, or log fields are not fixed. In this case, you cannot use a single mode for uniform parsing and processing but you can use a LogCollector plug\-in to process the log data after collection.

When you configure the LogCollector collection rules for text logs, simply enable the plug\-in feature, then specify the plug\-in configurations for processing the logs in order. When processing the collected log data, Torch Log Service (TLS) executes the corresponding processing logic in order based on the plug\-in configurations. For more information, refer to [Use LogCollector plug-ins to process logs](https://docs.byteplus.com/docs/tls/Use_LogCollector_plug-ins_to_process_logs).

The LogCollector plug\-in module offers a variety of plug\-ins. Along with the data collection feature of the LogCollector collection module, the post\-collection processing capabilities of TLS in complex log scenarios are enhanced. For more information on a list of supported plug\-ins, refer to [List of plug-ins](https://docs.byteplus.com/docs/tls/plug-ins_Overview#%E6%8F%92%E4%BB%B6%E5%88%97%E8%A1%A8). To determine whether to execute a specific plug\-in based on the log content, you can add plug\-in conditions in the plug\-in configuration. For example, you can specify that TLS verifies whether a field value is equal to a specified value or contains a specified string. For more information on a list of supported execution conditions, refer to [List of execution conditions](https://docs.byteplus.com/docs/tls/Set_plug-in_execution_conditions#%E6%89%A7%E8%A1%8C%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8).

<span id="注意事项"></span>
## Precautions


* After you enable your plug\-in configuration, you can add one or more LogCollector plug\-ins, and LogCollector executes these plug\-ins in the defined order. If one of the LogCollector plug\-ins fails to be executed, the entire procedure for processing LogCollector plug\-ins fails.

* After the plug\-in configuration is enabled, the existing advanced features remain valid. The advanced features including those to configure filters, use collection time, upload logs that fails to be parsed, parse collection paths, upload original logs, upload constant fields, and set extended configurations.

* LogCollector plug\-ins are designed to parse the content within a specific field. When you use the single\-line full\-text mode or multi\-line full\-text mode, the field name corresponding to the collected logs is `__content__`. Therefore, in your LogCollector plug\-in configuration, set the first field name to `__content__`.

* Processing container metadata fields through plug\-ins is not supported.

* The LogCollector plug\-in feature is continuously updated. We recommend that you use the latest version of LogCollector to experience the complete feature.


<span id="插件列表"></span>
## List of plug\-ins


|Category |LogCollector Plug\-in |Description |
|---|---|---|
|Field extraction |[delimiter plug-in](https://docs.byteplus.com/docs/tls/Field_extractor#delimiter-%E6%8F%92%E4%BB%B6) |Specifies that LogCollector extracts fields in delimiter\-based mode. |
||[fullregex plug-in](https://docs.byteplus.com/docs/tls/Field_extractor#fullregex-%E6%8F%92%E4%BB%B6) |Specifies that LogCollector extracts fields in full regex\-based mode. |
||[kv plug-in](https://docs.byteplus.com/docs/tls/Field_extractor#kv-%E6%8F%92%E4%BB%B6) |Specifies that LogCollector extracts fields in key\-value pair mode. |
|Field addition |[Field adder](https://docs.byteplus.com/docs/tls/Field_adder) |Specifies that LogCollector adds specific fields. |
|JSON parsing |[JSON parser](https://docs.byteplus.com/docs/tls/JSON_parser) |Specifies that LogCollector parses and expands fields in JSON mode. |
|Data masking |[Data masking](https://docs.byteplus.com/docs/tls/data_masking) |Replaces specific log content with its corresponding MD5 value to mask data. |
|String replacement |[String replace plug-in](https://docs.byteplus.com/docs/tls/String_replace_plug-in) |Replaces specific log content with a specific string. |
|Time format |[time resolution plugin](https://docs.byteplus.com/docs/undefined/66558b3534740002fdfed306) |Parses the time content in the original log. |
|Rename |[Rename plugin](https://docs.byteplus.com/docs/tls/Rename-plugin) |Renames field names. |
|Filter logs |[Filter log plugin](https://docs.byteplus.com/docs/tls/Filter-log-plugin) |Supports matching log field names with regular expressions to filter out logs that do not meet the criteria. |

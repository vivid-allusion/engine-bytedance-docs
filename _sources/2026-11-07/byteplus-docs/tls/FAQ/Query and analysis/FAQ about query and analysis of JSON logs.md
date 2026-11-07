---
title: "FAQ about query and analysis of JSON logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/FAQ-about-the-query-and-analysis-of-JSON-logs"
---

<span id="c7306606"></span>
## How to configure an index?

When configuring indexes for JSON logs, you can refer to the following configuration approach and examples.

<span id="4450af76"></span>
### Options of index types

TLS provides two types of index configurations: Full\-text index and Key\-value index. Refer to the following notes to select the appropriate index type. For more information, see [Configuration Index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="tip">If you configure both full\-text and key\-value indexes, the key\-value index configuration will take precedence for fields set with key\-value indexing.</div>



* Full\-text index: If you need to query all fields in the logs, create a full\-text index.

* Key\-value index: If you only need to query specific fields, create a Key\-value index for those fields to reduce indexing costs.

   If you need SQL analysis on a field, you must create a key\-value index for the target field and enable the statistics feature. For example, if you only analyze the status and method fields, you only need to configure key\-value indexes for these two fields and enable the statistics feature.


<span id="384d2f79"></span>
### Options of data types for indexed fields

The data types supported for indexed fields in TLS include text, long, double, and JSON. For more information, see [Index data types](https://docs.byteplus.com/docs/tls/Index-data-types-2).

When selecting the appropriate data type for the target field, you can refer to the following guidelines:


* Non\-standard JSON format: If the field value contains JSON\-like content but is not in standard JSON format, we recommend that you set it as text type.

* Standard JSON format: If the field value is in standard JSON format, we recommend that you set it as JSON type. When set to JSON type, TLS will automatically expand the JSON content.

   * When set to JSON type, TLS supports parsing valid parts of content that is not fully compliant with the JSON format.

   * After setting the type to JSON, you can further analyze subfields within a JSON object by creating separate indexes for each subfield. Index data types can be text, long, or double. After configuration, query and analysis can be precise to the subfield level. Query and analysis speed for subfields is improved. But additional index fees will generate.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Notice      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">TLS supports indexing subfields within JSON objects, but it is not recommended to index subfields that contain subfields themselves. If you index a nested JSON object within a JSON object, TLS will serialize the JSON value of the subfield as a string.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">TLS does not support indexing fields with JSON array values, nor does it support indexing fields within a JSON array.      </div>
      


<span id="e640b80e"></span>
### Configuration examples


* Log example

   `The logging` field and `process_info` field are both of JSON type.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ce3fb4b3427476a903c977dbb3c1086~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis requirements

   * Count log entries by each log level using `logging.level` field.

   * Count the number of logs output per minute using the `process_info.delivered` field.

   * Count the number of failed log entries for each processing task within a specified time range using `task_id` and `process_info.failed` fields.

* Index configuration instructions

   
   |Field |Description |
   |---|---|
   |`logging` |* `The logging` field uses JSON format. Set the index data type to JSON and enable statistics.<br><br>* `"logging.level"` refers to the log level. Set the index data type to text and enable statistics.<br><br>* `"logging.message"` is rarely queried. Therefore, separate index is not required. When analysis is needed, use JSON\-related functions. For details on JSON functions, see [JSON functions](https://docs.byteplus.com/docs/tls/JSON-functions). |
   |`process_info` |* `The process_info` field uses JSON format. Set the index data type to JSON and enable statistics.<br><br>* `"process_info.faild"` refers to the number of failed logs output during the processing task. Set the index data type to long and enable statistics.<br><br>* `"process_info.delivered"` refers to the output count during the processing task. Set the index data type to long and enable statistics. |
   |`task_id` |`The task_id` field refers to the processing task ID. Set its index data type to text and enable statistics. |
   

* Index configuration example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4630528562cb458f85025c12de11b3d4~tplv-goo7wpa0wc-image.image) </span>


<span id="2b26c0e3"></span>
## What is the difference between automatic JSON indexing and manual index configuration?

After enabling statistics for a parent JSON field, you can configure the following scenarios as needed:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d1c88d2536347608133eb216f67bc1c~tplv-goo7wpa0wc-image.image) </span>


|Subfield configuration |Enable only **Automatic Indexing** |Enable only **Automatic Index Statistics** |All disabled |
|---|---|---|---|
|Secondary field added |JSON parent fields do not support key\-value indexing or statistics, and therefore do not support query or SQL analysis. |||
||Secondary fields configured manually support indexing and statistics. This means these fields support query and SQL analysis. |||
||Subfields that are automatically indexed by the system:<br><br><br>* Supports key\-value index, i.e., supports query.<br><br>* **No statistics feature**, i.e., SQL analysis is not supported. |Subfields that are automatically indexed by the system:<br><br><br>* Supports key\-value index, i.e., supports query.<br><br>* **Supports statistics feature**, i.e., supports SQL analysis. |Subfields without automatic indexing. |
|Scenarios where no secondary fields added. |JSON parent field does not have a key\-value index but supports statistics. This means JSON parent field supports SQL analysis but does not support query. ||JSON parent field has both key\-value index and statistics. This means the JSON parent field supports both query and SQL analysis. |
||Subfields that are automatically indexed by the system:<br><br><br>* Supports key\-value index, i.e., supports query.<br><br>* **No statistics feature**, i.e., SQL analysis is not supported. |Subfields that are automatically indexed by the system:<br><br><br>* Supports key\-value index, i.e., supports query.<br><br>* **Supports statistics feature**, i.e., supports SQL analysis. |Subfields without automatic indexing. |

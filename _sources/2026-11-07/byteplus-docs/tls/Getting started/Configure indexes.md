---
title: "Configure indexes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/getting_started_configure_indexes"
---

Torch Log Service (TLS) allows you to query and analyze logs. Configure indexes before you query and analyze logs. When you configure indexes, specify the index type and the data type of each field. The index configurations determine the query method and the accuracy of results. This topic introduces how to configure indexes and offers a detailed explanation of index configurations.

<span id="c552ac9d"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources).

* We recommend that you collect log data through LogCollector or other methods before configuring indexes. For more information, refer to [Data collection overview](https://docs.byteplus.com/docs/tls/data_collection_overview).


<span id="fad4a1aa"></span>
## Precautions


|Category |Precautions |
|---|---|
|Enable indexing |You must enable at least one of the following: full\-text indexing and key\-value indexing. Logs collected when indexing is disabled cannot be queried. |
|Tokenization |In TLS, a 32,766\-character limit exists for words. When the full text or words are too long, the log may be discarded if no delimiter is set. |
|Full\-text indexing |* After enabling full\-text indexing, TLS will split the log into multiple text\-type words based on the delimiters. You can enter keywords for full\-text search or perform key\-value searches for specific fields.<br><br>   For example, you can use the statement `error or warning` to search for logs containing the keywords `error` or `warning`, or use the statement `level:error` to search for logs with the error level.<br><br>* When only full\-text indexing is enabled, you can only use search syntax for log retrieval. |
|Key\-value indexing |* After enabling key\-value indexing, TLS will first split the log based on field names, and then split the field values within each field based on delimiters.<br><br>* You can use the target field in analysis statements only after configuring key\-value indexing for the field and enabling the statistics function.<br><br>* To use key\-value search, enable key\-value indexing for relevant fields. After indexing is enabled, TLS sets indexes for certain reserved fields by default. For more information, refer to [Reserved fields](https://docs.byteplus.com/docs/tls/Reserved-fields-2).<br><br>* Indexes cannot be configured for fields starting with `__`, except for those in the format of `__tag__xxx__`. For example, indexes can be configured for `__tag__data_source__`, but cannot be configured for `__name__`.<br><br>* When configuring key\-value indexes, up to 100 log fields can be added. |
|Modifying indexes |You can modify indexes at any time. After you modify indexes:<br><br><br>* The modifications only apply to log data collected after the modification. The indexes of old data remain unchanged.<br><br>* In log queries, old data still follows old index rules, but key\-value search is no longer supported if the key\-value index is removed.<br><br>* In log analysis, only log data collected after the modification are included. |
|Index traffic |* Full\-Text Indexing<br><br>   Both field names and field values are stored as text types, and both will generate index traffic.<br><br>* Key\-Value Indexing<br><br>   * Text Type: Both field names and field values will generate index traffic.<br><br>   * Numeric Type: Field names of long and double types will not generate index traffic, and each field value will occupy 8 bytes of index traffic.<br><br>   * JSON Type: Both field names and field values (including subfields) will generate index traffic.<br><br>      * If no index is created for JSON subfields, the subfield is considered the value of the JSON type field, and TLS will calculate index traffic as a text type.<br><br>      * If an index is created for JSON subfields, TLS will calculate index traffic based on the data type of the subfield (text, long, double). |


<span id="9f60f7b2"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common Functions** \> **Query & Analysis**.

3. Select the topic for which you want to configure indexes, and click **Index configuration**.

4. Toggle the **enable index** switch, then select an index type as needed.

   TLS supports the following index types. For more information on configuration methods, refer to:

   * [Configure full-text indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes#1db996e0)

   * [Configure key-value indexes](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes#e3e54d2b)

   * [Configure indexes for reserved fields](https://docs.byteplus.com/docs/tls/getting_started_configure_indexes#9f7199fa)

5. Click **OK**.

   Index configurations are expected to take effect within 1 minute. Refresh the page later to view real\-time logs or query and analyze logs.


<span id="1db996e0"></span>
### Configure full\-text indexes

On the index configuration page, enable **Full\-text index**, then configure the following settings.


|Parameter |Description |
|---|---|
|Case sensitive |Specify whether to enable case\-sensitivity in log queries.<br><br><br>* Enabled: Queries are case\-sensitive. For example, logs containing `error` can only be found using `error` as the keyword, and cannot be found when you use `ERROR`.<br><br>* Disabled: Queries are case\-insensitive. For example, logs containing `error` can be found using either `error` or `ERROR`. |
|Contains Chinese |Specify whether to distinguish between Chinese and English characters in log queries.<br><br><br>* Enabled: If logs contain Chinese characters, tokenization is applied based on common Chinese syntax. In this case, you cannot set a custom delimiter.<br><br>* Disabled: The tokenization method depends on the setting of **Delimiter**: no tokenization or tokenization based on the specified delimiter.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Even with <strong>Contains Chinese</strong> disabled, you can still search for Chinese characters in logs, but the search keywords must exactly match the Chinese field.</div><br> |
|Delimiter |Specify whether to split log content based on a specified delimiter.<br><br><br>* Enabled: Split log content based on the specified delimiter, supporting queries based on the split log content. The default delimiters are `, '"=()[]{}?@&<>/:\n\t\r`, and the delimiters supported by TLS include uppercase and lowercase letters, digits, and the following symbols `!@#%^&*()-_=\\\"', <>/?\|;:\n\t\r[]{}.`.<br><br>* Disabled: Tokenization is not applied. Each log entry is to be queried as a whole. |


<span id="e3e54d2b"></span>
### Configure key\-value indexes

On the index configuration page, enable **Key\-value index**, then configure the following settings.

After key\-value indexing is enabled, TLS automatically suggests index configurations based on the collected log data. You can modify these suggestions, or delete the configurations and click **Add** to set indexes.

When TLS automatically configures key\-value indexes, the first log entry in the preview data is used by default.


* Click **Add** to retain existing index attributes and update the configurations of fields with the same key.

* Click **Cover** to replace existing index attributes.



|Parameter ||Description |
|---|---|---|
|Field name ||Specify the name of the log field, that is, the key in the key\-value pair.<br><br>When configuring key\-value indexes, up to 100 log fields can be added. |
|Field type ||Specify the data type of the log field. The data type affects the accuracy and precision of log query and analysis results. For more information, refer to [Index data types](https://docs.byteplus.com/docs/tls/Index-data-types-2).<br><br>Supported data types include text, long, double, and json. |
|Enable analytics ||Specify whether to enable the statistics feature.<br><br><br>* Enabled: The field is included in statistical analysis.<br><br>* Disabled: The field is excluded from statistical analysis. |
|Field configuration |Case sensitive |Specify whether to enable case\-sensitivity when you query and analyze logs based on the field.<br><br><br>* Enabled: Queries are case\-sensitive. For example, logs containing `error` can only be found using `error` as the keyword, and cannot be found when you use `ERROR`.<br><br>* Disabled: Queries are case\-insensitive. For example, logs containing `error` can be found using either `error` or `ERROR`. |
||Contains Chinese |Specify whether to distinguish between Chinese and English characters when you query logs based on the field.<br><br><br>* Enabled: If logs contain Chinese characters, tokenization is applied based on common Chinese syntax. In this case, you cannot set a custom delimiter.<br><br>* Disabled: The tokenization method depends on the setting of **Delimiter**: no tokenization or tokenization based on the specified delimiter. |
||Delimiter |Specify whether to split log content based on a specified delimiter when you query logs based on the field.<br><br><br>* Enabled: Split log content based on the specified delimiter, supporting queries based on the split log content. The default delimiters are `, '"=()[]{}?@&<>/:\n\t\r`, and the delimiters supported by TLS include uppercase and lowercase letters, digits, and the following symbols `!@#%^&*()-_=\\\"', <>/?\|;:\n\t\r[]{}.`.<br><br>* Disabled: Tokenization is not applied. Each log entry is to be queried as a whole. |


<span id="9f7199fa"></span>
### Configure indexes for reserved fields

When log data is written to TLS, TLS automatically adds some metadata fields for each log entry to record information such as the log source and timestamp. These metadata fields are referred to as reserved fields. After indexing is enabled, TLS automatically enables key\-value indexing and the statistics feature for some reserved fields such as `__time__`. For more information on the default index configurations of reserved fields, refer to [Reserved fields](https://docs.byteplus.com/docs/tls/Reserved-fields-2).

For fields without default index configurations, such as `__content__`, you can use **Reserved field index** to manually configure indexes. On the index configuration page, enable **Reserved field index**, then configure the related settings.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only the <code>__content__</code> field supports setting reserved field indexes. If the <code>__content__</code> field is set to the json type, the <strong>Automatic indexing of all text fields in Json</strong> function can be enabled.</div>


* <div data-tips="true" data-tips-type="tip">Support enabling both full\-text indexes and the reserved field <code>__content__</code> index simultaneously. When both are enabled, the index traffic costs and index storage costs will be doubled.</div>

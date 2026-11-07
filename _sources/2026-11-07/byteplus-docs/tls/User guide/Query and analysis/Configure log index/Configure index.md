---
title: "Configure index"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Configure-indexes-2"
---

The log service supports log query and analysis functions. You must configure the index before performing log query and analysis operations. When configuring the index, specify the index type and the data type of each field. The index configuration determines the query method and the precision of the query results.

This article explains the operation steps for configuring the index and provides detailed descriptions of the index configuration.

<span id="4b2b8e13"></span>
## Prerequisites


* The project and the log topic have been created. For details, refer to [project](https://docs.byteplus.com/docs/tls/Managing_projects) and [log topic](https://docs.byteplus.com/docs/tls/Managing_topics).

* It is recommended to collect log data through LogCollector or other methods before configuring the index. For details, refer to [collect log data](https://docs.byteplus.com/docs/tls/getting_started_collecte_logs).


<span id="c25c009b"></span>
## Notes


|Category |Note |
|---|---|
|Enable index |At least one of full\-text index or key\-value index must be enabled. Logs collected while the index is disabled cannot be queried. |
|tokenization |The log service word has a 32,766\-character limit. Logs with long texts or words may be discarded if delimiters are not set for full text or single words. |
|Full\-text index |* Full\-text index must be enabled before performing full\-text search.<br><br>* When only the full\-text index is enabled, you can only use [search syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2) for log queries. |
|key\-value index |* Enable key\-value indexing for the target field before performing key\-value queries.<br><br>* You can use the field in query and analysis statements only after configuring key\-value indexing for the target field and enabling statistics.<br><br>* You can add up to 500 log fields when configuring key\-value indexing. |
|Modify index |After configuring the index, you can modify it at any time. After modification:<br><br><br>* The new index only applies to new data collected after the modification; the index of existing old data will not be updated.<br><br>* When querying logs, old data still follows the old index rules, but if the key\-value index is deleted, key\-value queries will no longer be supported.<br><br>* When analyzing logs, old data is excluded from analysis; only logs collected after the index modification are analyzed. |


<span id="39cba86a"></span>
## index type


|index type |Description |
|---|---|
|Full text indexing |After enabling full\-text indexing, the log service splits the entire log into multiple text\-type tokens based on delimiters, allowing you to search the full text by keywords. For example, use `error or warning` to search logs containing the keywords `error` or `warning`. |
|Key\-value index |After enabling key\-value indexing for the target field, the log service first splits the log by field name (key), then splits each field’s value (value) by delimiters. Key\-value indexing supports setting data types as text, long, double, and json. For details, refer to [index data types](https://docs.byteplus.com/docs/tls/Index-data-types-2).<br><br>After creating a key\-value index, you can specify the field name and value (`Key:Value`) to search logs. |
|Reserved field index |When writing log data to Log Service, it automatically adds some metadata fields to each log to record the log source, timestamp, and other information. These fields are collectively called reserved fields in Log Service. After enabling the index function, Log Service defaults to turning on key\-value indexing and statistics for some reserved fields, such as `__time__`. For the default index configuration of reserved fields, see [reserved fields](https://docs.byteplus.com/docs/tls/Reserved-fields-2).<br><br>For fields without preset indexes, such as the `__content__` field, you can manually set indexes through **reserved field indexing**. |


<span id="89d37eca"></span>
## create index


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **common features** \> **query and analysis**.

4. On the left list of the **query and analysis** page, select the specified project and log topic.

5. On the query and analysis page for the specified log topic, click **index configuration**.

6. Enable **indexing** and select the index type as needed.

   Log Service supports the following types of index configurations. For detailed configuration methods, please refer to:

   * [full-text index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#940ba1a3)

   * [key-value index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#52f4e302)

   * [reserved field index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#1af9bb04)

7. Click **OK**.

   The index configuration is expected to take effect within 1 minute. Refresh the page later to view real\-time logs or query and analyze logs.


<span id="bf762c56"></span>
### full\-text index configuration

On the index configuration page, enable **full\-text index** and fill in the following settings.


|Configuration |Description |
|---|---|
|case sensitive |When searching, determine whether to distinguish case for English letters.<br><br><br>* Enabled: search distinguishes case. For example, when searching logs containing `error`, only the `error` keyword can be used; searching with `ERROR` will not find these logs.<br><br>* Disabled: search ignores case. For example, when searching logs containing `error`, using `error` or `ERROR` can both find these logs. |
|Contains Chinese |When searching, determine whether to tokenize Chinese log content according to Chinese grammar.<br><br><br>* Enable:<br><br>   * Chinese characters in logs: segment logs based on common Chinese grammar; custom Chinese segmentation is not supported.<br><br>   * Non\-Chinese characters in logs: segment logs according to the delimiter specified in the **delimiter** parameter.<br><br>* Disable: segment logs according to the delimiter specified in the **delimiter** parameter.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Even if the <strong>Include Chinese</strong> setting is off, you can still query Chinese characters in logs, but the search keyword must match the Chinese text exactly.</div><br><br><br><div data-tips="true" data-tips-type="tip">For example, if logs contain the Chinese field <strong>Access request failed</strong>:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When this feature is off, searching with the keyword <strong>failed</strong> will not find the log; you must use the full keyword <strong>Access request failed</strong> to find it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When this feature is on, searching with words like <strong>access</strong>, <strong>request</strong>, or <strong>failed</strong> can all find the log.</div><br> |
|delimiter |Whether to split log content based on the specified delimiter.<br><br><br>* Enabled: Log Service splits log content according to the specified delimiter. You need to perform queries based on the split log content. If the default delimiter does not meet your needs, you can customize the delimiter. For details about the delimiters supported by Log Service, please refer to the console interface.<br><br>* Disabled: No splitting. Each log is treated as a whole for query.<br><br><br>For example, the log content is `/var/log/access.log`.<br><br><br>* If the delimiter is set to a slash (/), the log will be split into `var`, `log`, and `access.log`. You can use any of these terms to query the log, such as `var`, `va*`, or `access.log`.<br><br>* If you use the default delimiter, the log will be split into `var`, `log`, `access`, and `log`. You can retrieve this log using any of these words, such as `var`, `va*`, or `access`.<br><br>* If tokenization is disabled, the entire log is treated as a single word `/var/log/access.log`. You must search by the full string `/var/log/access.log` or use wildcard search `/var/log/*` to retrieve this log. |


<span id="239ce868"></span>
### key\-value index configuration

On the index configuration page, enable **key\-value index** and fill in the related settings.

After enabling the key\-value index, you can extract indexes from the original logs or add indexes manually. It also supports automatic index update.


* extract index from original logs

   Click **Extract fields from raw logs** to open the **Auto Index Configuration** dialog, which automatically configures key\-value indexes based on the first log in the preview data by default.

   * Click **Append** to keep existing index properties; fields with the same key will update the configuration.

   * Click **Overwrite** to directly replace existing index properties.

* Auto update index

   Select **Auto Update** to automatically add new fields to the key\-value index. Fields generated by auto update display an **auto\-generated** label in the field name column; you can modify index properties as needed. The interface may take 2 to 3 minutes to display related indexes when first enabled.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Indexes generated by auto update must meet the following criteria:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Field name: only fields that comply with the log service field name standards are automatically added.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Field type: only supports text, long, and double types. json type fields are automatically added as <strong>text</strong> type.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Support modifying and deleting automatically added indexes. Modified indexes will not be overridden by automatically updated indexes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Executing the <strong>rebuild index</strong> operation does not trigger automatic index updates.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The total number of automatically updated and manually added indexes is limited to 500.   </div>
   

* Manually configure indexes

   Click **add field** to manually add index fields according to the table below.



|Configuration ||Description |
|---|---|---|
|Field name ||The name of the log field, which is the key in the key\-value pair.<br><br><br>* Only letters, numbers, spaces, underscores (_), hyphens (\-), and slashes (/) are supported; leading or trailing spaces are not allowed.<br><br>* Key names must be unique within the same index.<br><br>* Length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can add up to 500 log fields.</div><br> |
|field type ||Data type of log fields. Fill in the data type truthfully based on the actual situation. The data type setting affects the accuracy and correctness of query and analysis results. For detailed instructions, refer to [index data types](https://docs.byteplus.com/docs/tls/Index-data-types-2).<br><br>Supported data types include text, long, double, and json. |
|Statistics ||enable statistics<br><br><br>* Enabled: This field is included in statistical analysis and can be used in SQL query and analysis statements.<br><br>* Disabled: This field is not included in statistical analysis. |
|Field configuration |Case sensitive |When performing query and analysis by field, determine whether to distinguish case sensitivity for English letters.<br><br><br>* Enabled: case\-sensitive during query. For example, when querying logs containing `error`, only the keyword `error` can retrieve the log; querying with `ERROR` cannot find it.<br><br>* Disabled: case\-insensitive during query. For example, when querying logs containing `error`, the log can be retrieved using either `error` or `ERROR`. |
||Chinese word segmentation |During query and analysis, determine whether to segment Chinese content in logs according to Chinese grammar.<br><br><br>* Enabled:<br><br>   * Chinese characters in logs: segment logs according to common Chinese grammar; custom Chinese segmentation characters are not supported.<br><br>   * Non\-Chinese characters in logs: segment logs according to the delimiter specified in the **delimiter** parameter.<br><br>* Disabled: segment logs according to the delimiter specified in the **delimiter** parameter. |
||Delimiter |Search by field determines whether to split the log content using the specified delimiter.<br><br><br>* Enable: split the log content using the specified delimiter and search based on the split content. If the default delimiter does not meet your needs, you can customize the delimiter. For details on the delimiters supported by the Log Service, please refer to the console interface.<br><br>* Disable: no tokenization; each log is searched as a whole.<br><br><br>For example, the log content is `/var/log/access.log`.<br><br><br>* If the delimiter is set to a forward slash (/), the log will be split into `var`, `log`, and `access.log`. You can retrieve the log by using any of these terms, such as `var`, `va*`, or `access.log`.<br><br>* If you use the default delimiter, the log will be split into `var`, `log`, `access`, and `log`. You can retrieve the log by using any of these terms, such as `var`, `va*`, or `access`.<br><br>* If tokenization is disabled, the entire log is treated as a single term `/var/log/access.log`. You need to search using the full string `/var/log/access.log` or a fuzzy search like `/var/log/*` to retrieve this log. |
|Action |Modify description |Fill in the description information for the indexed fields. |


<span id="70a3abbd"></span>
### Reserved field index configuration

For reserved fields without preset indexes, such as the `__content__` field, you can manually set indexes through **reserved field index**. On the index configuration page, enable **reserved field index** and fill in the related settings. For detailed explanations of each configuration item, refer to [key-value index configuration](https://docs.byteplus.com/docs/tls/Configure-indexes-2#52f4e302).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, only the <code>__content__</code> field supports setting reserved field indexes. If the <code>__content__</code> field is set to json type, you can enable the <strong>automatic indexing of all text within Json</strong> feature.</div>


* <div data-tips="true" data-tips-type="tip">Supports enabling full\-text indexing and <code>__content__</code> reserved field indexing simultaneously. Enabling both will result in double indexing traffic fees and storage space fees.</div>



<span id="163f6fc5"></span>
## Indexing traffic explanation


|index type |Description |
|---|---|
|Full\-text index |Both field names and field values are stored as text type, generating index traffic. |
|Key\-value index |* text type: Both field names and field values generate index traffic.<br><br>* numeric type: Field names of long and double types do not generate index traffic. Each field value occupies 8 bytes of index traffic.<br><br>* JSON type: Both field names and field values (including subfields) generate index traffic.<br><br>   * If no index is created for JSON subfields, the subfield is treated as the value of a JSON type field. The log service calculates index traffic based on the text type.<br><br>   * When an index is created for a JSON subfield, the log service calculates index traffic according to the subfield’s data type (text, long, double). |


<span id=".6ZSu5YC857Si5byV6YWN572u"></span>
## Related actions

<span id="9c89dfa5"></span>
### Set maximum field length

When analyzing logs, the log service defaults to a maximum field value length of 2048 bytes (2 KB). To adjust the maximum field value length, set the **maximum length for statistics fields**, ranging from 64 to 16384.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the length of a single field value exceeds the specified maximum length, the excess part will be truncated and not included in the analysis.</div>


* <div data-tips="true" data-tips-type="tip">The updated maximum field length only applies to incremental data.</div>



<span id="76480138"></span>
## Next steps


* [Single-topic query log](https://docs.byteplus.com/docs/tls/Query-logs-2)

* [Analysis log](https://docs.byteplus.com/docs/tls/Analyze-logs-2)

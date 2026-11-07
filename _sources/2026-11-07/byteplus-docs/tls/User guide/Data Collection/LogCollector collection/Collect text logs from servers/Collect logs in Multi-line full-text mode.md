---
title: "Collect logs in Multi-line full-text mode"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/multi_line_full_text_mode"
---

LogCollector collection rules support the multi\-line full\-text mode. In multi\-line full\-text mode, LogCollector uses a specified regular expression for line beginning to match the start of a log. This helps identify a complete log entry.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In certain business scenarios, a complete log entry can contain line breaks and span multiple lines. In this case, if a line break is considered as the identifier that marks the end of each log entry, the system may incorrectly separate the log data. To fix this issue, you can collect logs in multi\-line full\-text mode. This mode uses a regular expression for line beginning in matching. In this mode, if a part of the log data matches the regular expression, this piece of data is identified as the start of a log entry. Besides, the next piece of data that matches the regular expression is identified as the start of the next log entry.

In multi\-line full\-text mode, Torch Log Service (TLS) neither extracts log fields nor structures the log data.

TLS adds the following metadata fields to log entries and creates indexes for the added fields.


|Reserved Field |Description |
|---|---|
|`__content__` |This field is used to encapsulate the original log data. This field does not have a preset index. To query log content, you must manually enable the full\-text index feature. |
|`__path__` |The source directory and filename of the log file. |
|`__source__` |The IP address of the log source server. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create a project](https://docs.byteplus.com/docs/tls/Managing_projects#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E9%A1%B9%E7%9B%AE) and [Create a topic](https://docs.byteplus.com/docs/tls/Managing_topics#.5Yib5bu65pel5b-X5Li76aKY).

* Create a host group and make sure that the heartbeat statuses of the hosts in the host group are in normal state. For more information, refer to [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group)or [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).

* Install the latest version of LogCollector on the log source server. For more information, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiALeWhq-WGmeWIneWni-mFjee9rg=="></span>
### Step 1: Select a log space


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, select a collection mode.

5. Select a project and a topic, and click **Next step: Select host group.** 

   The collected log data is stored in the selected topic.


<span id="c9753423"></span>
### Step 2: Select host groups


1. In the **All host groups** area, select a host group for log collection.

   If there is no host group available in the list, you need to create the host groups first. For specific operations, please refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group), [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group).

2. In the **Selected host group** area, confirm the selection, and click **Next step: Collection rule**.


<span id="eef7bb18"></span>
### Step 3: Configure a collection rule

<span id="e61e73e3"></span>
#### Configure basic information


1. Enter the **Rule name**.

   The **Rule name** is the name of the LogCollector collection rule.

   Alternatively, click **Import other collection configurations**, select a collection rule from a specified project in the current account, then import the existing collection rule. You only need to specify a collection rule name.

2. Select whether to enable **Container log collection**.

   It is disabled by default. Keep the default setting when you collect server logs or collect container logs in sidecar mode.

3. Set **Collection path**.

   **Collection path** specifies the filename and directory where the log data is stored. LogCollector matches directories to listen on log files in the directories that meet the rule. Up to 10 different collection paths can be set.

   You can specify complete directories and filenames, or use wildcards for fuzzy matching.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, a log file can only be collected into one topic and match one collection rule. If a file matches multiple collection rules, the latest collection rule applies.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the wildcard <code>**</code> is specified in log collection paths, multi\-level directory matching applies. In this case, TLS can listen on up to 8\-level directories.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, TLS supports the following wildcards: asterisks <code>*</code> , double asterisks <code>**</code>, and question marks <code>?</code> . You can configure up to one double asterisk <code>**</code> as the wildcard.   </div>
   

   The following table introduces the common methods of configuring collection paths and the corresponding examples:

   
   |Configuration methods |Example |Description |
   |---|---|---|
   |Complete directory and filename |`/var/log/access.log` |Specify a complete directory and filename without wildcards, listening on the specified file in the directory only.<br><br>In this example, TLS listens on the file named `access.log` in the `/var/log` directory. |
   |Filename fuzzy matching |`/var/log/*.log` |If you do not specify a filename, TLS listens on all log files. If you specify a filename rule, TLS only listens on files that meet the rule.<br><br>In this example, TLS listens on `.log` files in the `/var/log` directory. |
   |Path fuzzy matching |`/var/log/**/access.log`<br><br>`/var/log/*/access.log`<br><br>`/var/log/*` |When you use `*` for path fuzzy matching, TLS only listens on log files in the first\-level directory. When you use `**`, TLS listens on log files in the first\-level directory and its subdirectories. In this case, TLS can listen on up to 8\-level directories.<br><br>For example, `/var/log/**/access.log` means TLS listens on files named `access.log` in the `/var/log` directory and its subdirectories, up to 8 levels. |
   

4. Set **Collection Rules policy**.

   When log files under the same collection path are matched by multiple collection configurations, the following policies can be set:

   
   |Configuration |Description |
   |---|---|
   |Can be overwritten by new configuration |If there is an updated collection configuration, log files will not be collected according to the current configuration and will be collected based on the latest one. |
   |Permanent effect |Even if updated collection configurations exist, log files will continue to be collected based on the current configuration.<br><br>**Permanent effect** applies only to LogCollector version 2.1.0 and later and may result in duplicate collection fees. For more details, please refer to [File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected). |
   

5. Set **Collection path blacklist**.

   After you set a collection path denylist, the specified directories and files are ignored when TLS uses LogCollector to collect logs. After you check the **Enable** check\-box, set directories and files as prompted.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 10 denylists can be set in each collection rule.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use wildcards in log paths but want to exclude some directories or files, specify the complete path or filename in the denylist. For example, if the collection path is <code>/var/log/project/*.log</code> and you want to exclude all subdirectories in <code>/var/log/project</code>, then set <strong>Collection path blacklist</strong> to <strong>File path</strong> and set the path to <code>/var/log/project/**</code>.   </div>
   

   In a denylist, you can set the path type to **Directory path** or **File path**.

   
   |Parameter |Description |
   |---|---|
   |Directory path |TLS ignores the specified directories during collection. Both exact matching and wildcard matching are supported.<br><br><br>* Exact matching: Specify a complete directory name, such as `/var/log/mydata/new`.<br><br>* Wildcard matching: Use wildcards in a directory. The supported wildcards include asterisks `*` and question marks `?` . For example, `/var/log/mydata/n*` means TLS ignores directories starting with n in `/var/log/mydata/` during collection. |
   |File path |TLS ignores the specified files during collection. If you select this path type, you must configure file paths and filenames. Both exact matching and wildcard matching are supported.<br><br><br>* Exact matching: Specify a complete path and filename, such as `/var/log/mydata/access.log`.<br><br>* Wildcard matching: Use wildcards in a path and a filename. The supported wildcards include the following: asterisk `*`, question mark `?` and double asterisk `**`. You can specify up to one double asterisk `**` as a wildcard. For example, `/data/nginx/log/*/*/access.log` means TLS ignores files named `access.log` in the `/data/nginx/log` directory and its first and second\-level subdirectories during collection. |
   


<span id="bc19b697"></span>
#### Configure Log Format


1. Set **Collection policy**.

   The collection policy specifies whether LogCollector collects incremental logs or full logs. By default, incremental logs are collected.

   
   |Parameter |Description |
   |---|---|
   |Full |LogCollector collects logs from the start of each file, collecting historical log data. |
   |increment |LogCollector only collects new content in files. When new logs are written to log files within the monitoring range, it triggers LogCollector to collect logs.<br><br><br>* For the first\-time collection of a log file, LogCollector will automatically determine the collection position based on the incremental threshold you specify.<br><br>   * If the size of the new file does not exceed the specified incremental threshold, LogCollector collects logs from the beginning of the new file.<br><br>   * If the size of the new file exceeds the specified incremental threshold, LogCollector collects logs from a position that is the file's end minus the incremental threshold, thus collecting only the incremental logs.<br><br>* For log files that are not being collected for the first time, LogCollector will determine the collection position based on the Checkpoint and continue collecting from there. |
   

2. Set **Collection mode.** 

   
   |Parameter |Description |
   |---|---|
   |Collection mode |The mode in which LogCollector parses log files. Set it to **Multi\-line**. |
   |Log sample |We recommend that you specify more than two log data entries as examples to ensure that the regular expression can match the beginning of each line.<br><br>We recommend that you use real examples in the production environment. |
   |First line regular expression |The regular expression used to identify the start of a log entry. The piece of data that matches the regular expression is used as the start of the log entry. Both automatic generation and manual creation are supported. Once a regular expression is set, the page displays the number of line starts matched in the log examples. If this number is the same as the actual number of log entries, the regular expression is correct.<br><br><br>* **Auto generation**: Automatically generate a regular expression for line beginning based on the typed log examples. The highlighted part indicates the content matched by the regular expression.<br><br>* **Manual input**: Customize a regular expression for line beginning. If you customize a regular expression for line beginning, TLS uses it to match the log examples and sets the matched part as the start of a log entry. |
   

   After the preceding configuration items are set, click **Verify Now** to verify if the regular expression can match the line beginning of each log entry without mistakes.

3. Select whether to use the acquisition time.

   * **Acquisition point in time**: Use the system time of the server where the LogCollector is located when the log is collected as the log time.

   * **Custom time**: Extract the time that comes with the original log as log time. The relevant configuration is as follows:

      
      |Parameter |Description |
      |---|---|
      |Time key name |The name of the time field, using the `__content__`field or the time field specified through the plug\-in. When using the time field specified by the plug\-in, you need to Enable the **Plugin configuration** , extract the time from the log and specify the time field. |
      |Time regular |If you only parse part of the contents of a time field, you can use a regular expression to extract it. |
      |Time accuracy |After checking **Enable nanosecond time accuracy**, you can extract timestamps with nanosecond accuracy. For detailed instructions, please refer to [Enable LogCollector high precision time](https://docs.byteplus.com/docs/tls/Enable-LogCollector-high-precision-time). |
      |Time conversion format |Set the time conversion format according to the extracted time content. For example `01/March/2024 20:15:02`, you can configure the **time conversion format** to `% d/% b/% Y:% H:% M:% S`. For more information, refer to [Time format](https://docs.byteplus.com/docs/tls/time_format).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the time conversion format is filled in incorrectly and the time cannot be parsed correctly, the collection time shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, LogCollector collection time can be accurate to milliseconds, that is, when configuring the time conversion format, it supports configuration to milliseconds. If no millisecond resolution is specified in the time conversion format, the millisecond portion is automatically filled with 0.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After checking <strong>Enable nanosecond time accuracy</strong> in the collection configuration, it supports parsing the log time to nanosecond precision.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add a time zone to the log time and the original log time contains the time zone, you can add the time zone format (% z) to the <strong>time conversion format</strong> to extract the time zone. Alternatively, you can add a fixed time zone format (+ 08:00) to the <strong>time conversion format</strong> and select the appropriate <strong>time zone attribute</strong> .</div><br><br><br>   <div data-tips="true" data-tips-type="tip">For example <code>2024-03-03 15:00:00 + 08:00</code>, you can set the <strong>time conversion format</strong> to <code>% Y-% m-% d% H:% M:% S% z</code>, or set the <strong>time conversion format</strong> to <code>% Y-% m-% d% H:% M:% S + 08:00</code>and select the corresponding <strong>time zone attribute.</strong>   </div><br>    |
      |Time zone attribute |Set the time zone. Select UTC if you want to support daylight or winter time; otherwise, select GMT. |
      

4. Select whether to ignore the files that have not been updated.

   Once enabled, when the update time of the log file is not within the time range you specified, LogCollector will ignore this file and not perform collection.

5. Set whether to enable upload parsing failure log.

   * Enable: After enabling, you must also configure the F**ailure log key name**. The key name defaults to `LogParseFailed`. All logs that fail to parse are uploaded to TLS, using the configured failure log key name field as the key and the original log content as the value. 

   * Disable: Logs that fail to parse are not uploaded to TLS.


<span id="300a95bd"></span>
#### Configure plugin

Choose whether to enable **Plugin configuration**.

If complex and unstructured business logs cannot be parsed using common log collection modes like JSON, you can use LogCollector plug\-ins to process the collected logs. For more information, refer to [LogCollector plug-ins Overview](https://docs.byteplus.com/docs/tls/plug-ins_Overview).

<span id="f622c76f"></span>
#### Advanced settingsOptional


1. Enable **Advanced Settings**.

   Configure advanced settings as needed. We recommend that you keep the default settings unless otherwise needed.

   
   |Parameter |Description |
   |---|---|
   |Filter |Specify whether to enable log field filter rules. By default, it is disabled. After enabled, use regular expressions to set filter rules. Only logs that exactly match the regular expressions are collected, helping you collect valuable log data. |
   |Upload hostname field |Specify whether to upload the hostname field. This parameter is disabled by default.<br><br><br>* If you enable the parameter, a field is added to the original log to record the hostname of the log source. Specify the field name for **Hostname** . Default value: `hostname`.<br><br>* If you disable this parameter, the `hostname` field is not added. |
   |Parse collection path |Extract fields from the collection path using regular expressions, then add the fields as metadata to log data. By default, this feature is disabled.<br><br>After enabled, set **Sample collection path**, **Extract regular expression**, and **Extract result**.<br><br><br>* **Sample collection path**: Specify an example of the collection path in actual scenarios.<br><br>   * The example must be an absolute path.<br><br>   * The example cannot include the following wildcards: single asterisk`*`, question mark `?`, and double asterisks `**`.<br><br>* **Extract regular expression**: Specify a regular expression used to extract fields from the path. To successfully extract fields, it must match the collection path example.<br><br>* **Extract result**: It displays each field value parsed and extracted by TLS from the path example based on the regular expression. You must specify a key for each field.<br><br>   * Up to 100 keys can be configured.<br><br>   * Each key must be unique and cannot be empty. |
   |HashKey Routing Shard |Specify a HashKey to write data to a shard that meets the range requirements. By default, this feature is disabled.<br><br><br>* Enable: Use the HashKey Routing Shard mode for data collection. In this mode, data is written to the specified shard in sequence. This is suitable for scenarios requiring sequential data writes and consumption. In this case, you must set the HashKey. Then, TLS writes the data to the shard containing that key value. The HashKey value range is [00000000000000000000000000000000–ffffffffffffffffffffffffffffffff).<br><br>* Disable: Use the load\-balanced mode for data collection. In this mode, data packets are written to an available shard in a load\-balanced manner. This is suitable for scenarios where data consumption and writes are irrelevant to shards, such as scenarios not requiring a sequential order. |
   |Upload original log |Specify whether to upload raw log data as a field to TLS. It is disabled by default.<br><br><br>* Enable: Raw log data is encapsulated in a specified field, and uploaded to TLS together with the parsed log data. The field key can be specified using **Raw log key name**. The default key is `raw`, and the actual corresponding log field is `__raw__`.<br><br>* Disable: No raw log field is added. |
   |Upload constant field |After enabled, LogCollector encapsulates the specified field keys and values in each log entry. The following limits apply to constant fields:<br><br><br>* Up to 5 constant fields can be uploaded.<br><br>* Each field key must be unique and cannot be empty. The key must be 1 to 128 characters in length. It can contain letters, digits, and the following special characters: `-_./` It cannot start with an underscore ( _ ).<br><br>* Each value cannot be empty, with a maximum length of 512 KiB. |
   |Upload Host Group Label |Whether to upload the label information of the host group to TLS.<br><br><br>* Enable: LogCollector will upload the label information of the host group to the specified field. You can specify the field name in the **Host Group Label Key Name**, the default value is `host_group_label`.<br><br>* Disable: Do not upload the label information of the host group. |
   |Extended configuration |Specify the extended configuration of LogCollector in JSON object format. Currently, the supported parameters include CloseInactive, CloseRemoved, CloseRenamed, CloseEOF, and CloseTimeout. For more information on the parameters, refer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule).<br><br>For example, the configuration below means that the file handle is released if any of the following occurs: 1. No log data is written to the log file for 10 seconds. 2. The log file is removed or renamed. 3. LogCollector reads to the end of the file. 4. The monitoring duration of the log file exceeds 30 minutes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/213bf60ab3ed4bcd9db3ce9a768cd92b~tplv-goo7wpa0wc-image.image) </span> |
   

2. Confirm the collection rule, then click **Next step: Check the index configuration**..


<span id=".5q2l6aqk5LiJLeabtOaWsOe0ouW8lQ=="></span>
### Step 4: Update indexes


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. You can also click **Import existing index configuration** to import the index of other topics.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2) to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.


<span id=".5ZCO57ut5q2l6aqk"></span>
## Follow\-ups

After creating the collection configuration, LogCollector will collect logs and save them to the specified log topic. You can perform query and analysis operations in the log topic.

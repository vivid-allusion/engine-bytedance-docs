---
title: "Import logs from TOS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Import_data_from_tos"
---

TLS supports TOS data import, allowing you to structure the data stored in TOS and save it in TLS. This topic describes the steps to import data from TOS to TLS.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

For bulk import of large volumes of log files, you can do the following: upload log files to a TOS bucket; use TLS's log import feature to structure; import, and save files in TLS. Then you can perform real\-time query analysis and further processing to log data. When importing data from TOS, you can import all data from one or more objects in a specified bucket into TLS. Cross\-region import is supported, meaning the TLS topic and source bucket can be located in different regions. After creating an import task, you can view the progress and status in TLS console, or use service log analysis for detailed progress and status data.

TLS also adds the following metadata fields to imported log data.


|Field |Description |
|---|---|
|`__content__` |Original log data. Only add when **log extraction type** is set to **Single\-line full text**. |
|`__path__` |Source file directory and file name for the log. |
|`__source__` |Name of the storage bucket where the log source is located. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notice

The following are the limitations of the data import feature from TOS:


|Limits |Description |
|---|---|
|Import performance |The maximum processing speed supported by TOS data import tasks is 80 MB/s. If you need to increase the processing speed, submit your business requirements through the ticketing system. |
|Number of data import configurations |You can create up to 100 different types of data import configurations in a single project. |
|Single file size |The file size limit varies by compression mode. Files that exceed the limit will not be imported into TLS.<br><br><br>* Snappy compression format (non\-framing\-format): The file size limit is 350 MiB.<br><br>* Other compression formats or uncompressed files: The file size limit is 5 GiB. |
|Individual data entry size |The maximum log entry length is 512 KiB. Logs exceeding this size will be truncated and discarded; if a log entry exceeds 2 MiB, it will be directly discarded. |
|Import data scope |Only full import is supported; incremental import is not available.<br><br><br>* After creating the import task, TLS will not collect incremental content from newly added files in the bucket that meet the import rules.<br><br>* If a file is updated and has not yet been collected, TLS will collect the latest version of the file. |
|Bucket type |Importing data from deep cold archive storage buckets is not supported. |
|Edit import task |After creating a log import task, you can not modify the data source configuration or other settings for the task. If the configuration is incorrect, delete it and create a new one. |


<span id=".6LS555So6K-05piO"></span>
## Billing description

Importing data from TOS involves charges for TLS and TOS, including read traffic and write traffic. For detailed pricing information, see TLS  [Billing items based on pay-by-feature mode](https://docs.byteplus.com/docs/tls/Billing_items_based_on_pay-by-feature_mode)and TOS [Billing Overview](https://docs.byteplus.com/en/docs/tos/docs-billing-overview).


|Billing side |Billing item |Description |
|---|---|---|
|TOS |VPC outbound traffic |Reading data from TOS over a BytePlus VPC incurs VPC outbound traffic. |
||Number of requests |When reading data from TOS, billing is based on the number of requests for different storage types. |
|TLS |Write traffic |When TOS data is written to TLS, TLS write traffic fee is generated. Traffic fees are calculated based on the compressed data volume. |
||Log storage |After logs are stored in TLS, the backend automatically compresses them. Storage fees are calculated based on the actual compressed size. |
||Others |* We recommend that you enable indexing for imported data to facilitate future queries, analysis, and data statistics. Enabling indexing incurs index storage fees. Storage fees are calculated based on the space occupied by indexes that are created from the log data before compression.<br><br>* If imported data is later read, transformed, or shipped, charges will apply according to the billing standards. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Log files have been uploaded to a TOS bucket. For detailed steps, see[Upload logs](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

* A log project and log topic are created. For detailed steps, see [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources).

* Before using the log import or log shipping features for the first time, you must complete cloud resource access authorization to grant TLS permission to access and write resources. If authorization has not yet been granted, TLS will provide guidance when you create a log import task in the console. We recommend using the BytePlus primary account for authorization.  For more information, see [Cross-service access authorization](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id=".5Yib5bu65a-85YWl5Lu75Yqh"></span>
## Steps

<span id=".5q2l6aqk5LiALeWIneWni-mFjee9rg=="></span>
### Step 1 Select a log space


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4.  on the **Data import** tab, click **Byteplus TOS**.

5. Select a log space, then click **Next step: configure import rules**.

   
   |Configuration |Description |
   |---|---|
   |Log project |Name of the project used to store TOS data. |
   |Log topic |Name of the log topic used to store TOS data.<br><br>Exclusive log topics for cloud product logs and service logs do not support data import. |
   


<span id=".5q2l6aqk5LqMLeaVsOaNrua6kOmFjee9rg=="></span>
### Step 2 Configure import rules


1. Enter the **task name**.

   Set the name for the log import task.

2. Configure the data source.

   
   |Configuration |Description |
   |---|---|
   |Region where the bucket is located |Region where the TOS bucket is located. Supports cross\-region data import. |
   |IAM project of the bucket |IAM project to which the TOS bucket belongs. |
   |Bucket |TOS bucket that contains log files. |
   |Select file path |The path of the file to be imported in the TOS bucket.<br><br><br>* **Select file path**: Select a path or file directly from the dropdown list.<br><br>* **Enter path manually**: Enter the file prefix or the complete path. For example, if you set the file prefix as `accesslog/`, all files under the directory `accesslog/` will be imported.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">File prefixes do not support wildcards.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Leaving the path blank means importing all files in the bucket. If too many files exist in the bucket, traversing the bucket may reduce data import efficiency.</div><br> |
   |Compression mode |The compression mode for data in the TOS bucket. TLS supports importing data in the following compression modes.<br><br>Compression mode: No compression, snappy, gzip, lz4, tar.gz **.** <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Before setting lz4, make sure the data source uses LZ4Frame compression; otherwise, decompression may fail during import.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The tar.gz compression mode is only available for preview. If you have relevant business needs, contact your account manager for allowlist permission.</div><br> |
   

3. Configure the import method.

   
   |Configuration |Description |
   |---|---|
   |Log extraction type |TLS supports the following log parsing types:<br><br><br>* **Single\-line**: Each line is parsed as a log; uses `\n` as the end mark. After import, logs are stored in the default field `__content__` and are not further structured.<br><br>* **Multi\-line**: When importing multi\-line logs, you can specify a regular expression to match the first line of each log entry.<br><br>* **JSON:**  Extract logs into multiple key\-value pairs based on the JSON format. The top\-level object keys serve as field names; top\-level object values serve as field values; `\n` serves as the end of each log entry. The log attribute time is determined by the log collection time.<br><br>* **CSV**: Each log entry ends with `\n` as the end marker. Besides, each log entry can be structured using a specified separator. The log attribute time is determined by the log collection time. In this case, additional parameters are required. For details, see the table below. |
   |Import archived files |If you are importing TOS files stored as **Archive** or **Cold Archive**, you need to enable this feature. After enabling, the system will first thaw the archived files. Once thawing is complete, preview the files. Importing **Deep Cold Archive** storage files is not currently supported.<br><br><br>* Enable: Only enable when importing **Archive** or **Cold Archive** files.<br><br>   * Archive file: Thawing and restore takes about 1 minute.<br><br>   * Cold Archive file: Fast retrieval mode is used for thawing and restore. If an error is reported during preview, you can choose to skip preview or try again later.<br><br>* Disable: Disable in other cases. |
   |Upload failed parsing logs |Choose whether to upload logs that failed to parse. This feature is enabled by default.<br><br><br>* Enable: All logs that fail to parse will be uploaded to TLS, with the specified field as the key name and the original log content as the value. The key name can be specified via **Failure log key name**. It is defaulted as `LogParseFailed`.<br><br>* Disable: Logs with parsing failures will not be uploaded to TLS.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a2fda85d2a8445d9970da71ecd4bc091) </span> |
   |Time field |This configuration determines whether to use the value from the specified field as the log timestamp.<br><br>By default, TLS uses the system time at data import as the log timestamp. You can also specify a time field, and TLS will use the value of this field as the log timestamp. The related configuration is as follows:<br><br><br>* **Time key name**: The Key of the time field.<br><br>* **Time regex**: Use part of the value in the time field as the timestamp.<br><br>   * When the **log extraction type** is set to **single\-line full text** or **multi\-line full text**, you must use a regular expression to extract the time from the log.<br><br>   * When the **log extraction type** is set to **CSV** or **JSON** and you need to extract part of the time field, you can also use a regular expression for extraction.<br><br>* **Time conversion format**: Used to parse the value of the time field. For instructions on time formats, see [Time format](https://docs.byteplus.com/docs/tls/time_format). Example:<br><br>   * When the time field is `1651648409`, configure it as `%s`.<br><br>   * When the time field is `1651648416882`, configure it as `%F`.<br><br>   * When the time field is `2022-01-01T15:30:00.999+0800`, configure it as `%Y-%m-%dT%H:%M:%S.%f%z`.<br><br>* **Time zone**: Time zone can be set here. Supports GMT or UTC.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Notice   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need to support daylight saving time or standard time, select UTC; otherwise, select GMT.   </div><br>    |
   

   * If **log extraction type** is set to **multi\-line**, you also need to configure the following additional parameters:

      
      |Parameters |Description |
      |---|---|
      |Log example |We recommend that you provide at least two log samples to ensure the first\-line regular expression can match the first line of every log.<br><br>We suggest that you use real samples from the production environment. |
      |First\-line regular expression |This regular expression is used to identify the first line in each log entry, and the matched part is identified as the start of the log. Supports automatic generation or manual input. After configuration, the page displays the number of first lines matched in the log examples. If this matches the number of actual log entries, the first\-line regular expression is correct.<br><br><br>* Auto\-generate: Automatically generates the first\-line regular expression based on the entered log examples. The highlighted part in the example shows what the first\-line regular expression matches.<br><br>* Manual input: Customize the first\-line regular expression. TLS matches log samples using the specified first\-line regular expression and identifies the matched part as the start of a log entry. |
      

   * If **log extraction type** is set to **CSV**, you also need to configure the following additional parameters:

      
      |Parameters |Description |
      |---|---|
      |Separator |It is the separator between different fields in log data. Select the correct separator according to the log format to ensure every field can be accurately extracted. TLS supports configuring various common separators, such as spaces and commas.<br><br>When your log data uses a separator that is not in the options, you can set **separator** to **custom** and specify the corresponding separator in **custom separator**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Setting the <strong>separator</strong> as an invisible character is not supported yet.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only one separator can be specified, but a separator can contain multiple characters. For example, you can use double colons (::).</div><br> |
      |Quotation mark |If a log field value contains separators, enclose the entire field value within the specified quote character in the log; otherwise, the content may be incorrectly split by the separator. After you specify a separator and quote character, any content included in the quote character will be parsed by TLS as a complete field.<br><br>For example, if a raw log is `20220511 debug "parse meet error"` and the separator is set as space, then:<br><br><br>* If no quote character is set, the log will be split into `key1: 20220511`, `key2: debug`, `key3: "parse`, `key4: meet, key5: error"`.<br><br>* If the **quote character** is set to **double quotes**, the log will be split into `key1: 20220511`, `key2: debug`, `key3: "parse meet error"`.<br><br><br>Supported quote characters include **do not configure**, **single quote**, **double quotes**, or **custom**. If you choose a custom character, you need to set a **custom quote**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Setting the <strong>quote</strong> as an invisible character is not supported yet.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a field value contains a quote, you can use the escape character <code>\</code> to escape it. The escaped quote will be treated as regular text. For example, if the quote character is a double quotation mark, but the log entry <code>2022"0511"</code> contains double quotes, you can use <code>2022\"0511\"</code> to escape them.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only one quote character can be specified, but the quote can contain multiple characters, such as double colons (::).</div><br> |
      |Field name |After TLS parses and extracts log content using the specified separator, you need to assign a different field name to each log entry.<br><br>Content without an assigned field name will not be imported into TLS. Plus, field names must not be duplicated. Supported configuration methods:<br><br><br>* **First line as field name**: The first line of the CSV file is used as field names. Usually, the first line in a CSV file serves as the header for each data column.<br><br>* **Custom field**: If you select custom field, you can set field names manually. Multiple names can be separated with commas (,). |
      |Skip line count |Specify the number of log lines to skip. For example, if you set it to 1, logs will be imported starting from the second line in the CSV file. |
      

4. Click **Execution preview** to view the content of the file to be imported.

   After configuring the import rules, TLS provides data preview from the specified data source so you can check whether the data in the preview area matches the data to be imported. If the data is different, it means the data source configuration is incorrect. We recommend reconfiguring it.

5. Click **Next step: check index configuration**.


<span id=".5q2l6aqk5ZubLeabtOaWsOe0ouW8lQ=="></span>
### Step 3 Check index configuration


1. Check index configuration.

   Follow the prompts on the page to set or update the index as needed. You can also click **Import existing index configuration** to import indexes from other log topics.

   * If this log topic does not have an index configured, you can set one. For details, see [Configure index](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

   * If the index for this log topic is already configured, you can decide whether to update the index based on the log fields parsed by the collection rule.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Notice   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You must enable the index to query and analyze the collected log data.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The updated index settings only apply to new data written afterward. For more instructions and limitations on query and analysis, see <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Click **Next step: check index configuration**.


<span id="43bade5e"></span>
## Error handling mechanism


|Error item |Processing mechanism |
|---|---|
|Failed to read file |When reading a file, if the file is incomplete (due to issues like network issues or file corruption), the import task will automatically retry. If reading fails after three retries, the file will be skipped. |
|Large file |If a single file exceeds 5GB when reading, the import task will skip that file directly. |
|Compression format parsing error |If the file compression format is invalid or the wrong type is selected when decompressing, the import task will skip that file directly. |
|Data parsing error |When a data parsing error occurs, all logs that fail to parse are uploaded to TLS with the specified field as the key name and the original log content as the value.<br><br>The key name can be specified via **Failure log key name**. It is defaulted as `LogParseFailed`. |
|No TOS bucket exists |If the TOS bucket specified in the import task does not exist, the import task will fail. |


<span id=".5p-l55yL5a-85YWl5Lu75Yqh"></span>
## Related operations

After successfully creating the TOS data import task, you can view relevant information in the TLS console, including configuration details of the import setup and the progress of data import.

<span id=".5p-l55yL6YWN572u6K-m5oOF"></span>
### View configuration details


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4. Then on the **Data import** tab under **Task list**, click the log import task name.

5. On the **Configuration details** tab, view the task's configuration information.

   **You** can view the basic information, data source configuration, and log extraction mode for the import task.


<span id=".5p-l55yL5a-85YWl6L-b5bqm"></span>
### View import progress

The **Import task information** tab displays the status and progress of the import task in detail as follows:


|Display item |Description |
|---|---|
|Import task status |Status of the current import task. For detailed status descriptions, refer to the following table. |
|Import progress |Current task import progress is calculated as `Import progress = (Number of imported resources + Number of skipped resources + Number of failed resources + Number of nonexistent resources) / Total number of resources`. |
|Total number of resources |The number of files in the TOS bucket detected by TLS that meet the import rules. |
|Number of imported resources |Number of files imported by TLS. |
|Size of enumerated resources |Total size of files in the TOS bucket detected by TLS that meet the import rules, measured in GiB. |
|Size of imported resources |Size of files imported by TLS, measured in GiB. |
|Number of nonexistent resources |The number of files that TLS failed to locate due to file deletion during the import process. |
|Number of skipped resources during import |The number of files TLS skipped and did not import due to resource type mismatches, extraction failures, or unreadable files. |
|Number of failed resources |The number of files TLS failed to import. |


Import task status description:


|Status |Description |
|---|---|
|Importing |The import task is in progress. You can view the current progress of the task in **Import progress**. |
|Import completed |Import task is completed. All importable files that meet the import rules have been successfully imported into the specified log topic in TLS. |
|Import exception |Import task exception. If any file fails to import, the entire task will be marked as exception. File import may fail due to reasons such as incorrect decompression methods or data anomalies. We recommend that you resolve the exception and then re\-import the affected files.<br><br>Additionally, you can view detailed information about the problematic file in the service logs. For log fields, see  [Data import error logs](https://docs.byteplus.com/docs/tls/service_log_fields#.dG9zLeaVsOaNruWvvOWFpemUmeivr-aXpeW_lw==). |


<span id="346ae49b"></span>
### Copy import task

TLS supports copying data import tasks. If a similar data import task exists, you can copy all the configurations from an existing task, and then adjust the settings as needed to create a new data import task.


1.  Log in to[ TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4.  in the **Data import** tab under the **Task list** section, click **Copy** under the **Actions** column for the task to be copied.

5. Refer to the steps for creating an import task to confirm or modify the relevant parameter settings.


<span id=".5Yig6Zmk5a-85YWl5Lu75Yqh"></span>
### Delete imported tasks

If there is a failure or anomaly with a data import task, you can delete the task and re\-import data. If you have finished migrating historical log data, or no longer need to import logs to TLS, you can follow the steps below to delete log import tasks.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="default">Deleting a log import task does not affect logs that have already been imported successfully.</div>


* <div data-tips="true" data-tips-type="default">A deleted log import task can not be restored. Proceed with caution.</div>


1.  Log in to [Torch log service console](https://console.byteplus.com/tls).

2. Select the region where torch log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4.  Then in the **task list** section under **data import** tab, locate the log import task you need to delete, and click **Delete** in its **Actions** column.

5. Confirm the information for the task to be deleted in the popup dialog, and then click **Confirm**.


&nbsp;

---
title: "Import data from Kafka"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/import_data_from_kafka"
---

Torch Log Service (TLS) supports the Kafka data import feature. This document describes how to import data from Kafka into TLS.

<span id="46b45a46"></span>
## Background

TLS supports importing message data from a Kafka cluster into a specified TLS topic. Kafka data import function is usually used in scenarios such as cloud data migration in business, such as importing various system logs and application data aggregated by self\-built ELK systems into TLS to achieve centralized data storage, query analysis, and processing. TLS supports importing data from BytePlus message queue Kafka clusters and self\-built Kafka clusters. After creating an import task, you can view the import progress and status information in the TLS console or view the detailed progress and status information through service log analysis.

In addition, TLS adds the following metadata fields for the imported log data.


|Field |Description |
|---|---|
|`__content__` |Kafka news. |
|`__path__` |The field value is empty. |
|`__source__` |The service address of the Kafka cluster. |


<span id="e47900b0"></span>
## Precautions

The restrictions on importing data from Kafka are as follows:


|Restriction |Description |
|---|---|
|Kafka version |Kafka version must be above 0.11.x. |
|Number of concurrent subtasks |TLS creates multiple subtasks for concurrent import based on the number of Kafka topics.<br><br><br>* When the number of Kafka topics exceeds 2,000, TLS creates 16 subtasks.<br><br>* When the number of Kafka topics exceeds 1,000, TLS creates 8 subtasks.<br><br>* When the number of Kafka topics exceeds 500, TLS creates 4 subtasks.<br><br>* When the number of Kafka topics is less than or equal to 500, TLS creates 2 subtasks. |
|Maximum number of import tasks |A log project can contain up to 100 import tasks of different types. |


<span id="c7fcc908"></span>
## Cost information

Importing data from Kafka involves billing items such as write traffic, log storage. For specific pricing information, please refer to [Billable items](https://docs.byteplus.com/en/docs/tls/billable_items).


|Billing item |Description |
|---|---|
|Write traffic |Importing Kafka data to TLS incurs write traffic fees in TLS. |
|Log storage |When TLS stores logs, the TLS backend service automatically compresses the log data. Storage costs are calculated based on the compressed data size. |
|Other |* We recommend that you enable the indexing feature for imported data. This facilitates subsequent query, analysis, and data statistics collection. After the indexing feature is enabled, TLS charges index storage fees. You are charged based on the storage space occupied by the indexes created for log data before compression.<br><br>* Fees for subsequent operations such as data reading, data transformation, and data shipping on the imported data are calculated based on the standard billing policy. |


<span id="a4fdd483"></span>
## Before you begin


* A version\-compliant Kafka cluster has been created. For more information, refer to [Precautions](https://docs.byteplus.com/en/docs/tls/import_data_from_kafka#e47900b0).

* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/en/docs/tls/getting_started_creating_resources).


<span id="833ee517"></span>
## Create a import task

<span id="c10a315a"></span>
### Step 1: Configure the basic information


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **Data import** pane, select **Kafka import** .

5. Complete the basic information configuration, and click **Next step: Configure import rules**.

   
   |Parameter |Description |
   |---|---|
   |Project |The name of the destination TLS project that you want to use to store the log data imported from Kafka. |
   |Topic |The name of the destination TLS topic that you want to use to store the log data imported from Kafka.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot specify a dedicated topic that is used for storing service logs or logs of a cloud product.</div><br> |
   


<span id="462628aa"></span>
### Step 2: Configure an import configuration


1. Configure the import configuration.

   
   |Parameter |Description |
   |---|---|
   |Task name |The name of the log import task. |
   |Service address |The different types of Kafka clusters correspond to the different service addresses, detailed description is as follows:<br><br><br>* Message Queue for Kafka: Kafka instance access point. For more information, refer to [view endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).<br><br>   If the Kafka instance is in the same geography as the TLS project, you can use private network access, otherwise you need to use public network access.<br><br>* Self\-built Kafka cluster: IP address and port number or domain name and port number of Kafka Broker. Only public network access is supported.<br><br><br>Use a half\-width comma (,) to separate multiple service addresses. |
   |Kafka instance ID |When you are using Message Queue for Kafka, this should be set to the Kafka instance ID. For more information, refer to [view instance details](https://docs.byteplus.com/en/docs/kafka/viewing-instance-details). |
   |Do you need authentication |If you are using a public network service address , it is recommended to enable authentication and complete the following configuration according to the configuration on the Kafka side. For authentication instructions, see [Supported security mechanisms ](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints#supported-security-mechanisms).<br><br><br>* **Protocol type**: Secure transport protocol, optional values include plaintext, sasl_ssl, ssl, and sasl_plaintext.<br><br>* **Authentication Mechanism**: Password authentication mechanism  **,**  optional values include PLAIN, SCRAM\-SHA\-256 and SCRAM\-SHA\-512.<br><br>* **Username**: The Kafka SASL username used for authentication.<br><br>* **Password**: User password. |
   |Topic List |Kafka Topic name.<br><br>Multiple Kafka Topics should be separated by a half\-width comma (,). |
   |Consumer group |Kafka consumer group.<br><br>If left blank, the system will automatically create a Kafka consumption group. |
   |Starting position |The starting position of the data import. Optional:<br><br><br>* **Oldest data**: Import from the first data in the specified Kafka topic.<br><br>* **Latest data**: Import from the latest generated data in the specified Kafka topic. |
   |Encoding format |The encoding format of the data. Optional values include UTF\-8, GBK. |
   |Log extraction mode |The format of the data to be imported. Optional value:<br><br><br>* **Single\-line**: If you don't need to structure the data, you can choose **single\-line ** mode.<br><br>* **JSON**: If the data to be imported is in JSON format, you can choose the **JSON** mode. The import task parses the data into key\-value pair format and only parses the first layer of JSON data.<br><br>* **Single\-line complete regula**: Parses data through regular expressions, parsing data into key\-value pair formats. At this time, additional parameters need to be filled in, please refer to the following table for details. |
   |Upload parsing failure log |Whether to upload the log of failed parsing, the default value is enabled.<br><br><br>* Enabled: All logs that fail to parse are uploaded to TLS with the specified field as the key name and the original log content as the value. You need to specify the **failure log key name** to store the failed log.<br><br>* Disabled: logs that failed to parse are not uploaded to TLS. |
   |Failure log key name |Fields to hold logs of failed parses. |
   |Specify time field |Choose the log time field. You can use the system time when the log service imports the data as the log time, or you can specify a time field, and the log service will use the value of that field as the log time. <br><br><br>* System points in time(default): If you use system time or Kafka message timestamps as log timestamps, you also need to configure a default time source, which defaults to the current system time. <br><br>* Specify time field:<br><br>   * **Time key name**: Key of the time field.<br><br>   * **Time regular**: Use regular expressions to extract the time in the log.<br><br>   * **Time conversion format**: Time format, used to parse the value of a time field. For more information, refer to [Time format](https://docs.byteplus.com/en/docs/tls/time_format). For example, the time field value is `1651648409`, you can configure the **time conversion format** to `% s`; the time field value is `1651648416882`, you can configure the **time conversion format** to `% F`; the time field value is `2022-01-01 T15:30:00.999 + 0800`, you can configure the **time conversion format** to `% Y-% m-% dT% H:% M:% S.% f% z`.<br><br>   * **Time zone**: Time zone configuration. The default is the time zone where the machine is located, and it supports setting to GMT format or UTC format. |
   |Default time source |When you select **Time field** and choose ** System time in point**, you can use **System current time** or **Kafka timestamp** as log time. |
   

   If you set **the log extraction mode** to **single\-line full regular**, you need to set the following additional parameters. You can choose a different extraction mode to generate regular expressions manually or automatically, and confirm the extraction result of the regular expression for the log sample in the **Extract Results** area.

   
   |**Extraction mode** |**Description** |
   |---|---|
   |Auto generation |After you enable **Auto generation**, the system automatically generates regular expressions based on the fields that you select by dragging the mouse.<br><br><br>1. In the **Log sample** pane, drag the mouse from left to right to select the log fields that you want to extract.<br><br>2. Confirm the content of **Selected Value** displayed in the pop\-up window, then click **Generative** **regular**.<br><br>3. After all key\-value pairs that you want to collect are extracted, set a key for each field in the **Extract result** pane.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">We recommend that you do not select the fields that do not you want to collect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Keys in the <strong>Extract result</strong> pane cannot be empty and must be unique.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The <strong>Auto generation</strong> feature can only generate regular expressions for extracting English characters and cannot generate regular expressions for extracting Chinese characters.</div><br> |
   |Manual input |Disable **Auto generation**, then enter regular expressions manually. After you enter regular expressions, click **Verify Now**. Then, TLS extracts key\-value pairs from the sample log data in the **Log sample** pane based on the regular expressions.<br><br>Once **Verification successful** is displayed on the page, set a key for each field in the **Extract result** area.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Use brackets <code>()</code> to enclose the regular expression for extracting each key\-value pair. TLS considers the content enclosed in a pair of brackets <code>()</code> as a capture group and parse the content to a key\-value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For the fields that you do not want to collect, do not create regular expressions to extract them or delete extracted fields in the <strong>Extract result</strong> pane.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Keys in the <strong>Extract result</strong> pane cannot be empty and must be unique.</div><br> |
   

2. Click **Execution preview** to preview the files to be imported and click **Next: Check the index configuration**.

   After you complete the import configuration, TLS provides a data preview of the specified data source, and you can verify whether the data displayed in the preview pane is the consistent with the data that you want to import. If the data differs, it indicates that the data source configuration is incorrect. In this case, configure the data source again.


<span id="1df640ee"></span>
### Step 3: Check index configurations


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. You can also click **Import existing index configuration** to import the index of other topics.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2) to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/en/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/en/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.


<span id="a56a0c30"></span>
## View import task details

After a Kafka data import task is created, you can view the task details in the TLS console.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **Data import** pane, click the name of the log import task, then view the task configurations on the **configuration details**.

   On the **configuration details** tab, you can view the basic information and data source configuration.


<span id="b138d7ea"></span>
## Modify import task

After a Kafka data import task is created, you can modify the configuration of the import task at any time according to your business requirements.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. On the **Task list** area under the **Data import** tab, find the import task that you want to modify, then click **Edit** in the **Actions** column.

   For more information, refer to [Create a import task](https://docs.byteplus.com/en/docs/tls/import_data_from_kafka#833ee517).


<span id="OoqXlhp6"></span>
## Copy import tasks

TLS supports replicating data import tasks. When similar data import tasks exist, you can directly copy all configurations of an existing task and then modify the relevant configurations as needed to create a new data import task.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. Select the region where torch log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4. in the **Data import** tab's **Task list** area, click **Copy** in the **Operation** column of the task to be copied.

5. Refer to the steps for creating an import task to confirm or modify the relevant parameter configuration.


<span id="ef35119b"></span>
## Delete import task

If a data import task encounters faults or exceptions, delete the import task and create a new task to import the data. If all existing log data has been imported or you no longer need to import log data into BytePlus TLS, delete the log import task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Deleting a log import task does not affect the log data that has been imported.</div>


* <div data-tips="true" data-tips-type="tip">Once a log import task is deleted, it cannot be restored. Proceed with caution.</div>


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. On the **Task list** area under the **Data import** tab, find the import task that you want to delete, then click **Delete** in the **Actions** column.

5. In the pop\-up window, confirm the information about the task to be deleted, then click **Delete**.

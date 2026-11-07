---
title: "Import data from Elasticsearch"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Importing_data_from_Elasticsearch"
---

Torch Log Service (TLS) offers a convenient and efficient data import feature and supports various data sources such as Elasticsearch. This feature allows you to structure data in Elasticsearch and save log data in TLS for subsequent query and analysis. Log data in TLS can be consumed and processed on multiple platforms. This topic describes how to import data from Elasticsearch into TLS.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

Elasticsearch is a distributed, RESTful data search and analysis engine. In data migration scenarios such as service migration to the cloud and application relocation, you can quickly import data from an existing Elasticsearch, Logstash, and Kibana (ELK) stack into TLS. TLS supports data sources including BytePlus Elasticsearch clusters, self\-managed Elasticsearch clusters, and Elasticsearch clusters from other cloud service providers. When importing data from Elasticsearch, you can specify conditions in the query statement, set a time field, or use other methods to filter data. After creating an import task, you can view the import progress and status information in the TLS console or view the detailed progress and status information through service log analysis.

In addition, TLS adds the following metadata fields to imported log data:


|Field |Description |
|---|---|
|`__tag____index__` |The index of the source to which the log entry belongs. |
|`__tag____meta_id__` |The ID of the log file to which the log entry belongs. |
|`__source__` |The source URL of the imported index. It is the endpoint of the Elasticsearch cluster to which the index belongs. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only historical log data can be imported. The data that is written to Elasticsearch after the import task is created cannot be imported to TLS. After all historical data is imported, the import task automatically ends.

* Log data can only be imported to TLS over the internet. If your data source is a BytePlus Elasticsearch cluster or a self\-managed Elasticsearch cluster running on BytePlus ECS, you must allow the cluster to be accessed over the internet.

* After an import task is created, we recommend that you enable the field indexing feature. This helps you preview, query, and analyze the imported log data.

* If a field key in Elasticsearch starts with an underscore ( `_` ), TLS automatically adds a **tag** prefix to it. This allows for efficient indexing and log query and analysis.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Limited Item |Description |
|---|---|
|Maximum data entry size |The maximum size of a single data entry that can be imported is 1 MiB. If the size of a single data entry exceeds this limit, TLS discards the data entry. |
|Maximum number of import tasks |Each project can contain up to 100 import tasks. |
|Data range |Only historical data can imported to TLS. The data that is written to Elasticsearch after the import task is created cannot be imported to TLS. After all historical data is imported, the import task automatically ends. |
|Maximum number of concurrent tasks |Import tasks use the Scroll mode to pull data from Elasticsearch. However, the number of Scroll requests on the Elasticsearch server is limited. The total number of partitions on which log import tasks are performed in each Elasticsearch cluster cannot exceed this limit. Otherwise, some import tasks fail.<br><br>This limit is specified by the `search.max_open_scroll_context` parameter in the Elasticsearch cluster configurations. The default value is 500. |
|Import task modification |After a log import task is created, you cannot modify the data source and other configurations. In case of a configuration error, delete the configuration and create a new configuration. |


<span id=".5oCn6IO96K-05piO"></span>
## Performance description

The service performance of the Elasticsearch data import feature depends on multiple factors. The main factors include:


* Complexity of the Elasticsearch query statement: In an import task, an Elasticsearch query statement must be configured for data filtering. The more complex the query statement is, the longer period of time the Elasticsearch server consumes to execute the request. This affects the data reading speed of the import task.

* Write speed of a target topic: The number of shards in the target topic determines the data write speed. The maximum data writing speed for a single topic shard is 5 MiB/s. We recommend that you evaluate the number of shards in the target topic based on the amount of data. You can enable the automatic sharding feature or increase the number of shards for the target log topic if a large amount of data must be imported. For more information on sharding, refer to [Manage shards](https://docs.byteplus.com/docs/tls/Managing_shards).


<span id=".6LS555So6K-05piO"></span>
## Cost information

Importing data from Elasticsearch incurs fees for TLS log storage and read traffic over a VPC.


|Billable items |Description |
|---|---|
|Write traffic |Writing data from Elasticsearch into TLS incurs write traffic fees in TLS. Traffic is charged based on the amount of compressed data. |
|Log storage |When TLS stores logs, the TLS backend service automatically compresses the log data. Storage costs are calculated based on the compressed data size. |
|Others |* We recommend that you enable the indexing feature for imported data. This facilitates subsequent query, analysis, and data statistics collection. After the indexing feature is enabled, TLS charges index storage fees. You are charged based on the storage space occupied by the indexes created for log data before compression.<br><br>* Fees for subsequent operations such as data reading, data transformation, and data shipping on the imported data are calculated based on the standard billing policy. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create an Elasticsearch cluster.

* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources).

* Before importing data from a Elasticsearch cluster in Alibaba Cloud or Tencent Cloud, you must configure an IP address allowlist on the source node to allow your TLS data import task to access the data in the source node. For more information, refer to [IP address allowlist](https://docs.byteplus.com/docs/tls/consultation_faq_ip_address_allowlist).

* The first time you use the log import or log shipping feature, you must grant read and write permissions to TLS to allow it to access the data source. If you do not grant the permissions to TLS before you use the feature, TLS guides you to perform the required operations when you create a log import task in the console. We recommend that you use the credentials of your BytePlus account to grant permissions. For more information, refer to [Authorize cross-service access](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id=".5Yib5bu6LWVzLeaVsOaNruWvvOWFpeS7u-WKoQ=="></span>
## Create an Elasticsearch data import task

<span id=".5q2l6aqk5LiALeWfuuehgOS_oeaBr-mFjee9rg=="></span>
### Step 1: Configure the basic information


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **Data import** pane, select **Elasticsearch**.

5. Compete the basic information configuration.

   
   |Parameter |Description |
   |---|---|
   |Project |The name of the destination TLS project that you want to use to store the log data imported from Elasticsearch. |
   |Topic name |The name of the destination TLS topic that you want to use to store the log data imported from Elasticsearch.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot specify a dedicated topic that is used for storing service logs or logs of a cloud product.</div><br> |
   


<span id=".5q2l6aqk5LqMLeaVsOaNrua6kOmFjee9rg=="></span>
### Step 2: Configure a data source


1. Configure the data source.

   
   |Parameter |Description |
   |---|---|
   |Task name |The name of the log import task. |
   |ES access url |The endpoint of the Elasticsearch cluster. The value format is `http://host:port/`. |
   |Username |The username of your Elasticsearch cluster account.<br><br>This parameter is required only if user authentication is enabled for the Elasticsearch cluster. |
   |Password |The password that is used for logging on to the Elasticsearch cluster.<br><br>This parameter is required only if user authentication is enabled for the Elasticsearch cluster. |
   |Index list |The indexes that you want to import to TLS. You can specify multiple indexes and separate the indexes with commas ( , ). Eample: `indexA,indexB,indexC`. |
   |ES query |The query statement used to filter data. TLS only imports the data that matches the specified conditions. To import data without filtering, set it to `*` or leave it blank.<br><br>The query statement must comply with the query_string syntax in Elasticsearch. Example: `project:tls and owner:zhangsan`. For more information, refer to [Query string query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html?spm=a2c4g.11186623.0.0.7d377be1bNTZal#query-dsl-query-string-query). |
   |Specify time field |Specify whether to use a column in Elasticsearch as the timestamps of log entries. By default, TLS uses the system time when a log entry is imported as the timestamp of the log entry. You can also enable the **Specify time field** setting and specify the name of the column that indicates time in the Elasticsearch index. Then, TLS uses values in the specified column as the timestamps of log entries.<br><br>If you enable it, you must configure the following parameters:<br><br><br>* **Time field name**: The key of the time field.<br><br>* **Time field format**: The format based on which the value of the time field is parsed. For more information on supported time formats, refer to [Time format](https://docs.byteplus.com/docs/tls/time_format). If the value of the time field is `1651648409`, set the format to `%s`. If the value of the time field is `1651648416882`, set to `%F`. If the value of the time field is `2022-01-01T15:30:00.999+0800`, set the format to `%Y-%m-%dT%H:%M:%S.%f%z`.<br><br>* **Import time range**: The start time and end time of the log data that you want to import. TLS only imports the data with timestamps within the specified time range.<br><br>* **Time zone**: The time zone in which the time specified by the time field resides. |
   |Import mode |The data import mode. Only **Import history log** is supported. The data that is written to Elasticsearch after the import task is created cannot be imported to TLS. After all historical data is imported, the import task automatically ends. |
   |Preview |Click **Execution preview** to view the data that is imported based on the current configuration. If the data previewed does not meet your expectation, modify the configuration and retry. |
   

2. Confirm the configurations, then click **Next step**.


<span id=".5q2l6aqk5LiJLeabtOaWsOe0ouW8lQ=="></span>
### Step 3: Update indexes


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. You can also click **Import existing index configuration** to import the index of other topics.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2) to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.


<span id=".6aqM6K-B5pWw5o2u5a-85YWl57uT5p6c"></span>
## Verify data import results


1. In the left\-side navigation pane, click **Query and analysis**.

2. On the query and analysis page, preview the imported data.

   Data written to TLS becomes available for preview on the query and analysis page after approximately one minute. By default, the log data imported in the last five minutes is displayed. You can also set a custom time range or query statement. If you successfully preview or query the data imported from the Elasticsearch cluster, the import is successful.

   You can also view the status of the import task in the data import task list. For more information, refer to [Creating an Elasticsearch data import task](https://docs.byteplus.com/docs/tls/Importing_data_from_Elasticsearch#.5Yib5bu6LWVzLeaVsOaNruWvvOWFpeS7u-WKoQ==).


<span id=".5p-l55yL5a-85YWl5Lu75Yqh"></span>
## View import tasks

<span id=".5p-l55yL6YWN572u6K-m5oOF"></span>
### View import task details


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. In the **Data import** pane, Click the name of the log import task, then view the task configuration information on the **configuration details** tab. On the **configuration details** tab, you can view the basic information, data source configuration, and log extraction mode of the import task.

   
   |Parameters displayed ||Description |
   |---|---|---|
   |Basic information |Task name |The name of the data import task. |
   ||Task ID |The ID of the data import task. |
   ||Import task status |The status of the import task. For more information, refer to [Task status description](https://docs.byteplus.com/docs/tls/Importing_data_from_Elasticsearch#.5Lu75Yqh54q25oCB6K-05piO). |
   ||Task type |The type of the import task. `Elasticsearch` indicates the task is an Elasticsearch data import task. |
   ||Belonging topic ID |The topic in which the imported data is stored. You can configure an index as prompted on the page. This helps subsequent query, analysis, and statistics collection. |
   ||Created on |The time when the import task was created. |
   |Data source configuration |ES access url |The endpoint of the Elasticsearch cluster. |
   ||Username |The username of your Elasticsearch cluster account. |
   ||Password |The password for logging on to the Elasticsearch cluster. |
   ||Index list |The indexes that you want to import to TLS. |
   ||ES query |The query statement used to filter data. |
   ||Import mode |The data import mode. Only **Import history log** is supported. The data that is written to Elasticsearch after the import task is created cannot be imported to TLS. |
   ||Specify time field |Indicates whether a field in the Elasticsearch index is used to specify the timestamps of log entries. |
   ||Time field name |The key of the time field.<br><br>This parameter is displayed only when the **Specify time field** setting is enabled. |
   ||Time field format |The timestamp format.<br><br>This parameter is displayed only when the **Specify time field** setting is enabled. |
   ||Import time range |The start time and end time of the log data that is imported.<br><br>This parameter is displayed only when the **Specify time field** setting is enabled. |
   ||Time zone |The time zone in which the time specified by the time field resides.<br><br>This parameter is displayed only when the **Specify time field** setting is enabled. |
   


<span id=".5Lu75Yqh54q25oCB6K-05piO"></span>
### Task status description

An import task can be in one of the following statuses:


|Status |Description |
|---|---|
|Importing |The import task is in progress. You can determine the current progress of a task based on the values of the BytesTransferred and BytesTotal fields in the service log. |
|Import complete |The import task is completed. All data that meets the import rules has been successfully imported into the specified TLS topic. |
|Import exception |The import task is exceptional.<br><br>A failure in importing a data entry can lead to the failure of the entire task. Import failures occur if the index is deleted from Elasticsearch, networking failures occur on the Elasticsearch cluster, or other failures occur. In such a case, we recommend that you import the failed data again after resolving the issue that causes the import failure. In addition, you can view the detailed information about the failed index in the service log. For more information on log fields, refer to [Service log fields](https://docs.byteplus.com/docs/tls/service_log_fields). |


<span id="1yL8e62W"></span>
## Copy import tasks

TLS supports replicating data import tasks. When similar data import tasks exist, you can directly copy all configurations of an existing task and then modify the relevant configurations as needed to create a new data import task.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. Select the region where torch log service is located from the top navigation bar.

3. On the left navigation bar, select **Common functions** \> **Log Collection**.

4. in the **Data import** tab's **Task list** area, click **Copy** in the **Operation** column of the task to be copied.

5. Refer to the steps for creating an import task to confirm or modify the relevant parameter configuration.


<span id=".5Yig6Zmk5a-85YWl5Lu75Yqh"></span>
## Delete an import task

If a data import task encounters faults or exceptions, delete the import task and create a new task to import the data. If all existing log data has been imported or you no longer need to import log data into BytePlus TLS, delete the log import task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Deleting a log import task does not affect the log data that has been imported.</div>


* <div data-tips="true" data-tips-type="tip">Once a log import task is deleted, it cannot be restored. Proceed with caution.</div>


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common functions** \> **Log collection**.

4. On the **Data import** tab, find the log import task that you want to delete, then click **Delete** in the **Actions** column.

5. In the pop\-up window, confirm the information about the task to be deleted, then click **Delete**.


<span id=".6Zeu6aKY5aSE55CG5LiO5pWF6Zqc5o6S5p-l"></span>
## Troubleshooting and resolving issues


|Issue |Possible Cause |**Solution** |
|---|---|---|
|The “time out” error appears when previewing log entries. |* The Elasticsearch URL specified in the import task configuration is incorrect or invalid.<br><br>* The IP addresses of the BytePlus TLS servers are not added to the allowlist of the Elasticsearch cluster, and the Elasticsearch cluster denies access requests from BytePlus TLS. |* Check whether the Elasticsearch URL specified in the import task configuration is correct.<br><br>* Check whether the public IP addresses of the TLS servers are added to the allowlist of the Elasticsearch cluster. For more information, refer to [IP address allowlist](https://docs.byteplus.com/docs/tls/consultation_faq_ip_address_allowlist). |
|The “invalid argument” error appears when previewing log entries. |* The `query_string` used is invalid.<br><br>* The username or password configured for accessing the Elasticsearch cluster is incorrect. |* Check whether the query statement complies with the [Elasticsearch syntax](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html?spm=a2c4g.428046.0.0.68041c65lzlJxZ#query-dsl-query-string-query).<br><br>* Check whether the Elasticsearch username and password configured in the task configuration are correct. |
|When previewing imported log entries, you find that the timestamps of the imported log entries are not as expected. |The log time field is not configured or the specified format is incorrect. |Enable the **Specify time field** setting and set a correct time format. For supported time formats, refer to [Time format](https://docs.byteplus.com/docs/tls/time_format). |
|After log data is imported, you fail to retrieve certain log entries. |The log indexes are created after the log import task was started. Therefore, the indexes do not take effect on the log entries that were imported before indexing is enabled. |Log indexes are only effective for the log entries collected after indexing is enabled. New index configurations after modifications also only take effect on the log entries that are collected after the modifications. We recommend that you create indexes for the destination topic before you create an import task. |

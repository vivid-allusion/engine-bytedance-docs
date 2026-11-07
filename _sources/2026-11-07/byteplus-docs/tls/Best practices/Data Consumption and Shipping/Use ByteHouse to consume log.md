---
title: "Use ByteHouse to consume log"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_bytehouse_to_consume_logs"
---

ByteHouse supports using Kafka to transfer data in a streaming manner. This topic introduces how to use the Kafka protocol to write log data from Torch Log Service (TLS) to ByteHouse for consumption.

<span id="背景信息"></span>
## Background

TLS supports using the Kafka protocol to consume log data from specified topics. For example, the log data is written to ByteHouse for further analysis and processing. After you create a Kafka data import task in ByteHouse, data can be transferred through Kafka in a streaming manner. The data import task runs automatically, continuously reading log data from topics and writing the data into specified database tables.

Only some of the fields can be consumed, and settings such as the maximum message size can be configured. In addition, you can stop the data import task to reduce resource usage and resume the task if necessary. ByteHouse records offsets internally to ensure that no data loss occurs during the stop and resume processes.

<span id="费用说明"></span>
## Cost information

Consuming logs through ByteHouse incurs TLS read traffic fees. We recommend that you use a private endpoint to consume log data.

After logs are written to ByteHouse for consumption, storage fees are incurred on the ByteHouse side. If you query and analyze the logs in real time, compute fees are also incurred.

<span id="前提条件"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create resources](https://docs.byteplus.com/docs/tls/getting_started_creating_resources)

* Enable the feature of consumption using the Kafka protocol for the specified topic, and get **Kafka protocol consumer topic ID**. For more information, refer to [Use the Kafka protocol to consume logs](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs).

* We recommend that you use an IAM user for authentication. Before using an IAM user, make sure the IAM user is created by the BytePlus account and granted the required consumption permissions. For more information, refer to [Authorizable actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).

* Get the AccessKey pair of the current login account. For more information, refer to [Create an AccessKey pair](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).


<span id="注意事项"></span>
## Precautions

When you consume logs through ByteHouse, the maximum log size that can be consumed is 128 KB. Logs exceeding this limit cannot be consumed. This limit is specified by the Max Block Size parameter of the data import task, ranging from 65,536 to 131,072 bytes, with a maximum size of 128 KB.

<span id="导入日志到-bytehouse"></span>
## Import logs into ByteHouse

The ByteHouse console offers two versions of the **Data Loading** screen: an old version and a new version. This topic uses the old version of the **Data Loading** screen as an example to demonstrate how to create a Kafka data source and a data import task.


1. Log on to the ByteHouse console.

2. Create a database.

   1. On the upper\-left corner of the database page, click **New Database**.

   2. Configure the basic database information.

      
      |Parameter |Description |
      |---|---|
      |Database Name |The database name. |
      |Database Description |The database description. |
      

   3. Click **Create**.

3. Create a data table.

   1. On the details page of the specified database, click the **Tables** tab.

   2. On the upper\-right corner of the page, click  **+ Table**.

   3. Select **SQL or By Visualization**.

   4. On the **SQL** or **By Visualization** tab, set **Column Name** and **Data Type**.

      Design a new table schema based on the structure of source logs in TLS. We recommend that you only create columns required for storage or subsequent analysis.

   5. Click **Create Table**.

4. Create a Kafka data source.

   1. In the top menu bar, click **Data Loading**.

   2. On the upper\-left corner of the page, click **Data Sources**.

   3. On the **Data Sources** page, click  **+ Connect Data Source**.

   4. Select **Kafka Data Stream** as the data source type.

   5. Specify the basic information of the Kafka source.

      
      |Parameter |Description |
      |---|---|
      |Source Name |Specify a name for the Kafka data source. |
      |Kafka Broker list IP address |Specify the initial cluster connection URL, in the format of `Endpoint:Port number`, such as `tls-ap-southeast-1.ibytepluses.com:9093`. In this example:<br><br><br>* The endpoint is the endpoint of TLS in the current Region. Select the correct endpoint based on the Region and network type. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). We recommend that you use a private endpoint to reduce traffic costs.<br><br>* The port number is fixed to 9093. |
      |Auth Mode |Set the authentication mechanism. Keep the default setting as **PLAIN**. |
      |SSL |Specify whether to enable SSL. It is enabled by default. Keep the default setting. |
      |Username |Set it to the TLS project ID. |
      |Password |Set it to the AccessKey pair of your BytePlus account, in the format of `${access-key-id}#${access-key-secret}`, where:<br><br><br>* `${access-key-id}`: Replace it with your AccessKey ID.<br><br>* `${access-key-secret}`: Replace it with your AccessKey secret.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the current login user is an IAM user, set it to the AccessKey pair of the IAM user.</div><br> |
      

   6. Click **Connect**.

5. Create a data import task.

   1. In the top menu bar, click **Data Loading**.

   2. On the upper\-left corner of the page, click **New Loading Job**.

   3. Configure the **General Information**.

      
      |Parameter |Description |
      |---|---|
      |Job Name |Specify a name for the data import task. |
      |Description |Specify a description of the data import task. |
      

   4. Select a data source.

      
      |Parameter |Description |
      |---|---|
      |Type |Select **Kafka Data Stream**. |
      |Data Source |Select the Kafka data source created in Step 4. |
      |Topic |Specify the topic ID for consumption using the Kafka protocol, in the format of **`out-log topic ID`**, such as `out-0fdaa6b6-3c9f-424c-8664-fc0d222c****`. Alternatively, on the topic details page in the TLS console, view and copy **Kafka protocol consumer topic ID**. |
      

   5. Select a **destination table**.

      
      |Parameter |Description |
      |---|---|
      |Target Database |Specify the name of the database that stores TLS log data in ByteHouse. |
      |Target Table |Specify the name of the data table that stores TLS log data in ByteHouse. |
      

   6. Define the schema mapping. Set the mappings between log data fields in TLS and the fields in the ByteHouse data table. After the mappings are set, the specified fields are stored in ByteHouse with the corresponding column names and data types.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If log data exists in a topic, click <strong>Re\-Parser</strong> to automatically parse the data.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the table schema does not meet your needs, click <strong>Edit Target Table</strong> to modify the schema of the destination table.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The source column name and data type of a field must exactly match those of the corresponding field in the source log data. Otherwise, the field cannot be imported.      </div>
      

   7. Set **Default job execution settings**.

      
      |Parameter |Description |
      |---|---|
      |Loading Type |Specify how to load data. Currently, only **Append Data** is supported. Each time the job runs, log data is incrementally written to the destination table, without overwriting existing data. |
      |Max Block Size |Specify the maximum message size. Unit: bytes. The value range is 65,536 to 131,072 bytes, with a maximum size of 128 KB. |
      

   8. Click **Create**.

      After a data import task is created, it automatically runs to continuously consume log data from TLS through the Kafka protocol in a streaming manner.


<span id="查看导入任务"></span>
## View import tasks

On the **Data Loading** page, you can view the run information of real\-time data import tasks. To view the details of an import task, click the name of the task.


|Parameters displayed ||Description |
|---|---|---|
|Basic information |Data Source |The name of the Kafka data source. |
||Topic |The topic of the Kafka data source, that is, the TLS topic for consumption using the Kafka protocol. |
||Consumer Group |The name of a consumer group in ByteHouse. |
||Target Table |Specify the name of the data table that stores TLS log data in ByteHouse. |
||Total Ingested Records |The number of imported log records. |
||Created On |The date when the import task was created. |
|Sync History ||Each time a task is paused and restarted, the system creates an execution record in the back end. On the **Sync History** tab, you can view all the execution records of the task, including **Execution ID**, **Sync Start Time**, **Status**, **Duration**. You can also view the daily imported record changes over the past 14 days. |
|Schema Mapping ||The schema mapping information. |
|Consuming ||By default, the consumption status over the past 15 minutes is displayed for the import task. |
|Error Log ||By default, the errors in all execution records of the import task are displayed. |
|Config ||By default, the import task configurations in JSON format are displayed. |


<span id="同步状态说明"></span>
## Synchronization status

The following table describes the synchronization status of a data import task:


|Status |Description |
|---|---|
|Provisionning |After the data import task starts, the back end is allocating the corresponding compute resources. After the resources are allocated, the task status changes to running. |
|Running |The data import task is running properly. |
|Stop |The data import task stops. |
|Fail |The data import task failed. Possible reasons include configuration conflicts or data errors. We recommend that you verify the configuration and data source before restarting the import task. |


<span id="常见问题"></span>
## FAQs

<span id="新建-kafka-数据源时报错无法连接到-broker"></span>
### Cannot connect to the broker when creating a Kafka data source


* **Issue description**: When you create a Kafka data source in Step 4, the error "kafka connectivity test failed, ping failed with err: kafka: client has run out of available brokers to talk to...” is prompted.

* **Possible causes**: The feature of consumption using the Kafka protocol is not enabled for the topic, or **Kafka Broker list IP address**, **Username**, or **Password** is incorrect.

* **Solution**:

   * To enable the feature of consumption using the Kafka protocol for a specified topic, refer to [1 Enable the feature of using the Kafka protocol for consumption](https://docs.byteplus.com/docs/tls/use_the_kafka_protocol_to_consume_logs#_1-%E5%BC%80%E5%90%AFkafka%E6%B6%88%E8%B4%B9%E5%8A%9F%E8%83%BD).

   * Set the related parameters correctly.

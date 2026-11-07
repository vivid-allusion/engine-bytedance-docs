---
title: "Streaming import"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/streaming-import"
---

ByteHouse Enterprise supports real\-time data writing via Kafka. This tutorial describes how to use the ByteHouse Enterprise Edition console to import data from Kafka streams.

<span id="656750dc"></span>
# Function overview

Compared with inserting data via the engine (INSERT), the Kafka streaming import feature in the ByteHouse Enterprise console has the following characteristics:


* Supports at\-least\-once semantics, enables automatic failover between primary and standby write operations, and ensures stable high availability.

* Data is automatically balanced and imported into ByteHouse shards according to Kafka partitions, without the need to configure a shard key.

* By default, data consumption becomes visible after 8 seconds. Both efficiency and real\-time capability are taken into account.


For more information about the implementation principles, please refer to [HaKafka](https://docs.byteplus.com/docs/bytehouse/hakafka).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended that the Kafka version you use meets the following requirements; otherwise, data loss may occur during data consumption. For details, see <a href="https://issues.apache.org/jira/browse/KAFKA-9543">the Kafka Community Issue</a>.</div>



* <div data-tips="true" data-tips-type="warning"><code>>= 2.5.1</code></div>


* <div data-tips="true" data-tips-type="warning"><code>>= 2.4.2</code></div>



<span id="da0054e8"></span>
# Prerequisites


* Before importing Kafka data into ByteHouse, ensure that the Kafka account and password you are using have the following data permissions:

   * List topics

   * List consumer groups

   * Consume messages

   * Create consumers and consumer groups

* Obtain the IP address, username, and password for each proxy in the Kafka data source proxy list. If you need to access BytePlus Message Queue for Kafka through a private network, you must also obtain the VPC ID where the Kafka data source is located.

* In ByteHouse, make sure to create the target database and tables according to the structure of the source table. For details, see [Create a new database/table](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table).


<span id="03be7d5f"></span>
# Cautions


* When importing data from a Kafka data source into ByteHouse, if you access via the public network, related charges will apply. We recommend that you thoroughly review the billing rules for the service you use before using it.

* It is recommended to use private network access for BytePlus Message Queue for Kafka or BytePlus Cloud Native Message Engine BMQ service. When using the service, ensure that the service you are using is in the same region as the ByteHouse instance to maintain data transmission efficiency and avoid additional costs from cross\-region access.


<span id="ed111ce0"></span>
# Steps

<span id="0fc78ee2"></span>
## Create a data source


1. Log in to the ByteHouse Enterprise Edition console, click **Data Import**, and in the upper right corner, select the appropriate **cluster**.

2. Click the "+" in the **Data source** module, create a new data source, and select Kafka as the data source type.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d01b8036aaff4fa39f8d7b4bc629f5f4~tplv-goo7wpa0wc-image.image) </span>


<span id="d947be4b"></span>
## Configure a data source


1. In the data source configuration interface on the right, follow the on\-screen instructions to enter the following information in sequence:

   
   |Parameter items |Note |
   |---|---|
   |Source type |Select Kafka data source type. |
   |Source name |Task names must be unique and cannot duplicate those of other tasks. |
   |The Kafka broker list |Enter the corresponding Kafka Broker address. When filling in, **be sure to enter the IP addresses of all Broker nodes for the access point you are using**. If you need to enter multiple Broker addresses, separate them with commas (,). For example, `10.100.19.127:9092, 10.100.19.127:9093`. |
   |Authentication modes |The current Kafka data source supports four authentication modes: NONE (no authentication), PLAIN, SCRAM\-SHA\-256, and SCRAM\-SHA\-512. SSL encryption is also supported. You can select the appropriate option based on the port number of the IP address in the Kafka broker list. The mapping is as follows:<br><br><br>* **None (no authentication)** : The port number is 9092.<br><br>* **PLAIN、SCRAM\-SHA\-256、SCRAM\-SHA\-512**：<br><br>   * If SSL is not enabled, the port number is 9093.<br><br>   * If SSL is enabled, the port number is 9095. |
   |Security protocol |Supports selecting SASL_PLAINTEXT and SASL_SSL protocol types. |
   |Usernames and passwords |Enter the username and password that are authorized to access the Kafka instance. |
   

2. After you have entered the data source information, click the **OK** button to test the data source connectivity. If the test is successful, this means the data source has been created successfully.


<span id="6b1944e4"></span>
## Create import tasks


1. Under the Kafka data source, click **Create import task** to enter the new import task configuration interface, and complete the following configuration information:

   
   |Parameters |Note |
   |---|---|
   |**General information** ||
   |Task name |Enter the import task name. Numbers, letters, and underscores are supported, but the name cannot begin with a number. The maximum length is 128 characters, and the name must not duplicate any existing task. |
   |Description |Enter relevant descriptive information for this import task to facilitate subsequent maintenance and management. |
   |**Select data sources** ||
   |Source type |Choose a Kafka data source type. |
   |Data source |Select a successfully created Kafka data source from the dropdown menu.<br><br>If there is no data source that meets the requirements, you can click the **Create data source** button to go to create a new data source. |
   |Topic |Select existing Topic information from the Kafka data source using the dropdown. |
   |Group name |Optional. The Kafka Consumer Group name. If left blank, the system will automatically generate the Group name. |
   |Automatically reset offset |This refers to the offset from which consumption of the latest data produced by Kafka begins when a task is started for the first time. When the task is started again, consumption resumes from the offset where it was previously paused. |
   |Format |The most commonly used message format at present is JSONEachRow. |
   |Delimiter |Enter a message delimiter, typically '\n'. |
   |Number of consumers |Number of consumers; each consumer will create a thread. |
   |Write block size |The size of the write block. |
   |**Select the target table** ||
   |The target database |Select the target ByteHouse database for data import from the dropdown. |
   |Target data tables |Select the target ByteHouse table for data import from the dropdown menu. |
   |**Target schema configuration** ||
   |Extract a schema |Configure the mapping between Kafka information and ByteHouse table information here. It is recommended to use the "data mapping" feature, and sample Kafka messages using the **JSON** or **SQL** method for automatic matching. When adding field mappings, you can choose either **overwrite** or **incremental addition**. Matching must comply with the following rules:<br><br><br>* The source column and target column must be of the same type. ByteHouse does not support implicit type conversion. If the types do not match, you can perform the conversion using an "**expression**". For example, if the source column `a` is of Integer type and the target column is of String type, you need to enter `toString(a)` in the expression. Common type conversion functions can be found at [Type Conversion Function](https://docs.byteplus.com/docs/bytehouse/type-conversion-function).<br><br>* In the target columns, columns that cannot be null must have a corresponding source column. Nullable columns can be deleted here. |
   

2. After all source columns and target columns have been matched, click the **Submit** button in the lower right corner of the page. After submission, you can view the new import task under the corresponding data source in **Data Import**. After the task is created, the Kafka consumption task will start immediately.

3. Click the import task name to view the current execution status of the import task, including task execution ID, start time, duration, number of imported records, and other information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bd71dea152749b08928183a6dea1533~tplv-goo7wpa0wc-image.image) </span>


<span id="054defe2"></span>
## View execution plans

After the import tasks are created, you can view the detailed execution status of all import tasks in the **Execution plan**. You can click **Execution ID** to view the execution details of a specific task.

In the data import interface, click the **Execution Plan** button on the left to enter the execution plan list. You can filter execution plans using the following filter options:


* You can search for the corresponding execution plan by entering the task name or execution plan ID.

* You can also quickly filter execution plans by importing information such as task **status**, **time range**, **target data table**, **source type** and other information, and selecting the relevant content from the dropdown menu.

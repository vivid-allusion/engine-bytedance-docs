---
title: "Read Kafka data and write it into TOS"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Kafka_to_TOS"
---

BytePlus Flink is a fully managed streaming computing platform compatible with Apache Flink, supporting efficient real\-time data processing of massive data. LAS is a serverless Lakehouse data platform that provides massive data storage, management, computation, and interactive analysis capabilities. This article simulates a scenario demonstrating the interworking of Flink and LAS, thereby experiencing cross\-source query analysis and automatic metadata discovery capabilities.

<span id="45013ba7"></span>
## Scenario Introduction

The simulated scenario in this article mainly achieves: reading message queue Kafka data, writing it into object storage TOS, and mapping it as a Lakehouse analytic service LAS external table for data analysis.

In the Flink console, develop a Flink SQL task to implement the data flow chain from Datagen \-\> Kafka \-\> TOS, then create an external table in the LAS console, read files from the TOS data source, and map them to the newly created external table.

<span id="9c640d5f"></span>
## Precautions


* When writing files to TOS via a Flink task, use the filesystem connector. To ensure data consistency and fault tolerance, **enable Checkpoint** in the Flink parameter settings.

   If Checkpoint is not enabled, only temporary files will be written in the TOS Bucket, making data mapping to external tables impossible.

* The LAS external table data is updated, but the metadata is not automatically updated; you can configure a metadata discovery task to periodically update the metadata. However, the metadata discovery task has strict requirements for the TOS path format, which needs to be either `bucket/library/table/file` or `bucket/library/table/partition/file`.

   In this document, the TOS path format is defined as: `tos://doc_bucket/las_db/las_table_1` *.* 

* To ensure the security of network access, the cloud product services used in this document all use an internal network access mode, thus requiring the Flink resource pool, Kafka instances, TOS Bucket, and LAS external tables to be in the same region and the same VPC.


<span id="389c507f"></span>
## Prerequisites


* Create a Flink resource pool in advance, for related documents, please see [Create VCI resource pool](https://docs.byteplus.com/docs/flink/Create_VCI_resource_pool).

* Create Kafka instances, Topics, Groups, SASL Plain users in advance, and obtain the SASL_PLAINTEXT access point address of the Kafka instances; for related documents, please see [create Kafka instance](https://docs.byteplus.com/en/docs/kafka/creating-instance), [create Topic](https://docs.byteplus.com/en/docs/kafka/creating-topic), [create Group](https://docs.byteplus.com/en/docs/kafka/creating-group), [create SASL Plain user](https://docs.byteplus.com/en/docs/kafka/creating-SASLuser).

* Create TOS buckets and file paths in advance, using LAS database name and LAS table name as file paths; for related documents, please see [create bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket), [create folder](https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder).


<span id="ee994884"></span>
## Develop Flink SQL tasks


1. Log in to the [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar, then enter the project from the **project management** page.

3. Create a Flink SQL task.

   1. In the project's left sidebar, select **Task Development \> Tasks**, then click the plus button to create a task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/895387b71c97495f8b4ab2a91c93b15a~tplv-goo7wpa0wc-image.image" width="532px" /></div>



2. In the **Create Task** dialog, set the task name, type, folder, and engine version, then click **OK**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/321aa3ee98aa4d338df424103319c566~tplv-goo7wpa0wc-image.image" width="544px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fd87a77c19445f5a5258184a2e1d876~tplv-goo7wpa0wc-image.image" width="528px" /></div>


```Plain Text
  | | | \
  |**Configure** |**Description** |
  |---|---|
  | | | \
  |Task Name |Customize the task name, such as "datagen-kafka-tos". |\
  | |The name must be 1-48 characters long and can include digits, uppercase and lowercase English letters, underscores (_), hyphens (-), and periods (.). It must start and end with a digit or letter. |
  | | | \
  |Task Type |Select **Flink Task > Flink Stream > SQL**. |
  | | | \
  |Associated Folder |The system offers folder management functions for categorizing and managing tasks. |\
  | |You can directly select the default **Data Development Folder** or use a custom-created folder. |
  | | | \
  |Engine Version |Choose the engine version as needed; this document selects **Flink 1.16-byted** version. |
  | | | \
  |Task Description |Enter the description of the task, which generally describes the functionality implemented by the task. |
```



3. Write the business logic code for the SQL task in the task editing area.

   The sample code means: Write random numbers generated in real\-time by the Datagen connector into a Kafka Topic; then read the Kafka Topic data and output it to a TOS Bucket.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When writing files to TOS, use the filesystem connector. If you need to see the files written to TOS Bucket as soon as possible and ensure data consistency, additional configuration is required. You can set the connector's <strong>sink.rolling\-policy.file\-size</strong>, <strong>sink.rolling\-policy.rollover\-interval</strong> parameters, and enable <strong>Checkpoint</strong> in the Flink parameter configuration.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For more details on the rolling strategy of the Filesystem connector, please refer to the open source document <a href="https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/connectors/filesystem.html#rolling-policy">Filesystem\-Rolling Policy</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In a task, if there is a table that serves as both source and sink, we suggest you directly verify the SQL accuracy to ensure correctness before conducting tests online. If you perform debugging operations, you may encounter error messages like <code>Table:xxx should not be both source and sink.</code>.   </div>
   

   ```SQL
   create table orders (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time as localtimestamp
   ) WITH (
    'connector' = 'datagen',
    'rows-per-second'='1',
    'fields.order_status.length' = '3',
    'fields.order_id.min' = '1',
    'fields.order_id.max' = '10000',
    'fields.order_product_id.min' = '1',
    'fields.order_product_id.max' = '100',
    'fields.order_customer_id.min' = '1',
    'fields.order_customer_id.max' = '1000'
   );
   
   create table kafka_table (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp
   ) WITH (
       'connector' = 'kafka', 
       -- The security protocol is set to SASL_PLAINTEXT。
       'properties.security.protocol' = 'SASL_PLAINTEXT',  
       -- The SASL mechanism is PLAIN。
       'properties.sasl.mechanism' = 'PLAIN', 
       -- Configure JAAS。
       'properties.sasl.jaas.config' = 'org.apache.flink.kafka.shaded.org.apache.kafka.common.security.plain.PlainLoginModule required username="doc-user" password="qaP***6";',
       -- The SASL_PLAINTEXT access point for the Kafka instance
       'properties.bootstrap.servers' = 'kafka-***hd8md.kafka.byteplus.com:9093',
       --Group and Topic
       'topic' = 'topic-b', 
       'properties.group.id' = 'group-b', 
       -- The start mode for reading data. "earliest-offset" means reading from the earliest partition
       'scan.startup.mode' = 'earliest-offset',
       -- The interval for periodically scanning and discovering new topics and partitions.
       'scan.topic-partition-discovery.interval' = '120s', 
       'format' = 'json',
       -- Turn off idempotence
       'properties.enable.idempotence' = 'false'
   );
   
   
   insert into kafka_table 
   select * from orders;
   
   
   CREATE TABLE tos_sink (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar,
       order_update_time timestamp,
       dt STRING,
       `hour` STRING
     ) PARTITIONED BY (dt, `hour`)
   WITH (
     'connector' = 'filesystem',   -- Use the filesystem connector when accessing TOS resources.
     'path' = 'tos://wuch-doc-tos/las_db/las_table_1',  -- tos path, which consists of Bucket name and folder name. The folder name is LAS DB and Table name.
     'sink.rolling-policy.file-size' = '1M',  -- The maximum file memory limit. When this value is reached, the file is closed and a new file is opened for writing.
     'sink.rolling-policy.rollover-interval' = '5 min',  -- The file continues to be written for a certain period of time. When this value is reached, the file is closed and a new file is opened for writing.
     'format' = 'parquet'
   );
   
   
   insert into tos_sink
   select   
     order_id,
     order_product_id,
     order_customer_id,
     order_status,
     order_update_time,
     DATE_FORMAT (order_update_time, 'yyyy-MM-dd') as dt,
     DATE_FORMAT (order_update_time, 'HH') as `hour` 
     from kafka_table;
   ```
   

4. At the top of the code editing area, click the **verify** button.

   The system will automatically verify the correctness of your SQL statements, if errors occur, please modify the SQL statements based on the prompts given. After the inspection passes, the system displays `success`.

5. Enable Checkpoint.

   At the top of the code editing area, click **Parameter Configuration**, then enable Checkpoint.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a2defb6319e4bc0940c7338825618ac~tplv-goo7wpa0wc-image.image" width="556px" /></div>



5. Launch the task.

   1. Set the **execution mode** and **engine version**, then click **launch**.

      In this scenario, the execution mode is set to **STREAMING**, and the engine version is set to **Flink 1.16\-byted**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bdfd17213484a168e93a30a4f83d2bf~tplv-goo7wpa0wc-image.image" width="530px" /></div>



2. In the **Task Launch Settings** dialog, select the runtime resource pool, set task priority and scheduling strategy, then click **confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/302114602f064eb69cc13cf3f11323fb~tplv-goo7wpa0wc-image.image" width="668px" /></div>


```Plain Text
  | | | \
  |**Configuration** |**Description** |
  |---|---|
  | | | \
  |Execution Resource Pool |Select the Flink resource pool for task execution from the dropdown list. |
  | | | \
  |Task Priority |\
  | |The system's default preset priority is L3. You can set the task priority as needed, where a smaller number indicates a higher priority. |\
  | |Task priority determines the scheduling order within the task, with tasks of higher priority being scheduled first, meaning L3 is scheduled before L4. |
  | | | \
  |Scheduling Strategy |Configure the task scheduling strategy based on requirements: |\
  | | |\
  | |* GANG: Ensures that all instances of a task are scheduled together, meaning resources are allocated only when remaining resources meet the needs for normal task operation; if not, resources are not allocated. |\
  | |   This strategy prevents the phenomenon of resources being allocated but the task fails to start, thus solving the resource deadlock issue. |\
  | |* DRF: Considers multiple dimensions of resources, more rationally distributing resources evenly among tasks in the resource pool to enhance utilization. |\
  | |   For example: With 10 cores and 40 GB of resources remaining, Task A requires 10 cores and 20 GB of resources; Task B requires 2 cores and 8 GB of resources. If allocated to A, the remaining 0 cores and 20 GB of resources cannot be utilized; the DRF strategy would choose to allocate to B, leaving 8 cores and 32 GB available for subsequent tasks. |
  | | | \
  |Scheduling duration |\
  | |When set to GANG scheduling strategy, it is necessary to set the scheduling duration. |\
  | |If it exceeds the scheduling duration, the task will fail to schedule. If set to 0, it will retry indefinitely. |
```



6. Start the task.

   1. In the project's left navigation bar, select **Task Operations & Management \> Task Management**, then click the **start** button next to the target task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4afcd85079af40179f988648fd66015a~tplv-goo7wpa0wc-image.image" width="548px" /></div>



2. In the **Start Task** dialog, select **Start Fresh**, then click **confirm**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35ef94b135dc46588475b069107b7e92~tplv-goo7wpa0wc-image.image" width="530px" /></div>


```Plain Text
  Task initiation requires some time, please be patient. Once started successfully, the status will be **Running**.
```


<span id="159d9f5a"></span>
## Flink SQL Task Result Verification

Develop Flink SQL tasks through the Flink console to achieve the data flow link from Datagen \-\> Kafka \-\> TOS. You can verify the results of the task in the following three ways:


* Method One: Check the Flink UI

* Method Two: Query Kafka Topic messages

* Method Three: Check the TOS Bucket files


<span id="b542de57"></span>
### Method One: Check the Flink UI

After the Flink SQL task is running normally, you can enter the Flink UI page to view the task's execution.


1. In the BytePlus Flink console, select **Task Operations \> Task Management** from the navigation bar on the left. Then, click on the Flink UI behind the target task.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aafb1f73428f40429c0bc35aef66e665~tplv-goo7wpa0wc-image.image" width="578px" /></div>



2. The browser will automatically open the Flink UI page where you can view the task details.


<span id="bba2f94f"></span>
### Method Two: Query Kafka Topic Messages

Once the Flink SQL task is running normally, you can view the data in the target Topic on the Kafka console.


1. Log in to the [Message Queue Kafka console](https://console.byteplus.com/kafka).

2. On the **Instance List** page, click the instance name to enter the Kafka instance details page.

3. Under the **Message Query** tab, select **Query by Offset** or **Query by Time** to investigate the data in the Topic.

   For detailed information on querying Kafka Topic messages, please refer to [Message Query](https://docs.byteplus.com/en/docs/kafka/message-query).


<span id="fa8c0161"></span>
### Method Three: View TOS Bucket Files

Once the Flink SQL task is running smoothly, you can view the files in the target path on the TOS Bucket.


1. Log in to the [object storage console](https://console.byteplus.com/tos).

2. On the **bucket list** page, click the target storage bucket to enter the storage details page.

3. On the file list page of the storage bucket, enter the target folder and view the details of the written files.

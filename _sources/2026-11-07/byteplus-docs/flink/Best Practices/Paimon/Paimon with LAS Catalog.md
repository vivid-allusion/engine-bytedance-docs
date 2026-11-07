---
title: "Paimon with LAS Catalog"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Paimon_with_LAS_Catalog"
---

<span id="56ad0a68"></span>
## 1. Overview

Apache Paimon is an innovative streaming data lake storage technology, which combines LSM\-Tree structure with lake formats to provide high throughput, low\-latency data ingestion, complete streaming change subscriptions, and efficient OLAP querying capabilities. This manual will guide you on how to use the Flink engine for development tasks in Paimon, utilizing [LAS Catalog](https://www.volcengine.com/docs/6492/1263498) to manage the metadata of Paimon Lake universally.

<span id="d4e7839f"></span>
## 2. Environment Preparation

<span id="c560fc57"></span>
### 2.1 Activate Serverless Flink and LAS Catalog

Ensure that you have:


1. Activated **BytePlus Flink** and can create Flink SQL tasks in job development.

2. Purchased on\-demand or subscription\-based resource pools in **Resource Management \- Resource Pool**, and can submit Flink tasks normally.

3. Activated the LAS Catalog for unified metadata management services, and refer to the [LAS Catalog activation document](https://www.volcengine.com/docs/6492/1264537).


<span id="cb1803e0"></span>
### Flink Version Requirements


* Flink version must be \>= 1.16; supported features are as follows:

   * Flink 1.16 comes with Paimon 0.6 built\-in.

   * Flink 1.17 is equipped with Paimon 0.8.2 byte\-enhanced version, supporting syntax such as stored procedures.


<span id="7556e917"></span>
### Create Flink SQL Task

**Operation Path**: Job Development \- Flink SQL Job \- Create Job.

**Reference Document**: [Flink SQL tasks](https://docs.byteplus.com/docs/flink/Flink_SQL_tasks)

&nbsp;

<span id="a563b011"></span>
## Create Catalog

**Prerequisites**: As Flink syncs LAS metadata, it requires access through an API interface. Needs


1. Manage API key to create AccessKey / AccessKeySecret for sub\-accounts (These will be filled in later in hive\-site.xml).

2. Grant LASFullAccess permissions for sub\-accounts in permission management.


<span id="00902495"></span>
### 3.1 Creation and Authorization of LAS Data Directory

Create Paimon's Data Directory in LAS Catalog product, refer to [Data Directory Management](https://www.volcengine.com/docs/6492/1264529) for data directory creation. Name and storage location of the data directory need to be filled in.

> Note: The TOS buckets and directories need to be created in advance and must match the directory address in Flink SQL.


Also, in LAS Catalog permission management module, choose to authorize the newly created Catalog. Reference [Permission Management](https://www.volcengine.com/docs/6492/1264534) for permission allocation. Because it will be necessary to use Flink for database table creation and data writing operations later on. Therefore, it is advised to grant Admin permissions for Catalog to Flink developers. Ensure that the following tasks can be performed.

<span id="cc79f6b9"></span>
### Task 3.1: Upload Dependency Files


1. **Operation Path**: Console \- Enter Project \- Job Development \- Create SQL/CDC Task \- Parameter Configuration (Right\-hand Button) \- Dependency Files.

2. **Prepare Dependency Files**:

   1. Download the LAS Catalog Connector.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9595d5a70fe94ed0874ebf8d69ec389e~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT.jar">flink-sql-connector-hive-las-formation-3_2.12-1.16-byted-connector-SNAPSHOT.jar</Attachment>



2. Download the hive\-site.xml file template (the filename must remain exactly the same) and modify the relevant access and authentication information.


```XML
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <!--
  `metastore.catalog.default`  hive catalog name
  -->
  <property>
    <name>metastore.catalog.default</name>
    <value>paimon_test</value>
  </property>
  <property>
    <name>hive.server2.max.start.attempts</name>
    <value>5</value>
  </property>
  
  <!--
  `hive.client.las.region.name` las and flink region
  `hive.metastore.uris` the thrift address of las, should notice region
  -->
  <property>
    <name>hive.client.las.region.name</name>
    <value>cn-shanghai</value>
  </property>
  <property>
    <name>hive.metastore.uris</name>
    <value>thrift://lakeformation.las.cn-shanghai.byteplus.com:48869</value>
  </property>

  <property>
    <name>hive.hms.client.is.public.cloud</name>
    <value>true</value>
  </property>

  <!--
  `hive.client.las.ak/sk` are the AccessKeyId and AccessKeySecret for LAS service access. Please ensure the sub-account has LAS IAM permissions and Catalog data permissions before configuration.
  -->
  <property>
    <name>hive.client.las.ak</name>
    <value>__LAS_ACCESS_KEY__</value>
  </property>
  <property>
    <name>hive.client.las.sk</name>
    <value>__LAS_ACCESS_KEY_SECRET__</value>
  </property>
</configuration>
```



3. **Upload Dependency Files**: As shown in the figure, perform the file upload operation:


<span id="1a6166c8"></span>
### Task 3.3: Create LAS Catalog in Flink

The LAS Catalog provides a metadata thrift interface compatible with Hive. Thus, the method of using LAS Catalog in Flink is very similar to the method based on Hive Catalog. We can create the LAS Catalog with the following SQL:

```SQL
 CREATE CATALOG ${catalog_name} WITH (
    'type' = 'paimon',
    'metastore' = 'hive',
    -- The URI should be filled with the LAS internal network address as follows, with different regions for reference:
    'uri' = 'thrift://lakeformation.las.cn-guangzhou.byteplus.com:48869',
    'hive-conf-dir' = '/opt/tiger/workdir',
    'warehouse' = 'tos://${bucket_name}/${catalog_name}'
);
```


Two variables need to be defined as follows:


* `${catalog_name}`: The name of the Catalog, which needs to be consistent with the Catalog name in LAS.

* `${bucket_name}`: The name of the TOS (object storage) bucket for storing Paimon data.


The meaning of the WITH parameters is as follows:


* `type`: Select the Paimon type for the Catalog.

* `metastore`: Choose Hive for metadata management.

* `uri`: The metadata thrift interface for the LAS Catalog, you can refer to the address in the example and change `cn-guangzhou` to the same region as the Flink service.

* `hive-conf-dir`: Specifies the file path for hive\-site.xml. **Note**: According to the testing scheme in this document, you must fill in `/opt/tiger/workdir` here.

* `warehouse`: Maintain consistency with the data directory storage location in the LAS Catalog.


<span id="7ee094e2"></span>
## Create Database and Table

<span id="c5796924"></span>
### Create Database

Create a Database in the Catalog to organize and manage tables.

```SQL
CREATE DATABASE IF NOT EXISTS ${catalog_name}.${db_name};
```



* `${db_name}`: Customizable name of the Database.


<span id="9f446937"></span>
### Create Non\-Partitioned Table

Create a table within the Database, defining its structure and related settings. Here is an example of a non\-partitioned Primary Key table

```SQL
CREATE TABLE IF NOT EXISTS `${catalog_name}`.`${db_name}`.`${table_name}` (
    word varchar, -- Example field
    cnt bigint,
    PRIMARY KEY (word) NOT ENFORCED
) WITH (
    'bucket' = '4',  -- Control bucket count, recommend ~1GB data per bucket
    'changelog-producer' = 'input', -- Generate changelog for downstream streaming reads
);
```



* `${table_name}`: Customizable name of the table.

* `bucket`: Recommended number of buckets, with each bucket storing about 1GB of data.

* `changelog-producer`：

   * Set as `input`, indicating that it generates data based on upstream additions, for downstream stream reading. For specific reference [Changelog output mechanism](https://docs.byteplus.com/docs/flink/Connector_Paimon#79d03b88) make detailed choices. If a changelog is not required, use the `none` option to save storage and writing resources.


<span id="2a3ee186"></span>
### Create partitioned tables

Create tables in the Database, define table structures and related configurations. Here is an example of a partitioned table for a Primary Key table:

```SQL
CREATE TABLE
  IF NOT EXISTS paimon_test1.test_db5.test_table5 (
    word varchar, -- Example field
    cnt bigint,
    dt STRING,
    hh STRING,
    PRIMARY KEY (dt, hh, word) NOT ENFORCED -- Primary key fields for partitioned tables must include partition fields
  ) PARTITIONED BY (dt, hh)
WITH
  (
    'bucket' = '4', -- Control bucket count, recommend ~1GB data per bucket
    'changelog-producer' = 'none', -- Generate changelog for downstream streaming reads
    'metastore.partitioned-table' = 'true' -- Determine whether to sync partition info to LAS metadata management
  );
```



* `metastore.partitioned-table`: When enabled, partition information will be synchronized to the LAS metadata management, by default `false` is not enabled.


<span id="0b9965e6"></span>
## Data writing examples

The following example demonstrates how to use Flink SQL to write data into Paimon tables.

<span id="f0067c16"></span>
### Create data source tables

First, create a data source table to generate mock data.

```SQL
CREATE TABLE doc_source (word varchar)
WITH
  (
    'connector' = 'datagen',
    'rows-per-second' = '5',
    'fields.word.length' = '30'
  );
```



* `connector`: Generate mock data using the `datagen` connector.

* `rows-per-second`: The number of rows generated per second.

* `fields.word.length`: The length of the generated field `word`.


<span id="a8229d7e"></span>
### Write data to the Paimon table.

Write the data from the data source table to the Paimon table.

```SQL
INSERT INTO `paimon_test`.`default`.`doc_result`
select
  t.word,
  count(1)
from
  doc_source t
GROUP BY
  t.word;
```



* `paimon_test`: Catalog name.

* `default`: Database name.

* `doc_result`: Target table name.


<span id="10d1b961"></span>
### Enable Checkpoint.

Paimon's snapshot submission mechanism is closely related to Flink's Checkpoint, hence properly configuring Checkpoint parameters is crucial to ensure that downstream streaming or batch processing tasks can promptly perceive changes in upstream data. For example, with Flink's default Checkpoint interval set to 5 minutes, it means that only after completing a Checkpoint every 5 minutes can downstream tasks observe the latest data insertions, updates, or deletions. Therefore, adjusting the Checkpoint interval according to business needs is key to optimizing data visibility and processing timeliness.

> Note: You can decrease or increase the Checkpoint interval based on real\-time data requirements. It is generally recommended that the Checkpoint interval **not be less than 1 minute**. If there is severe data latency, frequent data updates, or low fresh data requirements, it is advisable to increase the Checkpoint time to 5 minutes or longer.


The Checkpoint can be enabled as illustrated below, set in **Job Development \- Configuration Parameters \- Checkpoint Configuration \- Checkpoint Interval**.

<span id="f313ebc1"></span>
## 6. Deploy Tasks

<span id="eedf47a0"></span>
### 6.1 Task Deployment

At this point, you can click the validation button in the toolbar to check some basic SQL syntax issues. Please note: If you encounter an error like `Caused by: org.apache.thrift.transport.TTransportException`, you can refer to [Errors when validating SQL](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog#2c8543ed) the description. You can temporarily ignore this issue.

If there are no other errors with the SQL, you can proceed to deploy the SQL task: select 'Deploy' from the toolbar, choose the appropriate resource pool, and skip the pre\-deployment in\-depth check. You can deploy the task.

After the task is successfully deployed, start the task from the Task Management page and check that the task is in 'Running' status.

<span id="b16b849c"></span>
### 6.2 Confirm successful task execution

You can access the TOS bucket management interface (relevant access permissions are required), where you can see that data files have been generated in the TOS directory of the data table. This indicates that the data has been written successfully.

<span id="33f75855"></span>
## 7. Data Reading Example

We have already confirmed that the data has been written successfully, the following example shows how to use BytePlus Flink to stream or batch read data from Paimon tables. Further verification of data accuracy can be confirmed.

<span id="1eca8e8b"></span>
### 7.1 Create a Print Table

Create a print table for outputting the read data.

```SQL
CREATE TABLE `print_table` (
    word varchar,
    cnt bigint
) WITH (
    'connector' = 'print'
);
```



* `connector`: Use the `print` connector to print data to the console.


<span id="b2fa73c7"></span>
### 7.2 Read Data from Paimon Table

Read data from the Paimon table and write it to the print table.

```SQL
INSERT INTO `print_table`
SELECT * FROM `paimon_test`.`default`.`doc_result`;
```



* `paimon_test`: Catalog name.

* `default`: Database name.

* `doc_result`: Source table name.


<span id="55b34e7b"></span>
## Frequently Asked Questions

<span id="2c8543ed"></span>
### Errors when validating SQL

If an error occurs while validating SQL (by clicking the validate button or automatically checking SQL during deployment), similar to `Caused by: org.apache.thrift.transport.TTransportException`, it indicates that the current connection to the LAS interface differs. Please do not panic; the current version temporarily cannot access LAS metadata during the SQL validation stage.

```Plain
org.apache.flink.table.api.ValidationException: Unable to create catalog 'paimon_test1'.

Catalog options are:
'hive-conf-dir'='/opt/tiger/workdir'
'metastore'='hive'
'type'='paimon'
'uri'='thrift://lakeformation.las.cn-beijing.byteplus.com:48869'
'warehouse'='tos://flink-cwz-paimon/paimon_test1'
        at org.apache.flink.table.factories.FactoryUtil.createCatalog(FactoryUtil.java:511)
        ...
Caused by: java.lang.RuntimeException: Failed to determine if database default exists
        at org.apache.paimon.hive.HiveCatalog.databaseExistsImpl(HiveCatalog.java:223)
        ... 9 more
Caused by: org.apache.thrift.transport.TTransportException
        at org.apache.thrift.transport.TIOStreamTransport.read(TIOStreamTransport.java:132)
        ... 15 more
```


Solution: During the task deployment process, choose more settings \- skip the pre\-deployment deep check.

<span id="29ca3600"></span>
### Access to the LAS interface fails during runtime

After executing and starting the task, if you find that the task fails and a similar error is reported in the logs as follows, this issue indicates that the LAS interface is not accessible.

```Plain
Caused by: org.apache.hadoop.hive.metastore.api.MetaException: Could not connect to meta store using any of the URIs provided. Most recent failure: org.apache.thrift.transport.TTransportException
```


Possible causes


1. The hive\-site.xml file was not uploaded, or the filename is incorrect

   1. Solution: Check whether the hive\-site.xml has been successfully uploaded to the dependencies and ensure that the filename is exactly as required.

2. The AK/SK for accessing LAS is incorrect, causing failed user authentication.

   1. Solution: Check the AccessKey and AccessKeySecret in hive\-site.xml for correctness.

3. The user accessing LAS does not have the LASFullAccess permission of IAM, please contact the administrator to activate this permission

   1. Solution: Contact the main account administrator to verify if LASFullAccess permissions have been granted for the user.


<span id="a8a27a50"></span>
### 8.3 Access to LAS reported unauthorized interface

After executing and starting the task, if the task fails and similar errors are reported in the logs, it indicates that the interfaces of LAS were not successfully authorized

```Plain
Caused by: org.apache.hadoop.hive.metastore.api.MetaException: Access denied: [DeniedPrivilege(resource:Resource{resourceScope='SCHEMA', catalogName='paimon_test1', schemaName='test_db'}, action:DESCRIBE)] for user: 31035840
```


Solution: This issue occurs because the specified account was not granted the necessary permissions in the LAS Catalog. To open permissions for the account, please refer to [Data Directory Management](https://www.volcengine.com/docs/6492/1264529) according to the action suggested by the error log.

<span id="a557a177"></span>
### Task 8.4 cannot start; error: LAS database does not exist

After executing and starting the task, if it is found that the task has failed and errors like org.apache.flink.table.catalog.exceptions.DatabaseNotExistException are found in the Run Events,

Solution: This issue is due to the fact that during the Flink task submission phase, the SQL is statically parsed without connecting to LAS to fetch existing databases, so it is mandatory to explicitly write the database creation statement in the SQL. Add the following statements in the SQL code:

```SQL
CREATE TABLE IF NOT EXISTS test_db;
```


After resubmitting the task, it will return to normal.

<span id="b5befc6f"></span>
### Issue 8.5: Incorrect format of hive\-site.xml

After executing and starting the task, if the task fails and the following error is found in the logs, com.ctc.wstx.exc.WstxParsingException:

```Plain
Caused by: java.lang.RuntimeException: com.ctc.wstx.exc.WstxParsingException: Illegal processing instruction target ("xml"); xml (case insensitive) is reserved by the specs.
 at [row,col {unknown-source}]: [2,5]
```


Solution: This may be due to incorrect formatting of hive\-site.xml used in LAS metadata dependencies. It is necessary to check if the XML file complies with the [grammatical standards](https://www.w3.org/TR/xml/). Common XML format issues can be referred to:


1. The content at the beginning of the file must be `<?xml ...`, and no invisible characters, spaces, or blank lines are allowed in front of the angle brackets.

2. The XML document must contain valid tags, such as special characters `<`, `>`, `&` that should not appear in the content and must be marked as plain text using CDATA syntax if they do.


<span id="e30e392f"></span>
### 8.6 How to delete LAS Catalog tables

If you need to delete tables from the LAS metadata, you must manually remove both the table information in the LAS metadata and the file path of the database table on the TOS directory. Deleting only the LAS metadata or only the data in the TOS directory will cause data inconsistency. The following types of errors can cause the task to fail:


1. Only deleting the TOS file path without deleting the LAS metadata

2. Only deleting the LAS metadata without deleting the TOS data


Solution: Determine which scenario it belongs to, and delete both the existing LAS metadata and TOS data to ensure the database table can continue to be written normally.

<span id="7b853b45"></span>
### In LAS, data tables are non\-partitioned, yet they appear as partitioned in the TOS file system.

If we use partitioned tables and notice discrepancies between LAS and TOS table information:


1. The LAS interface lists the tables as partitioned.

2. The TOS interface shows that partitions have been created for the data tables.


Solution: Paimon does not automatically synchronize the partition information of tables to LAS metadata management. To see the partition fields of data tables in LAS metadata management, add the following WITH parameters in the table creation statement:

```Plain
'metastore.partitioned-table' = 'true' -- Determines whether to sync partition information to LAS metadata management
```


> Note: Since partition fields cannot be dynamically added, after adding parameters, the existing data tables must be cleared (including LAS metadata and TOS data files) and recreated.

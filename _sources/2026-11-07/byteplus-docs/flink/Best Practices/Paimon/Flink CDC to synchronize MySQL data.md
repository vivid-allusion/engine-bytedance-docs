---
title: "Flink CDC to synchronize MySQL data"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_CDC_to_synchronize_MySQL_data"
---

<span id="17914211"></span>
## 1. Overview

Flink CDC 3 is Apache Flink's latest generation Change Data Capture solution, supporting efficient capturing and processing of database change data for seamless synchronization of full and incremental data. This manual will guide you on how to use Flink CDC 3.x with a FileSystem\-based metadata scheme to perform data synchronization tasks from MySQL to Paimon.

In the Paimon scenario, Flink CDC 3.x supports the following features:


* Automatic table creation (supports only Primary Key tables)

* Synchronization of table structure changes

* Real\-time data synchronization

* Supports metadata management based on both filesystem and LAS


<span id="677ef24a"></span>
## 2. Environment Preparation

<span id="97d0bec7"></span>
### Activate Serverless Flink

Ensure you have:


1. Activated the **BytePlus Flink** product and are able to create Change Data Capture tasks in job development.

2. Purchased on\-demand or subscription\-based resource pools in the **Resource Management \- Resource Pools** module, enabling normal Flink task submissions.


<span id="912937b8"></span>
### Flink Version Requirements

Flink version must be \>= 1.16, supporting Paimon 0.8.2 enhanced version in the Flink CDC YAML.

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: 127.0.0.1
  port: 3306
  username: admin
  password: pass
  tables: adb\.., bdb.user_table_[0-9]+, [app|web].order_\.
  server-id: 5401-5404

sink:
  type: paimon
  name: Paimon Sink
  catalog.properties.metastore: filesystem
  catalog.properties.warehouse: tos://<bucket-name>/<warehouse>

pipeline:
  name: MySQL to Paimon Pipeline
  parallelism: 2
```


<span id="80bc15ac"></span>
## MySQL Settings

<span id="56a6eaaa"></span>
### Basic Settings

Flink CDC currently supports automatic synchronization from MySQL. MySQL must meet the following prerequisites (This article uses a cloud database MySQL version for the demo):


1. Flink CDC supports MySQL versions 8.0+, versions 5.7+ are not currently supported

2. The MySQL and Flink networks need to be interconnected; it is recommended that MySQL and Flink use the same VPC and subnet, and set a whitelist in the security group for MySQL for Flink. Refer to [creating a whitelist](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/create-allowlist), [binding the whitelist to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-instances-to-allowlists).

> **Note**: The BytePlus Engine MySQL instance does not bind to any whitelist by default after creation, making it inaccessible by any IP.


3. Additionally, create a MySQL user for access, and grant the user read\-only permissions as well as `REPLICATION SLAVE` and `REPLICATION CLIENT` to access binlog. This article creates a flinkcdc account.


<span id="bfb6315f"></span>
### 3.2 MySQL sample data

For testing purposes, use the following SQL to create a database and import some demo data:

```SQL
-- create database
CREATE DATABASE app_db;

USE app_db;

-- create orders table
CREATE TABLE `orders` (
`id` INT NOT NULL,
`price` DECIMAL(10,2) NOT NULL,
PRIMARY KEY (`id`)
);

-- insert records
INSERT INTO `orders` (`id`, `price`) VALUES (1, 4.00);
INSERT INTO `orders` (`id`, `price`) VALUES (2, 100.00);

-- create shipments table
CREATE TABLE `shipments` (
`id` INT NOT NULL,
`city` VARCHAR(255) NOT NULL,
PRIMARY KEY (`id`)
);

-- insert records
INSERT INTO `shipments` (`id`, `city`) VALUES (1, 'beijing');
INSERT INTO `shipments` (`id`, `city`) VALUES (2, 'xian');

-- create products table
CREATE TABLE `products` (
`id` INT NOT NULL,
`product` VARCHAR(255) NOT NULL,
PRIMARY KEY (`id`)
);

-- insert records
INSERT INTO `products` (`id`, `product`) VALUES (1, 'Beer');
INSERT INTO `products` (`id`, `product`) VALUES (2, 'Cap');
INSERT INTO `products` (`id`, `product`) VALUES (3, 'Peanut');
```


<span id="1fd71554"></span>
## 4. Configure CDC synchronization task

<span id="997e77dc"></span>
### 4.1 Create a Flink CDC task

**Operation Path**: Job Development \- BytePlus Flink CDC Job \- Create Job

**Reference Document**: [Flink CDC Tasks](https://docs.byteplus.com/docs/flink/Flink_CDC_Tasks)

> Note: If LAS Catalog is chosen as the metadata management solution, it's necessary to select Paimon\-LAS as the data downstream type. And it is also necessary to finish data catalog creation and authorization in LAS Catalog in advance.


<span id="f9c41304"></span>
### 4.2 Upload the MySQL Driver file

After creating the Change Data Capture sync task, refer to the [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) documentation, download the MySQL Driver (recommended version 8.0.27), and upload it to the Para, download the MySQL Driver (recommended version 8.0.27), and upload it to the Parameter Configuration \- Dependency Files of the CDC task.

<span id="203a2eb4"></span>
### 4.3 Use FileSystem's Catalog

The specific configuration of Flink CDC can be referred from the [Paimon](https://docs.byteplus.com/docs/flink/CDC_Connector_Paimon)reference documentation. The core task configuration is as follows:

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: mysqlxxxxxxxxxxxx.rds.byteplus.com
  port: 3306
  # Database access username and password. Make sure the account has sufficient privileges (read-only + binlog).
  username: flinkcdc
  password: password
  tables: app_db.\.*
  # MySQL sync task ID. It's recommended to set a different ID range for each CDC task.
  server-id: 5401-5500
  # Session time zone on the database server, e.g., "Asia/Shanghai".
  # It determines how the TIMESTAMP type in MySQL is converted to STRING.
  # If not set, ZoneId.systemDefault() will be used to determine the server time zone.
  server-time-zone: Asia/Shanghai

sink:
  type: paimon
  name: Paimon Sink
  commit.user: flinkcdc
  catalog.properties.metastore: filesystem
  # Number of buckets per table. Currently, only a unified setting is supported.
  table.properties.bucket: 1
  catalog.properties.warehouse: tos://<bucket_name>/<catalog_name>

pipeline:
  name: MySQL to Paimon Pipeline
  parallelism: 2
```



* `<catalog_name`\>: The name of the Catalog, customizable.

* `bucket_name`: The name of the TOS (object storage) bucket for storing Paimon data.


<span id="2de60c98"></span>
### 4.4 Using the LAS Catalog

Specific configurations for Flink CDC can refer to [Paimon](https://docs.byteplus.com/docs/flink/CDC_Connector_Paimon)the reference document. The core task configuration is as follows:

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: mysqlxxxxxxxxxxxx.rds.byteplus.com
  port: 3306
  # Database access username and password. Make sure the account has sufficient privileges (read-only + binlog).
  username: flinkcdc
  password: password
  tables: app_db.\.*
  # MySQL sync task ID. It's recommended to set a different ID range for each CDC task.
  server-id: 5401-5500
  # Session time zone on the database server, e.g., "Asia/Shanghai".
  # It determines how the TIMESTAMP type in MySQL is converted to STRING.
  # If not set, ZoneId.systemDefault() will be used to determine the server time zone.
  server-time-zone: Asia/Shanghai

sink:
  type: paimon-las
  name: Paimon LAS Sink
  commit.user: flinkcdc
  catalog.properties.metastore: hive
  catalog.properties.uri: thrift://lakeformation.las.cn-beijing.byteplus.com:48869
  catalog.properties.warehouse: tos://<bucket_name>/<catalog_name>
  catalog.properties.hive-conf-dir: /opt/tiger/workdir
  # Number of buckets per table. Currently, only a unified setting is supported.
  table.properties.bucket: 1

pipeline:
  name: MySQL to Paimon LAS Pipeline
  parallelism: 2
```



* `catalog_name`: Name of the Catalog, customizable.

* `bucket_name`: The name of the TOS (object storage) bucket for storing Paimon data.

* `catalog.properties.*`: Paimon's Catalog parameters, see [Paimon with LAS Catalog](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog).

* `table.properties.*`: Paimon's table creation parameters, refer to [Paimon with LAS Catalog](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog).


**Note**: When using Flink CDC to sync data to Paimon, referring to [Paimon with LAS Catalog](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog) the document is also required in the process of using LAS metadata, generating AK/SK, enabling LAS permissions, and importing LAS dependency files.

<span id="d31045c3"></span>
### 4.5 Enable Checkpoint

Paimon's snapshot submission mechanism is closely associated with Flink's Checkpoint; hence, proper configuration of Checkpoint parameters is crucial to ensure that downstream streaming or batch tasks can promptly detect changes in upstream data. For example, with Flink's default Checkpoint interval set to 5 minutes, it means that only after every 5 minutes when a Checkpoint is completed can downstream tasks observe the latest data insertions, updates, or deletions. Therefore, adjusting the Checkpoint interval according to business needs is key to optimizing data visibility and process timeliness.

> **Note:**  The Checkpoint interval can be decreased or increased based on real\-time data requirements. It is generally recommended that the Checkpoint duration **not be less than 1 minute**. If data is significantly delayed, updated frequently, or the requirement for data freshness is not high, it is advisable to appropriately extend the Checkpoint duration to 5 minutes or longer.


To enable Checkpoint as shown below, go to **Job Development \- Configuration Parameters \- Checkpoint Configuration \- Checkpoint Interval** to set it.

<span id="03935436"></span>
## 5. Task deployment

<span id="3e3c393e"></span>
### 5.1 Deploying tasks

At this point, you can click the verification button in the toolbar to check some basic SQL syntax issues.

If there are no other errors with SQL, you can select to deploy the SQL task online. Go to the toolbar, choose 'Deploy', and select the appropriate resource pool for deployment.

Once deployed successfully, start the task on the task management page and check that the task has entered the 'Running' state.

<span id="26a78f7d"></span>
### 5.2 Confirm Successful Task Execution

You can access the TOS bucket management interface (relevant access permissions required) to see that the related data files have been generated in the TOS directory of the data table. This indicates that data has been written successfully.

<span id="a1216a4f"></span>
## 6. Data Retrieval Example

The following example demonstrates how to use BytePlus Flink to read data from a Paimon table in both streaming and batch modes.

<span id="ccb2541b"></span>
### 6.1 Create a Print Table

Create a print table for outputting the read data.

```SQL
CREATE TABLE `print_orders` (
  `id` INT,
  `price` DECIMAL(10,2),
) WITH (
  'connector' = 'print'
);
```



* `connector`: Use the `print` connector to print data to the console.


<span id="bf0d04b3"></span>
### Read Data from Paimon Tables

Retrieve data from Paimon tables and write to the printout.

```SQL
CREATE CATALOG paimon_cdc_test
WITH
  (
    'type' = 'paimon',
    'warehouse' = 'tos://<bucket_name>/paimon_cdc_test'
  );


CREATE DATABASE IF NOT EXISTS paimon_cdc_test.app_db;


INSERT INTO `print_orders`
SELECT * FROM `paimon_cdc_test`.`app_db`.`orders`;
```



* `paimon_cdc_test`: Catalog name.

* `app_db`: Database name.

* `orders`: Source table name.


<span id="9a8ef783"></span>
## Task Phase Query

<span id="d2a4114b"></span>
### Confirm the task is in full synchronization phase:

Check JMJobManager logs, the keyword for starting splits is as follows:

```Java
# 开始切分 split
2025-01-12 22:08:06,122 INFO  org.apache.flink.cdc.connectors.mysql.source.assigners.MySqlSnapshotSplitAssigner [] - Start splitting table app_db.con_bt_point_info into chunks...
```


After splitting, the snapshot split is started, where app_db.con_bt_point_info:0 represents the first split; based on the split number, the progress of the split handling can be viewed:

```Java
2025-01-12 22:08:42,644 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlSnapshotSplit{tableId=app_db.con_bt_point_info, splitId='app_db.con_bt_point_info:0', splitKeyType=[`point_id` BIGINT NOT NULL], splitStart=null, splitEnd=null, highWatermark=null} to subtask 1
```


<span id="d6e97438"></span>
### Confirm the task is in the incremental synchronization phase:

View JobManager logs to check the subtask index assigned to the binlog split:

```Java
2025-01-13 11:16:20,315 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlBinlogSplit{splitId='binlog-split', tables=[], offset={ts_sec=0, file=binlog.000426, pos=520322, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1521914, row=0, event=0}, endOffset={ts_sec=0, file=, pos=-9223372036854775808, kind=NON_STOPPING, row=0, event=0}, isSuspended=false} to subtask 0
```


Find the TM log corresponding to subtask 0:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d408907a50644a2d81927ee00ab48d6f~tplv-goo7wpa0wc-image.image" width="3268px" /></div>


Search in the TaskManager logs for keywords to monitor the binlog processing progress, where file and pos represent the binlog file and position read, respectively:

```Java
2025-01-13 11:21:19,039 INFO  org.apache.flink.cdc.connectors.mysql.source.reader.MySqlSourceReader [] - Binlog offset for tables [app_db.shipments, app_db.shipments90, app_db.shipments91, app_db.shipments89, app_db.shipments81, app_db.shipments82, app_db.shipments83, app_db.shipments84, app_db.shipments85, app_db.shipments86, app_db.shipments87, app_db.shipments88, app_db.shipments12] on checkpoint 2: {transaction_id=null, ts_sec=0, file=binlog.000426, pos=687715, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1522412, row=0, event=0, server_id=2051901732}
```


<span id="5aaa1254"></span>
## 8. Common Issues

<span id="0892ea19"></span>
### 8.1 JDBC Driver Not Found Error

**Issue**: If the task fails to start, the following exception information appears in the logs `Caused by: java.lang.ClassNotFoundException: com.mysql.cj.jdbc.Driver`.

**Solution**: This issue is due to compliance reasons; Flink CDC does not include MySQL Driver built\-in, please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) the documentation, download the official MySQL Driver (version 8.0.27 recommended), and upload it to the dependency files of the Flink CDC task.

<span id="a8d6f20c"></span>
### 8.2 Flink CDC Task Unable to Add Data After a Fresh Start

**Issue Phenomenon**: After running the Flink CDC task for a while, for various reasons, it may be necessary to discard the original state and synchronize from a completely new initial stage. If at this time the original Paimon table is not deleted, new data will not be able to be written.

**Solution**: This is due to defects in the downstream data of Flink CDC Paimon, with commit.user being constant, causing snapshots to start from version 0 during Paimon writes. Since it's behind the current Paimon table version, it always fails to publish. There are two solutions:


1. When starting anew, you need to delete all Paimon files on TOS to ensure a full sync from the beginning.

2. When starting anew, you need to change commit.user to a new value, such as `commit.user: v2`, to ensure the current new commit user snapshot can be published normally.


```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: mysqlxxxxxxxxxxxx.rds.byteplus.com
  port: 3306
  # Database access credentials. Ensure the account has sufficient access rights (read-only + binlog).
  username: flinkcdc
  password: ********
  tables: app_db.\.*
  # MySQL sync task ID. It is recommended to assign a different range for each CDC task.
  server-id: 5401-5500
  # Session time zone of the database server, e.g., "Asia/Shanghai". 
  # It controls how the TIMESTAMP type in MySQL is converted to STRING.
  # If not set, ZoneId.systemDefault() is used to determine the server time zone.
  server-time-zone: Asia/Shanghai

sink:
  type: paimon
  name: Paimon Sink
  commit.user: flinkcdc
  catalog.properties.metastore: filesystem
  table.properties.bucket: 1
  catalog.properties.warehouse: tos://flink-cwz-paimon/paimon_cdc_test

pipeline:
  name: MySQL to Paimon Pipeline
  parallelism: 2
```


<span id="b19f9437"></span>
### 8.3 MySQL Datetime and Paimon Timestamp type have time discrepancies

**Issue**: MySQL's datetime is a timezone\-unaware datatype, and many users use it to store local time. For example, `2025-01-09 10:00:00` in UTC+8 timezone. Due to the uncertainty of the timezone, Flink & Paimon default to using the UTC timestamp during conversion. Therefore, after writing into Paimon, viewing the time in UTC+8 shows the result as `2025-01-09 18:00:00`. This leads to a discrepancy with the time in MySQL.

**Solution:** 


1. Avoid using datetime type fields in MySQL, and instead use timestamp type fields that contain timezone information. In this way, Flink will perform timezone conversion based on server\-time\-zone information.

2. If it's unavoidable to use datetime types in MySQL, store the date in UTC time in the MySQL datetime fields, for example `2025-01-09 10:00:00 UTC+8` is stored as `2025-01-09 02:00:00` in the database.


<span id="c7b9de4e"></span>
### 8.4 CDC task fails to launch, indicating that dynamic bucket mode is not supported.

**Symptom**: Flink CDC fails to start, error message includes the key information `"Can't extract bucket from row in dynamic bucket mode"`

**Solution**: The current version of Flink CDC does not support dynamic bucketing mode (bucket = \-1) by Paimon. Therefore, it is necessary to specify the following fixed bucket parameters in the Paimon Sink.

```YAML
# Specifies the number of buckets when creating the table. It is recommended to set this based on data volume.
table.properties.bucket: 10
```


<span id="08998a1d"></span>
### 8.5 How to choose a changelog\-producer.

**Problem description**: Paimon supports the changelog\-producer option; which option is generally recommended in the CDC scenario.

**The solution**: Paimon's changelog\-producer feature supports downstream Flink tasks to read complete change logs, which can be configured with the following parameters:

```YAML
table.properties.changelog-producer: input
```


This option can be set according to [Changelog output mechanism](https://docs.byteplus.com/docs/flink/Connector_Paimon#79d03b88) common settings in Change Data Capture scenarios, which include two types:


1. `none`: Set it to none if not needed downstream, or it can be left unset.

2. `input`: If the downstream requires a changelog, since the upstream in Change Data Capture is itself a change log, simply select input.

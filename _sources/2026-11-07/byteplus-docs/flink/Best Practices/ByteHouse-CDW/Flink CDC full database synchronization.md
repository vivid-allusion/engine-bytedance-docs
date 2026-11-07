---
title: "Flink CDC full database synchronization"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_CDC_full_database_synchronization"
---

<span id="ba630a3c"></span>
## 1. Overview

Flink CDC 3.x is Apache Flink's next\-generation Change Data Capture solution, supporting efficient capture and processing of database change data, enabling seamless synchronization of full and incremental data. This manual guides you on using Flink CDC 3.x to synchronize data from MySQL to ByteHouse\-CDW.

In the ByteHouse\-CDW scenario, Flink CDC 3.x offers the following features:


* ✅ Real\-time full database synchronization

* ✅ Real\-time synchronization of database shards and tables

* ✅ Data transformation support for simple data processing

* ❌ Does not support automatic creation of databases, tables, or schema changes (requires manual creation of ByteHouse database tables in advance)


<span id="8615daf0"></span>
## 2. Environment preparation

<span id="c4fe1200"></span>
### 2.1 Activate Serverless Flink

Make sure you have:


1. Activated the **BytePlus Flink** product and can create Change Data Capture tasks in job development.

2. Already purchased on\-demand or subscription\-based resource pools in **Resource Management \- Resource Pools**, and can submit Flink tasks normally.


<span id="f7e26dca"></span>
### 2.2 Flink Version Requirements

The Flink version must be \>= 1.16, supporting ByteHouse\-CDW cloud data warehouse edition within the Change Data Capture YAML.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87af7c1bb0044b48bc3b4dc2940e9652~tplv-goo7wpa0wc-image.image" width="780px" /></div>


<span id="2100bc83"></span>
## 3. Preparation Steps

<span id="74363492"></span>
### 3.1 Basic Settings

Current Change Data Capture for Flink supports automated synchronization from MySQL. MySQL requires the following prerequisites (this article uses the cloud database version of MySQL for the demo):


1. Flink CDC supports MySQL versions 8.0+, versions 5.7+ are not currently supported

2. MySQL and Flink networks need to be interconnected. It is recommended that MySQL and Flink use the same VPC and subnet, and that a whitelist is set for Flink in the MySQL security group Refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist), [Associating instances to allowlists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_instances_to_allowlists_1)

> **Note**: By default, when a BytePlus RDS for MySQL instance is created, no whitelist is bound, and no IP can access the MySQL instance


In Flink Resource Management \- Resource Pool \- Resource Pool Details, view the network segment or security group of the resource pool

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1769679053b84e3cb29972884f058b1c~tplv-goo7wpa0wc-image.image) </span>

Add the above found network segment or security group to the MySQL allowlist

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e47966ecf7c94b259ac96b2c14b83a37~tplv-goo7wpa0wc-image.image) </span>


3. Additionally, create a MySQL access user and grant the user read\-only permissions and `REPLICATION SLAVE`, `REPLICATION CLIENT` permissions to access binlog This document creates the flinkcdc account


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dda74787f61a47c8b47caa26178f4521~tplv-goo7wpa0wc-image.image) </span>

<span id="fed45ceb"></span>
### 3.2 MySQL Sample Data

For testing purposes, the following SQL can be used to create a database:

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

-- create shipments table
CREATE TABLE `shipments` (
`id` INT NOT NULL,
`city` VARCHAR(255) NOT NULL,
PRIMARY KEY (`id`)
);

-- create products table
CREATE TABLE `products` (
`id` INT NOT NULL,
`product` VARCHAR(255) NOT NULL,
PRIMARY KEY (`id`)
);
```


Import some demo data using the following SQL:

```SQL
-- insert records
INSERT INTO `orders` (`id`, `price`) VALUES (1, 4.00);
INSERT INTO `orders` (`id`, `price`) VALUES (2, 100.00);

-- insert shipments
INSERT INTO `shipments` (`id`, `city`) VALUES (1, 'beijing');
INSERT INTO `shipments` (`id`, `city`) VALUES (2, 'xian');

-- insert products
INSERT INTO `products` (`id`, `product`) VALUES (1, 'Beer');
INSERT INTO `products` (`id`, `product`) VALUES (2, 'Cap');
INSERT INTO `products` (`id`, `product`) VALUES (3, 'Peanut');
```


<span id="fa85d0e1"></span>
### 3.3 Prepare ByteHouse database tables

Before this step, ensure ByteHouse and Flink resource pools share the same VPC, the network is accessible, proper permissions are set, and the correct API\-KEY is issued.

Manually create database tables: ByteHouse\-CDW currently does not support automatic table creation due to numerous table parameters. ByteHouse recommends two ways to create tables.


1. If the target table contains fewer than 100 million records, use MySQL table creation statements and execute them in the ByteHouse SQL worksheet with the MySQL dialect selected.

> Note: For existing MySQL instances, you can export all database table creation statements using the following command:

> `mysqldump -u <mysql_user> -p --no-data --skip-opt <target_db> > ddl.sql`


2. For tables with over 100 million records, use ByteHouse CDW’s table creation tool to carefully tune table parameters based on data import and query requirements, then start the Flink CDC task to import data.


<span id="2ae4d8c7"></span>
## 4. Configure CDC synchronization task

<span id="423bc343"></span>
### 4.1 Create Flink CDC task

**Operation path**: Job development \- Flink CDC job \- Create job

Reference documents:[Flink CDC Tasks](https://docs.byteplus.com/docs/flink/Flink_CDC_Tasks)

<span id="ea32fadf"></span>
### 4.2 Upload the MySQL Driver file

After creating the CDC sync task, refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) the documentation, download the MySQL Driver (version 8.0.27 recommended), and upload it to the CDC task’s **Parameter Configuration \- Dependencies**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a95fc756d44667b94bd74d039fc0ee~tplv-goo7wpa0wc-image.image" width="660px" /></div>


<span id="6471da08"></span>
### 4.3 Using Flink CDC YAML configuration

The specific configuration of Flink CDC can refer to [Bytehouse CDW](https://docs.byteplus.com/docs/flink/Bytehouse_CDW)the reference documentation. The core task configuration is as follows:

```YAML
################################################################################
# Description: Sync MySQL all tables to BH CDW
################################################################################
source:
   type: mysql
   name: MySQL Source
   hostname: db-xxx.xxx.ibytepluses.com
   port: 3306
   username: your-username
   password: your-password
   tables: app_db.\.*
   server-id: 5401-5420

sink:
  type: bytehouse-cdw
  name: Bytehouse CDW Sink
  region: ap-southeast-1
  host: tenant-xxxx.bytehouse.ibytepluses.com
  port: 19000
  virtual-warehouse: test
  api-token: xxx:xxx
  sink.buffer-flush.interval: 5s
  sink.buffer-flush.max-rows: 10000
  timestamp-offset: -8h

pipeline:
  name: MySQL to Bytehouse CDW Pipeline
  parallelism: 16
```


<span id="3d4e88a0"></span>
### 4.5 Enable Checkpoint

To ensure that real\-time tasks can recover from a state in case of failure, it is essential to set Flink's state submission strategy appropriately. For example, using Flink's default Checkpoint interval, if set to 5 minutes, it means that after completing a Checkpoint every 5 minutes, the next task recovery will resume from this state.

Activate Checkpoint as shown in the diagram, and configure settings at **Job Development \- Configuration Parameters \- Checkpoint Settings \- Checkpoint Interval**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41696f605adb424eaa0da0e0cc4e4e0e~tplv-goo7wpa0wc-image.image" width="670px" /></div>


<span id="cd77675f"></span>
## 5. Task Going Live

<span id="6bd77af8"></span>
### 5.1 Task Launch

At this point, you can click the verification button on the toolbar to check some basic SQL syntax issues.

If there are no other errors with the SQL, you can choose to launch the SQL task, select the toolbar \- go live, and choose the appropriate resource pool to go live.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36a9cecbab9d46688a3d380205beed19~tplv-goo7wpa0wc-image.image" width="738px" /></div>


After a successful launch, start the task from the task management page and check that the task is in a running state.

<span id="949a50db"></span>
### 5.2 Confirm Task Execution Success

You can enter the SQL worksheet function of ByteHouse\-CDW and use SQL queries to check whether the data has been correctly synchronized to the database.

<span id="893c7026"></span>
## 6 Task Phase Query

<span id="34cee623"></span>
### 6.1 Confirm Task is at Full Volume Synchronization Stage:

View JMJobManager logs, the keywords for starting the split are as follows:

```Java
# start split
2025-01-12 22:08:06,122 INFO  org.apache.flink.cdc.connectors.mysql.source.assigners.MySqlSnapshotSplitAssigner [] - Start splitting table app_db.con_bt_point_info into chunks...
```


After the split is completed, a snapshot split is initiated, where app_db.con_bt_point_info:0 indicates the first split, and the progress of the split can be seen based on the split number:

```Java
2025-01-12 22:08:42,644 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlSnapshotSplit{tableId=app_db.con_bt_point_info, splitId='app_db.con_bt_point_info:0', splitKeyType=[`point_id` BIGINT NOT NULL], splitStart=null, splitEnd=null, highWatermark=null} to subtask 1
```


<span id="38fff328"></span>
### 6.2 Confirm that the task is in the incremental phase of synchronization progress:

View JobManager logs to see the subtask index assigned for the binlog split:

```Java
2025-01-13 11:16:20,315 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlBinlogSplit{splitId='binlog-split', tables=[], offset={ts_sec=0, file=binlog.000426, pos=520322, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1521914, row=0, event=0}, endOffset={ts_sec=0, file=, pos=-9223372036854775808, kind=NON_STOPPING, row=0, event=0}, isSuspended=false} to subtask 0
```


Find the TM log corresponding to subtask 0:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d408907a50644a2d81927ee00ab48d6f~tplv-goo7wpa0wc-image.image" width="3268px" /></div>


Search TaskManager logs for keywords to view the binlog processing progress, where file and pos refer to the read binlog file and position:

```Java
2025-01-13 11:21:19,039 INFO  org.apache.flink.cdc.connectors.mysql.source.reader.MySqlSourceReader [] - Binlog offset for tables [app_db.shipments, app_db.shipments90, app_db.shipments91, app_db.shipments89, app_db.shipments81, app_db.shipments82, app_db.shipments83, app_db.shipments84, app_db.shipments85, app_db.shipments86, app_db.shipments87, app_db.shipments88, app_db.shipments12] on checkpoint 2: {transaction_id=null, ts_sec=0, file=binlog.000426, pos=687715, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1522412, row=0, event=0, server_id=2051901732}
```


<span id="27a14bee"></span>
## 7. Common Issues

<span id="60ea9a2f"></span>
### 7.1 JDBC Driver Not Found Error

**Issue Description**: If the task fails to start, the following exception message appears in the logs `Caused by: java.lang.ClassNotFoundException: com.mysql.cj.jdbc.Driver`.

**Solution**: This issue arises due to compliance reasons, Flink CDC does not have a built\-in MySQL Driver. Please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) the documentation, download the official MySQL Driver (version 8.0.27 recommended), and upload it to the dependency files of the Flink CDC task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce832564dc1c4c6b93110bc707805821~tplv-goo7wpa0wc-image.image) </span>

&nbsp;

<span id="36ab911b"></span>
### MySQL Datetime and ByteHouse Datetime have time differences

**Problem Phenomenon**: MySQL's datetime is a data type without timezone information, and many users use this type to store local time. For example, January 9, 2025, 10:00:00 in the UTC+8 timezone `2025-01-09 10:00:00`. Due to the inability to confirm the timezone, Flink & ByteHouse\-CDW use the UTC timestamp by default during conversion. Therefore, after being written, using the time of UTC+8 to check results in `2025-01-09 18:00:00`. This leads to a time difference with the time in MySQL.

**Solution:** 


1. Avoid using the datetime type field in MySQL, instead use the timestamp type field with timezone information. Thus, Flink combines the server\-time\-zone information for timezone conversion.

2. By setting up `timestamp-offset: -8h` in Flink CDC, during synchronization tasks, the timezone is automatically offset by minus 8 hours. Note that this time zone offset only applies to MySQL Datetime types.

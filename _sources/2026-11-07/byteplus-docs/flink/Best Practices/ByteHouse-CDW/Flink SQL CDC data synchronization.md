---
title: "Flink SQL CDC data synchronization"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_SQL_CDC_data_synchronization"
---

<span id="ba630a3c"></span>
## 1. overview

Flink CDC source is a set of Flink source connectors that capture change data from different databases through Change Data Capture (CDC). Some CDC sources integrate Debezium as the engine for capturing data changes, fully leveraging Debezium’s capabilities. This manual guides you to synchronize data from MySQL to ByteHouse\-CDW using Flink CDC 3.x.

In the ByteHouse\-CDW scenario, Flink CDC offers the following features:


* ✅ Real\-time synchronization of data tables

* ✅ Real\-time synchronization of data across multiple databases and tables

* ✅ Flexible real\-time ETL processing support for data transformation

* ❌ Automatic table structure changes (requires manual synchronization of ByteHouse database table changes in advance)


The following database versions are currently supported by Flink CDC. This document uses MySQL as an example to demonstrate how to use Flink CDC for data synchronization.


|Connector |Database |Driver |
|---|---|---|
|[mongodb-cdc](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.2/docs/connectors/flink-sources/mongodb-cdc/) |[MongoDB](https://www.mongodb.com/): 3.6, 4.x, 5.0, 6.0, 6.1, 7.0 |MongoDB Driver: 4.11.2 |
|[mysql-cdc](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.2/docs/connectors/flink-sources/mysql-cdc/) |[MySQL](https://dev.mysql.com/doc): 5.6, 5.7, 8.0.x<br><br>[RDS MySQL](https://www.byteplus.com/zh-CN/product/rds-mysql): 5.6, 5.7, 8.0.x<br><br>[Aurora MySQL](https://aws.amazon.com/cn/rds/aurora): 5.6, 5.7, 8.0.x<br><br>[MariaDB](https://mariadb.org/): 10.x<br><br>[PolarDB X](https://github.com/ApsaraDB/galaxysql): 2.0.1 |JDBC Driver: 8.0.28 |
|[postgres-cdc](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.2/docs/connectors/flink-sources/postgres-cdc/) |[PostgreSQL](https://www.postgresql.org/): 9.6, 10, 11, 12, 13, 14 |JDBC Driver: 42.5.1 |
|[sqlserver-cdc](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.2/docs/connectors/flink-sources/sqlserver-cdc/) |[Sqlserver](https://www.microsoft.com/sql-server): 2012, 2014, 2016, 2017, 2019 |JDBC Driver: 9.4.1.jre8 |


<span id="8615daf0"></span>
## 2. Environment Setup

<span id="c4fe1200"></span>
### 2.1 Activate Serverless Flink

Ensure you have completed the following:


1. Activated the **BytePlus Flink** product and can create Flink SQL tasks in job development.

2. Purchased an on\-demand or annual/monthly resource pool in the **Resource Management \- Resource Pool** module and can submit Flink jobs normally.

3. Flink version must be \>= 1.16, with built\-in support for Flink CDC and ByteHouse CDW Connector.


<span id="2100bc83"></span>
## 3. Preparation Steps

<span id="74363492"></span>
### 3.1 Basic Settings

Currently, Flink SQL CDC supports synchronization from MySQL. MySQL requires the following prerequisites (this article uses cloud database MySQL edition for the demo):


1. MySQL and Flink networks need to be connected. It is recommended to use the same VPC and subnet for MySQL and Flink, and allowlist Flink’s security group in MySQL. Refer to [creating a allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist) and [associating instances to allowlists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_instances_to_allowlists).

> **Note**: By default, no allowlist is associated after MySQL instance creation, so no IP can access this MySQL instance.


Check the resource pool subnet or security group in Flink Compute resource \- Resource pools \- Resource Pool Details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73e4b5efd182400291201d1b8766d2c2~tplv-goo7wpa0wc-image.image) </span>

Add the subnet or security group found above to the MySQL whitelist.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07c41a0585e74b40ba49e85980a48708~tplv-goo7wpa0wc-image.image) </span>


2. Additionally, create a MySQL access user with read\-only permissions and grant `REPLICATION SLAVE` and `REPLICATION CLIENT` privileges to access the binlog. This article creates the flinkcdc account.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8597c4fdb7a438cb1c8b475a0a4f6d6~tplv-goo7wpa0wc-image.image) </span>

<span id="fed45ceb"></span>
### 3.2 MySQL sample data

For testing purposes, you can create the database using the following SQL:

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
```


You can import partial demo data using the following SQL:

```SQL
-- insert records
INSERT INTO `orders` (`id`, `price`) VALUES (1, 4.00);
INSERT INTO `orders` (`id`, `price`) VALUES (2, 100.00);
```


<span id="fa85d0e1"></span>
### 3.3 Prepare ByteHouse database tables

Before this step, ensure ByteHouse and Flink resource pools share the same VPC and network connectivity is available (refer to [Debug network connectivity](https://docs.byteplus.com/docs/flink/Debug_network_connectivity)), with proper permissions set and a valid API\-KEY issued.

Create database tables manually:


1. If the target table data volume is small (no more than 100 million records), it is recommended to use MySQL create table statements and execute them in the ByteHouse SQL worksheet by selecting the MySQL dialect.

> Note: For existing MySQL instances, you can export all database create table statements using the following command:

> `mysqldump -u <mysql_user> -p --no-data --skip-opt <target_db> > ddl.sql`


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a4b6679299c4700be1c291631ea8b3d~tplv-goo7wpa0wc-image.image) </span>


1. For tables with data volumes exceeding 100 million, use ByteHouse CDW’s table creation tool to carefully configure parameters based on import and query requirements, then start the Flink SQL task to import data.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70a914d11f7d4d65b71c713d7acb27d8~tplv-goo7wpa0wc-image.image) </span>

<span id="2ae4d8c7"></span>
## 4. Configure the Flink SQL task

<span id="423bc343"></span>
### 4.1 Create a Flink SQL task

**Operation path**: Task development \- Tasks \- Flink SQL \- Create

**Reference document**: [Create Flink SQL Job](https://docs.byteplus.com/docs/flink/Create_Flink_SQL_Job)


1. Create a Flink SQL task using the wizard


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be8d16abfe8147a9a488b39049adf90b~tplv-goo7wpa0wc-image.image) </span>


2. Select Flink SQL streaming task and choose the required template


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a5b51590fb04388b2b1b8740a3a859f~tplv-goo7wpa0wc-image.image) </span>


3. Set the task name, storage location, and Flink engine version


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c70a3ba454724b57a266d9e179d685dc~tplv-goo7wpa0wc-image.image) </span>

<span id="ea32fadf"></span>
### 4.2 Upload the MySQL driver file

After creating the CDC sync task, refer to the [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources)documentation to download the MySQL driver (version 8.0.27 recommended), and upload it under **Parameter Configuration \- Dependency Files** for the CDC task.


1. Go to the [MySQL official website](https://downloads.mysql.com/archives/c-j/), select MySQL driver version 8.0.27, and choose the operating system as "**Platform Independent**".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e48951382fa549be9a244f100bb8461d~tplv-goo7wpa0wc-image.image) </span>


2. Select the TAR or ZIP package, then click the Download button. Extract the file and locate the mysql\-connector\-java\-8.0.27.jar file.

3. Upload the extracted JAR package to the file management module.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7092e8ecb771490b9828ddacde60d56c~tplv-goo7wpa0wc-image.image) </span>


4. Reference the JAR file in the Flink SQL task \- Params \- Dependency file


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28b42ba3704b4eef885e5626694b8823~tplv-goo7wpa0wc-image.image) </span>

<span id="6471da08"></span>
### 4.3 Complete the Flink SQL task code setup

For detailed Flink CDC configuration, refer to the following documents.


1. MySQL (example below): refer to [MySQL CDC](https://docs.byteplus.com/docs/flink/MySQL_CDC)

2. MySQL: refer to [MongoDB CDC](https://docs.byteplus.com/docs/flink/MongoDB_CDC)

3. Postgres SQL: refer to [Postgres CDC](https://docs.byteplus.com/docs/flink/Postgres_CDC)

4. SQL Server: refer to [SQLServer CDC](https://docs.byteplus.com/docs/flink/SQLServer_CDC)


The following documents show only the simplest MySQL\-CDC configuration options:


1. Create a Flink MySQL CDC data source


```SQL
CREATE TABLE orders (
    id INT,
    price DECIMAL(10, 2),
    PRIMARY KEY (id) NOT ENFORCED  -- If the database table to be synchronized defines a primary key, a primary key must also be defined here.
) WITH (
    'connector' = 'mysql-cdc',
    'hostname' = 'localhost',
    'port' = '3306',
    'username' = 'flinkuser',
    'password' = 'flinkpw',
    'database-name' = 'mydb',
    'table-name' = 'orders'
);
```



2. Create the ByteHouse\-CDW data downstream; refer to detailed parameters[ByteHouse CDW](https://docs.byteplus.com/docs/flink/ByteHouse_CDW)


```SQL
CREATE TABLE orders_bh (
    `id` INT,
    `price` DECIMAL(10, 2),
    PRIMARY KEY (id) NOT ENFORCED  -- If the database table to be synchronized defines a primary key, a primary key must also be defined here.
) WITH (
    'connector' = 'bytehouse-cdw',
    'jdbc.enable-gateway-connection' = 'true',
    'bytehouse.gateway.region' = 'XXXX_PRIVATE',
    'bytehouse.gateway.host' = 'tenant-xxxx-cn-beijing.bytehouse.byteplus.com',
    'bytehouse.gateway.port' = '19000',
    'bytehouse.gateway.api-token' = '<API_KEY>',
    'bytehouse.gateway.virtual-warehouse' = '<VIRTUAL_WAREHOUSE>',
    'database' = '<BYTEHOUSE_DB>',
    'table-name' = '<BYTEHOUSE_TABLE>'
);

```



3. Synchronize data from MySQL CDC to ByteHouse\-CDW in real time via Insert statements


```SQL
INSERT INTO orders_bh
SELECT * FROM orders;
```


<span id="cd77675f"></span>
## 5. Task deployment

<span id="6bd77af8"></span>
### 5.1 Task deployment

At this point, click the validation button on the toolbar to check basic SQL syntax errors

If there are no other SQL errors, choose to deploy the SQL task by selecting Deploy on the toolbar and pick an appropriate resource pool for deployment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b7dfeda05c641218e7ec835dfa044c3~tplv-goo7wpa0wc-image.image) </span>

After a successful deployment, start the task on the task management page and verify it enters the running state

<span id="949a50db"></span>
### 5.2 Confirm task execution success

Access ByteHouse\-CDW’s SQL worksheet function and use SQL queries to verify whether the data has been correctly synchronized to the database

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb6d821643fa435db362798491b443f5~tplv-goo7wpa0wc-image.image) </span>

<span id="893c7026"></span>
## 6 Task stage query

<span id="34cee623"></span>
### 6.1 Confirm task is syncing progress in the full snapshot phase:

Check the JMJobManager log for the key phrases indicating the start of split:

```Plain
2025-01-12 22:08:06,122 INFO  org.apache.flink.cdc.connectors.mysql.source.assigners.MySqlSnapshotSplitAssigner [] - Start splitting table app_db.con_bt_point_info into chunks...
```


After splitting, the snapshot split is issued. For example, app_db.con_bt_point_info:0 represents the first split, and the split number shows the processing progress of the split:

```Plain
2025-01-12 22:08:42,644 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlSnapshotSplit{tableId=app_db.con_bt_point_info, splitId='app_db.con_bt_point_info:0', splitKeyType=[`point_id` BIGINT NOT NULL], splitStart=null, splitEnd=null, highWatermark=null} to subtask 1
```


<span id="38fff328"></span>
### 6.2 Confirm task is syncing progress in the incremental phase:

Check the JobManager log to see the subtask index assigned to the binlog split:

```Java
2025-01-13 11:16:20,315 INFO  org.apache.flink.cdc.connectors.mysql.source.enumerator.MySqlSourceEnumerator [] - The enumerator assigns split MySqlBinlogSplit{splitId='binlog-split', tables=[], offset={ts_sec=0, file=binlog.000426, pos=520322, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1521914, row=0, event=0}, endOffset={ts_sec=0, file=, pos=-9223372036854775808, kind=NON_STOPPING, row=0, event=0}, isSuspended=false} to subtask 0
```


Locate the TM log corresponding to subtask 0:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d408907a50644a2d81927ee00ab48d6f~tplv-goo7wpa0wc-image.image" width="3268px" /></div>


Search for keywords in the TaskManager log to check binlog processing progress. File and pos represent the binlog file and position being read, respectively:

```Java
2025-01-13 11:21:19,039 INFO  org.apache.flink.cdc.connectors.mysql.source.reader.MySqlSourceReader [] - Binlog offset for tables [app_db.shipments, app_db.shipments90, app_db.shipments91, app_db.shipments89, app_db.shipments81, app_db.shipments82, app_db.shipments83, app_db.shipments84, app_db.shipments85, app_db.shipments86, app_db.shipments87, app_db.shipments88, app_db.shipments12] on checkpoint 2: {transaction_id=null, ts_sec=0, file=binlog.000426, pos=687715, kind=SPECIFIC, gtids=da643d88-c37e-11ef-a8e8-5254ac1c7b41:1-1522412, row=0, event=0, server_id=2051901732}
```


<span id="27a14bee"></span>
## 7. Common Issues

<span id="60ea9a2f"></span>
### 7.1 JDBC Driver Not Found Error

**Issue description**: If the task fails to start, the logs show the following exception: `Caused by: java.lang.ClassNotFoundException: com.mysql.cj.jdbc.Driver`.

**Solution**: This issue occurs due to compliance reasons. Flink CDC does not include a built\-in MySQL Driver. Please refer to the [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) documentation to download the official MySQL Driver (recommended version 8.0.27) and upload it to the dependencies of the Flink CDC task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28b42ba3704b4eef885e5626694b8823~tplv-goo7wpa0wc-image.image) </span>

<span id="36ab911b"></span>
### 7.2 Differences between MySQL Datetime and ByteHouse Datetime types

**Issue description**: MySQL datetime is a timezone\-unaware data type that many users use to store local time. For example, `2025-01-09 10:00:00` in the UTC+8 timezone. Since the timezone is unclear, Flink & ByteHouse\-CDW use the UTC timestamp by default during conversion. Therefore, after writing, viewing the time in UTC+8 shows the result as `2025-01-09 18:00:00`. This causes a time difference compared to MySQL.

**Solution:** 


1. Avoid using the datetime type field in MySQL and use the timestamp type field with timezone information instead. This allows Flink to perform timezone conversion based on the server\-time\-zone information.

2. You can set `timestamp-offset: -8h` in Flink CDC to automatically offset the time zone by subtracting 8 hours during the synchronization task. Note that this time zone offset only applies to MySQL Datetime types.

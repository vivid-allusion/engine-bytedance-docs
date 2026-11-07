---
title: "Operation manual for reading and writing Serverless Doris with Serverless Spark"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operation_manual_for_reading_and_writing_Serverless_Doris_with_Serverless_Spark"
---

<span id="88d24423"></span>
## Preparation

<span id="ef523e58"></span>
### Create a TOS bucket


1. Log in to the [TOS console](https://console.volcengine.com/tos/bucket/create) and create a TOS bucket. For specific creation methods, refer to: [Create TOS bucket](https://www.volcengine.com/docs/6349/75024).

2. Create the required directory based on the TOS bucket you created. This directory serves as the default storage directory for the Spark Doris Connector.


<span id="43200913"></span>
### Doris data preparation


1. Log in to the EMR Serverless console and [create a Doris instance](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/create).

2. After connecting to the instance, execute the following SQL statements to prepare the database and tables. For connection methods, see: [Connect to an instance](https://docs.byteplus.com/docs/undefined/69d786c73283c2052d14482c). For basic Doris usage, see: [Basic usage](https://docs.byteplus.com/docs/undefined/69a9626d8252b50542c49af0).


```SQL
CREATE DATABASE if not EXISTS online_database;
USE online_database;
CREATE TABLE table1
(
    siteid INT DEFAULT '10',
    citycode SMALLINT,
    username VARCHAR(32) DEFAULT '',
    pv BIGINT SUM DEFAULT '0'
)
AGGREGATE KEY(siteid, citycode, username)
DISTRIBUTED BY HASH(siteid) BUCKETS 10;
```



3. After data preparation is complete, you can view the data. If the data display content is as follows, data preparation is complete:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b72a14e2720e465e8b86b50efa01c73a~tplv-goo7wpa0wc-image.image" width="1036px" /></div>


<span id="2c76dfa9"></span>
### Serverless Spark data preparation


1. Create a resource queue.

   Log in to the [EMR Serverless console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/queue_manage) to create a Serverless [dedicated queue](https://www.volcengine.com/docs/6491/1391992). When the queue status changes to running, you can proceed to the next step.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When configuring a resource queue, you must enable the features related to <a href="https://www.volcengine.com/docs/6491/1511934">network configuration</a>, and the VPC network used by this queue must be exactly the same as the VPC network used by the Doris instance. This is the only way to ensure network compatibility and connectivity between the queue and the Doris instance, allowing tasks using this queue to successfully access the Doris instance.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to disable the <strong>global cross VPC routing</strong> feature, and only add the <code>set serverless.cross.vpc.access.enabled=true;</code> parameter to tasks that need to access Doris to enable network connectivity.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca78cb1beec444218886fe7113d78a0d~tplv-goo7wpa0wc-image.image) </span>

2. Create a database.

   Log in to the [EMR Serverless](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/query_analysis?projectName=default) page, click **Create job**, go to the **Create job** page, select the created **dedicated queue \> Default compute group**, and execute the `CREATE DATABASE IF NOT EXISTS ss_wr2sr;` command to create the database ss_wr2sr.

3. Create data tables.

   Log in to the [EMR Serverless](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/query_analysis?projectName=default)  **\> Create job \> Edit job** page, select the created **dedicated queue \> Default compute group**, and execute the following commands to create two data tables, ss_table1 and ss_table2, in the database ss_wr2sr.

   ```SQL
   CREATE TABLE if not exists ss_wr2sr.ss_table1(
     `siteid` int,
     `citycode` SMALLINT,
     `username` string,
     `pv` BIGINT
   );
   
   CREATE TABLE if not exists ss_wr2sr.ss_table2(
     `siteid` int,
     `citycode` SMALLINT,
     `username` string,
     `pv` BIGINT
   );
   ```
   


<span id="65b3cb7e"></span>
## Procedure


1. Read and write Doris data tables using Serverless Spark.

   Go to the [EMR Serverless](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/query_analysis?projectName=default) job editing page, enter the Spark SQL statements from the example SQL code block below, and click the **Job editing** page's lower left **Run** button to execute the SQL job.

   ```SQL
   -- Fill in the TOS address of the JAR dependency package
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   -- Optional parameter: set the default directory for Spark SQL.
   set spark.sql.catalog.{your_catalog_name}=org.apache.doris.spark.catalog.DorisTableCatalog;
   set spark.sql.catalog.{your_catalog_name}.doris.fenodes={fe_ip:fe_http_port};
   set spark.sql.catalog.{your_catalog_name}.doris.query.port=9030;
   set spark.sql.catalog.{your_catalog_name}.doris.user={user name};
   set spark.sql.catalog.{your_catalog_name}.doris.password={user password};
   
   show databases;
   SELECT * FROM {your_catalog_name}.online_database.table1;
   INSERT INTO {your_catalog_name}.online_database.table1 select * from db.table;
   ```
   

2. Read Doris data tables and write Hive data tables using Serverless Spark.

   Log in to the [EMR Serverless](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/query_analysis?projectName=default) job editing page, enter the Spark SQL statements from the example SQL code block below, and click the lower left **Run** button in the job editing box to execute the SQL job.

   ```SQL
   -- Fill in the TOS address of the JAR dependency package
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   
   set spark.sql.catalog.{your_catalog_name}=org.apache.doris.spark.catalog.DorisTableCatalog;
   set spark.sql.catalog.{your_catalog_name}.doris.fenodes={fe_ip:fe_http_port};
   set spark.sql.catalog.{your_catalog_name}.doris.query.port=9030;
   set spark.sql.catalog.{your_catalog_name}.doris.user={user name};
   set spark.sql.catalog.{your_catalog_name}.doris.password={user password};
   
   INSERT into ss_wr2sr.ss_table1 SELECT * FROM {your_catalog_name}.online_database.table1;
   ```
   

3. Read Hive data tables and write Doris data tables using Serverless Spark.

   Log in to the [EMR Serverless](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/serverless-spark/query_analysis?projectName=default) job editing page, enter the Spark SQL statements from the example SQL code block below, and click the lower left **Run** button in the job editing box to execute the SQL job.

   ```SQL
   -- Fill in the TOS address of the JAR dependency package
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   
   set spark.sql.catalog.{your_catalog_name}=org.apache.doris.spark.catalog.DorisTableCatalog;
   set spark.sql.catalog.{your_catalog_name}.doris.fenodes={fe_ip:fe_http_port};
   set spark.sql.catalog.{your_catalog_name}.doris.query.port=9030;
   set spark.sql.catalog.{your_catalog_name}.doris.user={user name};
   set spark.sql.catalog.{your_catalog_name}.doris.password={user password};
   
   INSERT into {your_catalog_name}.online_database.table1 SELECT * FROM ss_wr2sr.ss_table2;
   ```
   

4. For more examples and parameters, refer to the [Doris community documentation](https://doris.apache.org/zh-CN/docs/ecosystem/spark-doris-connector).


<span id="d096bdbe"></span>
## Dependency JAR addresses

Download the [required spark-doris-connector package](https://doris.apache.org/zh-CN/docs/ecosystem/spark-doris-connector#maven) from the Doris community documentation and upload it to the corresponding Volcano TOS path.

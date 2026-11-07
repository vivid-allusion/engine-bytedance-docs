---
title: "Serverless Spark operation manual for reading and writing StarRocks (storage-compute separation)"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/operations_for_reading_and_writing"
---

<span id="8ab5857e"></span>
# Environment preparation

<span id="ffd943d5"></span>
## Create a TOS bucket


1. Log in to the [TOS console](https://console.volcengine.com/tos/bucket/create), create a TOS bucket, and refer to the documentation for specific creation steps: [Creating a bucket](https://docs.byteplus.com/en/docs/tos/Creating-a-bucket).

2. Based on the TOS bucket you created, create the required directory. This directory serves as the default storage directory for the StarRocks instance.


<span id="e4d44913"></span>
## StarRocks data preparation


1. Log in to the [EMR Serverless StarRocks](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/create) console and create a StarRocks instance. For detailed creation steps, refer to the Volcano Engine official documentation: [Create instances](https://docs.byteplus.com/docs/E-MapReduce/Create_instances)

2. After connecting to the instance, execute the following SQL to prepare the database and tables. For connection methods, see the official documentation: [Connection instance](https://docs.byteplus.com/docs/E-MapReduce/Connection_instance).


```SQL
CREATE DATABASE if not EXISTS online_database;
USE online_database;
CREATE TABLE log_v1 (
    uid int,
    name varchar(64),
    age int, 
    phone varchar(16),
    last_login datetime,
    credits double
)
DUPLICATE KEY(uid, name);

CREATE TABLE log_v2 (
    uid int,
    name varchar(64),
    age int, 
    phone varchar(16),
    last_login datetime,
    credits double
)
DUPLICATE KEY(uid, name);
```



3. After data preparation is complete, you can view the data. If the data is displayed as follows, data preparation is complete:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30190850be184b5fb429532ce176fe07~tplv-goo7wpa0wc-image.image) </span>

<span id="b9cd81d6"></span>
### Serverless Spark data preparation


1. Create a resource queue: Log in to the [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless-spark/queue_manage) to create a Serverless Spark queue. Create a [按量付费](https://docs.byteplus.com/docs/undefined/68da347342e561058e056a9e) or [包年包月](https://docs.byteplus.com/docs/undefined/68da347342e561058e056a9f) queue as needed. When the queue status changes to Running, you can proceed to the next step.

2. Create a data catalog: Log in to the [Lakehouse Analytics Service](https://console.byteplus.com/las/) to create a custom data catalog (Catalog), and set the [TOS](https://console.volcengine.com/tos) storage location for it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default data directory is hive. To use this data directory, set the default TOS storage location for it.   </div>
   

3. Create a database: Log in to the job editing page, use the default data directory hive, create the database instance ss_w2r_sr, and use the following SQL:

   ```SQL
   CREATE DATABASE IF NOT EXISTS ss_w2r_sr;
   ```
   

4. Data tables: Log in to the [EMR Serverless Spark](https://console.byteplus.com/emr/) job editing page. Use the default data catalog hive, and create two data tables, log_v1 and log_v2, in the database instance ss_w2r_sr. Here, the location is the TOS address of the database instance plus the table name. The database instance address can be queried through [Lakehouse Analytics Service](https://console.byteplus.com/las/).

   ```SQL
   CREATE TABLE if not exists ss_w2r_sr.log_v1(
     `uid` int, 
     `name` string, 
     `age` int, 
     `phone` string, 
     `last_login` TIMESTAMP, 
     `credits` double)
   PARTITIONED BY ( 
     `date` string)
   ROW FORMAT DELIMITED
   FIELDS TERMINATED BY ','
   STORED AS TEXTFILE
   location 'tos://{Database TOS storage address}/log_v1';
   
   CREATE TABLE if not exists ss_w2r_sr.log_v2(
     `uid` int, 
     `name` string, 
     `age` int, 
     `phone` string, 
     `last_login` TIMESTAMP, 
     `credits` double)
   PARTITIONED BY ( 
     `date` string)
   ROW FORMAT DELIMITED
   FIELDS TERMINATED BY ','
   STORED AS TEXTFILE
   location 'tos://{Database TOS storage address}/log_v2';
   ```
   

5. Configure security group: Log in to Volcano Engine and create a security group instance. In the private network list, select the VPC used by the StarRocks instance, and set the inbound rules as shown below to complete the creation of the security group instance:


<span id="7e413580"></span>
# Execution steps


1. Read and write StarRocks data tables using Serverless Spark

   Log in to the job editing page, enter the Spark SQL statements from the following SQL code block examples, and click the "Run" button at the lower right corner of the job editing box to execute the SQL job.

   ```SQL
   -- starrocks fe url
   set spark.sql.catalog.starrocks.fe.http.url=http://{local ip address}:8030;
   set spark.sql.catalog.starrocks.fe.jdbc.url=jdbc:mysql://{local ip address}:9030;
   -- user name with admin right in starrocks instance
   set spark.sql.catalog.starrocks.user={user name};
   -- user password
   set spark.sql.catalog.starrocks.password={user password};
   -- starrocks instance TOS endpoint, such as https://tos-s3-cn-beijing.ivolces.com
   set spark.sql.catalog.starrocks.fs.s3a.endpoint={endpoint};
   -- starrocks instance TOS region, such as cn-beijing
   set spark.sql.catalog.starrocks.fs.s3a.endpoint.region={region name};
   set spark.sql.catalog.starrocks.fs.s3a.access.key={access key};
   set spark.sql.catalog.starrocks.fs.s3a.secret.key={secret key};
   
   set tqs.query.engine.type = sparkcli;
   set las.cross.vpc.access.enabled = true;
   set las.cross.vpc.vpc.id = {vpc id};
   set las.cross.vpc.subnet.id = {subnet id};
   set las.cross.vpc.security.group.id = {security group id};
   set las.cross.vpc.accountId = {volc account id};
   
   set spark.sql.catalog.starrocks.batch.size=8092;
   set spark.sql.catalog.starrocks.writer.mode=BYPASS;
   set spark.sql.catalog.starrocks.reader.mode=BYPASS;
   set spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled=true;
   set spark.sql.catalog.starrocks.fs.s3a.path.style.access=false;
   set spark.sql.catalog.starrocks.fs.s3a.retry.limit=27;
   set spark.sql.catalog.starrocks=com.starrocks.connector.spark.catalog.StarRocksCatalog;
   set spark.sql.storeAssignmentPolicy = ansi;
   -- depend jar address, please refer to "Dependency JAR addresses" for jar addresses of online regions
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   
   set spark.shuffle.manager = sort;
   set spark.dynamicAllocation.enabled = false;
   set spark.sql.serverless.lf.auth.enabled = false;
   set spark.sql.extensions=com.starrocks.connector.spark.StarRocksExtensions;
   
   use starrocks;
   insert into table online_database.log_v2
   select * from online_database.log_v1;
   select * from online_database.log_v2;
   ```
   

2. Read StarRocks data tables and write Hive data tables using Serverless Spark

   Log in to the job editing page, enter the Spark SQL statements from the following SQL code block examples, and click the "Run" button at the lower right corner of the job editing box to execute the SQL job.

   ```SQL
   -- starrocks fe url
   set spark.sql.catalog.starrocks.fe.http.url=http://{local ip address}:8030;
   set spark.sql.catalog.starrocks.fe.jdbc.url=jdbc:mysql://{local ip address}:9030;
   -- user name with admin right in starrocks instance
   set spark.sql.catalog.starrocks.user={user name};
   -- user password
   set spark.sql.catalog.starrocks.password={user password};
   -- starrocks instance TOS endpoint, such as https://tos-s3-cn-beijing.ivolces.com
   set spark.sql.catalog.starrocks.fs.s3a.endpoint={endpoint};
   -- starrocks instance TOS region, such as cn-beijing
   set spark.sql.catalog.starrocks.fs.s3a.endpoint.region={region name};
   set spark.sql.catalog.starrocks.fs.s3a.access.key={access key};
   set spark.sql.catalog.starrocks.fs.s3a.secret.key={secret key};
   
   set tqs.query.engine.type = sparkcli;
   set las.cross.vpc.access.enabled = true;
   set las.cross.vpc.vpc.id = {vpc id};
   set las.cross.vpc.subnet.id = {subnet id};
   set las.cross.vpc.security.group.id = {security group id};
   set las.cross.vpc.accountId = {volc account id};
   
   set spark.sql.catalog.starrocks.batch.size=8092;
   set spark.sql.catalog.starrocks.writer.mode=BYPASS;
   set spark.sql.catalog.starrocks.reader.mode=BYPASS;
   set spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled=true;
   set spark.sql.catalog.starrocks.fs.s3a.path.style.access=false;
   set spark.sql.catalog.starrocks.fs.s3a.retry.limit=27;
   set spark.sql.catalog.starrocks=com.starrocks.connector.spark.catalog.StarRocksCatalog;
   set spark.sql.storeAssignmentPolicy = ansi;
   -- depend jar address, please refer to "Dependency JAR addresses" for jar addresses of online regions
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   
   set spark.shuffle.manager = sort;
   set spark.dynamicAllocation.enabled = false;
   set spark.sql.serverless.lf.auth.enabled = false;
   set spark.sql.extensions=com.starrocks.connector.spark.StarRocksExtensions;
                                                        
   use starrocks;
   WITH temp AS (
       select uid, name, age, phone, last_login, credits from online_database.log_v1
   )
   insert overwrite table spark_catalog.ss_w2r_sr.log_v1 partition(date)
   select uid + cast(rand() * 900 + 10 as int), CONCAT(name,'_1'), age, phone, last_login, credits, '20240601' from temp;
   select * from spark_catalog.ss_w2r_sr.log_v1;
   ```
   

3. Read Hive tables using Serverless Spark and write to Starrocks tables

   Log in to the [EMR Serverless Spark](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless-spark/query_analysis?projectName=default) job editing page, enter the example Spark SQL statements in the following SQL code block, and click the "Run" button in the lower right corner of the job editor to execute the SQL job.

   ```SQL
   -- starrocks fe url
   set spark.sql.catalog.starrocks.fe.http.url=http://{local ip address}:8030;
   set spark.sql.catalog.starrocks.fe.jdbc.url=jdbc:mysql://{local ip address}:9030;
   -- user name with admin right in starrocks instance
   set spark.sql.catalog.starrocks.user={user name};
   -- user password
   set spark.sql.catalog.starrocks.password={user password};
   -- starrocks instance TOS endpoint, such as https://tos-s3-cn-beijing.ivolces.com
   set spark.sql.catalog.starrocks.fs.s3a.endpoint={endpoint};
   -- starrocks instance TOS region, such as cn-beijing
   set spark.sql.catalog.starrocks.fs.s3a.endpoint.region={region name};
   set spark.sql.catalog.starrocks.fs.s3a.access.key={access key};
   set spark.sql.catalog.starrocks.fs.s3a.secret.key={secret key};
   
   set tqs.query.engine.type = sparkcli;
   set las.cross.vpc.access.enabled = true;
   set las.cross.vpc.vpc.id = {vpc id};
   set las.cross.vpc.subnet.id = {subnet id};
   set las.cross.vpc.security.group.id = {security group id};
   set las.cross.vpc.accountId = {volc account id};
   
   set tqs.query.engine.type = sparkcli;
   set las.cross.vpc.access.enabled = true;
   set las.cross.vpc.vpc.id = {vpc id};
   set las.cross.vpc.subnet.id = {subnet id};
   set las.cross.vpc.security.group.id = {security group id};
   set las.cross.vpc.accountId = {volc account id};
   
   set spark.sql.catalog.starrocks.batch.size=8092;
   set spark.sql.catalog.starrocks.writer.mode=BYPASS;
   set spark.sql.catalog.starrocks.reader.mode=BYPASS;
   set spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled=true;
   set spark.sql.catalog.starrocks.fs.s3a.path.style.access=false;
   set spark.sql.catalog.starrocks.fs.s3a.retry.limit=27;
   set spark.sql.catalog.starrocks=com.starrocks.connector.spark.catalog.StarRocksCatalog;
   set spark.sql.storeAssignmentPolicy = ansi;
   -- depend jar address, please refer to "Dependency JAR addresses" for jar addresses of online regions
   set las.spark.jar.depend.jars = [{"fileName":"{dependency jar address}"}];
   
   set spark.shuffle.manager = sort;
   set spark.dynamicAllocation.enabled = false;
   set spark.sql.serverless.lf.auth.enabled = false;
   set spark.sql.extensions=com.starrocks.connector.spark.StarRocksExtensions;
           
   use starrocks;
   WITH temp AS (
     select uid, name, age, phone, last_login, credits from spark_catalog.ss_w2r_sr.log_v1
   )
   insert into table online_database.log_v1 
   select * from temp;
   select * from online_database.log_v1;
   ```
   


<span id="53bfe0e2"></span>
## Dependency JAR addresses


|**Region** |**JAR address** |
|---|---|
|North China \- Beijing |tos://emr\-serverless\-spark/spark/shared\-lib/starrocks\-connector/starrocks\-spark\-connector\-3.5_2.12\-1.1.2\-ve\-bypass\-4.jar |
|East China \- Shanghai |tos://emr\-serverless\-spark\-shanghai/spark/shared\-lib/starrocks\-connector/starrocks\-spark\-connector\-3.5_2.12\-1.1.2\-ve\-bypass\-4.jar |
|South China \- Guangzhou |tos://emr\-serverless\-spark\-guangzhou/spark/shared\-lib/starrocks\-connector/starrocks\-spark\-connector\-3.5_2.12\-1.1.2\-ve\-bypass\-4.jar |
|Southeast Asia \- Johor |tos://emr\-serverless\-spark\-ap\-southeast\-1/spark/shared\-lib/starrocks\-connector/starrocks\-spark\-connector\-3.5_2.12\-1.1.2\-ve\-bypass\-4.jar |
|East China \- Shanghai \- Autonomous Driving Cloud |tos://emr\-serverless\-spark\-cn\-shanghai\-autodriving/spark/shared\-lib/starrocks\-connector/starrocks\-spark\-connector\-3.5_2.12\-1.1.2\-ve\-bypass\-4.jar |

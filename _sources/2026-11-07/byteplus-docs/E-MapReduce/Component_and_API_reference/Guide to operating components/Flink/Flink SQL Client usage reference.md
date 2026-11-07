---
title: "Flink SQL Client usage reference"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Flink_SQL_Client_usage_reference"
---

The official Flink SQL client supports writing SQL, debugging, and submitting Flink jobs to a Flink cluster. For detailed usage instructions, refer to [Flink official documentation](https://nightlies.apache.org/flink/flink-docs-master/docs/dev/table/sqlclient/).

This article additionally introduces several use cases of Volcano Engine E\-MapReduce (EMR) Flink.

<span id="_1-flink-sql-client-运行模式"></span>
## 1 Flink SQL Client operation modes

Under Volcano EMR Flink, you can use the SQL client to submit Flink SQL jobs to either a standalone cluster or a Yarn cluster.

<span id="_1-1-standlone-集群场景"></span>
### 1.1 Standalone cluster scenario

In the standalone scenario, you need to start a standalone cluster first. You can run the following command in the `FLINK_HOME` directory (default is `/usr/lib/emr/current/flink`) to create it:

```bash
./bin/start-cluster.sh
```


After the standalone cluster is successfully started, you can execute the following command to launch the SQL client command\-line interface:

```bash
./bin/sql-client.sh embedded
```


To stop the standalone cluster, execute the following command:

```bash
./bin/stop-cluster.sh
```


<span id="_1-2-yarn-集群场景"></span>
### 1.2 Yarn cluster scenario

In the Yarn cluster scenario, multiple Flink job submission modes are supported, including Yarn\-Session mode, Per\-Job Cluster mode, and Application mode.

Flink SQL Client currently does not support [Application mode](https://issues.apache.org/jira/browse/FLINK-26541)

<span id="_1-2-1-session-模式"></span>
#### 1.2.1 Session mode

In Session mode, you need to execute the following command to start a Yarn Session:

```bash
./bin/yarn-session.sh -d
```


After the Yarn Session is successfully started, a `/tmp/.yarn-properties-root` file will be created, recording the Application ID of the most recent submission to Yarn. Execute the following command to launch the SQL client command\-line interface. Subsequent specified Flink SQL jobs will be submitted to the previously started Yarn Session Application.

```bash
./bin/sql-client.sh embedded -s yarn-session
```


You can execute the following command to stop the currently running Yarn Session.

```bash
cat /tmp/.yarn-properties-root | grep applicationID | cut -d'=' -f 2 | xargs -I {} yarn application -kill {}
```


<span id="_1-2-2-per-job-cluster-模式"></span>
#### 1.2.2 Per\-Job Cluster mode

Per\-Job Cluster mode does not require starting a cluster in advance. You can launch the SQL client command\-line interface and set `execution.target`. Each subsequent Flink SQL job will be submitted to Yarn as an independent job.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The yarn\-per\-job mode has been marked as deprecated in Flink 1.16.</div>


```bash
./bin/sql-client.sh embedded

Flink SQL> set execution.target=yarn-per-job;
[INFO] Session property has been set.
```


You can also predefine this parameter in the `flink-conf.yaml` configuration file.

```bash
# flink-conf.yaml
execution.target: yarn-per-job
```


<span id="_2-flink-sql-集成-tos"></span>
## 2 Flink SQL integration with TOS

Volcano EMR Flink supports multiple methods for reading and writing to TOS object storage, such as using Hive Connector, Hudi Connector, and more.

<span id="_2-1-flink-sql-集成-hive-connector"></span>
### 2.1 Flink SQL integration with Hive Connector

The following uses yarn\-session mode as an example to demonstrate how to integrate Hive Connector.


1. Launch the SQL client command\-line interface


```bash
./bin/yarn-session.sh -d
./bin/sql-client.sh embedded -s yarn-session -j connectors/flink-sql-connector-hive-3.1.2_2.12-1.16.1.jar
```



2. Create Hive Catalog and Demo database


```bash
Flink SQL> CREATE CATALOG hive WITH (
>   'type' = 'hive',
>   'hive-conf-dir' = '/etc/emr/hive/conf'
> );
[INFO] Execute statement succeed.

Flink SQL> use catalog hive;
[INFO] Execute statement succeed.

Flink SQL> create database demo_db;
[INFO] Execute statement succeed.

Flink SQL> show databases;
+---------------+
| database name |
+---------------+
|       default |
|       demo_db |
+---------------+
3 rows in set
```



3. Create a table


You can create Hive tables using other engines, such as Spark or Hive, or switch to Hive Dialect mode in the Flink SQL client.


* Create a table using Spark engine


```bash
# Launch the Spark SQL command-line interface
spark-sql

spark-sql> CREATE TABLE demo_tbl1 (
         >     uuid STRING,
         >     name STRING,
         >     age INT,
         >     ts TIMESTAMP
         > )
         > PARTITIONED BY (`partition` STRING);
Time taken: 0.652 seconds

spark-sql> desc formatted demo_tbl1;
uuid                        string
name                        string
age                         int
ts                          timestamp
partition                   string
# Partition Information
# col_name                  data_type                   comment
partition                   string

# Detailed Table Information
Database                    demo_db
Table                       demo_tbl1
Created Time                Fri Nov 25 15:04:43 CST 2022
Last Access                 UNKNOWN
Created By                  Spark 3.2.1
Type                        MANAGED
Provider                    hive
Comment
Table Properties            [bucketing_version=2, sink.partition-commit.policy.kind=metastore, transient_lastDdlTime=1669359883]
Location                    tos://xxxxx-v2/hms-warehouse/demo_db.db/demo_tbl1
Serde Library               org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe
InputFormat                 org.apache.hadoop.mapred.TextInputFormat
OutputFormat                org.apache.hadoop.hive.ql.io.IgnoreKeyTextOutputFormat
Storage Properties          [serialization.format=1]
Partition Provider          Catalog
Time taken: 0.085 seconds, Fetched 25 row(s)
```



* Create a table using Flink Hive Dialect


Starting from Flink 1.16, to use Hive Dialect mode, you need to adjust some Jar dependencies in the Flink system. For details, refer to [Flink SQL Client usage reference](https://docs.byteplus.com/docs/E-MapReduce/109229). You can execute the following command to prepare the required Jar packages.

```bash
# Enter FLINK_HOME
mv lib/flink-table-planner-loader-1.16.1.jar opt/
cp opt/flink-table-planner_2.12-1.16.1.jar lib/
cp connectors/flink-sql-connector-hive-3.1.2_2.12-1.16.1.jar lib/
```


After adjusting the Jar dependencies, you need to restart yarn\-session and sql\-client. The table creation content is as follows:

```bash
./bin/sql-client.sh embedded -s yarn-session

Flink SQL> set table.sql-dialect=hive;
[INFO] Session property has been set.

Flink SQL> CREATE CATALOG hive WITH (
>   'type' = 'hive',
>   'hive-conf-dir' = '/etc/emr/hive/conf'
> );
[INFO] Execute statement succeed.

Flink SQL> use catalog hive;
[INFO] Execute statement succeed.

CREATE TABLE `hive`.`demo_db`.`demo_tbl2` (
    uuid STRING, 
    name STRING, 
    age INT,
    ts TIMESTAMP
)
PARTITIONED BY (`partition` STRING)
LOCATION 'tos://{bucket_name}/hms-warehouse/demo_db.db/demo_tbl2'
TBLPROPERTIES (
    'sink.partition-commit.policy.kind'='metastore'
);
```


It is recommended that, in non\-hive dialect scenarios, connector Jar package dependencies should not be placed in the lib directory.


4. Read and write data

* Batch read and write data


```bash
Flink SQL> SET 'execution.runtime-mode' = 'batch'; # It is recommended to configure in flink-conf.yaml
[INFO] Session property has been set.

Flink SQL> INSERT INTO `hive`.`demo_db`.`demo_tbl1` VALUES
>   ('id21','Danny',23,TIMESTAMP '1970-01-01 00:00:01','par1'),
>   ('id22','Stephen',33,TIMESTAMP '1970-01-01 00:00:02','par1'),
>   ('id23','Julian',53,TIMESTAMP '1970-01-01 00:00:03','par2'),
>   ('id24','Fabian',31,TIMESTAMP '1970-01-01 00:00:04','par2'),
>   ('id25','Sophia',18,TIMESTAMP '1970-01-01 00:00:05','par3'),
>   ('id26','Emma',20,TIMESTAMP '1970-01-01 00:00:06','par3'),
>   ('id27','Bob',44,TIMESTAMP '1970-01-01 00:00:07','par4'),
>   ('id28','Han',56,TIMESTAMP '1970-01-01 00:00:08','par4');
[INFO] Submitting SQL update statement to the cluster...


Flink SQL> SET 'sql-client.execution.result-mode' = 'tableau'; # It is recommended to configure in flink-conf.yaml
[INFO] Session property has been set.

Flink SQL> select * from `hive`.`demo_db`.`demo_tbl1`;
+------+---------+-----+-------------------------------+-----------+
| uuid |    name | age |                            ts | partition |
+------+---------+-----+-------------------------------+-----------+
| id27 |     Bob |  44 | 1970-01-01 00:00:07.000000000 |      par4 |
| id26 |    Emma |  20 | 1970-01-01 00:00:06.000000000 |      par3 |
| id22 | Stephen |  33 | 1970-01-01 00:00:02.000000000 |      par1 |
| id25 |  Sophia |  18 | 1970-01-01 00:00:05.000000000 |      par3 |
| id21 |   Danny |  23 | 1970-01-01 00:00:01.000000000 |      par1 |
| id28 |     Han |  56 | 1970-01-01 00:00:08.000000000 |      par4 |
| id23 |  Julian |  53 | 1970-01-01 00:00:03.000000000 |      par2 |
| id24 |  Fabian |  31 | 1970-01-01 00:00:04.000000000 |      par2 |
+------+---------+-----+-------------------------------+-----------+
8 rows in set
```



* Streaming read and write data


When performing streaming writes to partitioned tables, you need to set a partition commit policy to notify downstream systems that a particular partition has been fully written and can now be read. For non\-partitioned tables, this setting is optional and can also be configured in the table properties when creating the table.

```bash
# Switch to streaming mode
Flink SQL> SET 'execution.runtime-mode' = 'streaming';
[INFO] Session property has been set.

# For partitioned tables, modify table properties or set this property when creating the table
Flink SQL> ALTER TABLE `hive`.`demo_db`.`demo_tbl1` SET ('sink.partition-commit.policy.kind'='metastore');
[INFO] Execute statement succeed.

Flink SQL> INSERT INTO `hive`.`demo_db`.`demo_tbl1` VALUES
>   ('id11','Danny',23,TIMESTAMP '1970-01-01 00:00:01','par1'),
>   ('id12','Stephen',33,TIMESTAMP '1970-01-01 00:00:02','par1'),
>   ('id13','Julian',53,TIMESTAMP '1970-01-01 00:00:03','par2'),
>   ('id14','Fabian',31,TIMESTAMP '1970-01-01 00:00:04','par2'),
>   ('id15','Sophia',18,TIMESTAMP '1970-01-01 00:00:05','par3'),
>   ('id16','Emma',20,TIMESTAMP '1970-01-01 00:00:06','par3'),
>   ('id17','Bob',44,TIMESTAMP '1970-01-01 00:00:07','par4'),
>   ('id18','Han',56,TIMESTAMP '1970-01-01 00:00:08','par4');
[INFO] Submitting SQL update statement to the cluster...

Flink SQL> select * from `hive`.`demo_db`.`demo_tbl1`;
+----+--------------------------------+--------------------------------+-------------+-------------------------------+--------------------------------+
| op |                           uuid |                           name |         age |                            ts |                      partition |
+----+--------------------------------+--------------------------------+-------------+-------------------------------+--------------------------------+
| +I |                           id14 |                         Fabian |          31 | 1970-01-01 00:00:04.000000000 |                           par2 |
| +I |                           id28 |                            Han |          56 | 1970-01-01 00:00:08.000000000 |                           par4 |
| +I |                           id26 |                           Emma |          20 | 1970-01-01 00:00:06.000000000 |                           par3 |
| +I |                           id13 |                         Julian |          53 | 1970-01-01 00:00:03.000000000 |                           par2 |
| +I |                           id12 |                        Stephen |          33 | 1970-01-01 00:00:02.000000000 |                           par1 |
| +I |                           id15 |                         Sophia |          18 | 1970-01-01 00:00:05.000000000 |                           par3 |
| +I |                           id18 |                            Han |          56 | 1970-01-01 00:00:08.000000000 |                           par4 |
| +I |                           id11 |                          Danny |          23 | 1970-01-01 00:00:01.000000000 |                           par1 |
| +I |                           id27 |                            Bob |          44 | 1970-01-01 00:00:07.000000000 |                           par4 |
| +I |                           id22 |                        Stephen |          33 | 1970-01-01 00:00:02.000000000 |                           par1 |
| +I |                           id17 |                            Bob |          44 | 1970-01-01 00:00:07.000000000 |                           par4 |
| +I |                           id25 |                         Sophia |          18 | 1970-01-01 00:00:05.000000000 |                           par3 |
| +I |                           id24 |                         Fabian |          31 | 1970-01-01 00:00:04.000000000 |                           par2 |
| +I |                           id16 |                           Emma |          20 | 1970-01-01 00:00:06.000000000 |                           par3 |
| +I |                           id23 |                         Julian |          53 | 1970-01-01 00:00:03.000000000 |                           par2 |
| +I |                           id21 |                          Danny |          23 | 1970-01-01 00:00:01.000000000 |                           par1 |
+----+--------------------------------+--------------------------------+-------------+-------------------------------+--------------------------------+
Received a total of 16 rows
```


<span id="_2-2-flink-sql-集成-hudi-connector"></span>
### 2.2 Flink SQL integration with Hudi connector

Flink integrates directly with Hudi to perform read and write operations on TOS, and synchronizes metadata to HMS for querying by other engines. The following example uses Yarn per\-job to demonstrate the relevant integration operations.

Flink integration with Hudi requires the hudi\-flink\-bundle package. Currently, in EMR clusters with Hudi enabled, the hudi\-flink\-bundle package is provided by default.


1. Launch the SQL client command\-line interface


```bash
./bin/sql-client.sh embedded -j connectors/flink-sql-connector-hive-3.1.2_2.12-1.16.1.jar
```



2. Create a Hudi table and enable HMS Hive Sync


For example, create a COW table and persist the Hudi table that Flink creates in HMS. For detailed information on Flink integration with Hudi, refer to [the official Hudi documentation](https://hudi.apache.org/docs/flink-quick-start-guide/).

```bash
CREATE CATALOG hive WITH (
  'type' = 'hive',
  'hive-conf-dir' = '/etc/emr/hive/conf'
);

CREATE TABLE `hive`.`demo_db`.`flink_hudi_cow_tbl_hms_sync_demo_original` (
  uuid VARCHAR(20),
  name VARCHAR(10),
  age INT,
  ts TIMESTAMP(3),
  `partition` VARCHAR(20)
)
PARTITIONED BY (`partition`)
WITH (
  'connector' = 'hudi',
  'path' = 'tos://{bucket_name}/hms-warehouse/demo_db.db/flink_hudi_cow_tbl_hms_sync_demo',
  'table.type' = 'COPY_ON_WRITE',
  'hive_sync.enable' = 'true',
  'hive_sync.mode' = 'hms',
  'hive_sync.metastore.uris' = 'thrift://{ip}:{port}',
  'hive_sync.table'='flink_hudi_cow_tbl_hms_sync_demo', 
  'hive_sync.db'='demo_db'
);
```



3. Perform read and write operations using Flink SQL


Write data to the COW table. After the data is successfully written, metadata will be synchronized to the table specified by `hive_sync.table`. In the COW scenario, only one target table is created. In the MOR scenario, in addition to the target table, `RO` and `RT` tables are also created.

```bash
INSERT INTO `hive`.`demo_db`.`flink_hudi_cow_tbl_hms_sync_demo_original` VALUES
  ('id41','Danny',23,TIMESTAMP '1970-01-01 00:00:01','par1'),
  ('id42','Stephen',33,TIMESTAMP '1970-01-01 00:00:02','par1'),
  ('id43','Julian',53,TIMESTAMP '1970-01-01 00:00:03','par2'),
  ('id44','Fabian',31,TIMESTAMP '1970-01-01 00:00:04','par2'),
  ('id45','Sophia',18,TIMESTAMP '1970-01-01 00:00:05','par3'),
  ('id46','Emma',20,TIMESTAMP '1970-01-01 00:00:06','par3'),
  ('id47','Bob',44,TIMESTAMP '1970-01-01 00:00:07','par4'),
  ('id48','Han',56,TIMESTAMP '1970-01-01 00:00:08','par4');
  
Flink SQL> show tables;
+-------------------------------------------+
|                                table name |
+-------------------------------------------+
|          flink_hudi_cow_tbl_hms_sync_demo |
| flink_hudi_cow_tbl_hms_sync_demo_original |
+-------------------------------------------+

Flink SQL> select * from `hive`.`demo_db`.`flink_hudi_cow_tbl_hms_sync_demo_original`;
+----+--------------------------------+--------------------------------+-------------+-------------------------+--------------------------------+
| op |                           uuid |                           name |         age |                      ts |                      partition |
+----+--------------------------------+--------------------------------+-------------+-------------------------+--------------------------------+
| +I |                           id38 |                            Han |          56 | 1970-01-01 00:00:08.000 |                           par4 |
| +I |                           id37 |                            Bob |          44 | 1970-01-01 00:00:07.000 |                           par4 |
| +I |                           id31 |                          Danny |          23 | 1970-01-01 00:00:01.000 |                           par1 |
| +I |                           id32 |                        Stephen |          33 | 1970-01-01 00:00:02.000 |                           par1 |
| +I |                           id35 |                         Sophia |          18 | 1970-01-01 00:00:05.000 |                           par3 |
| +I |                           id36 |                           Emma |          20 | 1970-01-01 00:00:06.000 |                           par3 |
| +I |                           id33 |                         Julian |          53 | 1970-01-01 00:00:03.000 |                           par2 |
| +I |                           id34 |                         Fabian |          31 | 1970-01-01 00:00:04.000 |                           par2 |
+----+--------------------------------+--------------------------------+-------------+-------------------------+--------------------------------+
```



4. Perform read operations using the Spark engine


```bash
spark-sql --conf 'spark.serializer=org.apache.spark.serializer.KryoSerializer' \
--conf 'spark.sql.extensions=org.apache.spark.sql.hudi.HoodieSparkSessionExtension' \
--conf 'spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog'

spark-sql> use demo_db;

spark-sql> show tables;
flink_hudi_cow_tbl_hms_sync_demo
flink_hudi_cow_tbl_hms_sync_demo_original
Time taken: 0.072 seconds, Fetched 2 row(s)

spark-sql> select * from flink_hudi_cow_tbl_hms_sync_demo;
20221125181029843        20221125181029843_2_0        id31        par1        1bde4613-4260-4349-bf4a-23a4a5d35c77_2-4-0_20221126092842836.parquet        id31        Danny        231970-01-01 08:00:01        par1
20221125181029843        20221125181029843_2_1        id32        par1        1bde4613-4260-4349-bf4a-23a4a5d35c77_2-4-0_20221126092842836.parquet        id32        Stephen        331970-01-01 08:00:02        par1
20221126092842836        20221126092842836_2_2        id42        par1        1bde4613-4260-4349-bf4a-23a4a5d35c77_2-4-0_20221126092842836.parquet        id42        Stephen        331970-01-01 08:00:02        par1
20221126092842836        20221126092842836_2_3        id41        par1        1bde4613-4260-4349-bf4a-23a4a5d35c77_2-4-0_20221126092842836.parquet        id41        Danny        231970-01-01 08:00:01        par1
20221125181029843        20221125181029843_1_0        id33        par2        4bd429d0-6af4-47c5-829f-887568c015f7_1-4-0_20221126092842836.parquet        id33        Julian        531970-01-01 08:00:03        par2
20221125181029843        20221125181029843_1_1        id34        par2        4bd429d0-6af4-47c5-829f-887568c015f7_1-4-0_20221126092842836.parquet        id34        Fabian        311970-01-01 08:00:04        par2
20221126092842836        20221126092842836_1_2        id44        par2        4bd429d0-6af4-47c5-829f-887568c015f7_1-4-0_20221126092842836.parquet        id44        Fabian        311970-01-01 08:00:04        par2
20221126092842836        20221126092842836_1_3        id43        par2        4bd429d0-6af4-47c5-829f-887568c015f7_1-4-0_20221126092842836.parquet        id43        Julian        531970-01-01 08:00:03        par2
20221125181029843        20221125181029843_0_0        id35        par3        8f4f152c-898c-44f1-aeea-4d8e158a24ff_0-4-0_20221126092842836.parquet        id35        Sophia        181970-01-01 08:00:05        par3
20221125181029843        20221125181029843_0_1        id36        par3        8f4f152c-898c-44f1-aeea-4d8e158a24ff_0-4-0_20221126092842836.parquet        id36        Emma        201970-01-01 08:00:06        par3
20221126092842836        20221126092842836_0_2        id46        par3        8f4f152c-898c-44f1-aeea-4d8e158a24ff_0-4-0_20221126092842836.parquet        id46        Emma        201970-01-01 08:00:06        par3
20221126092842836        20221126092842836_0_3        id45        par3        8f4f152c-898c-44f1-aeea-4d8e158a24ff_0-4-0_20221126092842836.parquet        id45        Sophia        181970-01-01 08:00:05        par3
20221125181029843        20221125181029843_3_0        id38        par4        24b3d004-5111-4ecd-8bb3-aa8ee80d5f7a_3-4-0_20221126092842836.parquet        id38        Han        561970-01-01 08:00:08        par4
20221125181029843        20221125181029843_3_1        id37        par4        24b3d004-5111-4ecd-8bb3-aa8ee80d5f7a_3-4-0_20221126092842836.parquet        id37        Bob        441970-01-01 08:00:07        par4
20221126092842836        20221126092842836_3_2        id48        par4        24b3d004-5111-4ecd-8bb3-aa8ee80d5f7a_3-4-0_20221126092842836.parquet        id48        Han        561970-01-01 08:00:08        par4
20221126092842836        20221126092842836_3_3        id47        par4        24b3d004-5111-4ecd-8bb3-aa8ee80d5f7a_3-4-0_20221126092842836.parquet        id47        Bob        441970-01-01 08:00:07        par4
Time taken: 7.876 seconds, Fetched 16 row(s)
```


<span id="_2-3-flink-sql-集成-doris-connector"></span>
### 2.3 Flink SQL integration with Doris connector

Huoshang EMR Flink supports writing data to Doris via the Flink Doris Connector, and the Doris Connector is built into the connector directory. The following example uses Yarn per\-job to demonstrate reading and writing Doris data with Flink.


1. Launch the SQL client command\-line interface


```shell
# 注意不同EMR版本，connector包的版本有差异，可根据实际connector的版本进行调整
/usr/lib/emr/current/flink/bin/sql-client.sh embedded \
-j connectors/flink-doris-connector-1.16-1.3.0-ve-1.jar
```



2. Connect to Doris remotely and create the target table.


Refer to [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109207) to create the corresponding user account.

```sql
-- mysql -hxxx.xxx.xx -P9030 -uxxxx -p

CREATE DATABASE demo_db;
USE demo_db;

CREATE TABLE all_employees_info (
    emp_no       int NOT NULL,
    birth_date   date,
    first_name   varchar(20),
    last_name    varchar(20),
    gender       char(2),
    hire_date    date
)
UNIQUE KEY(`emp_no`, `birth_date`)
DISTRIBUTED BY HASH(`birth_date`) BUCKETS 1
PROPERTIES (
"replication_allocation" = "tag.location.default: 1"
);
```



3. Create a Doris Sink table in Flink and insert data


```sql
-- create Doris sink table
CREATE TABLE doris_sink (
    emp_no       int ,
    birth_date   STRING,
    first_name   STRING,
    last_name    STRING,
    gender       STRING,
    hire_date    STRING
) 
WITH (
  'connector' = 'doris',
  'fenodes' = '192.168.1.41:8030',
  'table.identifier' = 'demo_db.all_employees_info',
  'username' = 'test_user',
  'password' = 'test_passwd',
  'sink.properties.two_phase_commit'='true',
  'sink.label-prefix'='doris_demo_emp_001'
);


Flink SQL> INSERT INTO `doris_sink` VALUES 
(10001,'1953-09-02','Georgi','Facello','M','1986-06-26'),
(10002,'1964-06-02','Bezalel','Simmel','F','1985-11-21'),
(10003,'1959-12-03','Parto','Bamford','M','1986-08-28'),
(10004,'1954-05-01','Chirstian','Koblick','M','1986-12-01'),
(10005,'1955-01-21','Kyoichi','Maliniak','M','1989-09-12'),
(10006,'1953-04-20','Anneke','Preusig','F','1989-06-02'),
(10007,'1957-05-23','Tzvetan','Zielinski','F','1989-02-10'),
(10008,'1958-02-19','Saniya','Kalloufi','M','1994-09-15'),
(10009,'1952-04-19','Sumant','Peac','F','1985-02-18'),
(10010,'1963-06-01','Duangkaew','Piveteau','F','1989-08-24');
```



4. Create a Doris Source table in Flink and read data


```sql
-- create Doris source table
Flink SQL> CREATE TABLE doris_source (
    emp_no       int ,
    birth_date   DATE,
    first_name   STRING,
    last_name    STRING,
    gender       STRING,
    hire_date    DATE
) 
WITH (
  'connector' = 'doris',
  'fenodes' = '192.168.1.41:8030',
  'table.identifier' = 'demo_db.all_employees_info',
  'username' = 'test_user',
  'password' = 'test_passwd',
  'doris.read.field' = 'emp_no,birth_date,first_name,last_name,gender,hire_date'
);

-- read data
Flink SQL> select * from doris_source;
+----+-------------+------------+--------------------------------+--------------------------------+--------------------------------+------------+
| op |      emp_no | birth_date |                     first_name |                      last_name |                         gender |  hire_date |
+----+-------------+------------+--------------------------------+--------------------------------+--------------------------------+------------+
| +I |       10001 | 1953-09-02 |                         Georgi |                        Facello |                              M | 1986-06-26 |
| +I |       10002 | 1964-06-02 |                        Bezalel |                         Simmel |                              F | 1985-11-21 |
| +I |       10003 | 1959-12-03 |                          Parto |                        Bamford |                              M | 1986-08-28 |
| +I |       10004 | 1954-05-01 |                      Chirstian |                        Koblick |                              M | 1986-12-01 |
| +I |       10005 | 1955-01-21 |                        Kyoichi |                       Maliniak |                              M | 1989-09-12 |
| +I |       10006 | 1953-04-20 |                         Anneke |                        Preusig |                              F | 1989-06-02 |
| +I |       10007 | 1957-05-23 |                        Tzvetan |                      Zielinski |                              F | 1989-02-10 |
| +I |       10008 | 1958-02-19 |                         Saniya |                       Kalloufi |                              M | 1994-09-15 |
| +I |       10009 | 1952-04-19 |                         Sumant |                           Peac |                              F | 1985-02-18 |
| +I |       10010 | 1963-06-01 |                      Duangkaew |                       Piveteau |                              F | 1989-08-24 |
+----+-------------+------------+--------------------------------+--------------------------------+--------------------------------+------------+
Received a total of 10 rows
```


<span id="_2-4-flink-sql集成starrocks-connector"></span>
### 2.4 Flink SQL integration with StarRocks connector

Similar to the Doris Connector, Huoshang EMR Flink supports writing data to StarRocks via the Flink StarRocks Connector, and the StarRocks Connector is built into the connector directory. The following example uses Yarn per\-job to demonstrate reading and writing StarRocks data with Flink.


1. Launch the SQL client command\-line interface


```shell
# 注意不同EMR版本，connector包的版本有差异，可根据实际connector的版本进行调整
/usr/lib/emr/current/flink/bin/sql-client.sh embedded \
-j connectors/flink-starrocks-connector-1.16-1.2.5-ve-1.jar

set execution.target=yarn-per-job;
```



2. Connect to StarRocks remotely and create the target table


Refer to [Basic usage](https://docs.byteplus.com/docs/undefined/69aa398ad5f8c20564ccdb1e) to create the corresponding user account.

```sql
-- mysql -hxxx.xxx.xx -P9030 -uxxxx -p

mysql> CREATE DATABASE demo_db;
mysql> USE demo_db;

mysql> CREATE TABLE all_employees_info (
    emp_no       int NOT NULL,
    birth_date   date,
    first_name   varchar(20),
    last_name    varchar(20),
    gender       char(2),
    hire_date    date
)
UNIQUE KEY(`emp_no`, `birth_date`)
DISTRIBUTED BY HASH(`birth_date`) BUCKETS 1
PROPERTIES (
"replication_allocation" = "tag.location.default: 1"
);
```



3. Create a StarRocks Sink table in Flink and insert data


```sql
-- create sink table
Flink SQL> CREATE TABLE sr_sink (
    emp_no       int ,
    birth_date   STRING,
    first_name   STRING,
    last_name    STRING,
    gender       STRING,
    hire_date    STRING
) 
WITH (
  'connector' = 'starrocks',
  'load-url' = '192.168.1.26:8030',
  'jdbc-url' = 'jdbc:mysql://192.168.1.26:9030',
  'database-name' = 'demo_db',
  'table-name' = 'all_employees_info',
  'username' = 'test_user',
  'password' = 'test_passwd'
);

Flink SQL> INSERT INTO `sr_sink` VALUES 
(10001,'1953-09-02','Georgi','Facello','M','1986-06-26'),
(10002,'1964-06-02','Bezalel','Simmel','F','1985-11-21'),
(10003,'1959-12-03','Parto','Bamford','M','1986-08-28'),
(10004,'1954-05-01','Chirstian','Koblick','M','1986-12-01'),
(10005,'1955-01-21','Kyoichi','Maliniak','M','1989-09-12'),
(10006,'1953-04-20','Anneke','Preusig','F','1989-06-02'),
(10007,'1957-05-23','Tzvetan','Zielinski','F','1989-02-10'),
(10008,'1958-02-19','Saniya','Kalloufi','M','1994-09-15'),
(10009,'1952-04-19','Sumant','Peac','F','1985-02-18'),
(10010,'1963-06-01','Duangkaew','Piveteau','F','1989-08-24');
```



4. Create a StarRocks Source table in Flink and query data


```sql
-- create source table
Flink SQL> CREATE TABLE sr_source (
    emp_no       int ,
    birth_date   STRING,
    first_name   STRING,
    last_name    STRING,
    gender       STRING,
    hire_date    STRING
) 
WITH (
  'connector' = 'starrocks',
  'scan-url' = '192.168.1.26:8030',
  'jdbc-url' = 'jdbc:mysql://192.168.1.26:9030',
  'database-name' = 'demo_db',
  'table-name' = 'all_employees_info',
  'username' = 'test_user',
  'password' = 'test_passwd'
);

Flink SQL> SELECT * FROM sr_source;
+----+-------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+
| op |      emp_no |                     birth_date |                     first_name |                      last_name |                         gender |                      hire_date |
+----+-------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+
| +I |       10001 |                     1953-09-02 |                         Georgi |                        Facello |                              M |                     1986-06-26 |
| +I |       10002 |                     1964-06-02 |                        Bezalel |                         Simmel |                              F |                     1985-11-21 |
| +I |       10003 |                     1959-12-03 |                          Parto |                        Bamford |                              M |                     1986-08-28 |
| +I |       10004 |                     1954-05-01 |                      Chirstian |                        Koblick |                              M |                     1986-12-01 |
| +I |       10005 |                     1955-01-21 |                        Kyoichi |                       Maliniak |                              M |                     1989-09-12 |
| +I |       10006 |                     1953-04-20 |                         Anneke |                        Preusig |                              F |                     1989-06-02 |
| +I |       10007 |                     1957-05-23 |                        Tzvetan |                      Zielinski |                              F |                     1989-02-10 |
| +I |       10008 |                     1958-02-19 |                         Saniya |                       Kalloufi |                              M |                     1994-09-15 |
| +I |       10009 |                     1952-04-19 |                         Sumant |                           Peac |                              F |                     1985-02-18 |
| +I |       10010 |                     1963-06-01 |                      Duangkaew |                       Piveteau |                              F |                     1989-08-24 |
+----+-------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+--------------------------------+
Received a total of 10 rows
```


<span id="_2-5-flink-sql-集成-bytehouse-云数仓版"></span>
### 2.5 Flink SQL integration with ByteHouse\-Cdw connector (Cloud Data Warehouse Edition)

Huoshang ByteHouse (Cloud Data Warehouse Edition) supports writing data to ByteHouse (Cloud Data Warehouse Edition) via the Flink ByteHouse\-Cdw Connector, and the ByteHouse\-Cdw Connector is built into the connectors directory. The following uses Yarn per\-job as an example to demonstrate writing to ByteHouse (cloud data warehouse edition) via datagen.


1. Refer to [ByteHouse cloud data warehouse edition / Quick Start](https://www.volcengine.com/docs/6517/76324) to create a bytehouse cluster and tables. The statements for creating the database and tables are as follows:

   ```shell
   create databese flink_bytehouse_test;
   ```
   

   ```shell
   CREATE TABLE `flink_bytehouse_test`.`cnch_table_test`
   (
        test_key   STRING,
        test_value UInt64,
        ts         UInt64
   )
   ENGINE = CnchMergeTree
   ORDER BY (test_key);
   ```
   

2. Launch the SQL client command\-line interface.

   ```shell
   # 注意不同EMR版本，connector包的版本有差异，可根据实际connector的版本进行调整
   /usr/lib/emr/current/flink/bin/sql-client.sh embedded \
   -j connectors/flink-sql-connector-bytehouse-cdw_2.12-1.25.4-1.16.jar 
   
   set execution.target=yarn-per-job;
   ```
   

3. Flink creates a ByteHouse (cloud data warehouse edition) sink table and inserts data into the ByteHouse (cloud data warehouse table) via datagen.


```shell
CREATE  TABLE random_source (
            test_key   STRING,
            test_value BIGINT,
            ts         BIGINT
        )
        WITH (
            'connector' = 'datagen',
            'rows-per-second' = '1'
        );

CREATE  TABLE cnch_table (test_key STRING, test_value BIGINT, ts BIGINT)
        WITH (
            'connector' = 'bytehouse-cdw',
            'database' = 'flink_bytehouse_test',
            'table-name' = 'cnch_table_test',
            'bytehouse.gateway.region' = 'VOLCANO',
            'bytehouse.gateway.access-key-id' = '<此处填写用户实际的 AK>',
            'bytehouse.gateway.secret-key' = '<此处填写用户实际的 SK>'
        );

INSERT INTO cnch_table
SELECT  *
FROM    random_source;
```



4. Go to the bytehouse [SQL worksheet](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/query) tab, click to select the corresponding role and the running compute group, and execute a query to check the number of inserted rows.


```shell
select count(*) from `flink_bytehouse_test`.`cnch_table_test`;
```


<span id="_2-6-flink-sql-集成-bytehouse-企业版"></span>
### 2.6 Flink SQL integration with ByteHouse (enterprise edition)

Similar to ByteHouse (cloud data warehouse edition), ByteHouse (enterprise edition) supports writing data to ByteHouse (enterprise edition) via the Flink ByteHouse\-CE connector. The ByteHouse\-CE Connector is built into the connectors directory (built\-in since EMR 1.8.0). The following uses Yarn per\-job as an example to demonstrate writing to ByteHouse (enterprise edition) via datagen.


1. Refer to ByteHouse (enterprise edition) [database and table creation](https://www.volcengine.com/docs/6464/152222) to create a bytehouse cluster and tables.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4fdee993c93392b7ee1b6d384cc7e842.png) </span>


2. Launch the SQL client command\-line interface.


```sql
/usr/lib/emr/current/flink/bin/sql-client.sh embedded \
-j connectors/flink-sql-connector-bytehouse-ce_2.12-1.25.4-1.16.jar  

set execution.target=yarn-per-job;
```



3. Insert data into ByteHouse (enterprise edition) via the gateway method.


```sql
CREATE  TABLE random_source (
            test_key   STRING,
            test_value BIGINT,
            ts         BIGINT
        )
        WITH (
            'connector' = 'datagen',
            'rows-per-second' = '1'
        );



CREATE  TABLE cnch_table (test_key STRING, test_value BIGINT, ts BIGINT)
        WITH (
            'connector' = 'bytehouse-ce',
            'clickhouse.shard-discovery.kind' = 'CE_GATEWAY',
            'bytehouse.ce.gateway.host' = '7322262036938936630.bytehouse-ce.ivolces.com',
            'bytehouse.ce.gateway.port' = '8123',            
            'sink.enable-upsert' = 'false',
            'clickhouse.cluster' = 'bytehouse_cluster_enct', -- bytehouse cluster name
            'database' = 'default', -- target database
            'table-name' = 'cnch_table_test', -- target table Important: it is a local table: {table_name}_local
            'username' = 'xxxx@bytedance.com', -- bytehouse user
            'password' = 'xxx' -- bytehouse password
        );

INSERT INTO cnch_table SELECT  * FROM  random_source;
```



4. Go to the ByteHouse (enterprise edition) [data query](https://console.volcengine.com/bytehouse-ce/region:bytehouse-ce+cn-beijing/data_query/query) page, select the corresponding cluster, and execute a query to check the number of inserted rows.


```sql
select count(*)  FROM `default`.`cnch_table_test`;
```

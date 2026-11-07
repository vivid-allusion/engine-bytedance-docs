---
title: "Spark Connector"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/spark-connector"
---

Spark Connector for ByteHouse is specifically designed for loading data into ByteHouse Enterprise Edition through Spark. This article introduces how to connect to ByteHouse using the Spark Connector, with detailed examples using both Spark SQL and EMR\-supported Serverless Spark.

<span id="35fe3e47"></span>
# Prerequisites

<span id="de3363ab"></span>
## Download drivers


* Spark Connector

   
   |Spark Version |Driver |Release Date |
   |---|---|---|
   |Version 3.5 and above |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd21b5f06a0d477596a58aa14e8ab851~tplv-goo7wpa0wc-image.image" name="clickhouse-spark-runtime-3.5_2.12-0.8.1.1.jar">clickhouse-spark-runtime-3.5_2.12-0.8.1.1.jar</Attachment><br> |2024\-09\-11 |
   

* ByteHouse JDBC

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ff3e95c029f48b5bc6e94faa86a1355~tplv-goo7wpa0wc-image.image" name="clickhouse-jdbc-0.4.6.jar">clickhouse-jdbc-0.4.6.jar</Attachment>
   


<span id="ac5583b8"></span>
## Add Maven dependencies

For Maven projects that compile with the Spark connector, add the following dependencies to your project's pom.xml file.

```XML
<dependency>
    <groupId>com.clickhouse</groupId>
    <artifactId>clickhouse-jdbc</artifactId>
    <version>0.4.6</version>
</dependency>
<dependency>
    <groupId>com.bytedance.bytehouse-ce</groupId>
    <artifactId>clickhouse-spark-runtime-3.5_2.12</artifactId>
    <version>0.8.1.1</version>
</dependency>
```


Then, add the following repository to the `pom.xml` file:

```XML
<repository>
    <id>bytedance</id>
    <name>ByteDance Public Repository</name>
    <url>https://artifact.bytedance.com/repository/releases</url>
</repository>
```


<span id="fee6e4a3"></span>
# Instructions

<span id="7e359396"></span>
## Spark SQL

You can refer to the commands below to connect to ByteHouse using the Spark SQL CLI.

```Bash
export SPARK_LOCAL_IP=localhost
export SPARK_HOME=/opt/tiger/spark
export CLICKHOUSE_HOST=<your-host>
export CLICKHOUSE_HTTP_PORT=8123
export CLICKHOUSE_USER=<your-username>
export CLICKHOUSE_PASSWORD='<your-password>'

$SPARK_HOME/bin/spark-sql \
  --conf spark.sql.catalog.clickhouse=xenon.clickhouse.ClickHouseCatalog \
  --conf spark.sql.catalog.clickhouse.host=${CLICKHOUSE_HOST:-127.0.0.1} \
  --conf spark.sql.catalog.clickhouse.protocol=http \
  --conf spark.sql.catalog.clickhouse.http_port=${CLICKHOUSE_HTTP_PORT:-8123} \
  --conf spark.sql.catalog.clickhouse.user=${CLICKHOUSE_USER:-default} \
  --conf spark.sql.catalog.clickhouse.password=${CLICKHOUSE_PASSWORD:-} \
  --conf spark.sql.catalog.clickhouse.database=default \
  --conf spark.sql.catalog.clickhouse.shard_discovery.kind=CE_API_CLUSTERS \
  --conf spark.sql.catalog.clickhouse.bytehouse_ce.api.account_id=xx \
  --conf spark.sql.catalog.clickhouse.cluster=xx \
  --conf spark.driver.bindAddress=127.0.0.1 \
  --conf spark.clickhouse.write.distributed.convertLocal=true \
  --conf spark.clickhouse.write.useShardsWriter=true \
  --conf spark.clickhouse.write.format=json \
  --conf spark.clickhouse.read.filterByPartition=false \
  --jars clickhouse-jdbc-0.4.6-all.jar,clickhouse-spark-runtime-3.5_2.12-0.8.1.1.jar
```


The key connection parameters are:


|Parameter ||Configuration Description |
|---|---|---|
|`export` |`CLICKHOUSE_HOST`、`CLICKHOUSE_USER`、 `CLICKHOUSE_PASSWORD` |Configuration for ByteHouse includes the domain name, username, and password for connection, for which details can be found in [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information). |
||`CLICKHOUSE_DATABASE` |Configured as the database name for ByteHouse. |
|`--jars` ||Specifies the actual file paths of the jars used in the configuration. |
|Other `spark` related parameters ||Please refer to the section [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector#e31a8be5) below. |


<span id="6370a95e"></span>
## Servless Spark

You can refer to the commands below to connect to ByteHouse using the Servless Spark method. The Servless Spark method is applicable to the BytePlus EMR (E\-MapReduce) service.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When connecting to ByteHouse in this manner, you need to manually download the driver and upload it to the TOS bucket in the same region with ByteHouse, for use by the connector below.</div>


```SQL
set serverless.spark.analysis=true;
set spark.hadoop.fs.tos.skip.resolve = true;
set las.cross.vpc.access.enabled = true;
set las.cross.vpc.vpc.id = <your-vpc-id>;
-- Use the sub-net in avalability zone B
set las.cross.vpc.subnet.id = <your-subnet-id>;
set las.cross.vpc.security.group.id = <your-securitygroup-id>;
set las.cross.vpc.accountId=<your-account-id>;
set las.cluster.type = vke;
set emr.serverless.spark.only.parse.enabled  = true;
set serverless.spark.access.key=<your-tos-ak>;
set serverless.spark.secret.key=<your-tos-sk>;
set spark.sql.catalog.clickhouse=xenon.clickhouse.ClickHouseCatalog;
set spark.sql.catalog.clickhouse.host=xx.bytehouse-ce.ibytepluses.com;
set spark.sql.catalog.clickhouse.protocol=http;
set spark.sql.catalog.clickhouse.http_port=8123;
set spark.sql.catalog.clickhouse.user=<your-username>;
set spark.sql.catalog.clickhouse.password=<your-password>;
set spark.sql.catalog.clickhouse.database=<your-database>;
set spark.sql.catalog.clickhouse.shard_discovery.kind=CE_API_CLUSTERS;
set spark.sql.catalog.clickhouse.bytehouse_ce.api.account_id=<your-account-id>;
set spark.sql.catalog.clickhouse.cluster=<your-cluster-name>;
set spark.sql.catalog.clickhouse.option.socket_timeout=6000000;
set spark.sql.catalog.clickhouse.option.connect_timeout=30000;
set spark.sql.catalog.clickhouse.option.custom_settings=max_execution_time=86400;
set spark.clickhouse.write.format=json;
set spark.clickhouse.read.filterByPartition=false;
set spark.clickhouse.write.distributed.convertLocal=true;
set spark.clickhouse.write.useShardsWriter=true;

set las.spark.jar.depend.jars = [{"schema":"","fileName":"tos://test-bh-tos/clickhouse-jdbc-0.4.6-all.jar"},{"schema":"","fileName":"tos://test-bh-tos/clickhouse-spark-runtime-3.5_2.12-0.8.1.1.jar"}];

-- Import data from the people_t table in hive to the people_t_copy table in ByteHouse 
use clickhouse;
insert into people_t_copy select * from spark_catalog.default.people_t; 
```


The key connection parameters are:


|Parameter |Configuration Description |
|---|---|
|`las.cross.vpc.**` related parameters |You can find this information on the ByteHouse Console **Manage Clusters\-Cluster Details\-Basic Information** page. |
|`serverless.spark.access.key`、`serverless.spark.secret.key` |You can refer to [Obtain Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|`clickhouse.host`<br><br>`clickhouse.user`<br><br>`clickhouse.password` |Public or private `HOST` address, as well as account and password information, you can refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information). |
|`clickhouse.database`<br><br>`clickhouse.cluster` |Set database name and cluster name |
|`las.spark.jar.depend.jars` |Fill in the TOS path of the actual driver jar file used |
|Other `Spark` related parameters |Please refer to the section [Configuration parameters](https://docs.byteplus.com/docs/bytehouse/spark-connector#e31a8be5) below. |


<span id="e31a8be5"></span>
## Configuration parameters


|Param |Whether is a required choice |Default |Data type |description |
|---|---|---|---|---|
|spark.sql.catalog.$ |✅ |None |string |Must be configured as a constant value: xenon.clickhouse.ClickHouseCatalog |
|spark.sql.catalog.${catalog}.host |✅ |None |string |ByteHouse Cluster connection address format: `xx.bytehouse-ce.ibytepluses.com`. You can refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information) to obtain the connection address. |
|spark.sql.catalog.${catalog}.http_port |No |8123 |int |ByteHouse HTTP connection port |
|spark.sql.catalog.${catalog}.protocol |No |http |string |ByteHouse HTTP Connection Protocol |
|spark.sql.catalog.${catalog}.user |✅ |None |string |Username for ByteHouse Connection |
|spark.sql.catalog.${catalog}.password |✅ |None |string |ByteHouse connection password |
|spark.sql.catalog.${catalog}.database |No |default |string |ByteHouse database name |
|spark.sql.catalog.${catalog}.timezone |No |server |string |Timezone information, optional values:<br><br><br>* server<br><br>* client<br><br>* UTC+3<br><br>* Standard time zones such as Asia/Shanghai |
|spark.sql.catalog.${catalog}.shard_discovery.kind |✅ |None |string |Must be configured to a constant value: CE_API_CLUSTERS |
|spark.sql.catalog.${catalog}.shard_discovery.host |No |None |string |Defaults to spark.sql.catalog.${catalog}.host |
|spark.sql.catalog.${catalog}.shard_discovery.port |No |80 |int |Shard discovery host port |
|spark.sql.catalog.${catalog}.bytehouse_ce.api.account_id |✅ |None | |BytePlus main account ID |
|spark.sql.catalog.${catalog}.cluster |✅ |None |string |Cluster name |
|spark.sql.catalog.${catalog}.option |✅ |None |map |JDBC parameters |
|spark.sql.catalog.${catalog}.option.socket_timeout |No |None |int |Client timeout |
|spark.sql.catalog.${catalog}.option.connect_timeout |No |None |int |Client connection timeout |
|spark.sql.catalog.${catalog}.option.custom_http_params |No |None |string |Custom JDBC parameters |
|spark.bytehouse.write.batchSize |No |10000 |int |JDBC write batch size |
|spark.clickhouse.write.repartitionByPartition |No |true |bool |Repartition data using the ClickHouse partition key before writing to meet the ClickHouse distribution |
|spark.clickhouse.write.distributed.useClusterNodes |No |true |bool |Write to all nodes of the cluster when writing distributed tables |
|spark.clickhouse.write.distributed.convertLocal |No |false |bool |When writing to a distributed table, convert it to a local table |
|spark.clickhouse.read.distributed.convertLocal |No |true |bool |When reading from a distributed table, convert it to reading from a local table |
|spark.clickhouse.read.filterByPartition |No |true |bool |Filter by _partition_id or partition value when reading the table |
|spark.clickhouse.write.localSortByPartition |No |true |bool |If true, sort locally by partition before writing |
|spark.clickhouse.write.localSortByKey |No |true |bool |If set to true, sort locally by keys before writing |
|spark.clickhouse.write.format |No |json |string |Currently only supports Json format |
|spark.clickhouse.write.useShardsWriter |No |false |string |If true, cache the rows in the shard before writing to it |
|spark.clickhouse.write.shardingStrategy |No |AUTO |string |Sharding strategy, supports HASH and AUTO |
|spark.clickhouse.write.shardingExpression |No |None |string |Partition expression, supports cityHash64(xx), intHash64(xx) and sipHash64(xx) |
|spark.clickhouse.read.format |No |json |string |Currently only supports JSON format |


<span id="8e60af57"></span>
## Data type mapping


|Spark data type |ByteHouse Data Type |Reading |Writing |
|---|---|---|---|
|**Integer types** |UInt8 |✅ |✅ |
||UInt16 |✅ |✅ |
||UInt32 |✅ |✅ |
||UInt64 |✅ |✅ |
||Int8 |✅ |✅ |
||Int16 |✅ |✅ |
||Int32 |✅ |✅ |
||Int64 |✅ |✅ |
|**Floating\-point numbers** |Float32 |✅ |✅ |
||Float64 |✅ |✅ |
||Decimal |✅ |✅ |
|**Boolean** |bool |✅ |✅ |
|**Strings** |String |✅ |✅ |
||FixedString |✅ |✅ |
|**Dates** |Date |✅ |✅ |
||DateTime |✅ |✅ |
|**UUID** |UUID |✅ |✅ |
|**Enum** |Enum8 |✅ |✅ |
||Enum16 |✅ |✅ |
|**Arrays** |Array(T) |✅ |✅ |
|**Maps** |Map(K, V) |✅ |✅ |


<span id="592548ee"></span>
## Supported Spark catalog functions


|Spark Catalog Functions |Support Project |Spark SQL Syntax |ByteHouse Enterprise Edition SQL Syntax |
|---|---|---|---|
|listTables |✅ |`show tables` |`SHOW TABLES` |
|loadTable |✅ |`show create table xx` |`SHOW CREATE TABLE xx` |
|createTable |❌ | |```SQL```<br>```CREATE TABLE [IF NOT EXISTS] [tableIdentifier] [UUID uuid]```<br>```(```<br>```    [tableColumnDfnt],```<br>```    [CONSTRAINT constraint_name CHECK columnExpr,]```<br>```    ...```<br>```) [engineClause]```<br> |
|dropTable |✅ |`drop table xx.xxx` |`DROP TABLE xx.xxx` |
|renameTable |✅ |`rename table xx to xxx` |`RENAME TABLE xx.xxx to xx.xxx` |
|listNamespaces |✅ |`show databases` |`SHOW DATABASES` |
|createNamespace |✅ |`create database xx` |`CREATE DATABASE xx` |
|dropNamespace |✅ |`drop database xx` |`DROP DATABASE xx` |

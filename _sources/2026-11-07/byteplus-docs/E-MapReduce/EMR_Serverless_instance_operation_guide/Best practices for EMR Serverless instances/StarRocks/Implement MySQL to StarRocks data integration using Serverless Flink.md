---
title: "Implement MySQL to StarRocks data integration using Serverless Flink"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Implement_MySQL_to_StarRocks_data_integration_using_Serverless_Flink"
---

<span id="_1-支持的版本"></span>
## 1 **Supported versions**

Supports collecting data from EMR\-3.1.1 and above StarRocks clusters, as well as OLAP services with fully managed StarRocks engines version 1.1.0 and above.

<span id="_2-使用前提"></span>
## 2 **Prerequisites**

<span id="_2-1-准备mysql的数据库信息"></span>
### 2.1 Prepare MySQL database information


* Prepare a cloud database MySQL instance within the same VPC network. You can go to the console to [create a MySQL instance](https://console.volcengine.com/db/region:db+cn-beijing/common/create?dbtype=rdsMysql).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed2e220ba9eab36b4e39e85f4d6777a1.png) </span>

<span id="_2-2-获取starrocks的数据库信息"></span>
### 2.2 Obtain StarRocks database information


1. When configuring the StarRocks data source, ensure that the EMR cluster information and database username and password are entered correctly:

2. The database username provided must have read and write permissions for the relevant database tables to ensure that task data can be properly read from or written to StarRocks.

   1. An account password is required. The root account does not have a password, which does not comply with security standards and cannot be used for data source configuration.

   2. You can access the [EMR Serverless OLAP](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/list) user management page

   * Log in to the [EMR Serverless OLAP](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/list) console.

   * In the top left menu bar, select the region as appropriate.

   * Click the target instance name.

   * Click the **User Management** tab.

   * When adding a user in the pop\-up dialog box, configure the following information and click **Confirm**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a3a8b89be2da007f60d495c2d1fb4e57.png) </span>


3. The VPC of the EMR StarRocks cluster and the dedicated integration resource group must be consistent.

   1. It is recommended that the MySQL data source and Serverless Flink resource pool be in the same private network.

   2. The subnets and security groups under the VPC should also be kept consistent as much as possible.

   3. If the VPCs are not consistent, you need to select the allowlist group in the security management of the StarRocks cluster and add inbound rules.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c1a3309f51d291b8d03ba3f4767959c.png) </span>

<span id="_2-3-创建serveless-flink集群"></span>
### 2.3 Create a Serverless Flink cluster


* The Flink resource pool is used to manage computing resources in the project. The computing resources in the resource pool are isolated and independent from each other. Task execution and debugging consume computing resources. Before developing tasks, you need to create a Flink resource pool. For details, see: [Create a Flink resource pool](https://www.volcengine.com/docs/6581/149867).

* To create a Flink task, refer to: [Develop a Flink SQL task](https://www.volcengine.com/docs/6581/149864).


<span id="_3-mysql-导入到starrocks链路"></span>
## 3 MySQL import to StarRocks pipeline

<span id="_3-1-准备mysql数据源"></span>
### 3.1 Prepare the MySQL data source

```sql
CREATE DATABASE test;

CREATE TABLE test.score_board(
    id int(11) NOT NULL COMMENT "",
    name varchar(255) NULL DEFAULT "" COMMENT "",
    score int(11) NOT NULL DEFAULT "0" COMMENT "",
PRIMARY KEY(id)
);


#准备若干条数据
INSERT INTO `score_board` VALUES (201, 'mysqlinsert',123), (202, 'mysql-uui',345);
```


<span id="_3-2-准备starrocks-表"></span>
### 3.2 Prepare the StarRocks table

```sql
mysql -uxxx -pxxx -h xxx -P 9030
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa9c8a3f29b7a257a5ce56ac8f6e2e7e.png) </span>

```sql
CREATE DATABASE test;

CREATE TABLE test.score_board(
    id int(11) NOT NULL COMMENT "",
    name varchar(65533) NULL DEFAULT "" COMMENT "",
    score int(11) NOT NULL DEFAULT "0" COMMENT ""
)
ENGINE=OLAP
PRIMARY KEY(id)
DISTRIBUTED BY HASH(id);
```


The StarRocks connector is currently only supported in the **Flink 1.16\-volcano** engine version.

<span id="_3-3-编写-flink任务运行导入"></span>
### 3.3 Write and run the Flink import task

The definition of the StarRocks data source connector is as follows

```sql
CREATE TABLE starrocks_table(
 name VARCHAR,
 score BIGINT
 ) WITH ('connector' = 'starrocks','jdbc-url'='jdbc:mysql://fe1_ip:query_port,fe2_ip:query_port,fe3_ip:query_port','load-url'='fe1_ip:http_port;fe2_ip:http_port;fe3_ip:http_port','database-name' = 'xxx','table-name' = 'xxx','username' = 'xxx','password' = 'xxx'
 );
SQL
```


Write data to the data source

```sql
CREATE TABLE
  mysql_jdbc (`id` INT, `name` STRING, `score` INT)
WITH
  (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://xxx.rds.ivolces.com:3306/xxx',
    'table-name' = 'xxx',
    'username' = 'xxx',
    'password' = 'xxx'
  );

CREATE TABLE
  `score_board_sr` (
    `id` INT,
    `name` STRING,
    `score` INT,
    PRIMARY KEY (id) NOT ENFORCED
  )
WITH
  (
    'connector' = 'starrocks',
    'jdbc-url' = 'jdbc:mysql://xxx:9030',
    'load-url' = 'xxx:8030',
    'database-name' = 'xxx',
    'table-name' = 'xxx',
    'username' = 'xxx',
    'password' = 'xxx'
  );

insert into
  score_board_sr
select
  *
from
  mysql_jdbc;
```


Start task execution

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3cdb352fc0f1fbe56fb67955670b17fd.png) </span>

Verify that data has been successfully written to StarRocks through Flink

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_504fdcca96afa9af7ba7e146fc67fc9c.png) </span>

<span id="_4-详细参数介绍"></span>
## 4 Detailed parameter description

**General parameters**


|Parameter |Required |Default value |Data type |Description |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to use. In this case, it is the starrocks connector. |
|jdbc\-url |Yes |(none) |String |IP address and query port information of FE nodes. If there are multiple entries, separate them with commas (,).<br><br>The format is jdbc:mysql://fe_ip1:query_port,fe_ip2:query_port.. |
|database\-name |Yes |(none) |String |StarRocks database name. |
|table\-name |Yes |(none) |String |StarRocks table name. |
|username |Yes |(none) |String |StarRocks user name. |
|password |Yes |(none) |String |StarRocks user password. |


**Source table parameters**


|Parameter |Required |Default value |Data type |Description |
|---|---|---|---|---|
|scan\-url |Yes |(none) |String |IP address and HTTP port information of FE nodes. If there are multiple entries, separate them with commas (,).<br><br>The format is fe_ip1:http_port,fe_ip2:http_port.. |
|scan.connect.timeout\-ms |No |1000 |String |The timeout duration for connecting to the StarRocks data warehouse, Unit: milliseconds. |
|scan.params.keep\-alive\-min |No |10 |String |The keep\-alive duration for a read task, Unit: minutes. |
|scan.params.query\-timeout\-s |No |600 |String |The maximum timeout duration for a read task, Unit: seconds. |
|scan.params.mem\-limit\-byte |No |1073741824 |String |The memory limit for a single query on a BE node, Unit: bytes. The default value is 1073741824, which is equivalent to 1GB. |
|scan.max\-retries |No |1 |String |The maximum number of retries after a read task fails |


**Result table parameters**


|Parameter |Required |Default value |Data type |Description |
|---|---|---|---|---|
|load\-url |Yes |(none) |String |The IP and HTTP port information of FE nodes. If there are multiple, separate them with commas (,).<br><br>The format is fe_ip1:http_port,fe_ip2:http_port.. |
|sink.semantic |No |at\-least\-once |String |Data write semantics. at\-least\-once: Default value. At least one write. exactly\-once: Write only once. No duplicate writes will occur. Note: When configured with exactly\-once write semantics, data is written only at checkpoint. Important: The sink.buffer\-flush.\* related parameters are invalid in this case. |
|sink.version |No |AUTO |String |The interface used for data loading. V1: Uses the Stream Load interface to load data. V2: Uses the Transaction Stream Load interface to load data. Requires StarRocks version 2.4 or later. AUTO: Determines whether StarRocks supports the Transaction Stream Load interface, then selects the version. If supported, V2 is selected; if not, V1 is selected. |
|sink.buffer\-flush.max\-bytes |No |94371840 |String |The maximum amount of data that the buffer can hold before writing to StarRocks. Range: [64MB, 10GB].<br><br>The default value is 94371840, which is equivalent to 90MB. |
|sink.buffer\-flush.max\-rows |No |500000 |String |The maximum number of data rows that the buffer can hold before writing to StarRocks. |
|sink.buffer\-flush.interval\-ms |No |300000 |String |Buffer flush interval, Unit: milliseconds. The value range is [64000, 5000000]. |
|sink.max\-retries |No |3 |String |The maximum number of retries for write tasks. The value range is [0, 10]. |
|sink.connect.timeout\-ms |No |1000 |String |The timeout duration for connecting to the StarRocks data warehouse, Unit: milliseconds. The value range is 100~60000. |
|sink.parallelism |No |NULL |String |Specify the parallelism.<br><br>If parallelism is not specified, the global parallelism is used. |
|sink.properties.\* |No |(none) |String |Result table properties.<br><br>Three parameters are listed here. To learn more, see [STREAM LOAD](https://docs.starrocks.io/zh-cn/latest/sql-reference/sql-statements/data-manipulation/STREAM%20LOAD#stream-load). sink.properties.format: The data format written to StarRocks. Supports CSV and JSON. The default value is csv. sink.properties.column_separator: Used to specify the column separator for CSV format. The default value is . sink.properties.row_delimiter: Used to specify the row delimiter for CSV format. The default value is<br><br>. |


**Data type mapping**


* Source table



|StarRocks field type |Flink field type |
|---|---|
|NULL |NULL |
|BOOLEAN |BOOLEAN |
|TINYINT |TINYINT |
|SMALLINT |SMALLINT |
|INT |INT |
|BIGINT |BIGINT |
|LARGEINT |STRING |
|FLOAT |FLOAT |
|DOUBLE |DOUBLE |
|DATE |DATE |
|DATETIME |TIMESTAMP |
|DECIMAL |DECIMAL |
|DECIMALV2 |DECIMAL |
|DECIMAL32 |DECIMAL |
|DECIMAL64 |DECIMAL |
|DECIMAL128 |DECIMAL |
|CHAR |CHAR |
|VARCHAR |STRING |



* Result table



|Flink field type |StarRocks field type |
|---|---|
|BOOLEAN |BOOLEAN |
|TINYINT |TINYINT |
|SMALLINT |SMALLINT |
|INTEGER |INTEGER |
|BIGINT |BIGINT |
|FLOAT |FLOAT |
|DOUBLE |DOUBLE |
|DECIMAL |DECIMAL |
|BINARY |INT |
|CHAR |STRING |
|VARCHAR |STRING |
|STRING |STRING |
|DATE |DATE |
|TIMESTAMP_WITHOUT_TIME_ZONE(N) |DATETIME |
|TIMESTAMP_WITH_LOCAL_TIME_ZONE(N) |DATETIME |
|ARRAY |ARRAY |
|MAP<KT,VT\> |JSON STRING |
|ROW |JSON STRING |


**Other reference examples**


* Result table example


```sql
CREATE TABLE datagen_source(
  id INTEGER,
  name STRING,
  score INTEGER
) WITH ('connector' = 'datagen','rows-per-second' = '1','fields.name.length' = '9','fields.id.min' = '1','fields.id.max' = '1000','fields.score.min' = '1','fields.score.max' = '1000'
);

CREATE TABLE starrocks_sink(
  id INTEGER,
  name STRING,
  score INTEGER,PRIMARY KEY (id) NOT ENFORCED
) WITH ('connector' = 'starrocks','jdbc-url' = 'jdbc:mysql://172.*.*.*:9030', 'load-url' = '172.*.*.*:8030', 'database-name' = 'xxx','table-name' = 'xxx','username' = 'xxx','password' = 'xxx','sink.parallelism' = '1'
);

INSERT INTO starrocks_sink
SELECT * FROM datagen_source;
```

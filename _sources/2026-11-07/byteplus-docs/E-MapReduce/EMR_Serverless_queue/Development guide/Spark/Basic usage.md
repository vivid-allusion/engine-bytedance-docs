---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/sq_spark_basic_usage"
---

<span id="_1-基础库表操作"></span>
## 1 **Basic database and table operations**

EMR SparkSQL is fully compatible with open\-source SparkSQL syntax. The following provides a note about basic database and table operations. For more detailed guides, refer to [the open-source SparkSQL syntax documentation](https://spark.apache.org/docs/3.2.1/sql-programming-guide.html).

<span id="_1-1-数据库操作"></span>
### 1.1 **Database operations**


1. Create a database


```sql
create database db_demo;
```



2. Create a database and specify a custom TOS bucket path for storage.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that the TOS bucket exists and that the current user has read and write permissions for the bucket path.</div>


```sql
create database db_demo location 'tos://您的tos bucket name/warehouse/';
```



3. View database information


```sql
desc database db_demo;
```



4. Delete a database


```sql
drop database db_demo;
```


<span id="_1-2-表操作"></span>
### 1.2 Table operations


1. Create a table


```sql
create table tb_demo(id int, name string);
```



2. Describe table information


```sql
desc table tb_demo;
```



3. Delete a table


```sql
drop table tb_demo;
```



4. Insert data


```sql
insert into tb_demo select 1,'name1';
```



5. Query table data


```sql
select * from tb_demo;
```


<span id="_1-3-udf操作"></span>
### 1.3 UDF operations


1. Upload a JAR file

2. Create a UDF


```sql
CREATE FUNCTION <schemaName>.<functionName> AS '<funcClassName>' using jar 'tos://您的tos bucket name/您的jar包地址';
```



3. Use a UDF


```sql
select <schemaName>.<functionName> ('aaabbB')
```


<span id="_2-spark-访问-hudi"></span>
## 2 Spark access to Hudi

<span id="_2-1-配置"></span>
### 2.1 Configuration

```sql
set spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog;
set spark.serializer=org.apache.spark.serializer.KryoSerializer;
```


<span id="_2-2-基础操作"></span>
### 2.2 Basic operations

```sql
CREATE DATABASE IF NOT EXISTS hudi_db location 'tos://您的tos bucket name/warehouse/hudi_db/';

use hudi_db;

create table if not exists test_hudi_tb (
    id bigint,
    name string
) using hudi;

insert into test_hudi_tb select 1, 'a1';

select * from test_hudi_tb;

drop table test_hudi_tb;
```


<span id="_3-spark-访问-iceberg"></span>
## 3 Spark access to Iceberg

<span id="_3-1-配置"></span>
### 3.1 Configuration

```sql
set spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog;
set spark.sql.catalog.iceberg.type=hive;
set spark.sql.storeAssignmentPolicy=ansi;
```


<span id="_3-2-基础操作"></span>
### 3.2 Basic operations

```sql
use iceberg;

CREATE DATABASE IF NOT EXISTS iceberg_db location 'tos://您的tos bucket name/warehouse/iceberg_db/';

use iceberg_db;

create table if not exists test_iceberg_tb (
    id bigint,
    name string
) using iceberg;

insert into test_iceberg_tb select 1, 'a1';

select * from test_iceberg_tb;

drop table test_iceberg_tb;
```


<span id="_4-spark-访问-deltalake"></span>
## 4 Spark access to DeltaLake

<span id="_4-1-配置"></span>
### 4.1 Configuration

```sql
set spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog;
```


<span id="_4-2-基础操作"></span>
### 4.2 Basic operations

```sql
CREATE DATABASE IF NOT EXISTS delta_db location 'tos://您的tos bucket name/warehouse/delta_db/';

use delta_db;

create table if not exists test_delta_tb (
    id bigint,
    name string
) using delta;

insert into test_delta_tb select 1, 'a1';

select * from test_delta_tb;

drop table test_delta_tb;
```


<span id="_5-spark-访问-paimon"></span>
## 5 Spark access to Paimon

<span id="_5-1-配置"></span>
### 5.1 Configuration

```sql
set spark.sql.catalog.paimon=org.apache.paimon.spark.SparkCatalog;
set spark.sql.catalog.paimon.metastore=hive;
-- Custom warehouse path
set spark.sql.catalog.paimon.warehouse=tos://您的tos bucket name/warehouse;
set spark.sql.storeAssignmentPolicy=ansi;
```


<span id="_5-2-基础操作"></span>
### 5.2 Basic operations

```sql
use paimon;

CREATE DATABASE IF NOT EXISTS paimon_db location 'tos://您的tos bucket name/warehouse/paimon_db/';

use paimon_db;

create table if not exists test_paimon_tb (
    id bigint,
    name string
) using paimon;

insert into test_paimon_tb select 1, 'a1';

select * from test_paimon_tb;

drop table test_paimon_tb;
```

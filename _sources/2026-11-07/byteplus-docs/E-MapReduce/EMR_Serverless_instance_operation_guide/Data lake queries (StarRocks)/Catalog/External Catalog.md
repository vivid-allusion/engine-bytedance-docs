---
title: "External Catalog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/External_Catalog"
---

<span id="_1-hive-catalog"></span>
## 1 Hive Catalog

<span id="_1-1-hdfs存储"></span>
### 1.1 HDFS storage


* Copy the contents of core\-site.xml and hdfs\-site.xml from the Hadoop cluster to the configuration management of the StarRocks cluster. The changes take effect after restarting the components.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f6a99ef30bc8536382da9e645158e8e.png) </span>


1. Create Hive catalog


```sql
CREATE EXTERNAL CATALOG hive_catalog 
PROPERTIES 
(
"hive.metastore.uris"="thrift://{hms_ip:hms_port}", 
"type" = "hive");
```



2. Query Hive table records


```sql
select * from  hive_catalog.db_1.table1 limit 1;
```


<span id="_1-2-tos存储"></span>
### 1.2 TOS storage


1. Create Hive catalog


```sql
CREATE EXTERNAL CATALOG hive_tos_catalog PROPERTIES (
    "type"="hive",
    "hive.metastore.uris" = "thrift://{hms_ip:hms_port}",
    "aws.s3.access_key"="xxx",
    "aws.s3.secret_key"="xxx==",
    "aws.s3.endpoint"="{endpoint,必须是s3格式的endpoint,例如: tos-s3-cn-beijing.ivolces.com}",
    "aws.s3.enable_ssl" = "false"
);
```



2. Query Hive TOS table records


```sql
select * from hive_tos_catalog.hive.hive_tos;
```


<span id="_2-hudi-catalog"></span>
## 2 Hudi Catalog

<span id="_2-1-hdfs存储"></span>
### 2.1 HDFS storage


* Copy the contents of core\-site.xml and hdfs\-site.xml from the Hadoop cluster to the configuration management of the StarRocks cluster. The changes take effect after restarting the components.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e82640779444fb42fe377ed957fbebdd.png) </span>


1. Create Hudi catalog


```sql
CREATE EXTERNAL CATALOG hudi_catalog PROPERTIES (
    "type"="hudi",
    "hive.metastore.uris"="thrift://{hms_ip:hms_port}", 
);
```



2. Query Hudi table records


```sql
select * from  hudi_catalog.db_1.table1 limit 1;
```


<span id="_2-2-tos存储"></span>
### 2.2 TOS storage


1. Create Hudi catalog


```sql
CREATE EXTERNAL CATALOG hudi_tos_catalog PROPERTIES (
    'type'='hudi',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}',
    "aws.s3.access_key"="xx",
    "aws.s3.secret_key"="xxx==",
    "aws.s3.endpoint"="{endpoint,必须是s3格式的endpoint,例如: tos-s3-cn-beijing.ivolces.com}",
    "aws.s3.enable_ssl" = "false"
);
```



2. Query Hudi table records


```sql
select * from  hudi_tos_catalog.db_1.table1 limit 1;
```


<span id="_3-iceberg-catalog"></span>
## 3 Iceberg Catalog

<span id="_3-1-hdfs存储"></span>
### 3.1 HDFS storage


1. Create Iceberg catalog


```sql
CREATE EXTERNAL CATALOG iceberg_catalog PROPERTIES (
    'type'='iceberg',
    'iceberg.catalog.type' = 'hive',
    'iceberg.catalog.hive.metastore.uris' = 'thrift://{hms_ip:hms_port}'
);
```



2. Query Iceberg table records


```sql
select * from iceberg_catalog.iceberg.iceberg_hdfs;
```


<span id="_3-2-tos存储"></span>
### 3.2 TOS storage


1. Create Iceberg catalog


```sql
CREATE EXTERNAL CATALOG iceberg_tos_catalog PROPERTIES (
    'type'='iceberg',
    'iceberg.catalog.type' = 'hive',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}',
    "aws.s3.access_key"="xxx",
    "aws.s3.secret_key"="xxxx==",
    "aws.s3.endpoint"="{endpoint,必须是s3格式的endpoint,例如: tos-s3-cn-beijing.ivolces.com}",
    "aws.s3.enable_ssl" = "false"
);
```



2. Query Iceberg table records


```sql
select * from iceberg_tos_catalog.iceberg.iceberg_tos;
```


<span id="_4-paimon-catalog"></span>
## 4 Paimon Catalog

<span id="_4-1-hdfs存储"></span>
### 4.1 HDFS storage


1. Create Paimon catalog


```sql
CREATE EXTERNAL CATALOG paimon_catalog_hdfs
PROPERTIES
(
    "type" = "paimon",
    "paimon.catalog.type" = "hive",
    "paimon.catalog.warehouse" = "{hdfs paimon root path}",
    "hive.metastore.uris" = "thrift://{hms_ip:hms_port}",
);
```



2. Query Paimon table records


```sql
set catalog paimon_catalog_hdfs;
show databases;

use test_db_hdfs;
show tables;

select * from paimon_catalog_hdfs.test_db_hdfs.test_tbl_hdfs;
```


<span id="_4-2-tos存储"></span>
### 4.2 TOS storage


1. Create Paimon catalog


```sql
CREATE EXTERNAL CATALOG paimon_catalog_fs
PROPERTIES
(
    "type" = "paimon",
    "paimon.catalog.type" = "filesystem",
    "paimon.catalog.warehouse" = "{hdfs paimon root path, 必须是s3协议，例如：s3://sr-qa/xxx}" ,
    "aws.s3.enable_ssl" = "false",
    "aws.s3.endpoint"="{endpoint,必须是s3格式的endpoint,例如: tos-s3-cn-beijing.ivolces.com}",
    "aws.s3.access_key" = "xxx",
    "aws.s3.secret_key" = "xxx=="
);
```



2. Query Paimon table records


```sql
set catalog paimon_catalog_fs;
show databases;

use test_db_fs;
show tables;

select * from paimon_catalog_fs.test_db_fs.test_tbl_fs;
```


<span id="_5-jdbc-catalog"></span>
## 5 JDBC Catalog

<span id="_5-1-语法"></span>
### 5.1 Syntax

```sql
CREATE EXTERNAL CATALOG <catalog_name
[COMMENT <comment]
PROPERTIES ("key"="value", ...)
```


Parameter explanations:

**catalog_name**

Name of the JDBC catalog. Naming requirements are as follows:


* Must consist of letters (a\-z or A\-Z), digits (0\-9), or underscores (_), and must start with a letter.

* The total length must not exceed 1023 characters.

* Catalog names are case\-sensitive.


**comment**

Description of the JDBC catalog. This parameter is optional.

**PROPERTIES**

Properties of the JDBC catalog, including the following required configuration items:


|Parameter |Note |
|---|---|
|type |Resource type, fixed value is jdbc. |
|user |Username for logging in to the target database. |
|password |Password for the target database user. |
|jdbc_uri |URI for the JDBC driver to connect to the target database. If using MySQL, the format is: "jdbc:mysql://ip:port". If using PostgreSQL, the format is "jdbc:postgresql://ip:port/db_name". |
|driver_url |URL for downloading the JDBC driver JAR package. Supports HTTP protocol or file protocol, for example https://repo1.maven.org/maven2/org/postgresql/postgresql/42.3.3/postgresql\-42.3.3.jar and file:///home/disk1/postgresql\-42.3.3.jar.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to use the TOS path method and change the file access permission to public read.</div><br> |
|driver_class |Class name of the JDBC driver. The following are the class names of JDBC drivers supported by common database engines: MySQL: com.mysql.jdbc.Driver (MySQL 5.x and earlier versions), com.mysql.cj.jdbc.Driver (MySQL 6.x and later versions) PostgreSQL: org.postgresql.Driver |


<span id="_5-2-mysql-catalog"></span>
### 5.2 Mysql Catalog


1. Create catalog


```python
CREATE EXTERNAL CATALOG jdbc_mysql
PROPERTIES
(
    "type"="jdbc",
    "user"="root",
    "password"="changeme",
    "jdbc_uri"="jdbc:mysql://127.0.0.1:3306",
    "driver_url"="https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.28/mysql-connector-java-8.0.28.jar",
    "driver_class"="com.mysql.cj.jdbc.Driver"
);
```



2. View catalog


```python
View all catalogs
SHOW CATALOGS;
View a catalog
SHOW CREATE CATALOG jdbc_mysql;
```



3. View catalog data

   1. Use [SHOW DATABASES](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_CATALOGS/) to view the databases in the cluster associated with the specified catalog:

   ```sql
   SHOW DATABASES FROM jdbc_mysql;
   ```
   

   2. Use [SET CATALOG](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/SET_CATALOG/) to switch the catalog in effect for the current session:

   ```sql
   SET CATALOG jdbc_mysql;
   ```
   

   3. Then use [USE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/USE/) to specify the database in effect for the current session:

   ```sql
   USE db_name;
   ```
   

   4. Alternatively, you can use [USE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/USE/) to directly switch the session to the specified database under the target catalog:

   ```sql
   USE jdbc_mysql.db_name;
   ```
   

   5. Use [SELECT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SELECT/) to query the target table in the target database:

   ```sql
   SELECT * FROM table_name;
   ```
   


<span id="_5-3-postgres-catalog"></span>
### 5.3 Postgres Catalog


1. Create catalog


```python
CREATE EXTERNAL CATALOG jdbc_pg
PROPERTIES
(
    "type"="jdbc",
    "user"="postgres",
    "password"="changeme",
    "jdbc_uri"="jdbc:postgresql://127.0.0.1:5432/jdbc_test",
    "driver_url"="https://repo1.maven.org/maven2/org/postgresql/postgresql/42.3.3/postgresql-42.3.3.jar",
    "driver_class"="org.postgresql.Driver"
);
```



2. View catalog


```python
View all catalogs
SHOW CATALOGS;
View a catalog
SHOW CREATE CATALOG jdbc_pg;
```



3. View catalog data

   1. Use [SHOW DATABASES](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SHOW_CATALOGS/) to view the databases in the cluster associated with the specified catalog:

   ```sql
   SHOW DATABASES FROM jdbc_pg;
   ```
   

   2. Use [SET CATALOG](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/SET_CATALOG/) to switch the catalog in effect for the current session:

   ```sql
   SET CATALOG jdbc_pg;
   ```
   

   3. Then use [USE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/USE/) to specify the database in effect for the current session:

   ```sql
   USE db_name;
   ```
   

   4. Alternatively, you can use [USE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/USE/) to directly switch the session to the specified database under the target catalog:

   ```sql
   USE jdbc_pg.db_name;
   ```
   

   5. Use [SELECT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SELECT/) to query the target table in the target database:

   ```sql
   SELECT * FROM table_name;
   ```

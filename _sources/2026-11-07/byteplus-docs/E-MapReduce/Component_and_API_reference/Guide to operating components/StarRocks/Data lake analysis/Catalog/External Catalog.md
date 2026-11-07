---
title: "External Catalog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/catalog_external_catalog"
---

<span id="_1-hive-catalog"></span>
## 1 Hive Catalog

<span id="_1-1-hdfs存储"></span>
### 1.1 HDFS storage


* Copy the contents of core\-site.xml and hdfs\-site.xml from the Hadoop cluster to configuration management in the StarRocks cluster. Changes take effect after restarting the component.

1. Create Hive Catalog


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


1. Create Hive Catalog


```sql
CREATE EXTERNAL CATALOG hive_tos_catalog PROPERTIES (
    'type'='hive',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}',
    "aws.s3.access_key"="xxx",
    "aws.s3.secret_key"="xxx==",
    "aws.s3.endpoint"="tos-s3-cn-beijing.ivolces.com",
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


* Copy the contents of core\-site.xml and hdfs\-site.xml from the Hadoop cluster to configuration management in the StarRocks cluster. Changes take effect after restarting the component.

1. Create Hudi Catalog


```sql
CREATE EXTERNAL CATALOG hudi_catalog PROPERTIES (
    'type'='hudi',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}'
);
```



2. Query Hudi table records


```sql
select * from  hudi_catalog.db_1.table1 limit 1;
```


<span id="_2-2-tos存储"></span>
### 2.2 TOS storage


1. Create Hudi Catalog


```sql
CREATE EXTERNAL CATALOG hudi_tos_catalog PROPERTIES (
    'type'='hudi',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}',
    "aws.s3.access_key"="xx",
    "aws.s3.secret_key"="xxx==",
    "aws.s3.endpoint"="tos-s3-cn-beijing.ivolces.com",
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


1. Create Iceberg Catalog


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


<span id="_3-2tos存储"></span>
### 3.2 TOS storage


1. Create Iceberg Catalog


```sql
CREATE EXTERNAL CATALOG iceberg_tos_catalog PROPERTIES (
    'type'='iceberg',
    'iceberg.catalog.type' = 'hive',
    'hive.metastore.uris' = 'thrift://{hms_ip:hms_port}',
    "aws.s3.access_key"="xxx",
    "aws.s3.secret_key"="xxxx==",
    "aws.s3.endpoint"="tos-s3-cn-beijing.ivolces.com",
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


1. Create Paimon Catalog


```sql
CREATE EXTERNAL CATALOG paimon_catalog_hdfs
PROPERTIES
(
    "type" = "paimon",
    "paimon.catalog.type" = "hive",
    "paimon.catalog.warehouse" = "hdfs://master-1-1.emr-xxx.offline-cn-beijing.emr-volces.com:8020/sr-qa/paimon-warehouse",
    "hive.metastore.uris" = "thrift://{hms_ip:hms_port}"
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


1. Create Paimon Catalog


```sql
CREATE EXTERNAL CATALOG paimon_catalog_fs
PROPERTIES
(
    "type" = "paimon",
    "paimon.catalog.type" = "filesystem",
    "paimon.catalog.warehouse" = "s3://sr-qa/xxx",
    "aws.s3.enable_ssl" = "false",
    "aws.s3.endpoint" = "tos-s3-cn-beijing.ivolces.com",
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

---
title: "Operate Iceberg data in Hive"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operate_Iceberg_data_in_Hive"
---

Hive supports accessing Iceberg data through internal tables or external tables. This document provides examples to introduce how to use Hive on E\-MapReduce (EMR) to access Iceberg data.

<span id="_1-前提条件"></span>
## prerequisites


1. Applicable to EMR version 1.2.0 and later (including EMR 1.2.0).

2. An EMR cluster has been created, and the Iceberg component is installed. There are two ways to install the Iceberg component.

   1. When creating an EMR cluster, select Iceberg as an optional component. For details, see: [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

   2. For an existing EMR cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.

3. After installing the Iceberg component, you need to restart the HiveServer2 service of the Hive component to load the Iceberg jar in the HiveServer2 process.

4. For data insertion operations, Hive's execution engine must be set to mr.


<span id="_2-操作步骤"></span>
## Procedure


1. Log in to the cluster primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run the following command in the Linux Bash shell of the cluster host to enter the Hive command line.

   ```Plain
   hive
   ```
   

   You can also refer to [Hive connection methods](https://docs.byteplus.com/docs/E-MapReduce/109265) to use the beeline command. For example:

   ```java
   beeline -u jdbc:hive2://master-1-1:10000/default -n hive -p <hive用户的密码>
   ```
   

3. Configure the Catalog information for Iceberg.

   Hive supports the following Catalog types for Iceberg: Hive, Hadoop, or empty. The configuration items vary depending on the type. Refer to [Iceberg parameter configuration](https://docs.byteplus.com/docs/E-MapReduce/109285). The following example uses the Hive type to create a Catalog named Iceberg:

   ```Plain
   SET iceberg.catalog.iceberg.type=hive;
   SET iceberg.catalog.iceberg.uri=thrift://master-1-1:9083;
   SET iceberg.catalog.iceberg.clients=10;
   ```
   

4. Create a table.

   ```sql
   CREATE DATABASE IF NOT EXISTS iceberg_db;
   
   CREATE EXTERNAL TABLE iceberg_db.table_a1(i INT, s STRING)
   STORED BY 'org.apache.iceberg.mr.hive.HiveIcebergStorageHandler'
   TBLPROPERTIES ('iceberg.catalog'='iceberg');
   ```
   

5. Insert data.

   ```sql
   -- Change Hive's execution engine to mr
   SET hive.execution.engine = mr;
   INSERT INTO iceberg_db.table_a1 VALUES(0, 'a');
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For INSERT operations, only the mr engine is supported .   </div>
   

6. Query the table.

   ```sql
   SELECT * FROM iceberg_db.table_a1;
   ```
   

7. Delete the table.

   ```sql
   DROP TABLE IF EXISTS iceberg_db.table_a1;
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deleting a table also deletes its data, but an empty directory with the table name will remain on HDFS.   </div>

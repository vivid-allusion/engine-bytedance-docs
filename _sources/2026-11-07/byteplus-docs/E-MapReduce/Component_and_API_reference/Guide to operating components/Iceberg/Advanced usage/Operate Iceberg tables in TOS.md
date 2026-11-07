---
title: "Operate Iceberg tables in TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operate_Iceberg_tables_in_TOS"
---

The data of Iceberg tables can be stored in Volcano Engine Object Storage Service (TOS). This section introduces examples of creating Iceberg tables in TOS using different engine components.

<span id="_1-前提条件"></span>
## 1 Prerequisites


* Applicable to Volcano Engine E\-MapReduce (EMR) versions after 3.1.0 (such as 3.2.1, 3.3.0, and more).

* The account executing the operation must have TOS authentication and read/write permissions. Refer to [Hadoop uses Proton](https://docs.byteplus.com/docs/undefined/69a96941fbfc73052b82bac5).


<span id="_2-spark-组件操作示例"></span>
## 2 Spark component operation example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">An EMR cluster containing Iceberg and Spark components has been created. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105456">Create clusters (version 3.18.0 and earlier)</a>.</div>


   1. <div data-tips="true" data-tips-type="tip">When creating an EMR cluster, select Iceberg as an optional component</div>


   2. <div data-tips="true" data-tips-type="tip">For an installed EMR cluster, refer to <a href="https://docs.byteplus.com/docs/E-MapReduce/105409">Add/restart services</a> to add the Iceberg service.</div>


2. <div data-tips="true" data-tips-type="tip"><strong>Spark operation example</strong> is not compatible with EMR2.x versions. For Spark component operations on Iceberg tables in EMR2.x versions, refer to <a href="https://docs.byteplus.com/docs/E-MapReduce/109286">Operate Iceberg tables in TOS (applicable to EMR 2.x versions)</a>.</div>



<span id="_2-1-操作步骤"></span>
### 2.1 Procedure


1. Log in to the EMR cluster primary node. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run commands to read and write Iceberg configurations via Spark SQL, and operate Iceberg in Spark SQL. For details, see the Spark component operation example in [Basic usage of Iceberg](https://docs.byteplus.com/docs/E-MapReduce/109275).

3. After completing the configuration and entering the spark\-sql command line, specify the TOS address when creating a database or table. Alternatively, configure the warehouse address of the Iceberg table as the TOS address. Choose either method. As follows:

   * Start SparkSQL and specify the TOS address

      Here, the Iceberg catalog name is configured as hive. Example:

   ```sql
   spark-sql \
     --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
     --conf spark.sql.catalog.hive=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.hive.type=hive \
     --conf spark.sql.catalog.hive.uri='{hive metastore address}'
     --conf spark.sql.catalog.hive.warehouse='{TOS address}'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Descriptions of the configuration items in the example can be found in <strong>Advanced Iceberg usage</strong> under <a href="https://docs.byteplus.com/docs/E-MapReduce/109285">Iceberg parameter configuration</a>. When running on an EMR cluster, the parameter <code>spark.sql.catalog.hive.uri</code> can be omitted.   </div>
   

   * Create a database and specify the TOS address:

   ```sql
   CREATE  DATABASE IF  NOT EXISTS  hive.iceberg_db_1 LOCATION    '{TOS地址}';
   ```
   

   * Create a table and specify the TOS address:

   ```sql
   CREATE TABLE IF NOT EXISTS hive.iceberg_db_1.spark_pokes(
       rank BIGINT,     
       suite STRING
   ) 
   USING iceberg
   LOCATION  '{TOS地址}';
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>{TOS address}</code> needs to be modified according to your actual situation. You can refer to the following example: tos://ceshi/autotest/iceberg/spark   </div>
   

<span id="_2-2-样例"></span>
### 2.2 Example


1. Start SparkSQL

   ```sql
   spark-sql \
     --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
     --conf spark.sql.catalog.hive=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.hive.type=hive \
     --conf spark.sql.catalog.hive.uri=thrift://emr-master-1:9083 \
     --conf spark.sql.catalog.hive.warehouse='tos://{bucket name}/tmp/warehouse'
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>{</code><strong><code>bucket name</code></strong><code>}</code> needs to be modified according to your actual situation. You can refer to the following example: tos://ceshi/autotest/iceberg/spark   </div>
   

2. Basic operations

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To operate Iceberg tables created by Spark in Trino, Presto, or Hive, go to the <strong>Cluster Details \> Service List \> HDFS \> Service Parameters</strong> page, add the <code>iceberg.engine.hive.enabled=true</code> configuration in the hdfs\-site parameters of HDFS, and restart the HDFS and Hive components. Then, create Iceberg tables in Spark and operate the tables in Hive.   </div>
   

   * Create a database

   ```sql
   CREATE DATABASE IF NOT EXISTS hive.iceberg_db;
   ```
   

   * Create a table

   ```sql
   CREATE TABLE IF NOT EXISTS hive.iceberg_db.spark_pokes(
       rank BIGINT, 
       suite STRING
   ) 
   USING iceberg;
   ```
   

   * View table information

   ```sql
   SHOW CREATE TABLE hive.iceberg_db.spark_pokes;
   ```
   

   The table information shows that the LOCATION address of the table data is stored in TOS.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f6301e5ec9b9235a118d2f41ad70b2d.png) </span>

   * Write data

   ```sql
   INSERT INTO hive.iceberg_db.spark_pokes VALUES (1, 'name1'), (2, 'name2');
   ```
   

   * Query data

   ```sql
   SELECT * FROM hive.iceberg_db.spark_pokes;
   ```
   

   * View table data on TOS


<span id="_3-hive-操作示例"></span>
## 3 Hive operation example

<span id="_3-1-操作步骤"></span>
### 3.1 Procedure

Hive can store data in TOS by specifying the LOCATION parameter when creating a database or table. For example:


* Create a database and specify the TOS address:

   ```sql
   CREATE DATABASE IF NOT EXISTS iceberg_db LOCATION  '{TOS地址}';
   ```
   

* Create a table and specify the TOS address:

   ```sql
   CREATE EXTERNAL TABLE iceberg_db.table_a1(i INT, s STRING)
   STORED BY 'org.apache.iceberg.mr.hive.HiveIcebergStorageHandler'
   LOCATION  '{TOS地址}'
   TBLPROPERTIES ('iceberg.catalog'='{iceberg catalog名称}');
   ```
   


<span id="_3-2-样例"></span>
### 3.2 Example


1. After starting the Hive console, configure the relevant Iceberg settings

   ```sql
   SET iceberg.catalog.iceberg_catalog.type=hive;
   SET iceberg.catalog.iceberg_catalog.uri=thrift://emr-master-1:9083;
   SET iceberg.catalog.iceberg_catalog.clients=10;
   SET iceberg.catalog.iceberg_catalog.warehouse=tos://{桶名称}/tmp/warehouse;
   ```
   

2. Create a database and table

   ```sql
   CREATE DATABASE IF NOT EXISTS d1 LOCATION 'tos://{桶名称}/tmp/warehouse/d1'; 
   
   CREATE EXTERNAL TABLE d1.t1(i INT, s STRING)
   STORED BY 'org.apache.iceberg.mr.hive.HiveIcebergStorageHandler'
   TBLPROPERTIES ('iceberg.catalog'='iceberg_catalog');
   
   CREATE DATABASE IF NOT EXISTS d2;
   CREATE EXTERNAL TABLE d2.t1(i INT, s STRING)
   STORED BY 'org.apache.iceberg.mr.hive.HiveIcebergStorageHandler'
   LOCATION  'tos://{桶名称}/tmp/warehouse/d2/t1'
   TBLPROPERTIES ('iceberg.catalog'='iceberg_catalog');
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>{</code><strong><code>bucket name</code></strong><code>}</code> needs to be modified according to your actual situation. You can refer to the following example: tos://ceshi/autotest/iceberg/hive   </div>
   

3. View table information

   ```sql
   SHOW CREATE TABLE d2.t1;
   ```
   

   The table information shows that the LOCATION address of the table data is stored in TOS.

4. Insert data

   ```sql
   INSERT INTO d1.t1 VALUES(1, 'a');
   INSERT INTO d2.t1 VALUES(1, 'a');
   ```
   

5. View data in TOS


<span id="_4-trino-presto-组件操作示例"></span>
## 4 Trino/Presto component operation example

The operation procedure for Presto/Trino is similar. The following uses Trino as an example.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An EMR cluster containing Iceberg, Trino, and Presto components has been created. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105456">Create clusters (version 3.18.0 and earlier)</a>.</div>


<span id="_4-1-添加配置参数"></span>
### 4.1 Add configuration parameters

Add configuration parameters in HDFS, then restart the HDFS and Trino components:


1. Log in to [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, go to **Cluster Management \> Cluster List \> Cluster Details \> Service List \> HDFS \> Service Parameters**.

3. In the HDFS service parameters interface, click **Add custom parameter**, select the configuration file core\-site, add the `fs.file.impl.disable.cache=true` parameter, and click the **Save** button to save the parameters.

4. After completing the parameter configuration, restart the HDFS and Trino components.


<span id="_4-2-执行命令"></span>
### 4.2 Run commands

Run the Trino CLI command to create an Iceberg table and specify the TOS address:


1. Log in to the primary node of the EMR cluster. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Access the Trino CLI and use the Iceberg connector to obtain the Metastore. For details, see [Iceberg integration with Trino/Presto](https://docs.byteplus.com/docs/E-MapReduce/109282).

3. Create a table and set the table's location address to the TOS address:

   ```shell
   CREATE TABLE iceberg.default.t1 (
       order_id BIGINT,
       order_date DATE,
       account_number BIGINT,
       customer VARCHAR,
       country VARCHAR
    )
    WITH (
       location='{TOS地址}',
       format = 'ORC',
       partitioning = ARRAY['bucket(account_number, 10)','country']
    )
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example, <code>{TOS address}</code> needs to be modified according to your actual situation. You can refer to the following example: tos://ceshi/autotest/iceberg/trino   </div>
   

4. Insert data:

   ```sql
   INSERT INTO iceberg.default.t1 VALUES (2, CAST('2021-01-12' AS DATE), 670011, 'bcd', 'ca');
   ```
   

5. Query data:

   ```sql
   SELECT * FROM iceberg.default.t1;
   ```

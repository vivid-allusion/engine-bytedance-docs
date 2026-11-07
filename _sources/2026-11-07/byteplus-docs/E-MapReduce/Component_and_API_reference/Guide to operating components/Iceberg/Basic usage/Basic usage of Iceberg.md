---
title: "Basic usage of Iceberg"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Basic_usage_of_Iceberg"
---

This article describes how to create and perform other operations on Iceberg tables using Spark SQL in an E\-MapReduce (EMR) cluster.

<span id="_1-前提条件"></span>
## 1 prerequisites


1. Applicable to EMR versions 1.2.0 and later (including EMR 1.2.0).

2. This article does not apply to EMR2.x versions. For Spark operations on Iceberg tables in EMR2.x versions, please refer to [Basic usage of Iceberg (applicable to EMR 2.x versions)](https://docs.byteplus.com/docs/E-MapReduce/109274)

3. An EMR cluster has been created and the Iceberg component is installed. There are two ways to install the Iceberg component:

   1. When creating an E\-MapReduce cluster, select Iceberg as an optional component. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

   2. For an existing E\-MapReduce cluster, refer to [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409) to add the Iceberg service.


<span id="_2-操作步骤"></span>
## 2 procedure


1. Log in to the cluster's primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

2. Run the following commands to read and write Iceberg configurations using Spark SQL:

   To operate Iceberg in Spark SQL, you must first configure the Catalog. The Catalog configuration uses **spark.sql.catalog.<catalog_name\>**  as the prefix. For example, if 'iceberg' is used as the Catalog name, the parameters are as follows:

   ```plain
   spark-sql \
     --conf spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions \
     --conf spark.sql.catalog.iceberg=org.apache.iceberg.spark.SparkCatalog \
     --conf spark.sql.catalog.iceberg.type=hive \
     --conf spark.sql.catalog.icenerg.uri=thrift://master-1-1:9083 
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the examples in this article, 'iceberg' is the Catalog name you created. To ensure that the databases and tables you operate are under the specified Catalog, you need to prefix the database and table names in your commands with 'iceberg'. For example:</div>



1. <div data-tips="true" data-tips-type="tip">To access the database 'iceberg_db' under 'iceberg', use <strong>iceberg.iceberg_db</strong>.</div>


2. <div data-tips="true" data-tips-type="tip">To access the table 'table1' under the database 'iceberg_db' in 'iceberg', use <strong>iceberg.iceberg_db.table1</strong>.</div>



The descriptions of the configuration items in the above command example are as follows. You can also refer to the **Advanced Iceberg usage** [Iceberg parameter configuration](https://docs.byteplus.com/docs/undefined/69a967d63002e40527b57408)section for more explanations of configuration items:


* spark.sql.extensions: SparkSQL extension module. The fixed value is org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions.

* spark.sql.catalog.iceberg: Catalog name. The fixed value is org.apache.iceberg.spark.SparkCatalog.

* spark.sql.catalog.iceberg.type: Catalog type, which can be set to hive or hadoop. This example uses hive.

* spark.sql.catalog.iceberg.uri: The URL address of Hive Metastore, in the format thrift://host:port. Check the value of the `hive.metastore.uris` parameter in the hive\-site configuration file of the Hive component. When running on an EMR cluster, the parameter `spark.sql.catalog.hive.uri` can be omitted.


Run the following command to enter the spark\-sql command line.

```Plain
spark-sql>
```



3. Basic operations on database tables

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To operate Spark\-created Iceberg tables in Trino, Presto, or Hive, go to the <strong>Cluster Details \> Service List \> HDFS \> Service Parameters</strong> page, add the <code>iceberg.engine.hive.enabled=true</code> configuration in the hdfs\-site service parameters of HDFS, and restart the HDFS and Hive components. Then create Iceberg tables in Spark and operate them in Hive.   </div>
   

   * Create database

      ```sql
      CREATE DATABASE IF NOT EXISTS iceberg.iceberg_db;
      ```
      

   * Create table

      ```sql
      CREATE TABLE  IF  NOT EXISTS  iceberg.iceberg_db.spark_pokes(
           rank  BIGINT, 
           suite STRING
      ) 
      USING  iceberg;
      ```
      

      Here, the CREATE TABLE statement supports COMMENT, PARTITIONED BY, TBLPROPERTIES, and other syntax. For detailed configuration, refer to the [official documentation](https://iceberg.apache.org/docs/latest/configuration/).

      For example, to set partition properties using PARTITIONED BY, see the following example:

      ```sql
      CREATE TABLE IF NOT EXISTS iceberg.iceberg_db.spark_pokes(
       rank BIGINT, 
       suite STRING
      ) 
      USING iceberg
      PARTITIONED BY (suite);
      ```
      

   * Write data

      ```sql
      INSERT INTO iceberg.iceberg_db.spark_pokes VALUES (1, 'name1'), (2, 'name2');
      ```
      

   * Query data

      ```sql
      SELECT * FROM iceberg.iceberg_db.spark_pokes;
      ```
      

   * Update data

      ```sql
      UPDATE iceberg.iceberg_db.spark_pokes SET suite = 'volcano' WHERE rank = 2;
      ```
      

   * Delete data

      ```sql
      DELETE FROM iceberg.iceberg_db.spark_pokes WHERE rank = 2;
      ```
      

   * Delete table

      ```sql
      DROP TABLE iceberg.iceberg_db.spark_pokes;
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When deleting a table using the DROP TABLE method, only the table's metadata is removed from Hive Metastore, while the table's data is retained.      </div>

---
title: "Use SparkSQL Warehouse to access Lance tables"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Use_SparkSQL_Warehouse_to_access_Lance_tables"
---

The EMR Serverless SparkSQL Warehouse compute group is designed for specialized and efficient execution of Spark SQL and has provided Lance integration capability. Users can configure the Lance Catalog within the SparkSQL Warehouse compute group and access Lance tables via SQL. This article introduces how to access Lance tables using the SparkSQL Warehouse compute group.

<span id="2dbf24eb"></span>
# Prerequisites

Before you begin, please confirm the following:


* The user has operation permissions for the target LAS Catalog. For detailed authorization steps, see [Permission Management](https://docs.byteplus.com/id/docs/Byteplus_LAS/Permission_Management).

* The user has obtained permissions for [EMR Serverls Queues](https://console.byteplus.com/emr/serverless/) and has created an available EMR Serverless queue. For detailed authorization steps, see [Create a sub-account and grant permissions](https://docs.byteplus.com/en/docs/E-MapReduce/Preparation_sq#create-sub-users) and [Queue Permission Management](https://docs.byteplus.com/en/docs/E-MapReduce/Permission_management_and_control). For detailed steps to create a queue, see [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue).


<span id="d1dedece"></span>
# Procedure

<span id="f679b6d6"></span>
## Step 1: Create a SparkSQL Warehouse compute group

Create a SparkSQL Warehouse compute group in the target Serverless queue. Configure compute resources and other parameters as needed for your business requirements during creation. For the entry point to create a SparkSQL Warehouse compute group, parameter descriptions, and management methods, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d247af417476463f9fa10e289d70760b~tplv-goo7wpa0wc-image.image) </span>

<span id="4ced1d7c"></span>
## Step 2: Configure Spark parameters

After creating the compute group, click the compute group name to enter the **compute group details page**. In the **Parameter configuration** section of the SparkSQL Warehouse compute group, add the Spark parameters required to access Lance tables.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab8e23a71fe34eecb8dd98d6b3b51bb6~tplv-goo7wpa0wc-image.image) </span>

**Example parameters:** 

```Bash
spark.executorEnv.JAVA_HOME=/usr/local/jdk17u
spark.kubernetes.driverEnv.JAVA_HOME=/usr/local/jdk17u
tqs.query.engine.type=sparkcli
spark.sql.storeAssignmentPolicy=ANSI
emr.serverless.spark.custom.parse.enabled=true
serverless.spark.lance.enabled=true
spark.executor.extraClassPath=/opt/emr/current/spark/extensions/lance/*:/opt/emr/current/spark/extensions/proton/*:/opt/emr/current/spark/extensions/paimon/*:/opt/emr/current/spark/extensions/iceberg/*:/opt/emr/current/spark/extensions/hudi/*:/opt/emr/current/spark/extensions/delta/*
spark.driver.extraClassPath=/opt/emr/current/spark/extensions/lance/*:/opt/emr/current/spark/extensions/proton/*:/opt/emr/current/spark/extensions/paimon/*:/opt/emr/current/spark/extensions/iceberg/*:/opt/emr/current/spark/extensions/hudi/*:/opt/emr/current/spark/extensions/delta/*
spark.sql.catalog.lance=org.lance.spark.LanceNamespaceSparkCatalog
spark.sql.extensions=org.lance.spark.extensions.LanceSparkSessionExtensions
spark.sql.catalog.lance.impl=las2
```



|**Parameter items** |**Note** |
|---|---|
|`spark.executorEnv.JAVA_HOME` |Configure the Java installation path used by the Executor process to ensure the Executor uses the specified version of the JDK. |
|`spark.kubernetes.driverEnv.JAVA_HOME` |Configure the Java installation path used by the Driver process running on Kubernetes. |
|`tqs.query.engine.type` |Specify the query engine type to select the engine used for submitting or executing query tasks. |
|`spark.sql.storeAssignmentPolicy` |Configure the field assignment policy for Spark SQL. When set to ANSI, Spark processes type conversions and assignments according to ANSI SQL rules. |
|`emr.serverless.spark.custom.parse.enabled` |Enabling this option allows the execution of extended SQL features of the lance\-spark connector. |
|`serverless.spark.lance.enabled` |Enables Lance\-related capabilities in Serverless Spark. |
|`spark.executor.extraClassPath` |Adds additional ClassPath entries to the Executor process for loading extension dependencies such as Lance, Proton, Paimon, Iceberg, Hudi, and Delta. |
|`spark.driver.extraClassPath` |Adds additional ClassPath entries to the Driver process for loading extension dependencies such as Lance, Proton, Paimon, Iceberg, Hudi, and Delta. |
|`/opt/emr/current/spark/extensions/proton/*:/opt/emr/current/spark/extensions/paimon/*:/opt/emr/current/spark/extensions/iceberg/*:/opt/emr/current/spark/extensions/hudi/*:/opt/emr/current/spark/extensions/delta/*` |A list of six paths joined by colons`:`<br><br>```Bash```<br>```/opt/emr/current/spark/extensions/lance/*```<br>```/opt/emr/current/spark/extensions/proton/*```<br>```/opt/emr/current/spark/extensions/paimon/*```<br>```/opt/emr/current/spark/extensions/iceberg/*```<br>```/opt/emr/current/spark/extensions/hudi/*```<br>```/opt/emr/current/spark/extensions/delta/*```<br><br><br>Specifies the paths for extension dependencies such as Lance, Proton, Paimon, Iceberg, Hudi, and Delta. |
|`spark.sql.catalog.lance` |The Spark Catalog implementation for Lance. |
|`spark.sql.extensions` |Configures Spark SQL Extensions (Spark SQL extensions) to enable Lance\-related SQL extension capabilities. |
|`spark.sql.catalog.lance.impl` |The default value is las2, indicating that table metadata is obtained from the LAS metadata center. |


<span id="bf7ce708"></span>
## Step 3: Execute Lance table queries


1. In the upper right corner of the compute group page, click **SQL Editor.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709645eb1f4849f3bd909ffe05b004d4~tplv-goo7wpa0wc-image.image) </span>

2. Go to the **SQL Editor** page, click the compute group dropdown in the upper right corner **compute group**, and select the SparkSQL Warehouse compute group created in Step 1,

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dc892adb4df4981b1724a400ac0d892~tplv-goo7wpa0wc-image.image) </span>

3. Execute the query statement to access Lance table data. Example query:

   ```SQL
   SELECT * FROM lance.<las_catalog_name>.<las_database_name>.<table_name> LIMIT 10;
   ```
   

   Replace `<las_catalog_name>`, `<las_database_name>`, and `<table_name>` with the actual LAS Catalog name, database name, and Lance table name, respectively.


<span id="e6dbdb28"></span>
# FAQs


* If the query returns a permission error, first confirm whether the current user has access permissions for the target LAS Catalog and table.

* If the query cannot recognize the Lance Catalog, check whether parameters such as `spark.sql.catalog.lance`, `spark.sql.extensions`, and `serverless.spark.lance.enabled` are correctly configured.

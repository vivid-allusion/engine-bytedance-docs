---
title: "Note for using Spark with lakehouse tables"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Note_for_using_Spark_with_lakehouse_tables"
---

EMR SparkSQL is fully compatible with the open\-source SparkSQL syntax. The following provides an overview of basic database and table operations. For more detailed guidance, refer to [the open-source SparkSQL syntax documentation](https://archive.apache.org/dist/spark/docs/3.2.1/sql-programming-guide.html).

<span id="4006d3c4"></span>
# Usage note

SQL syntax not officially supported by Spark requires additional support by setting the following parameters (for example, procedures in Iceberg).

```SQL
set emr.serverless.spark.custom.parse.enabled = true;
```


<span id="5ed4f7b2"></span>
# Basic operations

<span id="34e412bb"></span>
## **Database operations**

```SQL
-- Create a database
create database db_demo;

-- Create a database and specify a custom TOS bucket path for storage -- Important: Ensure that the TOS bucket exists and that the current user has read and write permissions for the bucket path.
create database db_demo location 'tos://您的tos bucket name/warehouse/';

-- View database information
desc database db_demo;

-- Delete a database
drop database db_demo;
```


<span id="3e0ea0e3"></span>
## Table operations

```SQL
use db_demo;
-- Create a table
create table tb_demo(id int, name string);

-- Create a table and specify a custom TOS bucket path for storage. The created table is an external table.
create table tb_demo(id int, name string) LOCATION 'tos://您的tos bucket name/xxx/tb_demo';

-- Create an external table, same effect as above
create EXTERNAL table tb_demo(id int, name string) LOCATION 'tos://您的tos bucket name/xxx/tb_demo';
DESCRIBE EXTENDED  tb_demo;

-- Describe table information
desc table tb_demo;

-- Query the table creation statement
show create table tb_demo;

-- Delete a table
drop table tb_demo;

-- Insert data
insert into tb_demo select 1,'name1';

-- Query table data
select * from tb_demo;
```


<span id="96e2aea4"></span>
## UDF operations

```SQL
-- Upload UDF, upload to the corresponding TOS path -- Create a UDF, default in the hive catalog
CREATE FUNCTION <schemaName>.<functionName> AS '<funcClassName>' using jar 'tos://您的tos bucket name/您的jar包地址';

-- Use UDF in Spark
select dbname.udfname('aaabbB');
select hive.dbname.udfname('aaabbB');

-- Use UDF in presto
select hive.dbname.udfname('aaabbB');
```


<span id="8f6c5972"></span>
# Spark accesses Hive

```SQL
create database if not exists test_hive_db;
create table if not EXISTS test_hive_db.test_tb(id int, name string);

insert into table test_hive_db.test_tb values(1, 'hehe'),(2, 'haha');
select * from test_hive_db.test_tb;

drop table if exists test_hive_db.test_tb;
drop database if exists test_hive_db;
```


<span id="ac485560"></span>
# Spark accesses Iceberg

```SQL
-- Default parameters
set spark.sql.catalog.spark_iceberg_catalog=org.apache.iceberg.spark.SparkCatalog;
set spark.sql.catalog.spark_iceberg_catalog.type=hive;
set spark.sql.storeAssignmentPolicy=ansi;
use spark_iceberg_catalog;

create database if not exists test_iceberg_db;
create table if not EXISTS test_iceberg_db.test_tb(id int, name string) using iceberg;

insert into table test_iceberg_db.test_tb values(1, 'hehe'),(2, 'haha');
select * from test_iceberg_db.test_tb;

drop table if exists test_iceberg_db.test_tb;
drop database if exists test_iceberg_db;

-- Access iceberg metadata tables, such as history, snapshots, and other metadata tables
set spark.sql.threePartIdentifier.catalogService.enabled=false;
select * from test_iceberg_db.test_tb.history;
```


<span id="aae5a492"></span>
# Spark accesses Paimon

```SQL
-- Default parameters
set spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
set spark.sql.catalog.spark_paimon_catalog.metastore=hive;
set spark.sql.storeAssignmentPolicy=ansi;
-- Custom warehouse path
set spark.sql.catalog.spark_paimon_catalog.warehouse=tos://tos_bucket_name/warehouse;
use spark_paimon_catalog;

create database if not exists test_paimon_db;
create table if not EXISTS test_paimon_db.test_tb(id int, name string) using paimon;

insert into table test_paimon_db.test_tb values(1, 'hehe'),(2, 'haha');
select * from test_paimon_db.test_tb;

drop table if exists test_paimon_db.test_tb;
drop database if exists test_paimon_db;
```


<span id="3e2926d9"></span>
# Spark accesses Hudi

```SQL
-- Default parameters
set spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog;
set spark.serializer=org.apache.spark.serializer.KryoSerializer;

create database if not exists test_hudi_db;
create table if not EXISTS test_hudi_db.test_tb(id int, name string) using hudi;

insert into table test_hudi_db.test_tb values(1, 'hehe'),(2, 'haha');
select * from test_hudi_db.test_tb;

drop table if exists test_hudi_db.test_tb;
drop database if exists test_hudi_db;
```


<span id="957b159f"></span>
# Spark accesses DeltaLake

```SQL
-- Default parameters
set spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog;

create database if not exists test_del_db;
create table if not EXISTS test_del_db.test_tb(id int, name string) using delta;

insert into table test_del_db.test_tb values(1, 'hehe'),(2, 'haha');
select * from test_del_db.test_tb;

drop table if exists test_del_db.test_tb;
drop database if exists test_del_db;
```


<span id="fa4f6533"></span>
# Accessing a custom LAS Catalog data directory

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note</div>


<div data-tips="true" data-tips-type="tip">To create an LAS Catalog data directory, you can go to the LAS console for operations.</div>


To access data directories in LAS Catalog other than Hive, use the following methods:


1. For DDL, you can set the parameter for the LAS Catalog data directory to be accessed, for example:

   ```SQL
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;  -- Specify your_las_catalog as the LAS Catalog data directory to be accessed
   
   --DDL
   create database if not exists test_hive_db;
   create table if not EXISTS test_hive_db.test_tb(id int, name string);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Important: The <code>spark.hadoop.hive.metastore.catalog.default</code> parameter applies to the entire current session. All databases and tables in the current session should exist within the same LAS Catalog data directory.   </div>
   

2. For DML and DQL, in addition to setting the above parameter, you can also specify databases and tables in a custom LAS Catalog data directory by using a three\-part naming convention in the table name, for example:

   ```SQL
   insert into table your_las_catalog.test_hive_db.test_tb values(1, 'hehe'),(2, 'haha');
   
   select * from your_las_catalog.test_hive_db.test_tb;
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DDL does not support using three\-part access to access multiple LAS Catalog data directories.   </div>
   

Complete examples for each lakehouse format are provided below.

<span id="e88b91dd"></span>
## Spark accesses Hive tables in a custom LAS Catalog


* DDL

   ```SQL
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   --DDL
   create database if not exists test_hive_db;
   create table if not EXISTS test_hive_db.test_tb(id int, name string);
   ```
   

* DML&DQL：

   ```SQL
   insert into table your_las_catalog.test_hive_db.test_tb values(1, 'hehe'),(2, 'haha');
   
   select * from your_las_catalog.test_hive_db.test_tb;
   ```
   

   Session\-specified catalog: Only one catalog can be accessed in SQL

   ```SQL
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   --DML&DQL
   insert into table test_hive_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_hive_db.test_tb;
   ```
   


<span id="d80bfe93"></span>
## Spark accesses Iceberg tables in a custom LAS Catalog


* DDL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_iceberg_catalog=org.apache.iceberg.spark.SparkCatalog;
   set spark.sql.catalog.spark_iceberg_catalog.type=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   use spark_iceberg_catalog;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   create database if not exists test_iceberg_db;
   create table if not EXISTS test_iceberg_db.test_tb(id int, name string) using iceberg;
   ```
   

* DML&DQL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_iceberg_catalog=org.apache.iceberg.spark.SparkCatalog;
   set spark.sql.catalog.spark_iceberg_catalog.type=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   
   -- Access method: custom catalog.database.table
   use spark_iceberg_catalog;
   insert into table your_las_catalog.test_iceberg_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from your_las_catalog.test_iceberg_db.test_tb;
   
   -- Access method: spark_iceberg_catalog.custom_catalog.database.table
   insert into table spark_iceberg_catalog.your_las_catalog.test_iceberg_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from spark_iceberg_catalog.your_las_catalog.test_iceberg_db.test_tb;
   ```
   

   Session\-specified catalog: Only one catalog can be accessed in SQL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_iceberg_catalog=org.apache.iceberg.spark.SparkCatalog;
   set spark.sql.catalog.spark_iceberg_catalog.type=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   use spark_iceberg_catalog;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   -- Access method: database.table
   insert into table test_iceberg_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_iceberg_db.test_tb;
   
   -- Access iceberg metadata tables, such as history, snapshots, and other metadata tables
   set spark.sql.threePartIdentifier.catalogService.enabled=false;
   select * from test_iceberg_db.test_tb.history;
   ```
   


<span id="cf3642d7"></span>
## Spark accesses Paimon tables in a custom LAS Catalog

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Caution</div>


<div data-tips="true" data-tips-type="tip">The Generic Catalog syntax in the community Spark Paimon Connector documentation does not support access to custom LAS Catalogs:</div>


<div data-tips="true" data-tips-type="tip">spark.sql.catalog.spark_catalog=org.apache.paimon.spark.SparkGenericCatalog</div>



* DDL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
   set spark.sql.catalog.spark_paimon_catalog.metastore=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   -- Custom warehouse path
   set spark.sql.catalog.spark_paimon_catalog.warehouse=tos://tos_bucket_name/warehouse;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   use spark_paimon_catalog;
   create database if not exists test_paimon_db;
   create table if not EXISTS test_paimon_db.test_tb(id int, name string) using paimon;
   ```
   

* DML&DQL：

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Three\-part access supports accessing multiple catalogs, but does not support DDL.   </div>
   

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
   set spark.sql.catalog.spark_paimon_catalog.metastore=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   -- Custom warehouse path
   set spark.sql.catalog.spark_paimon_catalog.warehouse=tos://tos_bucket_name/warehouse;
   
   use spark_paimon_catalog;
   -- Access method: custom catalog.database.table
   insert into table your_las_catalog.test_paimon_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from your_las_catalog.test_paimon_db.test_tb;
   ```
   

   Session\-specified catalog: Only one catalog can be accessed in SQL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_paimon_catalog=org.apache.paimon.spark.SparkCatalog;
   set spark.sql.catalog.spark_paimon_catalog.metastore=hive;
   set spark.sql.storeAssignmentPolicy=ansi;
   -- Custom warehouse path
   set spark.sql.catalog.spark_paimon_catalog.warehouse=tos://tos_bucket_name/warehouse;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   use spark_paimon_catalog;
   -- Access method: database.table
   insert into table test_paimon_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_paimon_db.test_tb;
   ```
   


<span id="b2a0ad76"></span>
## Spark accesses Hudi tables in a custom LAS Catalog


* DDL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog;
   set spark.serializer=org.apache.spark.serializer.KryoSerializer;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   create database if not exists test_hudi_db;
   create table if not EXISTS test_hudi_db.test_tb(id int, name string) using hudi;
   ```
   

* DML&DQL

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Three\-part access supports accessing multiple catalogs, but does not support DDL.   </div>
   

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog;
   set spark.serializer=org.apache.spark.serializer.KryoSerializer;
   
   -- Access method: custom catalog.database.table
   insert into table your_las_catalog.test_hudi_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from your_las_catalog.test_hudi_db.test_tb;
   ```
   

   Session\-specified catalog: Only one catalog can be accessed in SQL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.hudi.catalog.HoodieCatalog;
   set spark.serializer=org.apache.spark.serializer.KryoSerializer;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   -- Access method: database.table
   insert into table test_hudi_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_hudi_db.test_tb;
   ```
   


<span id="e8599946"></span>
## Spark accesses DeltaLake tables in a custom LAS Catalog


* DDL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   create database if not exists test_del_db;
   create table if not EXISTS test_del_db.test_tb(id int, name string) using delta;
   ```
   

* DML&DQL

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Three\-part access supports accessing multiple catalogs, but does not support DDL.   </div>
   

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog;
   
   -- Access method: custom catalog.database.table
   insert into table your_las_catalog.test_del_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from your_las_catalog.test_del_db.test_tb;
   ```
   

   Session\-specified catalog: Only one catalog can be accessed in SQL

   ```SQL
   -- Default parameters
   set spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog;
   
   -- Specify a custom Catalog and adjust as needed based on actual requirements
   set spark.hadoop.hive.metastore.catalog.default=your_las_catalog;
   
   -- Access method: database.table
   insert into table test_del_db.test_tb values(1, 'hehe'),(2, 'haha');
   select * from test_del_db.test_tb;
   ```
   


<span id="500e9899"></span>
# Configure custom lake format versions

The built\-in lake format versions for EMR Serverless Spark are as follows:


* Spark：3.5.1

* Paimon：0.8.1

* Iceberg：1.5.2

* Hudi：0.15.0

* Delta：3.1.0


When the built\-in lake format versions (such as Paimon, Iceberg, and others) do not meet specific business requirements, EMR Serverless Spark allows users to upgrade or switch versions by introducing custom Jar packages.

The following uses upgrading to Paimon version 1.3 as an example to illustrate the procedure:


1. Prepare and upload the Connector package


Download the Connector package compatible with the Spark version from the official website of the corresponding lake format.


* Example: For the Paimon 1.3 download address, refer to [Note for using Spark with lakehouse tables](https://docs.byteplus.com/docs/E-MapReduce/95190).

* Procedure: Upload the downloaded Jar package (such as paimon\-spark\-3.5\-1.3.1.jar) to your TOS path.

2. Set the dependency Jar package to be introduced


Set relevant parameters in the compute group or task configuration according to the task type to introduce custom dependencies:


* General compute group: Set the parameter at the task level `las.spark.jar.depend.jars=[{"fileName":"tos://your_tos_path/paimon-spark-3.5-1.3.1.jar"}]`.

* SparkSQL compute group: Configure the parameter in the compute group `spark.jars=tos://your_tos_path/paimon-spark-3.5-1.3.1.jar`.

3. Exclude built\-in lake format packages


To avoid version conflicts, you must exclude the built\-in lake format packages of serverless Spark by configuring parameters:


* Configuration parameter: `serverless.spark.excluded.extensions=paimon`.

* Parameter description: Supported lake format packages for removal are `paimon,iceberg,hudi,delta`, separated by commas for multiple formats.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Caution</div>



1. <div data-tips="true" data-tips-type="tip"><strong>Spark version compatibility</strong>: Custom JAR packages must strictly be compatible with the Spark version (3.5.1) of EMR Serverless Spark. Using mismatched versions may result in class loading exceptions or errors during task execution.</div>


2. <div data-tips="true" data-tips-type="tip"><strong>Lake format version compatibility</strong>: When upgrading the major version of the lake format (such as Paimon 0.8 → 1.3), carefully read the official Release Notes to confirm whether the new version introduces incompatible API changes, configuration adjustments, or underlying data format changes, and verify the readability of old tables and the data migration plan in advance.</div>


3. <div data-tips="true" data-tips-type="tip">This feature is only supported in the Java environment; the native Bolt engine is not supported.</div>

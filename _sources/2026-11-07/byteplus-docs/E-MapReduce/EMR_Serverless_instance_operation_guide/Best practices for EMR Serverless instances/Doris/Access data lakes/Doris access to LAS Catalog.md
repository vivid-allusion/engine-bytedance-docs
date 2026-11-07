---
title: "Doris access to LAS Catalog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Doris_access_to_LAS_Catalog"
---

In Volcano Engine EMR Serverless, Doris instances support direct access to the LAS Catalog. This article provides key operation steps and important notes.

<span id="6b9634e3"></span>
# Supported versions


* 2.x version: Doris version 2.1.11 and above supports access to the LAS Catalog.

* 3.x version: Doris version 3.0.8 and above supports access to the LAS Catalog.


<span id="7c0ecf05"></span>
# Preparation

<span id="5e026ab9"></span>
## Obtain LAS Catalog information


1. Log in to the Volcano Engine console with an account that has permission to access the LAS Catalog, and obtain the user's AK/SK for accessing the LAS Catalog.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b96b63b898824e9d853cde49b5c82966~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d7145edab244f059f2f272cd50f059d~tplv-goo7wpa0wc-image.image) </span>


<span id="a3b324a1"></span>
## Obtain Doris database information


1. Click the Doris instance card \- User Management, and create a new user for connecting to the Doris engine.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/464ac607379f4b27a9b1bc230571f2ad~tplv-goo7wpa0wc-image.image" width="3836px" />   </div>
   

2. Click the Doris instance card \- Network Connection to obtain connection information (optionally enable public IP).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9202ed3cfb3d47e483e834fce0802fd0~tplv-goo7wpa0wc-image.image) </span>


<span id="279a2d40"></span>
# Doris instance access to LAS Catalog

The following code sample demonstrates how to create an LAS Catalog and query databases and tables in the LAS Catalog using a Doris instance.

<span id="1d8373d6"></span>
## Hive

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For access to non\-LAS Catalogs, see <a href="https://docs.byteplus.com/docs/undefined/69a9678e3f58f805314f0666">Hive basic operations</a>.</div>



1. Create Hive Catalog

   ```SQL
   CREATE CATALOG ${自定义catalog名称} PROPERTIES (
     'type' = 'hms',
     'hive.metastore.type' = 'las',
     'hive.metastore.uris' = 'thrift://lakeformation.las.${region}.ivolces.com:48869',
     'hive.metastore.catalog.default' = '${las catalog名称}', 
     'warehouse' = '${las catalog存储TOS路径}',
     -- LAS authentication
     'las.hive.metastore.service'   = 'catalog_service',
     'las.hive.metastore.region'    = '${region}',
     'las.hive.metastore.access.key'= '${AK}',
     'las.hive.metastore.secret.key'= '${SK}',
     'las.tos.endpoint' = 'tos-${region}.ivolces.com',
     -- S3/TOS access configuration
     'aws.s3.enable_ssl' = 'false',
     'aws.s3.region' = '${region}',
     'aws.s3.endpoint' = 'tos-s3-${region}.ivolces.com',
     'aws.s3.access_key' = '${AK}',
     'aws.s3.secret_key' = '${SK}'
   ); 
   ```
   

   The following parameters:

   * `las.tos.endpoint` : The endpoint for Proton to access TOS.

   * `aws.s3.endpoint`: The endpoint for backend access to S3.

   * `hive.metastore.catalog.default`: Used to switch between multiple LAS Catalogs and specifies the Catalog that belongs to LAS.

2. Switch the Catalog and view the databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Hive tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```
   


<span id="1834828c"></span>
## Iceberg

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For access to non\-LAS Catalogs, see <a href="https://docs.byteplus.com/docs/undefined/6a182bd7a58760054cb6be65">Access the Iceberg Catalog through a Doris instance</a>.</div>



1. Create Iceberg Catalog

   ```SQL
   CREATE CATALOG ${自定义catalog名称} PROPERTIES (
     'type' = 'iceberg',
     'iceberg.catalog.type' = 'las',
     'iceberg.catalog.warehouse' = '${las catalog存储TOS路径}',
     'hive.metastore.uris' = 'thrift://lakeformation.las.${region}.ivolces.com:48869',
     'hive.metastore.catalog.default' = '<las_catalog_name>', 
     -- LAS authentication
     'las.hive.metastore.service'   = 'catalog_service',
     'las.hive.metastore.region'    = '${region}',
     'las.hive.metastore.access.key'= '${AK}',
     'las.hive.metastore.secret.key'= '${SK}',
     'las.tos.endpoint' = 'tos-${region}.ivolces.com',
     -- S3/TOS access configuration
     'aws.s3.enable_ssl' = 'false',
     'aws.s3.region' = '${region}',
     'aws.s3.use_instance_profile' = 'false',
     'aws.s3.use_aws_sdk_default_behavior' = 'false',
     'aws.s3.endpoint' = 'tos-s3-${region}.ivolces.com',
     'aws.s3.access_key' = '${AK}',
     'aws.s3.secret_key' = '${SK}'
    ); 
   ```
   

   The following parameters:

   * `las.tos.endpoint` : The endpoint for Proton to access TOS.

   * `aws.s3.endpoint`: The endpoint for backend access to S3.

   * `hive.metastore.catalog.default`: Used to switch between multiple LAS Catalogs and specifies the Catalog that belongs to LAS.

2. Switch the Catalog and view the databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Iceberg tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```
   


<span id="4903bee2"></span>
## Paimon

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For access to non\-LAS Catalogs, see <a href="https://docs.byteplus.com/docs/undefined/69a967db8a3fb00506e9d36e">Basic usage</a>.</div>



1. Create Paimon Catalog

   ```SQL
   CREATE CATALOG doris_308_paimon_hns PROPERTIES (
     'type' = 'paimon',
     'paimon.catalog.type' = 'las',
     'hive.metastore.uris' = 'thrift://lakeformation.las.cn-beijing.ivolces.com:48869',
     'hive.metastore.catalog.default' = '${las catalog名称}', 
     'warehouse' = '${las catalog存储TOS路径}',
     -- LAS authentication
     'las.hive.metastore.service'   = 'catalog_service',
     'las.hive.metastore.region'    = '${region}',
     'las.hive.metastore.access.key'= '${AK}',
     'las.hive.metastore.secret.key'= '${SK}',
     'las.tos.endpoint' = 'tos-${region}.ivolces.com',
     -- S3/TOS access configuration
     'aws.s3.enable_ssl' = 'false',
     'aws.s3.region' = '${region}',
     'aws.s3.endpoint' = 'tos-s3-${region}.ivolces.com',
     'aws.s3.access_key' = '${AK}',
     'aws.s3.secret_key' = '${SK}'
     ); 
   ```
   

   The following parameters:

   * `las.tos.endpoint` : The endpoint for Proton to access TOS.

   * `aws.s3.endpoint`: The endpoint for backend access to S3.

   * `hive.metastore.catalog.default`: Used to switch between multiple LAS Catalogs and specifies the Catalog that belongs to LAS.

2. Switch the Catalog and view the databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Iceberg tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```

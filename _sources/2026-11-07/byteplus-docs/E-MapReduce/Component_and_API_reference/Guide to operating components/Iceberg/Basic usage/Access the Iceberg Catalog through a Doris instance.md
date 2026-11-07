---
title: "Access the Iceberg Catalog through a Doris instance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Access_the_Iceberg_Catalog_through_a_Doris_instance"
---

This article describes how to access the Iceberg Catalog through a Doris instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Doris version used has the following restrictions:</div>



* <div data-tips="true" data-tips-type="warning">2.x version: Doris supports this starting from version 2.1.11 and above.</div>


* <div data-tips="true" data-tips-type="warning">3.x version: Doris supports this starting from version 3.0.8 and above.</div>


1. Create a catalog.

   
   <Tabs>
   <Tab zoneid="BieTakWmWa" title="HMS Catalog">
   <TabTitle>HMS Catalog</TabTitle>
   
   ```SQL
   CREATE CATALOG iceberg_hms_on_s3_catalog PROPERTIES (
       'type' = 'iceberg',
       'iceberg.catalog.type' = 'hms',
       'hive.metastore.uris' = '<hms_url>',
       'las.tos.endpoint' = '<tos_bucket_warehouse>',
       'aws.s3.region'= 'cn-beijing',
       'aws.s3.endpoint' = '<tos_s3_endpoint>',
       'aws.s3.access_key' = '<ak>',
       'aws.s3.secret_key' = '<sk>'
   );
   ```
   
   
   Details:
   
   
      * `las.tos.endpoint`: The endpoint for proton to access tos.
   
      * `aws.s3.endpoint`: The endpoint for backend access to s3.
   
   
   </Tab>
   <Tab zoneid="ComvexjI4q" title="LAS Catalog">
   <TabTitle>LAS Catalog</TabTitle>
   
   For details, see [Doris 访问 LAS Catalog](https://docs.byteplus.com/docs/undefined/698008803c928c0509be188b).
   
   
   </Tab>
   </Tabs>
   

2. Switch catalogs and view databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Paimon tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```

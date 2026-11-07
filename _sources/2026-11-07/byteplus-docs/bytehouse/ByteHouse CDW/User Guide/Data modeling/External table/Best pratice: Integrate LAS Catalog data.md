---
title: "Best pratice: Integrate LAS Catalog data"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-integrate-las-catalog-data"
---

This document describes how to access data on **LAS Catalog** from ByteHouse using **external tables**, enabling data processing without importing data into ByteHouse while leveraging its data warehouse acceleration capabilities to improve efficiency.

<span id="41939448"></span>
# Prerequisites

Ensure that the BytePlus account conducting the foreign table actions has acquired the following permissions:


* Access to the LAS Catalog, along with read and write permissions at the library table level.

* Additionally, when writing data to LAS, also possess TOS access permissions and the HNS (Hierarchical Buckets) feature enabled in TOS.


<span id="2ea61a57"></span>
# Background

The organizational structure of LAS Catalog data is a three\-tier data structure: **Catalog / Database / Table**, for example:

```SQL
catalog: benchmark
database: ssb100parquet
table: lineorder_flat
```


This means that the data is stored in the lineorder_flat table under the ssb100parquet database of the benchmark catalog.under the ssb100p**arquet databalineorder_flat table under the ssb100parquet database of the benchmark** catalog.

<span id="15eef7d1"></span>
# Configure LAS external tables in ByteHouse

<span id="7f0a0a6d"></span>
## Configure external tables

As an example, this SQL command is used to create an external table named 'las' in the 'ext' database within ByteHouse, and map it to the 'ssb100parquet.lineorder_flat' table in the LAS benchmark catalog within ByteHouse.

```SQL
CREATE DATABASE IF NOT EXITS ext

CREATE TABLE ext.las
ENGINE = CnchHive('thrift://lakeformation.las.{REGION}.ibytepluses.com:48869', 'ssb100parquet', 'lineorder_flat')
SETTINGS 
    meta_type = 'lf',
    lf_metastore_catalog = 'benchmark', 
    lf_metastore_region = '{REGION}', 
    lf_metastore_ak_id = 'AKLTMjNkMDRlMXXXXXXXXXXWUzZ******',
    lf_metastore_ak_secret='WVXXXXXXXXXXXXXXXXXX******', 
    lf_metastore_url = 'thrift://lakeformation.las.{REGION}.ibytepluses.com:48869',
    endpoint = 'tos-s3-{REGION}.ibytepluses.com', 
    ak_id = 'AKLTMjNkMDRlMXXXXXXXXXXWUz******', 
    ak_secret='WVXXXXXXXXXXXXXXXXXX******';
```


Parameter descriptions are as follows:


* `thrift://lakeformation.las.{REGION}.ibytepluses.com:48869`: This link specifies the connection address of the available region where LAS is located. You can modify it by referring to the following content according to the region you are using:

   
   |region |lf_metastore_url |
   |---|---|
   |cn\-hongkong |thrift://lakeformation.las.cn\-hongkong.ibytepluses.com:48869 |
   |ap\-southeast\-1 |thrift://lakeformation.las.cn\-ap\-southeast\-1.ibytepluses.com:48869 |
   

* `ssb100parquet, lineorder_flat`: indicates that the created external table is mapped to the 'ssb100parquet.lineorder_flat' table in LAS.

* `meta_type`: Fixed as 'lf', indicating that the created external table is mapped into the Catalog of LAS. Further configuration required:

   * `lf_metastore_catalog = 'benchmark'`: Indicates that the created external table is mapped to a catalog named 'benchmark' in LAS.

   * Authentication parameters for LAS:

      ```SQL
      lf_metastore_region = 'cn-beijing', 
      lf_metastore_ak_id = 'AKLTMjNkMDRlMXXXXXXXXXXdkYzM4OWUzZD******',
      lf_metastore_ak_secret='USDCWEDSDCSXXXXXXXXXXXXXD******', 
      ```
      

      User's access_key and secret_key information for accessing metadata of tables in LAS

   * LAS data storage TOS information:

      ```SQL
      endpoint = 'tos-s3-cn-beijing.ibytepluses.com', 
      ak_id = 'AKLTMjNkMDRlMXXXXXXXXXXdkYzM4OWUzZD******', 
      ak_secret='USDCWEDSDCSXXXXXXXXXXXXX******',
      ```
      

      User's access_key and secret_key information for accessing the actual storage data in TOS tables


<span id="66a77849"></span>
## Common actions

View column information of tables in ByteHouse.

```SQL
DESCRIBE TABLE ext.las
```


<span id="a8ea97ed"></span>
# Configure LAS Catalog in ByteHouse

<span id="86379d14"></span>
## Configure Catalog

```SQL
CREATE EXTERNAL CATALOG `las_catalog` PROPERTIES　
    aws.s3.endpoint='tos-s3-cn-beijing.ibytepluses.com',　
    aws.s3.access_key='AKLTMjNkMDRlMXXXXXXXXXXWUzZ******',　
    aws.s3.secret_key='WVXXXXXXXXXXXXXXXXXX******',　
    lf_metastore_ak_id='AKLTMjNkMDRlMXXXXXXXXXXWUzZ******',
    lf_metastore_ak_secret='WVXXXXXXXXXXXXXXXXXX******',　
    lf_metastore_catalog='benchmark',　
    lf_metastore_region='cn-beijing',　
    lf_metastore_url = 'thrift://lakeformation.las.cn-beijing.ibytepluses.com:48869',
    type='lf';
```


The meaning of specific parameters is similar to that described earlier for LAS external tables.

<span id="e837b1d8"></span>
## Common actions

Users can access tables in Hive directly using the naming method `catalog_name.db_name.table_name`, for example,

```SQL
select count() from las_catalog.ssb100parquet.lineorder_flat;
```


List database names in LAS Catalog

```SQL
show databases from las_catalog
```


List table names in the Database

```SQL
show tables from las_catalog.ssb100parquet
```


Get the table creation statement

```SQL
show create table las_catalog.ssb100parquet.lineorder_flat
```


Write data

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, <strong>writing data to TOS Buckets without activated HNS is not supported</strong>. For more information about TOS Bucket HNS, see the <a href="https://www.volcengine.com/docs/6349/1278171">TOS Help Documentation</a>.</div>


```SQL
insert into/overwrite las_catalog values (xxx);
insert into/overwrite las_catalog select * from xxx settings enable_optimizer =1;
```

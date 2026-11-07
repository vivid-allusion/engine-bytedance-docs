---
title: "Hive Catalog"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hive-catalog"
---

Beyond using external tables to access Hive data, Bytehouse CDW also supports access through External Catalog.

<span id="ccc8c28a"></span>
# Create Catalog

<span id="0b2297dc"></span>
## Create LasFormation Catalog

<span id="82596d76"></span>
### DDL definition

```SQL
CREATE EXTERNAL CATALOG `las_catalog` PROPERTIES　
aws.s3.access_key='AK',　
aws.s3.endpoint='tos-s3-{REGION}.ibytepluses.com',　
aws.s3.secret_key='SK',　
lf_metastore_ak_id='AK',
lf_metastore_ak_secret='SK',　
lf_metastore_catalog='LF_CATALOG_NAME',　
lf_metastore_region='{REGION}',　
lf_metastore_url = 'thrift://las_formation_endpoint',　type='lf';
```


You need to modify the following parameters based on actual conditions:


* aws.s3.access_key, aws.s3.secret_key: Modify to TOS's AK/SK

* lf_metastore_ak_id, lf_metastore_ak_secret: Modify to LasFormation's AK/SK

* lf_metastore_catalog: Modify to the catalog name of LasFormation

* Change lf_metastore_region to region information

* Change lf_metastore_url to the endpoint address of LasFormation, for more details, refer to [LAS Connection Address Help Document](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80-2).


<span id="fdd50b1b"></span>
### Write to Las

After creating a Catalog, you can write data into the LasFormation table as shown below:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before writing into the LasFormation table, please confirm:</div>



* <div data-tips="true" data-tips-type="warning">LasFormation access rights available</div>


* <div data-tips="true" data-tips-type="warning">TOS access rights available</div>


* <div data-tips="true" data-tips-type="warning">TOS has HNS (hierarchical buckets) feature enabled</div>



<div data-tips="true" data-tips-type="warning">Currently, CDW <strong>does not support writing into TOS Buckets without HNS enabled</strong>. For more information about TOS Bucket's HNS, refer to <a href="https://www.volcengine.com/docs/6349/1278171">TOS Help Documentation</a>.</div>


```SQL
insert into/overwrite las_catalog values (xxx);
insert into/overwrite las_catalog select * from xxx settings enable_optimizer =1;
```


<span id="999ff272"></span>
## Create Hive Catalog

Data use in s3

```SQL
create external catalog hive_s3
properties
  type='hive',
  hive.metastore.uri = 'thrift://hive_thrift_server_ip:port',
  aws.s3.region= 's3_region',
  aws.s3.endpoint = 's3_endpoint',
  aws.s3.access_key = 's3_ak',
  aws.s3.secret_key = 's3_sk'
```


Data use in hdfs

```Plain
create external catalog hive_hdfs
properties
    type='hive',
    hive.metastore.uri = 'thrift://hive_thrift_server_ip:port',
```


Note that for Hive external tables stored on HDFS, we only support reading data from HDFS configured in `cnch-config.yaml`.

<span id="48753c91"></span>
## Create Glue Catalog

We have also experimentally supported AWS Glue Datacatalog.

```Plain
create external catalog glue_s3
properties
type='glue',
    aws.glue.endpoint = 'glue_endpoint',
    aws.glue.region='glue_region',
    aws.glue.catalog_id='glue_catalog_id',
    aws.glue.access_key = 'glue_ak',
    aws.glue.secret_key = 'glue_sk',
    aws.s3.region= 's3_region',
    aws.s3.endpoint = 's3_endpoint',
    aws.s3.access_key =   's3_ak',
    aws.s3.secret_key =   's3_sk'
```


The `glue_catalog_id` here is a 12\-digit AWS account name. For details, refer to [Aws Account ID Doc](https://repost.aws/questions/QUWxpW7KY7RsCj2ttURvb7jQ/get-glue-data-catalog-name-id).

<span id="776f449b"></span>
# View Catalog

View all Catalogs.

```SQL
show external catalogs;
```


View the schema of a specified Catalog.

```SQL
show create external catalog your_catalog_name;
```


<span id="7375e5db"></span>
# Delete External Catalog

Users can delete the External Catalog as follows

```SQL
drop external catalog your_catalog_name;
```


<span id="b81a446d"></span>
# Use Catalog

Assume the user has already created an External Catalog named `hive_s3`

<span id="41bab5f1"></span>
## Three\-part naming

Users can directly access tables in Hive using the three\-part naming format `catalog_name.db_name.table_name`, for example

```SQL
select * from hive_s3.hive_db_name.hive_table_name;
```


ByteHouse's native CnchMergeTree tables can also be accessed with the following SQL

```SQL
select * from cnch.cnch_db_name.cnch_db_name;
    -- this is equivalent to select * from  cnch_db_name.cnch_db_name; 
```


`cnch` (abbreviation for cloud\-native\-clickhouse) is used as the default Catalog name for Bytehouse CDW.

<span id="eec49ed6"></span>
## Cross\-Catalog query

Using the External Catalog, users can directly join Hive external tables with Cnch's CnchMergeTree tables

```SQL
 select * from hive_s3.hive_db.hive_table union all select (1) from cnch.cnch_db.cnch_table;
```


<span id="f2037229"></span>
## Show Databases and Tables

List database names in the Catalog

```SQL
 show databases from hive_catalog
```


List table names in the database

```SQL
 show tables from hive_catalog.database
```


Get the table creation statement

```Plain
 show create table hive_catalog.database.table
```


Please note, the `show create table` result for external tables is similar to the following

```SQL
CREATE TABLE hive_catalog$$hive_db_name.hive_table_name UUID 'some-uuid' (--field list -- cc_call_center_sk Nullable(Int64), cc_call_center_id Nullable(String))) ENGINE = CnchHive(hive_catalog, hive_db_name, hive_table_name) PARTITION BY tuple() SETTINGS endpoint = 'hive_endpoint', ak_id = 's3_ak', ak_secret = 's3_sk', region = 's3_region'
```


<span id="9d0c270d"></span>
## Switch Catalog

Users can use the following SQL to change the default Catalog

```SQL
switch catalog hive_s3;
```


When running again

```SQL
select * from tpcds.call_center;
```


Bytehouse CDW will then read data from the call_center table in the tpcds database in Hive. To switch back to the default Catalog, users can use:

```SQL
switch catalog cnch;
```


Users can also use:

```Plain
use hive_s3.tpcds
```


Directly switch the default database to Hive's tpcds database. To switch to internal tables in Bytehouse CDW, directly use:

```Plain
use cnch.cnch_database_name
```

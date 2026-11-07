---
title: "Hive external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hive-external-table"
---

CnchHive, provided by the Bytehouse team, is a table engine that supports federated querying through external tables. Users can query data in Hive external tables directly without data import, enhancing flexibility and convenience in data processing. This article will introduce how to create, query, and write to external tables.

<span id="1245f68a"></span>
# Background Information

The functionality of external tables aims to provide data processing capabilities for data outside of ByteHouse's internal tables. With a simple DDL statement, you can create an external table on ByteHouse, linking ByteHouse tables with external data sources.


* External tables only incur computation costs on the ByteHouse side, following ByteHouse's computing resource billing rules. For details, please see [Computational resources](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing#cadb49e9).

* When using external table functions, the data of the external table **will not** be duplicated and stored on ByteHouse, incurring storage costs. For storage costs, please pay attention to the billing rules for storage on the external data source side.

* When accessing external data sources via ByteHouse external tables, the external data source may incur costs for computation, access, data transfer, etc., which are subject to the billing methods of the external data source; please refer to the corresponding product descriptions.


<span id="6a3c9f85"></span>
# Usage Restrictions


* Currently, only data in Parquet/Orc/CSV/Text formats is supported.

* Currently, only select and insert operations on Hive external tables are supported, alert is not supported; and currently, only Hive tables are supported, not views.

* When the schema of the Hive table in the external data source changes, automatic synchronization to the ByteHouse external table is not supported; you need to recreate the Hive external table in ByteHouse.


<span id="e083760c"></span>
# Prerequisites

Before starting operations, please ensure you have the following necessary permissions and information:


|Condition Segmentation |Description |
|---|---|
|Data Access Rights |Access permission for Hive external table metadata and its S3 storage service usage is required. |
|Access Key |Access key for Hive external table metadata and its S3 storage service usage is required. |
|Regional and Endpoint Information |Retrieve metadata for Hive external tables and the regions and endpoint information of the S3 storage service used. |
|Hive external table metadata information |Retrieve the catalog, database, and table names of the Hive external table. |


<span id="e69ab080"></span>
# Create External Table

By creating an external ByteHouse table, you can import the description of Hive external table data into ByteHouse for processing Hive data.

When creating a Hive external table, you need to specify the library table information of the associated Hive external table, currently supporting the following two settings:


* [Method one: (Recommended) Create an external catalog and external table](https://docs.byteplus.com/docs/bytehouse/hive-external-table#57caacb4)

* [Method two: Directly specify Hive external table in DDL](https://docs.byteplus.com/docs/bytehouse/hive-external-table#7a7b903c)


<span id="57caacb4"></span>
## Method one: (Recommended) Create an external catalog and external table

This method introduces an external catalog. First, you need to create an external catalog and save the corresponding connection parameters, when creating the external table, just specify the engine and virtual warehouse information. For subsequent access to the external table, you can directly access it using the three\-part notation catalog.db.table.

This chapter utilizes the BytePlus Lake AI Data Service (LAS) as an example of the created external catalog and external table, using BytePlus Torch Object Storage (TOS) for storage services. You can replace the parameters in the example based on the actual storage media and Hive external table information you use.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about accessing the LAS Catalog via external tables in ByteHouse, please see <a href="https://docs.byteplus.com/docs/bytehouse/best-practice-integrate-las-catalog-data">Best pratice: Integrate LAS Catalog data</a>.</div>



1. Create an External Catalog.

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
   

   
   |Parameters |Configuration description |
   |---|---|
   |Create external catalog |Customize the display name of the external catalog in ByteHouse. |
   |PROPERTIES parameter |Defines the connection information for data storage and metadata.<br><br><br>* `aws.s3.access_key` and `aws.s3.secret_key`: Modify these to the AK/SK of the storage service. Using BytePlus TOS as an example, please refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey) for how to obtain these.<br><br>* `aws.s3.endpoint`: Modify this to the endpoint address of your storage service, using BytePlus TOS as an example. For details, please see the information in the S3 Endpoint column within [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).<br><br>* `lf_metastore_ak_id` and `lf_metastore_ak_secret`: Modify these to the AK/SK of the external catalog, using BytePlus LAS as an example. For how to obtain these, please refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).<br><br>* `lf_metastore_catalog`: Modify this to the name of the external catalog, using BytePlus LAS as an example. You can log into the [LAS Control Panel](https://console.volcengine.com/las/region:las+cn-beijing/next/metadata/data_directory?CatalogName=hive), select **Data Lake\>Metadata Management** from the left navigation menu, and obtain the required catalog name.<br><br>* `lf_metastore_region`: Modify this to the region information of the external catalog, using BytePlus LAS as an example. For details, please refer to [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).<br><br>* `lf_metastore_url`: Modify this to the endpoint address of the external catalog, using BytePlus LAS as an example. For details, please refer to [LAS Connection Address Help Documentation](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80). |
   

2. Create an external table.

   ```SQL
   CREATE TABLE t 
   Engine = CnchHive('thrift://host:port', 'hive_database_name', 'hive_table_name')
   SETTINGS cnch_vw_default ='your_vw';
   DESCRIBE TABLE t;
   ```
   

   The parameter explanation is as follows:

   
   |Parameters |Configuration Description |
   |---|---|
   |Table Creation Description |The column names and types of Hive tables as well as information like Partition By key and Cluster By key will be automatically deduced and established during table creation. **Columns default to Nullable type**. The column type mapping rules are explained in the [Reference: Column type mapping](https://docs.byteplus.com/docs/bytehouse/hive-external-table#884e7416) section below. |
   |Engine parameters (Engine) |* `thrift://host:port`: the service address of the Hive external table. Taking BytePlus LAS as an example, see the [LAS connection address help document](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80) for details.<br><br>* `hive_database_name` and `hive_table_name`: specify the Hive external table to associate. For BytePlus LAS, you can log in to the [LAS console](https://console.volcengine.com/las/region:las+cn-beijing/next/metadata/data_directory?CatalogName=hive), select **Data Lake \> Metadata Management** in the left navigation bar, then click the linked catalog name to view and obtain the required database and table names. |
   |Settings (SETTINGS) |`cnch_vw_default`: used to specify the virtual warehouse. You can view the available virtual warehouses and copy the virtual warehouse ID on the **Virtual Warehouse** page of the ByteHouse console. If this parameter is not set, the default virtual warehouse you configured in ByteHouse will be used. |
   


<span id="7a7b903c"></span>
## Method two: Directly specify Hive external table in DDL

The example in this section uses TOS as a storage medium, directly specifying LAS as a Hive external table in the general create table DDL. You can replace the parameters in the example with the storage service and Hive external table information you are using.

```SQL
CREATE TABLE t 
Engin = CnchHive('thrift://hive_metastore:port', 'hive_database_name', 'hive_table_name')
SETTINGS endpoint = 'thrift://lakeformation.las.{REGION}.ibytepluses.com:48869',
         region = '{REGION}',
         ak_id = 'AKLTMjU3ZTYzOG********yMGE0ZmJiZjc2ODkxZWMxY2Q',
         ak_secret = 'WlRkak56Ump**********sT0RCaU9UQm1NREV4WkRWaU1HWQ==',
         cnch_vw_default ='your_vw';
DESCRIBE TABLE t;
```



|Parameter |Configuration description |
|---|---|
|Table Creation Description |The column names and types of the Hive table, as well as information like Partition By key and Cluster By key, will be automatically deduced and established during table creation. Columns are created as Nullable type by default, see the section below for column type mapping rules. |
|Engine Parameters (Engine) |* `thrift://hive_metastore:port`: Specifies the Hive Metastore service address, for example, using the BytePlus LAS, please refer to [LAS Connection Address Help Document](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80).<br><br>* `hive_database_name`, `hive_table_name`: Specify the database in Hive, for example, using the BytePlus LAS, you can log into the [LAS Console](https://console.volcengine.com/las/region:las+cn-beijing/next/metadata/data_directory?CatalogName=hive), select **Data Lake\>Metadata Management** from the left navigation bar, click on the associated catalog name to view and obtain the required database and table names. |
|Setting Parameters (SETTINGS) |* `endpoint`: The connection address of the external data source. For example, using the BytePlus LAS, refer to the [LAS Connection Address Help Document](https://www.volcengine.com/docs/6492/1264542#%E8%BF%9E%E6%8E%A5%E5%9C%B0%E5%9D%80) for obtaining methods.<br><br>* `region`: The service region of the external data source, leave blank if not provided by the service provider. For example, using BytePlus LAS, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for details.<br><br>* `ak_id/ak_secret`: A key with Hive access permission (including Hive Metastore and corresponding object storage), which you can obtain from the administrator. For example, using BytePlus LAS, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey) for the acquisition method.<br><br>* `cnch_vw_default`: Used to specify the virtual warehouse. You can view the available virtual warehouse list and copy the virtual warehouse ID on the **Virtual Warehouse** page of the ByteHouse console. If this parameter value is not configured, the default virtual warehouse configured in ByteHouse will be used. |


<span id="f42e439a"></span>
# Query external tables

The querying of Hive external tables is essentially the same as querying regular tables. For example,


* Catalog Method

   ```SQL
   select * from  las_catalog.db.table where xxx;
   ```
   

* General Method

   ```SQL
   select * from  t where xxx;
   ```
   


<span id="573ae2ea"></span>
## Query acceleration: Enable disk cache


1. Apply to enable the Disk Cache feature.

   ByteHouse provides you with disk caching capabilities, allowing part of the data to be cached on your local disk to enhance query efficiency. This feature is disabled by default. If you wish to use this feature, you can contact technical support to enable it.

2. After the feature is enabled, the default disk caching feature will be used when querying external table data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to turn off the disk cache for a particular query, you can set the SETTINGS parameter when creating an external table, <code>disk_cache_mode = 'SKIP_DISK_CACHE'</code>.   </div>
   

<span id="abe113c1"></span>
## Enable BSP mode

BSP mode enables task\-level fault tolerance and finer\-grained scheduling. When a query encounters an error, it can automatically retry the current task instead of retrying from the beginning, thus reducing the cost of retries. Additionally, when the memory needed for a query is immense, even exceeding a single machine's memory, parallelism can be increased to reduce the memory usage per unit of time.

You can enable BSP mode during a query by specifying the settings parameters. The settings parameters are described as follows:


|Parameter name |Type |Default |Description |
|---|---|---|---|
|bsp_mode |Bool |0 (off) |Set to 1 to enable BSP mode. Queries execute in stages when BSP mode is enabled. Shuffle joins connect the stages. Task\-level retries occur on failure. |
|distributed_max_parallel_size |UInt64 |equals to worker quantity |When a single query uses a large amount of memory, increasing this parameter can enhance the operator’s degree of parallelism, reduce the amount of data processed by each parallelism unit, and decrease the memory usage per unit time. It must be enabled in bsp_mode, then `distributed_max_parallel_size` value can exceed the number of workers. Suggestion is to set it as a multiple of the number of workers. |
|bsp_max_retry_num |UInt64 |3 |The maximum number of retry times for a task. ByteHouse supports setting the `bsp_max_retry_num` parameter starting from version 2.0.4. Different versions's default values are as follows:<br><br>In ByteHouse versions 2.0.4/2.1, retries are tracked at the query granularity, with a default of 5 retries. In ByteHouse version 2.2, retries are tracked at the segment granularity, with a default of 3 retries.<br><br>You can view the current ByteHouse version through the path **ByteHouse Console**\>**Tenant management**\>**Basic information**. |


Example:

```SQL
select * from  t SETTINGS bsp_mode = 1, distributed_max_parallel_size = 4;
```


<span id="fe74d80c"></span>
# Write to external table

The data writing operations for Hive external tables are essentially the same as those for regular tables. For example, writing data to a LAS external table after creating the LAS Catalog:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please confirm before writing to the LAS Formation table:</div>



* <div data-tips="true" data-tips-type="warning">Have LAS Formation access Permission</div>


* <div data-tips="true" data-tips-type="warning">Have TOS access Permission</div>


* <div data-tips="true" data-tips-type="warning">TOS has activated HNS (Hierarchical Bucket) <Function</div>



<div data-tips="true" data-tips-type="warning">Currently, CDW <strong>does not support the writing of TOS Buckets that have not activated HNS</strong>. For more about the introduction of TOS Buckets' HNS, please refer to <a href="https://www.volcengine.com/docs/6349/1278171">TOS Help Documentation</a>.</div>



* Catalog mode

   ```SQL
   insert into/overwrite las_catalog.db.table values (xxx);
   insert into/overwrite las_catalog.db.table select * from xxx settings enable_optimizer =1;
   ```
   

* General Methods

   ```SQL
   insert into/overwrite db.t values (xxx);
   ```
   


When writing data outward, ByteHouse also supports enabling BSP mode. For operational details, please refer to [Enable BSP mode](https://docs.byteplus.com/docs/bytehouse/hive-external-table#abe113c1).

<span id="884e7416"></span>
# Reference: Column type mapping


|Hive column <Type |CnchHive column <Type |description |
|---|---|---|
|INT/INTERGER |Nullable INT/INTERGER |None |
|BIGINT |Nullable BIGINT |None |
|TIMESTAMP |Nullable DateTime |None |
|STRING |Nullable String |None |
|VARCHAR |Nullable FixedString |Internal conversion to FixedString |
|CHAR |Nullable FixedString |Internal conversion to FixedString |
|DOUBLE |Nullable DOUBLE |None |
|FLOAT |Nullable FLOAT |None |
|DECIMAL |Nullable DECIMAL |None |
|MAP |Nullable Map |None |
|ARRAY |Nullable Array |None |

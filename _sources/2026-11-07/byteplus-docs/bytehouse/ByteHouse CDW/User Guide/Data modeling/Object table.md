---
title: "Object table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/object-table"
---

ByteHouse Cloud Data Warehouse supports managing metadata of unstructured data in object storage through object tables, which is suitable for multimodal data management scenarios. This tutorial describes how to manage object tables using SQL statements and the console's visual interface.

<span id="a05b2c3f"></span>
# Background information

<span id="1ee202a6"></span>
## Feature overview

An object table is a special table type in ByteHouse Cloud Data Warehouse, used to obtain metadata of unstructured data (such as text, images, and more) in object storage (without storing the original data). The object table reads metadata from files in the specified path of object storage, generates indexes, and maps them to a fixed table structure. The fields in the table correspond one\-to\-one with the files in object storage.

Currently, ByteHouse only supports reading object metadata from BytePlus Object Storage TOS, typically using a fixed table structure that includes the following contents:


|**Column name** |Type |**Description** |
|---|---|---|
|key |String |The relative storage path name of the data object under the specified path in object storage. |
|url |String |The complete storage path name of the data object in object storage. |
|size |UInt64 |The size of the data object, in bytes. |
|last_modified_time |DateTime |The last modification time of the data object on TOS. |
|content_type |String |Content type, provided by the application or identified by the file extension, such as text/plain. The extension is identified using Golang's native `mime.TypeByExtension()`. |
|storage_class |String |The storage class of the data object on TOS. For the specific supported storage classes, see [TOS supported storage classes](https://docs.byteplus.com/en/docs/tos/docs-storage-type).<br><br>The possible values for the storage class of a data object are as follows:<br><br><br>* STANDARD: Standard storage.<br><br>* IA: Infrequent access storage.<br><br>* INTELLIGENT_TIERING: Intelligent tiering storage.<br><br>* ARCHIVE_FR: Archive flashback storage.<br><br>* ARCHIVE: Archive storage.<br><br>* COLD_ARCHIVE: Cold archive storage.<br><br>* DEEP_COLD_ARCHIVE: Deep cold archive storage. |
|crc64 |UInt64 |The 64\-bit CRC value of the object, calculated according to the ECMA\-182 standard. |
|etag |String |The etag is an entity tag created when each object is generated, used to identify whether the content of an object has changed between two updates. |
|metadata |Map(String, String) |Metadata of the TOS object, which can be extended. |


**Table creation configuration and synchronization logic**


* **Table creation** **configuration**: When creating a table, you must specify the target path in object storage and configure the refresh policy. After creating the table, you can also modify the table properties to change the refresh policy and object storage\-related information. For details, see [Modify the object table](https://docs.byteplus.com/docs/bytehouse/82792#5cd356b1).

* **Synchronization logic**: ByteHouse currently supports asynchronous refresh and synchronous (manual) refresh:

   * Asynchronous refresh pulls the latest full metadata from the target path in object storage according to the scheduled rules you set when creating the table. ByteHouse also supports manually triggering a temporary refresh.

   * Synchronous (manual) refresh must be triggered manually using the REFRESH TABLE statement or the console button.

   * For refresh operations, see the following documentation:

      * REFRESH TABLE statement: [Refresh object tables](https://docs.byteplus.com/docs/bytehouse/82792#29495d3e)

      * Manual trigger via console button: [Manually refresh object tables](https://docs.byteplus.com/docs/bytehouse/82792#2344a26e)


**Supported features**

ByteHouse supports convenient management of object tables through SQL statements or the console's visual interface. The currently supported features are described as follows:


|Functionality |SQL statement |Console visual operation |
|---|---|---|
|Create object table |✅ |❌<br><br>(Currently, only SQL statements executed in the console SQL worksheet are supported for creating object tables.) |
|View object table<br><br>(Table structure and CREATE TABLE DDL) |✅ |✅ |
|Refresh object table |✅ |✅ |
|Query object table |✅ |❌<br><br>(Currently, only SQL statements executed in the console SQL worksheet are supported for querying object tables.) |
|Modify object table properties |✅ |❌<br><br>(Currently, only SQL statements executed in the console SQL worksheet are supported for modifying object table properties.) |
|Delete object table |✅ |❌<br><br>(Currently, only SQL statements executed in the console SQL worksheet are supported for deleting object tables.) |


<span id="57d31e40"></span>
## Application scenarios

Object tables are suitable for multimodal data management scenarios (such as unstructured data like images and text in AI applications). They can improve data management efficiency, enhance business adaptation flexibility, and ensure data storage security.

<span id="3c3d9e48"></span>
## Billing


* Object tables in ByteHouse only incur computation fees and metadata storage fees, following ByteHouse's computation resource billing rules.

* When using the object table feature, the data in the object table **will not** be duplicated in ByteHouse, and no storage fees will be incurred. For storage fees, please refer to the billing rules of the object table data source's storage side.

* When accessing the object table data source using ByteHouse object tables, the object table data source may incur computation, access, data transfer, and other fees. The specific billing method depends on the object table data source; please refer to the relevant product documentation.


<span id="5adcfb4b"></span>
# Usage restrictions


* This feature is in Beta. Please submit a ticket or contact the ByteHouse team to obtain allowlist access.

* This feature requires ByteHouse engine version 2.3.3 or above. Before use, confirm that your engine version meets this requirement. You can check the current engine version on the ByteHouse console's **Tenant management** \> **Basic information** page. If your engine version does not meet the requirement, you can submit a ticket and contact the ByteHouse team to upgrade the engine.


<span id="03ef4567"></span>
# Prerequisites

Before using object tables, obtain the relevant permissions and connection information for BytePlus Object Storage Service (TOS).


|Subitems |Required permissions and connection information |
|---|---|
|Permissions |Grant read permissions for the target TOS data object to the account you are using. |
|Connection information |* Access key with TOS access permissions: Access Key ID (AK) / Secret Access Key (SK). For details on how to obtain these, see [Access Key (key) management](https://www.volcengine.com/docs/6291/65568).<br><br>* TOS region and access domain name (endpoint): You can log in to the TOS console and view the required endpoint via **Bucket list** \> **Bucket name** \> **Overview** \> **Access domain name** path. As shown in the figure below, the endpoint is `tos-s3-cn-beijing.volces.com`. For a list of commonly used endpoints, see [Region and access domain name (Endpoint)](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/215701f3ecaa4f4ca9476dd8e5c7b001~tplv-goo7wpa0wc-image.image) </span><br><br>* Storage path information for the target data file. |


<span id="59b9f0dd"></span>
# Create and use object tables

This section describes how to create, refresh, and modify object tables using SQL statements.

<span id="a8d6db27"></span>
## Create object tables

When creating an object table, you do not need to specify the table schema. This is because object tables can read metadata from object storage in a fixed pattern and automatically generate the table schema. For more information, see [Feature overview](https://docs.byteplus.com/docs/bytehouse/82792#1ee202a6).

After creating the table, you can view the schema of a specific object table using SQL statements. For details, see [View table structure](https://docs.byteplus.com/docs/bytehouse/82792#1c8733d5). You can also view it in the ByteHouse console. For details, see [View object tables](https://docs.byteplus.com/docs/bytehouse/82792#c8effc41).

<span id="4e1a0a34"></span>
### Syntax

```SQL
CREATE OBJECT TABLE [IF NOT EXISTS] [db.]ob_table_name 
ENGINE = CnchMergeTree
REFRESH = [ASYNC [EVERY (INTERVAL refresh_interval) ] | MANUAL]
PROPERTIES 
    [type = 'TOS'],
    region = 'region',
    endpoint = 'end_point',
    access_key_id = 'access_key_id',
    secret_access_key = 'secret_access_key',
    locations = ['bucket_name/[folder_name]/*', ...]
[COMMENT comment]
```



|Parameters |Required |Configuration description |
|---|---|---|
|CREATE OBJECT TABLE |Yes |Used to create an **object table** in ByteHouse, which links to data in the object storage data service. It supports mapping file data in object storage through the table structure, allowing direct queries without manual import. |
|IF NOT EXISTS |No |Used to avoid errors from duplicate creation. If an object table with the specified name already exists, the creation operation will not be performed and no error will be reported. |
|[db.]<ob_table_name\> |Yes |Specify the database where the object table resides and customize the object table name. If you have executed `USE db` before running the creation statement, or specified the database on the SQL worksheet page in the ByteHouse cloud data warehouse console, you may omit the database name here. |
|[COMMENT] |No |Table comment, used to describe the purpose of the object table. |
|ENGINE |Yes |Set to CnchMergeTree. |
|REFRESH |Yes |Used to configure the synchronization refresh policy for the object table. This parameter determines how the object storage data mapped in the table will be updated after the table is created. Supports the following parameter values:<br><br><br>* ASYNC: Asynchronous refresh, periodically synchronizes object storage data at the interval you specify. `EVERY (INTERVAL refresh_interval)` is used to specify the refresh interval. The interval can be set to SECOND (seconds), MINUTE (minutes), HOUR (hours), DAY (days), WEEK (weeks), or MONTH (months). For example: `REFRESH ASYNC EVERY (INTERVAL 10 SECOND)`. It is recommended to set it to 30 to 60 minutes.<br><br>* MANUAL: Synchronous refresh mode. You need to manually execute the REFRESH TABLE command or perform a manual refresh in the ByteHouse Cloud Data Warehouse console. For detailed instructions, see<br><br>   * REFRESH TABLE command: [Refresh object tables](https://docs.byteplus.com/docs/bytehouse/82792#29495d3e).<br><br>   * Manual refresh in the console: [Manually refresh object tables](https://docs.byteplus.com/docs/bytehouse/82792#2344a26e). |
|PROPERTIES |Yes |Used to set the connection information, data path and other parameters of the object storage service. All the parameters are string type and need to be quoted with single quotes.<br><br><br>* type: Set the type of object storage service you are using. Currently, only TOS is supported. In the syntax, `[]` indicates that the parameter is optional. When actually using it, you do not need to add `[]`.<br><br>* region: Enter the region where your object storage service is located. For example, `ap-southeast-1`. If you are using BytePlus Object Storage TOS, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint) for region information.<br><br>* endpoint: The access endpoint of the object storage, used to establish a network connection with the object storage. If you are using BytePlus Object Storage TOS, you can log in to the TOS console and go to [Bucket List](https://www.volcengine.com/docs/6349/107356?lang=zh) \> Bucket Name \> Overview \> Access Domain Name to view the required endpoint. As shown in the figure below, the endpoint is `tos-ap-southeast-1.bytepluses.com`. For a list of common endpoints, see [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint).<br><br>* access_key_id: The access key ID (AK) for the object storage, used for authentication. It must have read permissions for object storage. If you are using BytePlus Object Storage TOS, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for how to obtain it.<br><br>* secret_access_key: The access key secret (SK) for the object storage. If you are using Volcano Engine Object Storage TOS, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for how to obtain it.<br><br>* locations: Set as the storage path of the data files in the object storage. The path format requirements are as follows:<br><br>   * An asterisk can appear within or at the end of the object name.<br><br>   * Multiple asterisks are not supported. For example, the path `bucket_name/folder-*/temp/*.csv` is invalid.<br><br>   * Using an asterisk in the bucket name is not supported.<br><br>      Examples:<br><br>   * To read all files in the specified path whose file names contain "sample": `bucket_name/folder_name/sample*`<br><br>   * To read all files in the specified path with the PDF format: `bucket_name/folder_name/*.pdf`<br><br>   * To read all files in the specified path whose names contain "sample" and are in JPG format: `bucket_name/folder_name/sample*.jpg` |


The following examples show how to create object tables in ByteHouse Cloud Data Warehouse, covering typical scenarios such as different file path matching and data refresh modes (manual or automatic). Before executing the example statements, replace the placeholders in the examples (such as region, access endpoint, access key, bucket name, file path, and more) with your actual object storage configuration information.

<span id="98c74476"></span>
### Example 1: Locations specifies only the bucket

When `locations` specifies only the object storage bucket, the created object table will traverse all subdirectories within the bucket.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_1 
ENGINE = CnchMergeTree
REFRESH ASYNC EVERY (INTERVAL 10 SECOND) 
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket';
```


<span id="18196f2a"></span>
### Example 2: Locations uses wildcards

When `locations` specifies the object storage bucket and uses wildcards, the created object table will traverse all subdirectories within the bucket, which has the same effect as in the previous example.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_2 
ENGINE = CnchMergeTree
REFRESH ASYNC EVERY (INTERVAL 10 SECOND) 
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/*';
```


<span id="9591ceb6"></span>
### Example 3: Locations specifies path and file format

When `locations` precisely specifies a subdirectory and filters file formats by suffix, the object table reads only files in that directory that match the specified format.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_3 
ENGINE = CnchMergeTree
REFRESH ASYNC EVERY (INTERVAL 10 SECOND) 
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/test/*.pdf';
```


<span id="b5488ba7"></span>
### Example 4: Manual refresh

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_4
ENGINE = CnchMergeTree
REFRESH MANUAL
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/test/*.pdf';
```


<span id="65cd804f"></span>
### Example 5: Specify multiple folders

When `locations` configures multiple paths under the same bucket, the object table will traverse all specified paths and filter files that match the format. This is suitable for reading the same type of data distributed across multiple directories.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_5 
ENGINE = CnchMergeTree
REFRESH ASYNC EVERY (INTERVAL 10 SECOND) 
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/test1/*,bh-demo-bucket/test2/*.pdf';
```


<span id="a4649f53"></span>
## View object tables

The operation for viewing object tables is the same as for regular tables.

<span id="1c8733d5"></span>
### View table structure

**Syntax**

```SQL
DESCRIBE TABLE [db.]ob_table_name 
```


**Example**

```SQL
DESCRIBE TABLE test_ob.ob_demo_1 
```


<span id="ba8770d7"></span>
### View table creation DDL information

**Syntax**

```SQL
SHOW CREATE TABLE [db.]ob_table_name 
```


**Example**

```SQL
SHOW CREATE TABLE test_ob.ob_demo_1 
```


<span id="29495d3e"></span>
## Refresh object tables

After creating the table, you can also trigger a refresh operation for the object table using the `REFRESH` command, which supports both synchronous and asynchronous refresh. You can also manually perform a refresh through the ByteHouse Cloud Data Warehouse console. For details, see [Manually refresh object tables](https://docs.byteplus.com/docs/bytehouse/82792#2344a26e).

The `REFRESH` policy configured during table creation defines the **default data synchronization rules** for the object table. After creating the table, you can manually trigger a refresh operation as needed using the `REFRESH OBJECT TABLE` command. This command supports synchronous (`SYNC`) and asynchronous (`ASYNC`) execution modes to meet refresh requirements for different scenarios.

<span id="3fb726c0"></span>
### Syntax

```SQL
REFRESH OBJECT TABLE [db.]ob_table_name [SYNC | ASYNC]; 
```



|Parameters |Required |Configuration description |
|---|---|---|
|REFRESH OBJECT TABLE |Yes |Refresh the object table. |
|[db.]ob_table_name |Yes |The full name of the object table to be refreshed, including the database and table name. If you execute `USE db` before running the creation statement, or specify the database on the SQL worksheet page in the ByteHouse console, you may omit the database name here. |
|[SYNC |ASYNC] |Choose one<br><br><br>* SYNC: Executes the refresh synchronously, blocking the current session until the refresh task is completed and the result is returned. You can query the latest data immediately after completion.<br><br>* ASYNC: Executes the refresh asynchronously, submitting the refresh task to the background for execution. The task identifier is returned immediately, and the current session is not blocked. Data synchronization takes effect after the task is completed. |


<span id="9e47d4f0"></span>
### Configure asynchronous refresh during table creation

In the following example, after creating the table, the system immediately starts the "automatic asynchronous refresh task every 10 seconds." You can also manually trigger a refresh using commands.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_1 
ENGINE = CnchMergeTree
REFRESH ASYNC EVERY (INTERVAL 10 SECOND) 
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/test1/*';
```


To manually trigger a refresh task, execute the following commands:


* Manually trigger an asynchronous refresh task

   ```SQL
   REFRESH OBJECT TABLE test_ob.ob_demo_1 ASYNC 
   ```
   

* Manually trigger a synchronous refresh task

   ```SQL
   REFRESH OBJECT TABLE test_ob.ob_demo_1 SYNC 
   ```
   


<span id="0f63c194"></span>
### Example 2: Configure synchronous refresh when creating a table

In the following example, a synchronous refresh policy is configured during table creation. The system does not perform automatic refresh actions; data synchronization can only be triggered using the `REFRESH OBJECT TABLE` command.

```SQL
CREATE OBJECT TABLE test_ob.ob_demo_2 
ENGINE = CnchMergeTree
REFRESH MANUAL
PROPERTIES
   region = 'your_region',
   endpoint = 'https://tos-your-region.volces.com',
   access_key_id = 'your_access_key_id',
   secret_access_key = 'your_secret_access_key',
   locations = 'bh-demo-bucket/test1/*';
```


After creating the table, there are no automatic refresh actions, and the first query of the object table returns no data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ebeeab677814a61a149b1dbee22a71d~tplv-goo7wpa0wc-image.image) </span>

At this point, you can read data by manually executing the refresh command.


* Manually trigger an asynchronous refresh task

   ```SQL
   REFRESH OBJECT TABLE test_ob.ob_demo_2 ASYNC 
   ```
   

* Trigger a synchronous refresh task

   ```SQL
   REFRESH OBJECT TABLE test_ob.ob_demo_2 SYNC 
   ```
   


After refreshing, query the object table again. At this time, the table contains data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f451f47e3f3426a8e806f7a874b3a0e~tplv-goo7wpa0wc-image.image) </span>

<span id="190cfa6a"></span>
## Query the object table

The query operation for object tables is the same as for regular tables.

```SQL
SELECT * FROM [db.]ob_table_name WHERE xxx; 
```


<span id="5cd356b1"></span>
## Modify the object table

After creating an object table, ByteHouse supports adjusting the core configuration of the object table using the `ALTER TABLE` statement, including the **refresh policy** (REFRESH) and **object storage\-related properties** (PROPERTY). This allows you to adapt to changes in business scenarios, such as adjusting data refresh frequency, rotating object storage keys, or migrating data paths, without rebuilding the table.

<span id="8fcabb96"></span>
### Syntax

```SQL
ALTER TABLE [db.]ob_table_name MODIFY REFRESH|PROPERTY expr 
```



|Parameter |Required |Configuration description |
|---|---|---|
|[db.]ob_table_name |Yes |The full name of the object table to be refreshed, including the database and table name. If you execute `USE db` before running the creation statement, or specify the database on the SQL worksheet page in the ByteHouse console, you may omit the database name here. |
|MODIFY REFRESH expr |Choose one |Specifies the refresh policy for modifying the object table, used to replace the REFRESH rule configured during table creation. |
|MODIFY PROPERTY expr |Choose one |Specifies the object storage properties associated with the object table to be modified, such as region, access key, and data path. |


<span id="22461120"></span>
### Example 1: Change the refresh policy from manual refresh to asynchronous refresh

```SQL
ALTER TABLE test_ob.ob_demo_1 MODIFY REFRESH ASYNC EVERY(INTERVAL 10 second); 
```


<span id="c65c4a18"></span>
### Example 2: Change the refresh policy from asynchronous refresh to manual refresh

```SQL
ALTER TABLE test_ob.ob_demo_2 MODIFY REFRESH MANUAL;
```


<span id="b4acc320"></span>
### Example 3: Modify table properties

```SQL
ALTER TABLE test_ob.ob_demo_2 MODIFY PROPERTY region = 'your_new_region',
   endpoint = 'https://tos-your-new-region.volces.com',
   access_key_id = 'your_new_access_key_id',
   secret_access_key = 'your_new_secret_access_key',
   locations = 'bh-demo-bucket-new/*';
```


<span id="4385c8d3"></span>
## Delete the object table

The deletion of object tables is the same as the operation for regular tables.

```SQL
DROP TABLE [db.]ob_table_name; 
```


<span id="fc57feb5"></span>
# Visual management of object tables

You can manage object tables in the ByteHouse console. The console supports executing object table creation and usage statements via SQL worksheets, viewing created object tables and table creation DDL on the database page, and manually executing refresh operations on object tables.

<span id="109c88c8"></span>
## Create and use object tables via SQL worksheets

In the ByteHouse cloud data warehouse console, you can use the SQL statements from the above sections in **Data Query** to create and use object tables. For more details on using SQL worksheets, see [SQL Worksheet](https://docs.byteplus.com/docs/bytehouse/docs-query-editor-and-worksheet).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9f0a29d2a514385b53b679bb7bac079~tplv-goo7wpa0wc-image.image) </span>

<span id="c8effc41"></span>
## **View object tables**

After the object table is created, click **Database** at the top. Find the target database in the database list and click its name. On the database details page, click the **Object table** tab to view the object tables in the current database.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/810c84eb4cd64a5a887a1f2a6d131df8~tplv-goo7wpa0wc-image.image) </span>

You can click the **object table name** to go to the object table details page and view the columns and synchronization tasks of the object table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f36c7712fed4e628c9400f51a4dedc7~tplv-goo7wpa0wc-image.image) </span>

<span id="c6bc1b87"></span>
### **View the CREATE TABLE DDL of the object table**

On the object table details page, click the **DDL** button to view the CREATE TABLE DDL.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69655a6d651d4e019a9d59f0d7dc1373~tplv-goo7wpa0wc-image.image) </span>

<span id="2344a26e"></span>
### **Manually refresh object tables**

On the object table details page, click **Async tasks** and then **Manually Start**. The system will automatically refresh the object table.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The first refresh may be delayed. Please wait 1–2 minutes and refresh the page again to check the task status.</div>

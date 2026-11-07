---
title: "Batch import"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/batch-import"
---

Batch import is suitable for scenarios where you want to load pre\-prepared data into ByteHouse in a single operation. Currently, it supports data sources such as S3\-compatible object storage, Hive, ClickHouse, and others. This tutorial introduces the batch import feature and explains how to import data from different data sources into ByteHouse.

<span id="c5bc8d09"></span>
# Function overview

ByteHouse supports batch import using external compute engines. Compared with inserting data using `INSERT` via the engine, the batch import feature has the following characteristics:


* Supports multi\-threaded parallel import, enabling faster import of large files.

* Part files are written directly during import, without passing through the engine. During import, Spark and Flink resources are scheduled and external computing resources are used, resulting in less impact on query performance. For files with partitions, after the import task generates a Part, the Part name will include partition information.

* After completing a full Part file and mounting it, the issue of having too many Parts and slow merging caused by `INSERT` will not occur.


After creating a batch import task, ByteHouse supports setting the task to execute immediately or creating a scheduled import task. You can edit, clone, or delete tasks, and view task status and details. If a conflict occurs during the execution of an import task, ByteHouse allows you to manually resolve the conflict and restore the task.

<span id="0a22e00b"></span>
## Loading mode

When using the ByteHouse batch import feature, the minimum import unit is a complete partition, rather than a row. A partition is a logical unit within a table in ByteHouse, separated based on the partition key. If duplicate partition field values occur in two consecutive imports, a partition conflict will result. For example, the first import creates the `'2022-02-02'` partition. In the second import, some rows also have the partition key value `'2022-02-02'`, and a new `'2022-02-02'` partition is generated during the import process, which results in a conflict.

To handle potential conflicts during import, ByteHouse provides four loading modes: incremental merge, partition overwrite, post\-processing, and ignore conflicts. You can set the **conflict resolution method** parameter when creating an import task:


*  **(Recommended)**  **Incremental merge**: Newly imported partition data is merged into existing partitions.

* **Overwrite partition**: A new partition overwrites the old partition with the same name.

* **Follow\-up processing**: Each time you import, if a partition conflict occurs, the current import task will enter a pending conflict resolution state. You must manually select either full load or incremental load.

* **Ignore conflicts**: If the new partition has the same name as the existing partition, it will not be imported.


<span id="0cef41e4"></span>
## Supported data sources

ByteHouse Enterprise supports the following data sources:


* S3\-compatible object storage: Supports importing file data from standard object storage services, including BytePlus Torch Object Storage Service (TOS), Alibaba Cloud Object Storage Service (OSS), AWS S3, self\-hosted MinIO, and others. Supported file types include CSV, JSON, and Parquet.

* Hive: Supports importing data from Hive tables.

* ClickHouse: Supports importing data from ClickHouse or ByteHouse tables.


<span id="cefd354d"></span>
# Prerequisites

Before adding a data source, ensure that you have the following necessary permissions and information:


* Please ensure that the data source and the ByteHouse cluster can communicate with each other over the network.

* Please ensure that the access credentials for the data source (for example, the object storage Access Key/Secret Key) have permissions for the relevant path and database tables.


<span id="c3536b2e"></span>
# Preparation

Create the target database and table in ByteHouse Enterprise. For instructions on the creation process, see [Create a new database/table](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table). Support for target table engines varies depending on the data source. Details are as follows:


|Data source types |Supported target table engines |
|---|---|
|Object storage |HaMergeTree/HaUniqueMergeTree |
|Hive ||
|ClickHouse |HaMergeTree/HaUniqueMergeTree/MergeTree/ReplacingMergeTree/ReplicatedMergeTree |


<span id="87f64d56"></span>
# Create a data source

Creating a data source is intended to establish a connection between ByteHouse and external data storage systems, such as object storage, Hive, and more, in order to provide the ability to access data sources for subsequent import tasks.


1. Log in to the ByteHouse Enterprise console. Click **Data import** at the top. In the upper right corner, switch to the target cluster. Click **Data source** to navigate to the new data source page, and then click **add a New Source \>** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad9ec6f230b6466d91751425faab776d~tplv-goo7wpa0wc-image.image) </span>

2. In the interface for creating a new data source on the right, configure the data source connection information. Different types of data sources require different configuration parameters. For details, see the following parameter descriptions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3632c5da69ca47ec90e5e8799877a0bf~tplv-goo7wpa0wc-image.image) </span>

   * **Object storage**

      
      |Parameter |Configuration instructions |
      |---|---|
      |Source type |Select S3. |
      |Source name |Custom source name. |
      |Endpoint |The access domain name configured for the data source.<br><br>If you are using TOS as your object storage, you can refer to the S3 Endpoint column in the TOS documentation for relevant information. For details, see [Region and endpoint of TOS](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |
      |Region |Set the region to where the data source is located.<br><br>If you are using TOS as your object storage, you can refer to the Region ID column in the TOS documentation for relevant information. For details, see [Region and endpoint of TOS](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |
      |Access key |Set it to the Access Key (AK) of the data source.<br><br>If you are using TOS as your object storage, please refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for information on how to obtain your Access Key. |
      |Key |Set it to the Secret Key (SK) of the data source.<br><br>If you are using TOS as your object storage, please refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for how to obtain it. |
      |The source object storage is MinIO |If your data source is MinIO, please check this option. |
      

   * **ClickHouse**

      
      |Parameter |Configuration instructions |
      |---|---|
      |Source type |Set it as ClickHouse. |
      |Source name |Customize your source name. |
      |ClickHouse host |Configure the host address for the ClickHouse service you use. If there are multiple host addresses, separate them with a comma (`,`). Example: `192.168.0.1:8123, 192.168.2.234:8123`. |
      |Clickhouse username |The username configured for the ClickHouse service you use. |
      |Clickhouse password |Password configured for your ClickHouse service. |
      

   * **Hive**

      
      |Parameter items |Configuration instructions |
      |---|---|
      |Source type |Set it to Hive. |
      |Source name |Customize your data source name. |
      |Hive Metastore Uri |The access address for the Hive Metastore service, used by ByteHouse to obtain metadata for Hive tables. Example: `thrift:// 192.168.0.1:9083`. |
      |Contents of hdfs\-site.xml |Configure the content as the actual `hdfs-site.xml` file used in the Hive cluster. This allows ByteHouse to access the data files of Hive tables that are actually stored on HDFS. |
      

3. After configuration is complete, click **OK** to finish creating the data source.


<span id="116005dc"></span>
# Create import tasks


1. In the **Data source** module, click **Target data source**. Then, on the right, click **New import job**. This will take you to the new task creation interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8f19c80063840a394666c37f7e8d7da~tplv-goo7wpa0wc-image.image) </span>

2. Enter general information for the import task, and customize the task name and description. Note that the task name cannot be the same as any other task name.

   Verify that the cluster time zone is consistent with the time zone of the imported data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a7d7821dbf1441187c1a78460c20669~tplv-goo7wpa0wc-image.image) </span>

   The cluster time zone must be consistent with the time zone of the imported data; otherwise, data errors will occur in time\-related columns. To adjust the time zone, click **Update timezone**. The system will navigate to the cluster time zone configuration page, where you can select your time zone.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1571953baa9a44baa6bdd09931afb675~tplv-goo7wpa0wc-image.image) </span>

3. Select and configure data sources. The configuration parameters required for different data sources vary. You can refer to the parameter documentation for each data source when configuring.

   * **Object storage**

      Set the source type to S3, select the target data source you created, and configure the detailed information for the data source, including the bucket name, the path to the source file, the format, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adc45a61718749b39ea7feb9e40b0423~tplv-goo7wpa0wc-image.image) </span>

      If your data source file is in CSV or JSON format, you need to configure the corresponding format parameters for the source file.

      
      |Format |Configuration options |Configuration instructions |
      |---|---|---|
      |CSV |Field delimiters |Set the delimiter for different fields in the data source file. |
      ||Encoding |Set the encoding format for the data source file. |
      ||Quotation character |Set the symbol used to enclose special characters in the data source file. |
      ||Escape character |Disable the symbol originally used as the quote character in the data source file. |
      ||Skip the first line |Set whether to ignore the first line of the data source file. |
      ||The first row contains column headers |Set whether the data source file contains a header row.<br><br><br>* No header: ByteHouse will use "_c0" and "_c1" as source column names to map the schema to the target table.<br><br>* With a header: ByteHouse will separate the header to map the schema to the target table. |
      ||One record spanning multiple lines |Specify whether to allow a record to contain multiple lines. |
      ||Ignore leading and trailing spaces |Set whether to ignore leading and trailing spaces in each field value of the source file. |
      |JSON |One record spanning multiple lines |Set whether a record can contain multiple rows. |
      ||Allow comments |Configure whether comments can be added to files to support compatibility with situations where JSON files contain comments. |
      

   * **ClickHouse**

      Select the data source type as ClickHouse, set **Data source** to the target data source you created, and select the ClickHouse database to be imported.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00ac874c2a7644bc96dfb1d79ba5d8d0~tplv-goo7wpa0wc-image.image) </span>

   * **Hive**

      Select Hive as the data source type, and choose the target data source that you created.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be6bedc3c25b4a348120034cd5d22877~tplv-goo7wpa0wc-image.image) </span>

4. Select the target database and table for import.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76626002d9f6473aab16325643aebf57~tplv-goo7wpa0wc-image.image) </span>

5. Define a schema mapping. After you set the data source and target table, the system automatically populates the Schema mapping table and generates the mapping between the data source and the target table. If the generated Schema does not match the actual situation, you can also adjust the mapping relationship using the following methods.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b37b07f87ad2466da34cdc6691700b97~tplv-goo7wpa0wc-image.image) </span>

   * **Data mapping**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only object storage supports adjusting mapping relationships through data mapping.      </div>
      

      1. Click **Data source**, then select a schema description file from the drop\-down list. ByteHouse automatically reads files from the object storage path you set. As needed, you can select files to use as schema sample files.

      2. Choose **Mapping Method**. Both **Override** and **Incremental** are supported.

      3. After completing the setup, click **OK**. ByteHouse will automatically generate a new data mapping.

   * **Parse JSON**

      1. Click **JSON**, and enter the schema mapping.

      2. Select **Mapping Method**. Both **Override** and **Incremental** are supported.

      3. After completing the setup, click **Parse**. ByteHouse will automatically generate a new data mapping.

   * **Parse SQL**

      1. Click **SQL**, and enter the schema mapping relationship.

      2. Choose **Mapping Method**. Both **Override** and **Incremental** are supported.

      3. After setup is complete, click **Parse**. ByteHouse will automatically generate new data mappings.

   * **Manual adjustment**

      In the mapping table, you can manually adjust the mapping between source and target column names and customize expressions.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, batch import does not support using expressions (expression) for simple data conversion. You must ensure that the data formats of the source and target data are consistent.   </div>
   

6. Select a partition conflict resolution method to handle data conflicts caused by duplicate partition field values during import.

   * (**Recommended**) **Incremental merge**: Newly imported partition data is merged into old partitions.

   * **Partition overwrite**: The new partition overwrites the old partition with the same name.

   * **Ignore conflicts**: If the new partition has the same name as the old partition, it will not be imported.

   * **Follow\-up processing**: If a partition conflict occurs during import, the current task status changes to "Conflicted" and enters the pending conflict resolution state. You can manually choose to keep either the new partition or the old partition based on the number of rows in each. After processing is complete, the system will continue to perform the import task. Pausing the current task does not affect other tasks.

7. Select **Submit** to complete the creation.


<span id="d2cb5d67"></span>
# Start importing data

After creation is complete, ByteHouse will redirect to the **Start Job** interface, where you can configure tasks and start importing. Both immediate execution and scheduled tasks are supported. Scheduled tasks can be configured as recurring or one\-time tasks, and you can set the execution time as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15dabe306acd4529a060c86eb418e167~tplv-goo7wpa0wc-image.image) </span>

You can also go to the **Data Import** tab, click **the target data source name**, click **the import task name**, enter the task details page, click **Start**, and enter the **Start Job** interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bdc3db1bef3c4d8d858000b0c0a93feb~tplv-goo7wpa0wc-image.image) </span>

<span id="f52a0109"></span>
## Execute immediately


1. On the **Start Job** interface, click **Run Immediately** and select the file to import. Different data sources require different configuration parameters:

   * **S3 protocol object storage**: Select the file to be imported. Both selecting files and entering an expression are supported.

      
      |Selection method |Configuration instructions |
      |---|---|
      |Document |Select a file from the drop\-down list. This method supports selecting up to 10 files, with a maximum size of 2 GB per file. |
      |Expression |Select files using expressions. This is suitable for scenarios that require batch file selection. The following wildcards can be used:<br><br><br>* ? represents placeholders<br><br>* indicates all<br><br>* You can enter 0\-9, a\-z, and more in [ ].<br><br><br>Example:<br><br><br>* `data?.json`: Filters files with the prefix `data`, the suffix `.json`, and only one character between them.<br><br>* `data[0-100].json`: Import files named from`data0.json` to `data100.json`. |
      

   * **ClickHouse**: You need to enter the SELECT statement for the data to be imported.

   * **Hive**: You need to set the data source parallelism and enter the name of the Hive table to be imported. By default, the degree of parallelism is set to 1. Increasing the degree of parallelism improves import speed.

2. Click **Run** to have ByteHouse automatically start executing the import task.


<span id="8301efdc"></span>
## Create a scheduled task

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only importing from object storage is supported via scheduled tasks.</div>



1. In the **Start Job** interface, click **Create cron task.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d78e9c6d976e4728af505826ab7ced00~tplv-goo7wpa0wc-image.image) </span>

2. Select a file. When using expressions to match files for import, you can use the following wildcards:

   * ? indicates a placeholder;

   * represents all;

   * You can enter 0\-9, a\-z, and many other characters in [ ].

      Example entry

   * `data?.json`: Filter files with the prefix `data`, the suffix `.json`, and with exactly one character different in the middle.

   * `data[0-100].json`: Files to be imported are named from `data0.json` to `data100.json`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b349ca4c1f1640508e05aeffb14320b5~tplv-goo7wpa0wc-image.image) </span>

3. Define scheduled tasks. Enter the task name and select the execution type. You can set it as periodic or one\-time, and specify the execution time.

   It is recommended to monitor the execution status of periodic tasks at their scheduled execution times. If any conflicts or task execution failures occur, promptly handle exceptions to prevent data loss and business impact. For information on handling task failures or conflicts, please refer to [Task tracking](https://docs.byteplus.com/docs/bytehouse/batch-import#36f60c39).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1067f91167564ec6a2825c852144d5e7~tplv-goo7wpa0wc-image.image) </span>

4. Click **Create**, and ByteHouse will execute the import task at the time you set.


<span id="36f60c39"></span>
# Task tracking

After starting a task, you can view the currently executing import task on the task details page, including information such as task status, execution time, data source details, target data table, and import information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6926d458f758470890755a16fa6ba525~tplv-goo7wpa0wc-image.image) </span>


* If the execution status is "**Stopped**" (gray icon), it indicates that the current task has been completed successfully.

* If the execution status is **Failed** (red cross icon), you can click the execution ID, hover the mouse over the **failure icon**, and click **View more** to check the error information and adjust the configuration accordingly.

* If the execution status is "**Conflicted**" (red exclamation mark), you can resolve the conflict by following the conflict resolution steps. For operation details, see [Resolve conflicts](https://docs.byteplus.com/docs/bytehouse/batch-import#83e4f450).


<span id="83e4f450"></span>
## Resolve conflicts


1. On the task details page, click **Resolve**, view partition conflict details, and resolve conflicts.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa60853521d44266bc22d920734cef41~tplv-goo7wpa0wc-image.image) </span>

2. Select a conflict resolution method as needed, and click **Replace and Resume Job**.

   * **Select partitions**: It means retaining the new partition and discarding all data from the old partition.

   * **Do not select partitions**: The old partition is retained, and the newly imported partition is discarded.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6545cd0b8bea4593ad9730f36f8397d9~tplv-goo7wpa0wc-image.image) </span>


After conflict resolution is complete, the import task will be completed immediately and enter the **Stopped** status, which means the import was successful.

<span id="2c4532d8"></span>
# Manage import tasks

<span id="21090107"></span>
## Edit a task

After a task is created, you can edit the task to adjust its configuration. Currently, you can modify the task name, description, target table schema configuration, and conflict resolution method.


1. On the **Data source** interface, click the **target data source**, then click the **task name** to enter the task details page.

2. Click the `...` button in the upper right corner Click the **Edit Task** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c001f051e1a442f6938779befdf3051c~tplv-goo7wpa0wc-image.image) </span>

3. In the task editing interface, you can adjust the task configuration as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85135ea6ff9a4daba2e28e832cb3f85f~tplv-goo7wpa0wc-image.image) </span>

4. After making changes, click **Submit**. The changes will take effect immediately.


<span id="ae610cb1"></span>
## Clone a task

You can clone a task based on an existing one and adjust it as needed. The data source type cannot be modified when cloning a task.


1. In the **Data source** interface, click **target data source**, click **task name** to enter the task details page.

2. Click the `...` button in the upper right corner Click the **Clone** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adc3a73b26f54542957ceeeb40a4ecbb~tplv-goo7wpa0wc-image.image) </span>

3. In the clone import task interface, configure the task. For the operation steps, refer to [Create import tasks](https://docs.byteplus.com/docs/bytehouse/batch-import#116005dc).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d9f56bd016f4891b88b4dfa831567a4~tplv-goo7wpa0wc-image.image) </span>

4. After configuration is complete, click **Submit**. The changes will take effect immediately.


<span id="98c76014"></span>
## Delete a task

If you no longer need a task, you can delete it.


1. On the **data source** page, click **target data source**, then click **task name** to enter the task details page.

2. Click the `...` button in the upper right corner Click the **Delete** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb4456622d4042b0b310686a8ae96553~tplv-goo7wpa0wc-image.image) </span>

3. Click **OK**, and the task will be deleted.

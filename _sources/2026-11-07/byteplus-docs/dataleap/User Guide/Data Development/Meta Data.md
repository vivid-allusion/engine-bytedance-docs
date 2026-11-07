---
title: "Meta Data"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/meta_data"
---

During task development, metadata enables you to preview table fields, partition information, and data for tables used in EMR Serverless Spark/Presto, ByteHouse Cloud Data Warehouse, and ByteHouse CE. You can also jump to and view the status of tasks generated for related tables, and perform convenient actions such as generating table query statements with one click.

<span id="bf7290dc"></span>
## 1 Usage restrictions


* The content available for viewing in metadata tables or views varies depending on the engine. The specific differences are as follows:

   
   |Engine types |Table fields |Generate a usage statement |Data preview |Partition information |Related tasks |More actions (import data from a local CSV file) |
   |---|---|---|---|---|---|---|
   |EMR Serverless Spark/Presto |Support |Support |\- |Support |Support |Support |
   |EMR Doris |Support |Support |\- |\- |Support |\- |
   |ByteHouse CDW |Support |Support |\- |\- |Support |\- |
   |ByteHouse CE |Support |Support |\- |\- |Support |\- |
   

* Except for the EMR Serverless Spark/Presto engines, the metadata list interface for other engines has not temporarily made the relevant entry in [More actions](https://docs.byteplus.com/docs/dataleap/69493#4e70cd6a) available.


<span id="_2-使用前提"></span>
## 2 Prerequisites for use


1. In the DataLeap project console, the corresponding engine services are already bound, including Volcengine E\-MapReduce (EMR), EMR Serverless StarRocks, EMR Serverless Spark/Presto, ByteHouse Cloud Data Warehouse Edition, ByteHouse CE, and Lakehouse Analytics Service (LAS). For details on binding operations, see [Configure Service Binding Information](https://docs.byteplus.com/docs/dataleap/create_project#54f5e209).

2. To view metadata, you must first create and execute a metadata collector under the corresponding engine type in the data map. For details, see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

3. To preview specific table data in the metadata list, the currently logged\-in account must have query permissions on the table. For details on permission application operations, see [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission).


<span id="_3-功能介绍"></span>
## 3 Feature overview

<span id="_3-1-功能入口"></span>
### 3.1 Function entry points


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc) **.** 

2. On the **Overview** interface, among the displayed projects, click **IDE Development** under the desired project to enter that project.

3. On the **Data Development** interface, in the left navigation bar, click the **Metadata** button to go to the **Meta Data** page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71052c41b6e04bafa72f79d74385406f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-查找库表"></span>
### 3.2 Find database tables

The database page supports searching for database table information under the corresponding engine.


1. When you select the engine type corresponding to the metadata database in the dropdown box at the top of the metadata interface, the instance information and database and table information for the current engine will be displayed.

2. In the search box:

   1. You can enter a database name, table name, or keyword to search for relevant databases and tables.

   2. You can also click the **Collapse** button to the right of the input box. In the window on the right, the EMR Serverless Spark, ByteHouse CE and ByteHouse Cloud Data Warehouse engines allow you to filter by database name.


<span id="_3-3-查看表字段并生成查询语句"></span>
### 3.3 View table fields and generate query statements


1. After selecting a table name, you can view all field names, types, and descriptions in the table fields section.

2. When a table contains many fields, you can enter the field name in the search box to search for the relevant field you want to query.

3. Click the checkbox on the left. After selecting the fields, click **Generate usage statement** on the right:

   1. If the node code editor on the right is not open, a query statement will be generated in the **Generate Usage Statement** dialog. You can copy the statement and execute it in the node code editor. Click the **Confirm** button to close the dialog.

   2. If a node code editor is open on the right, clicking **Generate usage query** will automatically generate a query statement in the editor.


<span id="_3-5-分区信息"></span>
### 3.4 The partition information

Click **Partition information** to view the latest partitions, update time, number of rows, and partition size for tables in EMR Serverless Spark/Presto,. You can also enter a partition value in the search box to search for related partition information.

<span id="_3-6-任务信息"></span>
### 3.5 Related tasks

Click **Related tasks** to view basic information about output tasks for EMR Serverless Spark/Presto, ByteHouse CE, and ByteHouse Cloud Data Warehouse tables and views, such as task ID, task name, task cycle level, task owner, and more. Click the highlighted **task name** to jump to and open the configuration for the corresponding node task.

<span id="4e70cd6a"></span>
### 3.6 More actions

With the EMR Serverless Spark and EMR Serverless Presto engines, more operational capabilities are supported, such as creating tables, importing CSV files, and more.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Functions such as creating tables and importing CSV files are not currently supported for metadata of other engines here. Support for these features will be available in the future.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b4801d2dd294fb29d16e8f2127e5ec6~tplv-goo7wpa0wc-image.image) </span>


* Create a table: Click the **Create Table** button to navigate to the **Data Map** interface, where you can create a LAS Catalog table. For details on the creation operation, see [Manage LAS Catalog Tables](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_Tables).

* Import CSV: Supports uploading local CSV files to an object storage TOS Bucket, and, by configuring a TOS2Hive integration task, writing the CSV data into Hive tables under the EMR Serverless engine. For detailed instructions, see [Write local data to a Hive table](https://docs.byteplus.com/docs/dataleap/write_local_data_to_hive_table).

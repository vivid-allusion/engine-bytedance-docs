---
title: "Create a new database/table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-a-new-database-table"
---

A database is a logical grouping of data. Each database contains many tables, and tables are where data is stored, consisting of structured rows and columns. This tutorial introduces how to create databases and tables in ByteHouse Enterprise, and how to clone tables.

<span id="2c644333"></span>
# **Create a database**

You can create multiple databases based on your business needs, and you also need to select the target database when creating a table. Therefore, if no database exists in the current cluster, please create one first. **Steps**:


1. Log in to the [ByteHouse Enterprise Console](https://console.byteplus.com/bytehouse-ce) and navigate to the \*\*Data object \*\*interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3457a224e6604c56b811ead159afbcb0~tplv-goo7wpa0wc-image.image) </span>

2. In the upper left corner, use the dropdown to select a cluster. If you need to create a new cluster, please refer to [Create a cluster](https://docs.byteplus.com/docs/bytehouse/create-a-cluster).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd5b62931fce4dc5a7c4b90dfd045bff~tplv-goo7wpa0wc-image.image) </span>

3. On the left, click the ➕ **New** button and select **Create Database**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73ad9f5ad41c4f6a84143ead34036b46~tplv-goo7wpa0wc-image.image) </span>

4. Customize the database name and description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e1a41177b654f4dbfa98929cb24f297~tplv-goo7wpa0wc-image.image) </span>

   The database naming rules are as follows:

   * The name must start with a letter or an underscore and can only contain letters, numbers, and underscores.

   * Do not use the following keywords: 'system', 'default', or 'admin'.

   * The maximum length must not exceed 63 characters.

5. Click the **Create** button to complete database creation.


<span id="9642fe40"></span>
# Create a table


1. Log in to the [ByteHouse Enterprise Console](https://console.byteplus.com/bytehouse-ce) and navigate to the \*\*Data object \*\*interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf23e6f8a11e49d3ad4bd73befe3a705~tplv-goo7wpa0wc-image.image) </span>

2. In the upper left corner, use the dropdown to select a cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/594ab7c15a634aa99a17249ce853ba5a~tplv-goo7wpa0wc-image.image) </span>

3. On the left, click the ➕ **New** button. You can **create a table visually**, use **DDL template**, or **create tables in batch**. For specific operations, please refer to the corresponding sections below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58a32a6f8277424e97649163a924cc05~tplv-goo7wpa0wc-image.image) </span>

   * [Create a table visually](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table#b18c54b7)

   * [Create table using DDL template](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table#39b3445d)

   * [Batch table creation](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table#ec63355e)


<span id="b18c54b7"></span>
## Create a table visually

**Steps**:


1. Click **Create table** to enter the table creation page.

2. Configure the basic information of the table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/073a03b8525d45d691c46e86dea52fea~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration details |
   |---|---|
   |Cluster & Database |Select an existing cluster and database. The table will be created in the selected location. |
   |Table engine |* The default is HaMergeTree, which is largely compatible with the community ReplicatedMergeTree engine. For details, see [HaMergeTree](https://docs.byteplus.com/docs/bytehouse/hamergetree).<br><br>* To enable deduplication based on a unique key, select HaUniqueMergeTree. After selecting this engine, you can choose the unique key, effective range, and version field. For usage, refer to [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree). |
   |Table name & description |Customize the table name and description. |
   

3. Configure the column information of the table. You can add columns in several ways:

   * To import columns in a batch, click **Uploading and Importing**.

   * To add columns one by one, click **Add column**.

   * To add multiple columns manually, click **Add multiple**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94482fd688f4475292b7cca29f5b22a4~tplv-goo7wpa0wc-image.image) </span>

      For column information:

   * "Data type": Please refer to [data types supported by the ClickHouse community](https://clickhouse.com/docs/en/sql-reference/data-types/) for settings.

   * "Nullable": This corresponds to the `Nullable` attribute in ClickHouse.

4. Configure the table's advanced keys. At the bottom of the page, configure the table's sorting key, partition key, shard key, and so on.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/582028f0ae3a4bb3b6544315cd347a87~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Order by key, partition key, and unique key must not be nullable.   </div>
   

   
   |Parameters |Configuration details |
   |---|---|
   |Order by key (ORDER BY) |To improve query performance, ByteHouse organizes data according to the order of the sort key when storing data. The core rules and configuration recommendations are as follows:<br><br><br>1. **Field constraint**: The sort key supports non\-unique values, but cannot be set to the Nullable type.<br><br>2. **Configuration recommendation**:<br><br>   * Preferably select one to three fields that are frequently used as query filter conditions. The higher the usage frequency, the higher the sorting priority should be.<br><br>   * If multiple fields have similar usage frequency, it is recommended to place fields with smaller cardinality in a higher sorting position.<br><br>3. Partition fields do not need to be used as sort keys; both can be configured independently.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The order by key cannot be modified after table creation.</div><br> |
   |Partition key (PARTITION BY) |Optional types:<br><br><br>* Time type (Date/DateTime): Using a time type (Date/DateTime) is best practice, and you can only set a TTL (data lifecycle) when a time\-based partition is selected. Partition granularity options include DAY (by day), HOUR (by hour), and MONTH (by month).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to consider hourly (HOUR) partitioning only when the single\-day data volume exceeds 10 billion; if the data volume is too small, monthly partitioning can be selected. Otherwise, daily partitioning is recommended.   </div><br>   <br><br>   * Number type (Int / UInt / Float)<br><br>   * String type (String)<br><br>* If partitioning is not required, the partition key can be left unselected.<br><br>* The partition field cannot be Nullable.<br><br><br>Partition key is used for data sharding storage, supporting multiple type configurations.<br><br><br>* Available data types:<br><br>   * Time type (Date/DateTime): Setting it as a time type is best practice. Partition granularity options include DAY (by day), HOUR (by hour), and MONTH (by month). ByteHouse supports configuring TTL (data lifecycle) for tables only when the partition key is set to this type.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">It is recommended to consider hourly (HOUR) partitioning when the single\-day data volume exceeds 10 billion, or if the data volume is too small, monthly partitioning can be selected. Otherwise, daily partitioning is recommended.      </div><br>      <br><br>   * Number type (Int/UInt/Float)<br><br>   * String type (String)<br><br>* If partitioning is not required to optimize query or data management, the partition key can be left unconfigured.<br><br>* The partition field cannot be of Nullable type. |
   |Data lifecycle (TTL) |It is used to set data retention rules, effective at the table level.<br><br>Data retention time is calculated based on the "partition field"; therefore, TTL cannot be set for tables without time\-based partitions, and the system will automatically set retention to permanent.<br><br><br>* After enabling transfer to cold storage, data with lower access frequency can be stored on lower\-cost cold disks to reduce storage costs. When using the HaUniqueMergeTree engine, data is not moved according to the local storage limit.<br><br>* After enabling data deletion, unnecessary data can be deleted according to the time cycle to reduce storage costs. |
   |Sharding key<br><br>(Required for HaMergeTree engine configuration) |The sharding field ensures that data in a column is evenly distributed across all nodes in the cluster, maximizing cluster performance and improving query efficiency.<br><br>Fields frequently used in GROUP BY are typically selected as sharding fields.<br><br>The sharding field only supports String, Int, UInt, Date, DateTime, and DateTime64 types, and cannot be of Nullable type. |
   |Unique key<br><br>(Required for HaUniqueMergeTree engine configuration) |The unique key is used to determine data deduplication (upsert) based on selected fields, and supports multi\-field configuration.<br><br><br>* Unique key (**Required**): Each table can have only one unique key, supporting up to 3 fields to form a composite key. If there are more than 3 fields, you can calculate the 64\-bit hash value of all unique fields yourself and use this hash field as the unique key. If the hash value is signed, you need to use the Int64 type.<br><br>* Scope of unique key (**Required**): There are two types:<br><br>   * If it is [partition\-level uniqueness], the unique key must be unique within the partition.<br><br>   * If it is [table\-level uniqueness], the unique key must be unique within the table. Table\-level uniqueness incurs additional write overhead; it is **recommended to prioritize partition\-level uniqueness**.<br><br>* Version field (optional): When writing multiple data entries with the same unique key, by default, the latest data written is retained. If a version field is specified, the data with the maximum version will be retained. If table\-level uniqueness is used, you can additionally use the partition expression as the version field, that is, for the same unique key, the data from the latest partition will be retained. |
   |Skipping index (INDEX) |If a query's filter conditions include fields in a skipping index, ByteHouse can pre\-filter data and reduce I/O, which accelerates query performance. You can select columns to set it as skipping indexes in the interface and set the type of skipping index.<br><br>The following index types are currently supported: `set`, `minmax`, `bloom_filter`, `tokenbf_v1`, `ngrambf_v1`. The supported configuration parameters are as follows:<br><br><br>* **General parameters**:<br><br>   * **GRANULARITY** (**index granularity**): All types of indexes support setting GRANULARITY, and the default value set in the console is 1. It is generally recommended to set it to 1 to achieve higher filtering rates. The larger the GRANULARITY value, the less storage is occupied, but the corresponding filtering effect may be weakened. The currently supported configuration range is 1~10.<br><br>* **Exclusive parameters**: Different indexes support different configuration parameters; please configure as needed.<br><br>   * `set`: Supports setting a single parameter, which is the maximum number of values in each data block. The value range is 0–256. When this parameter is set to 0, an unlimited number of discrete values can be stored. If the number of values in a data block exceeds the maximum capacity, the index will be empty.<br><br>   * `minmax`: No dedicated parameters.<br><br>   * `bloom_filter`: Supports setting the allowed "false positive rate", with a value range of 0 to 1. If not specified, the default value is 0.025. This parameter is optional. Not applicable to Map, JSON, or Geometry data types.<br><br>   * `tokenbf_v1`: Only applicable to String and FixedString data types. Supports setting three parameters:<br><br>      * **Filter size**: Measured in bytes. The larger the filter, the lower the false positive rate, but the storage cost will increase accordingly.<br><br>      * **Number of hash functions**: The more hash functions, the lower the false positive rate.<br><br>      * **Seed value for Bloom filter hash functions**.<br><br>   * `ngrambf_v1`: Only applicable to String and FixedString data types. Supports setting four parameters:<br><br>      * **ngram length**;<br><br>      * **Filter size**: Measured in bytes. The larger the filter, the lower the false positive rate, but the storage cost will increase accordingly.<br><br>      * **Number of hash functions**: The more hash functions, the lower the false positive rate.<br><br>      * **Seed value for Bloom filter hash functions**.<br><br><br>For more instructions on using skip indexes, see [Skipping index](https://docs.byteplus.com/docs/bytehouse/skipping-index).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The skip index cannot be modified through the visual method after the table is created. Please operate with caution.</div><br> |
   

5. After completing the form, click **Create** in the lower right corner to submit the table creation task. If there is no error message, the creation is successful.


<span id="39b3445d"></span>
## Create table using DDL template

**How to use**:


1. Click **Created with DDL template**, select the required DDL template on the DDL template page, and click **Use This Template**. The system will automatically jump to the query window, where you can modify the table fields as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb3cd8fda42f42c6bcf8fdf7e58035a4~tplv-goo7wpa0wc-image.image) </span>

2. After completing the modifications, select **All nodes** and click **Run** to create the table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93099980e2d4451e930c8b014feff1e3~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about DDL templates, see <a href="https://docs.byteplus.com/docs/bytehouse/create-a-database-table-based-on-ddl-template">Create a new database/table: Based on the DDL template</a>.</div>


<span id="ec63355e"></span>
## Batch table creation

**How to use**:


1. Click **Batch table creation**, select the database on the batch table creation page, and enter the corresponding table creation statements in the editor. For a detailed description of the table creation statements, see [SQL syntax](https://docs.byteplus.com/en/docs/bytehouse/sql-syntax).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d199236545c4c78b2160449718413ce~tplv-goo7wpa0wc-image.image) </span>

   In the editor, you can also perform the following operations:

   
   |Operation |Description |
   |---|---|
   |Download SQL |Download the SQL statements edited in the editor to local for saving. |
   |Upload SQL |Upload the SQL statements to be executed in the form of a local file, and batch execute them in the editor. |
   |SQL formatting |Format the written SQL to improve statement readability. |
   |Copy SQL |You can copy the written SQL statements. |
   |Clear all SQL |Clear all SQL statements written in the editor. |
   

2. Click **SQL optimize**, and the system will adjust the SQL statements according to built\-in rules to better align with ByteHouse table creation best practices.

3. Click **Optimized**, preview the table configuration information on the preview table page. If the configuration is correct, click Create.

   The system will display "**Table creation job has been submitted**", indicating that the task was submitted successfully.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a16bd6e4b0ac4e258be12b0ecefed83f~tplv-goo7wpa0wc-image.image) </span>

4. In the list on the **Data object** page, click the **Refresh** button to view the created tables under the corresponding database.


<span id="d7e1c122"></span>
## Non\-visual table creation method

When creating tables using the CLI, JDBC, or other programmatic methods, the relevant table structures and data will be synchronized to the ByteHouse Enterprise Edition Console every 5 minutes. ByteHouse supports synchronization of the following table engines and corresponding synchronization rules:


* **Synchronized as** "**Logical Table**": HaMergeTree tables or HaUniqueMergeTree tables associated with a [Distributed table](https://clickhouse.com/docs/en/engines/table-engines/special/distributed) will be synchronized as a "Logical Table". Such tables have the same functionality as tables created in the ByteHouse Enterprise Console and comply with ByteHouse table creation best practices. Therefore, you can perform operations such as modifying tables, deleting partitions, and creating import tasks in the ByteHouse Enterprise Edition Console as usual.

* **Synchronized as** "**Custom Table**": HaMergeTree tables or HaUniqueMergeTree tables not associated with a Distributed table, or other [MergeTree family tables](https://clickhouse.com/docs/en/engines/table-engines/mergetree-family/) in the community (such as MergeTree, DuplicatedMergeTree, and many other), will be synchronized as a "Custom Table" because they do not comply with ByteHouse table creation best practices. Such tables are only displayed in the ByteHouse Enterprise Console. Querying these tables is supported, but operations such as modifying tables, deleting partitions, and creating import tasks are not supported.

* **Synchronized** **as** "**external table**": Tables from MySQL, S3, Hive, and other [Integration engine](https://clickhouse.com/docs/en/engines/table-engines/integrations/) tables will be synchronized as "external tables". These tables are only displayed in the ByteHouse Enterprise Console. You can query these tables, but modifying tables, deleting partitions, or creating import tasks is not supported. Caution: In the Integration engine, tables from the Kafka engine and RabbitMQ engine will not be synchronized for now, as querying these tables may result in data loss.


<span id="c07622e4"></span>
# Clone tables

Cloning a table means creating a new table using the same schema and data as the **original table**.

**Steps**:


1. On the \*\*Data object \*\*page, click a data table to open its details page.

2. Click the  **...**  button in the upper right corner, then click **Clone**.

3. Click **Visual clone** or **SQL clone**.

   
   |Clone method |Operation instructions |
   |---|---|
   |Visual clone |The system will jump to the clone table page. You can refer to the configuration instructions in [Create a table visually](https://docs.byteplus.com/docs/bytehouse/create-a-new-database-table#b18c54b7) to configure the clone table information. After configuration is complete, click **Clone**, and the system will automatically create the clone table. |
   |Clone by SQL |The system will jump to the SQL edit page, where you can adjust the table creation command as needed. After editing is complete, click Run, and the system will automatically create the clone table. |

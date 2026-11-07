---
title: "Guide to config data conversion for solutions"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/guide_to_config_data_conversion_for_solutions"
---

DataSail provides real\-time and batch synchronization solutions for entire databases, as well as real\-time synchronization solutions for sub\-databases and sub\-tables. It also supports adding custom SQL conversion rules. It supports performing various data conversion operations on data collected from the source system to meet the requirements of different business scenarios.

Data conversion can be applied to various lightweight data processing scenarios. For example:


* **Split, merge, and reorder fields**: You can use the SELECT statement flexibly to split, merge, or reorder fields in the source table.

* **Data cleaning and filtering**: You can use WHERE clauses to filter redundant data, handle missing values, correct data errors, and more.

* **Preprocessing**: You can use conditional functions to perform preprocessing on data, such as standardization and other preprocessing operations. For example, you can standardize null values.

* **Format conversion**: You can use conversion functions and encryption/decryption functions to convert data from one format to another.


<span id="f238cf98"></span>
## 1. Precautions


* The conversion rule functionality is currently in the **BETA public testing phase** and is still rapidly evolving, especially in areas such as function support and boundary condition handling. We welcome you to try and provide suggestions.

* It currently supports commonly used functions compatible with Flink 1.11 (see details [Data conversion function library](https://docs.byteplus.com/docs/dataleap/data_conversion_function_library)) and their input and output behavior, and continuously introduces Flink functions from later versions, as well as additional functions, such as JSON functions and AES encryption and decryption functions, to further expand processing capabilities.

* Input conversion SQL statements only support internal Flink SQL statements; SQL syntax specific to the source or target datasource type is not supported.


<span id="6d844dc0"></span>
## 2 Operation steps

You can access the data convert configuration in the following ways:

<span id="2f4932ae"></span>
### 2.1 Enter data conversion configuration

Currently, **Batch synchronization, Full Load + CDC synchronization, and Full Load + CDC(Sharded DB) synchronization** solutions support the configuration of data conversion rules.


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Select the project to which the task belongs, enter the data development interface, and access the Data synchronization solution configuration interface at the top.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c847f2b11c2148238b4dc5b60d425c70~tplv-goo7wpa0wc-image.image) </span>

3. In the Data Pipelines interface, click the **Build a new data pipeline** button in the upper right corner, select the corresponding synchronization plan from the dropdown, and enter the plan configuration interface.

4. Complete the plan's **Basic Configuration**, click **Next**, and go to the **Mapping Configuration** interface.

5. In the mapping configuration interface, after you complete the selection of datasource DB tables, you can begin data conversion configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ad9686bd38640f291adf968cc8fff63~tplv-goo7wpa0wc-image.image) </span>


For details on the Basic Configuration Action, see [Operation details for each solution](https://docs.byteplus.com/en/docs/dataleap/data_synchronization_solutions).

<span id="69304016"></span>
### 2.2 Configure convert rules

<span id="9b95188a"></span>
#### Entire DB synchronization

For full DB synchronization solutions (including batch full DB synchronization and real\-time full DB synchronization), you can go to the **Mapping configuration \> Data transformation configuration** section, click **Configuration details**, and in the statement input box, enter the SQL transformation statement for the selected tables. The source table name after FROM supports regular expressions, and the database\-table separator (.) does not require escaping. The example is as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Input Convert SQL statements support only internal Flink SQL statements and do not support SQL syntax specific to source or target datasource types.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fd0bb3c095b4c5e893e9bd08d4a738d~tplv-goo7wpa0wc-image.image) </span>

On the right side of the statement text box, you can perform the following actions:


1. Delete: After you add multiple SQL Convert Statements, you can perform the Delete Action on any Convert Statement except the first one. The first Convert Statement can be adjusted using the **Move Up, Move Down** buttons.

2. Add: You can add multiple SQL conversion statements.

3. Move up: Move the SQL Convert statement for the current row up.

4. Move down: Move the SQL Convert statement associated with the current row down.


The relationship between SQL rules and database tables is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd6f61dc497e4158867adf583677e2e3~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Supports <code>SELECT *</code> syntax. For example, you can use <code>SELECT *, 'Hello' AS new_field</code> to uniformly add a new field named new_field to each selected table. The schema (field names and types) of each table can be different.</div>


2. <div data-tips="true" data-tips-type="warning">After applying SQL conversion, if the primary key name of the source table changes (for example, id becomes new_id), you need to explicitly specify the new primary key name in <strong>data conversion configuration \> Advanced parameters</strong>, such as: primary_keys=new_id (as shown in the figure above). Otherwise, an error will occur. An example of the error message is as follows:</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98a634b3ef0a44c6b01a0b3881d4eb91~tplv-goo7wpa0wc-image.image" width="984px" />   </div>
   

3. <div data-tips="true" data-tips-type="warning">Each rule can match multiple tables among the selected tables (the source table name <strong>supports regular expressions</strong>, and <strong>it is not necessary to add escape characters for separators</strong>, which means you should write <code>db_name.table_prefix.*</code> instead of <code>db_name\.table_prefix.*</code> or <code>db_name.table_prefix\.*</code>). However, <strong>each table can only be matched by one rule</strong>; otherwise, an error will occur. An example of the error message is as follows:</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a68404c75d344747b0b7f263b2b37c48~tplv-goo7wpa0wc-image.image" width="1356px" />   </div>
   

4. <div data-tips="true" data-tips-type="warning">For a Datasource such as PostgreSQL that has a three\-level structure, make sure that the source table selected in the FROM clause contains all hierarchy levels. For example, <code>FROM db_name.schema_name.table_prefix.*</code>.</div>


5. <div data-tips="true" data-tips-type="warning">Currently, SQL statements <strong>do not yet support Chinese character constant values</strong>. If you wish to use Chinese, temporarily decode Base64 strings that contain Chinese characters using the FROM_BASE64() function. For example, use <code>WHERE name = FROM_BASE64('5ZOI5ZOI')</code> instead of <code>WHERE name = 'haha'</code>.</div>


6. <div data-tips="true" data-tips-type="warning">Currently, in SQL statements, <strong>numeric constant values containing a decimal point</strong> are, by default, inferred to be of the DECIMAL type. If you want to use it as the DOUBLE type, an explicit CAST is required. Example <code>CAST(123.456 AS DOUBLE)</code>.</div>


7. <div data-tips="true" data-tips-type="warning">Only one SQL statement is allowed per row. Multiple SQL statements are separated by rows, and the statements are executed in parallel.</div>



After completing the Conversion statement configuration, in the **Destination database/table mapping configuration** section below, configure the **DB/Table name mapping configuration**. Once this is done, click the **Refresh source table and destination table mapping** button. If the syntax is correct, the structure of the transformed new table will be displayed.

<span id="4d3b8783"></span>
#### 2.2.2 Sub\-database sub\-table

In sub\-database sub\-table mode, the configuration method for conversion rules is similar to that of the whole database synchronization plan. The main differences are as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Precautions for sub\-database and sub\-table</div>



1. <div data-tips="true" data-tips-type="warning">The source table of a sub\-database sub\-table only supports exact matches and does not support selecting specific upstream tables; otherwise, an error will occur (see the following figure). For example, for MySQL and other data sources with a two\-level structure, you need to write <code>FROM .*..*</code>. For PostgreSQL and other data sources with a three\-level structure, you need to write <code>FROM .*..*..*</code>.</div>


   <div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f57fdccd03f4410fae9b377d0bc86ae8~tplv-goo7wpa0wc-image.image" width="1940px" />   </div>
   

2. <div data-tips="true" data-tips-type="warning">It is recommended that the SELECT field in sub\-database and sub\-table scenarios include the <code>_src_meta_info_</code> field. This applies even when using <code>SELECT *</code>; it is suggested to explicitly add this field, for example, <code>SELECT *, _src_meta_info_</code>. This field is used to identify the actual upstream table from which this data entry is input, and also helps prevent write errors caused by duplicate IDs when data from multiple sub\-tables is involved, as well as other related issues.</div>


3. <div data-tips="true" data-tips-type="warning">The sub\-database sub\-table feature temporarily does not support DDL change strategy settings. For example, operations such as adding new columns, deleting columns, or modifying column types at runtime are not supported.</div>



<span id="69a46806"></span>
## 3 Metadata field descriptions

We can reference some data fields in the SELECT statement. For example:

```SQL
SELECT __database_name__ AS dbName, __schema_name__ AS schemaName, __table_name__ AS tableName, __op_type__ AS opType, __ts_ms__ AS transMs FROM my_database..*
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">It is not allowed to apply any functions or transformations to metadata fields. For example, <code>CONCAT(__table_name__ , '-SUFFIX')</code> and <code>__ts_ms__ + 100</code> are not allowed.</div>


* <div data-tips="true" data-tips-type="warning">For target datasources such as ByteHouse, <strong>table field names are not allowed to start with "__"</strong>. Therefore, when referencing metadata fields, you must use <code>AS</code> to assign a new name to the metadata field. For example, <code>__table_name__ AS table_name</code>. Directly mapping the original field name to the downstream table is not allowed.</div>



<span id="730cb6d7"></span>
### Mapping relationship of metadata fields related to the datasource

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Description of the mapping relationship in the table below:</div>



* <div data-tips="true" data-tips-type="tip">Three\-level structure (Database, Schema, Table). For example: PostgreSQL, SQL Server.</div>


* <div data-tips="true" data-tips-type="tip">Ordinary two\-level structure (Database, Table), for example: MySQL, MongoDB, StarRocks, and Doris</div>




|Structure classification ||__database_name__ |__schema_name__ |__table_name__ |
|---|---|---|---|---|
|Three\-level structure |PostgreSQL |Database |Schema |Table |
||GaussDB |Database |Schema |Table |
||SQL Server |Database |Schema |Table |
|Ordinary secondary structure |MySQL |Database |* (Output: null; the same applies below) |Table |
||MongoDB |Database |\- |Table |
||veDB |Database |\- |Table |
||StarRocks |Database |\- |Table |
||Doris |Database |\- |Table |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In sub\-database sub\-table mode, if the convert statement requires the use of the above metadata fields, the SELECT statement must contain the <code>_src_meta_info_</code> field (with a special exception: when using SELECT \*, this field will be included automatically and does not need to be added manually). Otherwise, the following error message will appear:</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed55f8eaef004c6c8f04f8bbb9e07823~tplv-goo7wpa0wc-image.image" width="2362px" /></div>


<span id="ff8fcbd3"></span>
### 3.2 Data\-related metadata fields


* `__op_type__`：

   Returns the type of this data entry (in string form). Possible values are INSERT, UPDATE_BEFORE, UPDATE_AFTER, and DELETE.

* `__ts_ms__`：

   * For CDC jobs: return the **business timestamp** when data is written to Binlog. If it cannot be obtained, return \-1.

   * For batch jobs: **The default value of this field is 0.**  You can modify the default value of this field for batch jobs using the `job.transform.ts_ms_field_value_for_batch` advanced parameter.

      * Additionally, if the value of the `job.transform.ts_ms_field_policy_for_batch` advanced parameter is set to `EPOCH_TIME`, this field returns the actual reading time for each data entry (dynamic change).

* `_src_meta_info_`：

   In sub\-database sub\-table mode, this is used to indicate the source database/table information for this data entry and to prevent conflicts when writing data entries with the same key.

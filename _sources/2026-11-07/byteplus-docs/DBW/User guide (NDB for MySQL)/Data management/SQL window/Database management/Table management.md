---
title: "Table management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Table_management"
---

This topic describes how to visually create, delete, and edit tables on the Database Workshop (DBW) console to manage the entire lifecycle of tables.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [created an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [created an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_database_and_account#.5Yib5bu66LSm5Y-3).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


|**Actions** |**Precautions** |
|---|---|
|Create a table |Creating tables on system databases is not supported. |
|Query a table |* Querying tables on system databases is not supported.<br><br>* After a table is successfully queried, editing of the execution results is only supported for tables that meet the following conditions:<br><br>   * Single table query.<br><br>   * The table must have a primary key or a unique index in all columns.<br><br>   * The execution result is not queried through the table alias.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When querying a view, editing the execution result is also not supported.   </div><br>    |
|Edit table structure |* Editing tables on system databases is not supported.<br><br>* Due to time constraints on DDL execution, large tables may fail to execute. Therefore, it is recommended that you do not make structural or index adjustments to large tables on the DBW console.<br><br>* Columns can not be modified if an index or foreign key is set. To adjust, delete the index or foreign key first.<br><br>* To modify the foreign key information, please modify the foreign key name first. |
|Rename table |* Renaming tables on system databases is not supported.<br><br>* After renaming the table, you will not be able to access the table through the original table name. Please proceed with caution. |
|Copy table structure |* Copy table structure only supports copying the original table structure and cannot copy the original table data.<br><br>* Copying table structure on the system database is not supported.<br><br>* Foreign keys will be filtered during the result copying process. |
|Delete a table |* Deleted tables cannot be recovered, so proceed with caution.<br><br>* Deleting tables in the system database is not supported.<br><br>* Dropping a table may cause database performance degradation because the database needs to process many files. It is recommended not to perform this operation during peak business hours. |


<span id=".5Yib5bu66KGo"></span>
## Create a table


1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Create table**.

4. On the **Create table@{database name}**  tab, configure the following parameters.

   1. Configure the basic information, as shown in the following table.

      
      |**Parameter** ||**Description** |
      |---|---|---|
      |**Table name** ||Custom table name. Naming rules:<br><br><br>* The database name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Storage engine** ||Select a Storage engine from the drop\-down list. Currently only InnoDB is supported. |
      |**Character set** ||From the drop\-down list, select the character set.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">MySQL 5.7 supports <code>latin1</code>, <code>ascii</code>, <code>utf8</code>, and <code>utf8mb4</code> formats.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MySQL 8.0 supports <code>latin1</code>, <code>ascii</code>, <code>utf8mb3</code>, and <code>utf8mb4</code> formats.</div><br> |
      |**Validation rule** ||Select a validation rule from the drop\-down list. |
      |**Remarks** ||(Optional) Remarks information of the form to help you identify the purpose of the form. |
      |**Row format** ||(Optional) Select the target Row format from the drop\-down list. The following formats are supported:<br><br><br>* **REDUNDANT**: The supported Tablespace systems are System Tablespace, single\-table file Tablespace, and general Tablespace.<br><br>* **COMRPACT**: With compact Storage characteristics, the supported Tablespace systems are System Tablespace, single\-table file Tablespace, and general Tablespace.<br><br>* **DYNAMIC**: (Default) With compact Storage characteristics, enhanced variable\-length Column Storage, and support for large Index prefixes. The supported Tablespace systems are System Tablespace, single\-table file Tablespace, and general Tablespace.<br><br>* **COMPRESSED**: It has compact storage characteristics, enhanced variable\-length column storage, supports large index prefixes and compression, and also supports system tablespace, single\-table file tablespace, and general tablespace. |
      |**Average row length** ||The value range is 0~2^31\-1, that is, the maximum value is 2147483647. If this parameter is not set, the default is empty. |
      |**Minimum row** ||The value range is 0~2^31\-1, that is, the maximum value is 2147483647. If this parameter is not set, the default is empty. |
      |**Maximum row** ||The value range is 0~2^31\-1, that is, the maximum value is 2147483647. If this parameter is not set, the default is empty. |
      |**Advanced configuration** |**HTAP** **Tables** |Select whether to check Enable HTAP properties. After enabling HTAP, it can simultaneously meet the business needs to handle a large number of transaction operations and complex data analytics queries, that is, through a database system, it can simultaneously meet the business's OLTP (TP) and OLAP (AP) requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enabling HTAP does not automatically synchronize data from TP tables to AP tables. To perform synchronization, submit an SQL ticket for execution. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Creating_a_regular_SQL_change_ticket">Creating a regular SQL change ticket</a>.</div><br> |
      ||**DISTRIBUTION_KEYS** |Select a column name for data distribution from the drop\-down list. You need to add related column information on the **Column Information** tab first. |
      ||**DISTRIBUTION_NUMBER** |Set the number of data distributions. The value must be a positive integer. If not set, the default is 11. |
      ||**INC_STATS** |Select column field attributes from the drop\-down list. Used for incremental statistical information collection to optimize query plans and execution. You need to add relevant information of the column in the **Column information** tab first. |
      

   2. On the **Column information** tab, click **Add column** to configure column information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**No.**  |Indicates the serial number of the column. Modification is not supported. |
      |**Column name** |Custom column name. Naming rules:<br><br><br>* The column name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Type** |Select the attribute of the column from the drop\-down list. The following types are supported:<br><br><br>* **String**, including `char`, `varchar`, `tinyText`, `text`, `mediumText`, `longText`, `enum`, `set`, and `json` types.<br><br>* **Binary**, including the `binary`, `varbinary`, `tinyblod`, `blod`, `mediumblod`, and `longblod` types.<br><br>* **Number**, including the `tinyint`, `smallint`, `mediumit`, `int`, `bigint`, `float`, `bit`, `double`, `bool`, `boolean`, `decimal`, `numeric`, and `real` types.<br><br>* **Spatial data**, including the `geometry`, `point`, `linestring`, `polygon`, `multipoint`, `multilinestring`, `multipolygon`, and `geometrycollec` types.<br><br>* **Date and time**, including the `date`, `datetime`, `timestamp`, `time`, and `year` types. |
      |**Length/Configuration** |Configure the length/configuration of the **type**. When the **type** selects the following **type**, the length/configuration of the **type** needs to be configured:<br><br><br>* **String**, `including` `char`, `varchar`, `text`, `enum`, and `set` types.<br><br>* **Binary**, `including` `binary`, `varbinary`, and `blod` types.<br><br>* **Number**, `including` `tinyint`, `smallint`, `mediumit`, `int`, `bigint`, `float`, `bit`, `decimal`, and `numeric` types.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the <code>type</code> selects <code>enum</code> or <code>set</code>, you need to define a specific collection for the column.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the type is <code>decimal</code> or <code>numeric</code>, setting the decimal place is also supported.   </div><br>    |
      |**Remarks** |(Optional) Remarks for the column to help you identify the purpose of the column |
      |**Null allowed** |(Optional) Select whether to allow null values. Setting a primary key is not supported when **Null allowed** is selected. |
      |**Auto\-increment column** |(Optional) Select whether to set an auto\-increment column. |
      |**Primary key** |(Optional) Select whether to set a primary key. When choosing to set a primary key, setting null allowed is not supported. If you need to select multiple columns, the order will be arranged from small to large according to the serial number. |
      |**Default value** |(Optional) Set the default value for the current column. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a column, click the delete icon in front of the target column serial number.      </div>
      

   3. On the **Index** tab page, click **New index** to configure index information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**No.**  |Indicates the serial number of the index, which cannot be modified. |
      |**Index name** |Custom index name. Naming rules:<br><br><br>* The index name is unique within the table.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Include column** |Select the columns to include from the drop\-down list box. Multiple selections are supported. |
      |**Index type** |Select an index type from the drop\-down list. The following types are supported:<br><br><br>* **UNIQUE**: Represents a unique index that does not allow duplicates.<br><br>* **FULLTEXT**: Represents a full\-text index. Suitable for scenarios such as searching for long articles.<br><br>* **NORMAL**: Represents a normal index.<br><br>* **SPATIAL**: Represents a spatial index. |
      |**Index method** |Select the Index method from the drop\-down list. Currently, only BTREE is supported, which means that the index stores data in a B+ Tree structure. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete an index, select the target index and click <strong>Delete</strong>.      </div>
      

   4. (Optional) On the **Foreign key** tab, click **Add foreign key** to configure Foreign key information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**No.**  |Indicates the serial number of the foreign key, which cannot be modified. |
      |**Foreign key name** |Custom foreign key name. Naming rules:<br><br><br>* The foreign key name is unique within the table.<br><br>* The foreign key name cannot contain the `FOREIGN KEY` keyword.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Include column** |In the drop\-down box, select the columns to include. Multiple selections are supported. |
      |**Reference database** |In the drop\-down list, select the database you want to reference. |
      |**Reference table** |Select the table you want to reference from the drop\-down list. |
      |**Reference column** |Select the columns to reference from the drop\-down list. Multiple selections are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The referenced columns need to have indexes Set. For specific operations, see the previous step.</div><br> |
      |**When deleting** |When selecting to delete the primary table in the drop\-down list, the following options are supported for changes to the child table:<br><br><br>* **NoAction**: The primary table can only be deleted when the child table does not exist. When the child table exists, the child table is deleted, and the primary table remains unchanged.<br><br>* **Restrict**: The primary table can only be deleted when the child table does not exist.<br><br>* **Cascade**: When the primary table is deleted, the child table is deleted synchronously. When the child table is deleted, the primary table remains unchanged.<br><br>* **SetNull**: When the primary table is deleted, the child table is automatically updated to NULL. When the child table is deleted, the primary table remains unchanged.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Different versions of MySQL have differences in the default action of the child table <0\>data</a\> when the primary table is deleted, as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the MySQL version is 5.7, when the primary table is deleted, the default action of the child table <0\>data</a\> is Restrict.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the MySQL version is 8.0, the default action for deleting data from a table is NoAction when the primary table is dropped.</div><br> |
      |**When updating** |Select how the data in the child table changes when updating the primary table in the drop\-down list. The following options are supported:<br><br><br>* **NoAction**: The primary table can be updated only when the child table does not exist. When the child table exists, the child table is updated and the primary table remains unchanged.<br><br>* **Restrict**: The primary table can be updated only when the child table does not exist. When the child table exists, the child table is updated and the primary table remains unchanged.<br><br>* **Cascade**: When the primary table is updated, the child table is updated synchronously. The primary table remains unchanged when the child table is updated.<br><br>* **SetNull**: When the primary table is updated, the slave table is automatically updated to NULL. The primary table remains unchanged when the child table is updated.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Different versions of MySQL have different default actions for slave table data when the primary table is updated, as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the MySQL version is 5.7, the default action for the slave table data is Restrict when the primary table is updated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the MySQL version is 8.0, the default action for the slave table data is NoAction when the primary table is updated.</div><br> |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a foreign key, select the target foreign key and click <strong>Delete</strong>.      </div>
      

5. Click **Submit**.


<span id=".5p-l6K-i6KGo"></span>
## Query a table


1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Query table**.

4. on the **SQL**  **query** tab, click **Execute** in the command execution area.

   In the **Execution result** area, you can view the detailed information of the table. At the same time, you can also manage the table, as shown in the following table:

   
   |**Actions** |**Description** |
   |---|---|
   |**Add rows** |1. In the **Execution result** area, right\-click any row, click **Add rows**, and set the parameter information of the row to be added in the added row.<br><br>2. (Optional) To cancel this change, click **Reset**.<br><br>3. Click **Submit**, in **Execute** In the **SQL** dialog box, confirm whether the SQL statement is correct, and then click **Execute**. |
   |**Delete row** |1. In the **Execution result** area, right\-click the target row you want to delete, and then click **Delete row**.<br><br>2. (Optional) To cancel this change, click **Reset**.<br><br>3. Click **Submit**, in **Execute** In the **SQL** dialog box, confirm whether the SQL statement is correct, and then click **Execute**. |
   |**Modify Row** |1. In the **Execution result** area, modify the rows that need to be changed.<br><br>2. Click **Submit**.<br><br>3. (Optional) If you need to cancel this change, click **Reset**.<br><br>4. In the **Execute SQL** dialog box, confirm that the SQL statement to be executed meets the requirements, and click **Execute**. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can also on the <strong>SQL</strong>   <strong>query</strong> tab's command execution area, edit the query statement as needed, and click <strong>Execute</strong>.</div>


* <div data-tips="true" data-tips-type="tip">While editing a table, you can click <strong>Revoke</strong> to undo the current modification. After saving the changes, you cannot undo them.</div>


* <div data-tips="true" data-tips-type="tip">After a table is successfully queried, editing of the execution results is only supported for tables that meet the following conditions:</div>


   * <div data-tips="true" data-tips-type="tip">Single table query.</div>


   * <div data-tips="true" data-tips-type="tip">The table must have a primary key or a unique index in all columns.</div>


   * <div data-tips="true" data-tips-type="tip">The execution result is not queried through the table alias.</div>


* <div data-tips="true" data-tips-type="tip">When querying a view, editing the execution result is also not supported.</div>



<span id=".57yW6L6R6KGo57uT5p6E"></span>
## Edit table structure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Due to time constraints on DDL execution, large tables may fail to execute. Therefore, it is recommended that you do not make structural or index adjustments to large tables on the DBW console.</div>


* <div data-tips="true" data-tips-type="tip">Editing changes to the HTAP properties of a table is not supported.</div>


* <div data-tips="true" data-tips-type="tip">When a column has an index or foreign key setting, it cannot be modified while editing the table structure. To adjust, delete the index or foreign key first.</div>


* <div data-tips="true" data-tips-type="tip">When you need to modify the foreign key information, modify the foreign key name first.</div>


1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Edit table structure**.

4. In the **Edit table structure_{table name@database name}**  command execution area, edit the table's **Basic information**, **Column information**, **Index**, or **Foreign key**. For more information, refer to [Creating a table](https://docs.byteplus.com/en/docs/DBW/Table_management#.5Yib5bu66KGo).

5. Click **Submit**.

6. In the **Execute** **SQL** dialog box, confirm the change statement.

7. Click **Execute**.


<span id=".6YeN5ZG95ZCN6KGo"></span>
## Rename table

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After renaming, accessing the original name of the table is no longer supported. Proceed with caution.</div>



1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visualization area of the **Data interaction platform**, **expand** the **Table**, right\-click the target table, and select **Rename**.

4. In the **Rename table {table name}**  dialog box, enter the new table name in the **Rename to** text box. The table name can be customized. Naming rules are as follows:

   * The database name is unique within the database.

   * The length must be between 1 and 64 characters, and can not be empty.

   * The name must start with a letter and end with a letter or a digit.

   * It consists of lowercase letters, numbers, underscores (_), or hyphens (\-).

5. Click **OK**.


<span id=".5aSN5Yi26KGo57uT5p6E"></span>
## Copy table structure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Copy table structure only supports copying the original table structure and cannot copy the original table data.</div>


* <div data-tips="true" data-tips-type="tip">Foreign keys will be filtered during the result copying process.</div>


1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, **expand** Table, right\-click the target table, and select **Copy table structure**.

4. In the **Create a new table and copy the table structure** dialog box, configure the following **Parameter** information:

   * **Copy to database**: In the drop\-down list, select the database where the copied table needs to be placed.

   * **Table name**: In the **Table name** text box, customize the name of the table. If it is not set, the **Default** is original table name_copy.

5. Click **OK**.


<span id=".5Yig6Zmk6KGo"></span>
## Delete a table

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A deleted table can not be recovered. And deleting tables may degrade database performance because the database needs to process more files. Exercise caution when performing this operation.</div>



1. Log in to the [Data interaction platform of NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-vedb-for-mysql).

2. On the top menu bar of the **Data interaction platform** page, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Delete table**.

4. In the **Drop table** dialog box, re\-enter the table name in the **Confirm to delete** input box, and click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DataExecCommands](https://docs.byteplus.com/en/docs/DBW/dataexeccommands) |Call the DataExecCommands interfaceAPI to execute an SQL command. |
|[DataSessionKeepAlive](https://docs.byteplus.com/en/docs/DBW/datasessionkeepalive) |Call the DataSessionKeepAlive API to keep an SQL session alive. |
|[DataCloseSession](https://docs.byteplus.com/en/docs/DBW/dataclosesession) |Call the DataCloseSession API to close an SQL session. |
|[DataCancelExec](https://docs.byteplus.com/en/docs/DBW/datacancelexec) |Call the DataCancelExec API to cancel SQL execution. |

---
title: "Table management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/table-management-for-PG"
---

This topic describes how to visually create, delete, and edit tables on the Database Workshop (DBW) console to manage the entire lifecycle of tables.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance, an account, a database and a table have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account), [Creating a database](https://docs.byteplus.com/en/docs/DBW/database-management-for-PG) and [Creating a table](https://docs.byteplus.com/en/docs/DBW/schema-management-for-PG).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


|**Actions** |**Precautions** |
|---|---|
|**Create a table** |* Creating tables on system databases is not supported.<br><br>* When creating a table, the operations must comply with the PG syntax restrictions. |
|**Query a table** |* Querying tables on system databases is not supported.<br><br>* Editing query results is not supported now. |
|**Edit table structure** |* Editing tables on system databases is not supported.<br><br>* Due to time constraints on DDL execution, large tables may fail to execute. Therefore, it is recommended that you do not make structural or index adjustments to large tables on the DBW console.<br><br>* Columns can not be modified if an index or foreign key is set. To adjust, delete the index or foreign key first, and then add the index or foreign key. |
|Delete a table |A deleted table can not be recovered. In addition, deleting a table requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation. |


<span id=".5Yib5bu66KGo"></span>
## Create a table


1. [Log on to the data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **data interaction platform**, expand the **Table**, right\-click the target table, and select **Create table**.

4. On the **Create table@{database name}**  tab, configure the following parameters.

   1. Configure the basic information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Table name** |Custom table name. The rules for table names are as follows:<br><br><br>* The database name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Tables** |From the drop\-down list, select the target table. |
      |**Owner** |Optional. Select the owner of the table from the drop\-down list. |
      |**Tablespace** |Optional. Select the tablespace to which the table belongs from the drop\-down list. Currently, **pg_default** and **pg_global** are supported. |
      |**Fill factor** |Optional. Set the fill factor for the table. |
      |**Remarks** |Optional. Enter remarks for the table. Remarks. It is recommended to provide business\-related information. |
      

   2. On the **Column information** tab, click **Add column** to configure column information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Column name** |Custom column name. Naming rules:<br><br><br>* The column name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Type** |Select the attribute of the column from the drop\-down list. The following types are supported:<br><br><br>* **String**, including types of `char`, `varchar`, `text`, `citext`, `name`, `bytea`, `tsquery`, and `oid`,<br><br>* **Numeric**, including types of `smallint`, integer, `decimal`, `real`, `double precision`, `smallserial`, `serial`, `bigserial`, `int2vector`, `geometry`, `geography`, `money`, `int4range`, `int8range`, `numrange`, `tsrange`, `datarange`, `bit`, `date`, `time`, `timestamp`, `interval`, `boolean`, `enum`, `point`, `line`, `lseg`, `box`, `path`, `polygon`, `circle`, `inet`, `cidr`, `xml`, `macaddr`, `json`, `jsonb`, `uuid`, `regproc`, `regprocedure`, `regoper`, `regoperator`, `regclass`, `regtype`, `regconfig`, and `regdictionary`. |
      |**Array** |Optional. Check the box to select an array as needed. An array can hold multiple values of the same data type, like a list or collection. Check the box to select an array if you want to store multiple similar entries in a row. |
      |**Nullable** |Optional. Set whether to select Nullable as needed. Indicates whether NULL values can be inserted in this column. When Nullable is selected, setting a primary key is not supported. |
      |**Primary key** |Optional. Set whether to select the primary key as needed. When choosing to set a primary key, setting nullable is not supported. |
      |**Default value** |Optional. Set the default value. |
      |**Precision** |Optional. Set the precision. |
      |**Decimal point** |Optional. Set the decimal point position of the column. |
      |**Validation rule** |Optional. Select a validation rule for the column from the drop\-down list. |
      |**Remarks** |Optional. Enter remarks for the column. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a column, click the delete icon in front of the target column serial number.      </div>
      

   3. On the **Index information** tab, click **Add index** to configure index information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Index name** |Custom index name. Naming rules:<br><br><br>* The index name is unique within the table.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Include column** |Select the columns to include from the drop\-down list box. Multiple selections are supported. |
      |**Index type** |Select an index type from the drop\-down list. The following types are supported:<br><br><br>* **index**: This index type represents a performance optimization tool. By creating an index on one or more columns of a table, you can retrieve data faster.<br><br>* **unique**: This index type represents a constraint that ensures all values in a specific column or combination are unique. This index helps with data consistency and integrity. |
      |**Index method** |Select an indexing method from the drop\-down list. The following options are currently supported:<br><br><br>* **btree**: Indicates that the index stores data in a B+ Tree structure.<br><br>* **gist**: Indicates a highly flexible index that can be used for various indexing styles.<br><br>* **Hash**: Indicates that the index can convert data values into unique hash codes using a hash function. This index can only be used for equality queries.<br><br>* **spgist**: Indicates that the index is a type that can use any non\-overlapping partitioning method, which can process point data and perform effective range lookups. |
      |**Concurrent?**  |Select whether to enable concurrency as needed. After being selected, normal read and write operations are allowed during index creation, reducing blocking time. |
      |**Remarks** |Optional. Enter remarks for the index. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete an index, select the target index and click <strong>Delete index</strong>.      </div>
      

   4. On the **Foreign key** tab, click **Add foreign key** to configure foreign key information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Foreign key name** |Custom foreign key name. |
      |**Definition** |Click **Edit**. In the **Definition** dialog box, click **Add a row**, set the **Include column**, **Reference table**, and **Reference column** of the definition, and click **OK**. |
      |**Deferrable** |Optional. Check whether it can be delayed as needed. If the extension is set at the same time after checking, the foreign key constraint check will be postponed until the transaction is submitted. |
      |**Deferred** |Optional. Check the box to postpone as needed. Check this box to indicate that the foreign key constraint can be checked until the end of the transaction. You must check both deferred and deferrable for the foreign key constraint check to take effect at the end of the transaction. |
      |**Exact match** |Optional. Check whether to enable exact match as required. If this option is selected, the values of the foreign key columns of the subtable should be exactly the same as the values of the primary key columns of the primary table when applying the foreign key constraint. A row is allowed to be inserted into or updated to the subtable only when the values in the foreign key column of the subtable exist in the primary key column of the primary table. |
      |**Do not verify** |Optional. Check whether not to validate as required. If selected, the constraint is not immediately checked when the foreign key constraint is created or modified. In this scenario, there may be rows that violate the new constraint unless an additional validation is performed. |
      |**When deleting** |Optional. Select how to handle foreign key data in the subtable when the referenced main data (from the primary table) is deleted from the drop\-down list. The values are as follows:<br><br><br>* **NO ACTION**: (Default policy) If a row in the primary table is deleted, and there are foreign keys in the subtable that depend on that row, the deletion operation will be blocked.<br><br>* **RESTRICT**: Indicates that the deletion will be blocked immediately if there are unfinished transactions.<br><br>* **CASCADE**: Indicates that if a row in the primary table is deleted, all foreign keys in the subtable that depend on that row will also be deleted. This is usually used to maintain the referential integrity of the database, especially in relationships between primary tables and subtables.<br><br>* **SET NULL**: Indicates that if a row in the primary table is deleted, all foreign keys in the subtable that depend on that row will be set to NULL. This is a non\-strict ON DELETE policy that allows deleting rows in the primary table without deleting rows in the subtable, simply setting the foreign keys in the subtable to NULL.<br><br>* **SET DEFAULT**: Indicates that if a row in the primary table is deleted, all foreign keys in the subtable that depend on that row will be set to the default value in their column definition. This is a flexible ON DELETE policy that uses the column definition's default value instead of directly deleting the row in the subtable or setting it to NULL. When using this policy, make sure to set a default value. |
      |**When updating** |Optional. Select how to handle foreign key data in the subtable when the referenced main data (from the primary table) is updated from the drop\-down list. The values are as follows:<br><br><br>* **NO ACTION** (Default): If an attempt is made to update referenced data in the primary table and foreign keys in the subtable are associated with it, the update operation will be blocked.<br><br>* **RESTRICT**: Indicates that the update will be blocked immediately if there are uncompleted transactions.<br><br>* **CASCADE**: If the referenced data is updated (for example, if the primary key value changes), then all foreign key data referencing this data will be automatically updated to the new value.<br><br>* **SET NULL**: If the referenced data is updated, then all foreign keys referencing the data will be set to NULL. Using this method requires ensuring that the foreign key column allows NULL values.<br><br>* **SET DEFAULT**: If the referenced data is updated, then all foreign keys referencing this data will be set to the default value of their column. Using this method requires ensuring that a default value is set for the foreign key column. |
      |**Remarks** |Optional. Enter remarks for the foreign key. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a foreign key, select the target foreign key and click <strong>Delete foreign key</strong>.      </div>
      

   5. On the **Exclusive constraint** tab, click **Add exclusive constraint**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom exclusive constraint name. |
      |**Definition** |Click **Definition**, in the **Definition** dialog box, click **Add a row**, set **Field**, **Operator class**, **Sort**, **Null ordering**, **Operator**, and click **OK**. You can also click **Delete** to delete the added definition. |
      |**Tablespace** |Optional. Select a tablespace from the drop\-down list. |
      |**Access method** |Optional. Select an access method from the drop\-down list. Currently, **btree**, **gist**, **hash**, and **spgist** are supported. |
      |**Fill factor** |Optional. Set the fill factor of the exclusion constraint. |
      |**Deferrable** |Optional. Check whether it can be delayed as needed. |
      |**Deferred** |Optional. Check the box to postpone as needed. |
      |**Remarks** |Optional. Enter remarks for the exclusive constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete an exclusive constraint, select the target exclusive constraint and click <strong>Delete exclusive constraint</strong>.      </div>
      

   6. On the **Unique constraint** tab, click **Add unique constraint**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom unique constraint name. |
      |**Field** |From the drop\-down list, select the field. |
      |**Tablespace** |Optional. Select a tablespace from the drop\-down list. |
      |**Fill factor** |Optional. Set the fill factor for the unique constraint. |
      |**Deferrable** |Optional. Check whether it can be delayed as needed. |
      |**Deferred** |Optional. Check the box to postpone as needed. |
      |**Remarks** |Optional. Enter remarks for the unique constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a unique constraint, select the target unique constraint and click <strong>Delete unique constraint</strong>.      </div>
      

   7. On the **Check constraint** tab, click **Add check**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom check constraint name. |
      |**Check** |Check if it is a Boolean expression that defines the conditions that a column or combination of columns must meet. |
      |**Non\-inheritance** |Optional. Check if it is non\-inheritance as needed. When selected, this check constraint can only be applied to the current table and will not be applied to any subtables inherited from this table. |
      |**Do not verify** |Optional. Check whether not to validate as required. When checked, RDS for PostgreSQL will not check whether all rows already existing in the table meet the new check constraint. This will only apply the constraint to rows inserted or updated later. |
      |**Remarks** |Optional. Enter remarks for the check constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To delete a check constraint, select the target check constraint and click <strong>Delete check constraint</strong>.      </div>
      

5. Click **Submit**.

6. In the **SQL preview** dialog box, confirm the statement for creating a table.

7. Click **Execute**.


<span id=".57yW6L6R6KGo57uT5p6E"></span>
## Edit table structure


1. [Log on to the data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database to select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Edit table structure**.

4. In the **Edit table structure_{table name@database name}**  command execution area, edit the table's **Basic information**, **Column information**, **Index**, **Foreign key**, **Exclusive constraint**, **Unique constraint**, or **Check constraint**. For more information, refer to [Creating a table](https://docs.byteplus.com/en/docs/DBW/table-management-for-PG#.5Yib5bu66KGo).

5. Click **Submit**.

6. In the **Execute SQL** dialog box, confirm the change statement.

7. Click **Execute**.


<span id=".5p-l6K-i6KGo"></span>
## Query a table


1. [Log on to the data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database to select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Query table**.

4. In the **SQL query** command execution area, click **Execute (F8)**  or press **F8**.

   In the **Execution rResult** area, you can view the query result of the table. At the same time, you can also manage the table, as shown in the following table:

   
   |**Actions** |**Description** |
   |---|---|
   |**Add rows** |1. In the bottom menu bar of the **Execution result** area, click **Add row**.<br><br>2. Click the icon after the target column NULL<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_712773616342c1e13ec1b4393c5dd23e.png) </span>In the **Edit field: Field name** dialog, set the parameter information for the row to be added.<br><br>3. (Optional) If you need to cancel this change, click **Reset**.<br><br>4. Click **Submit**. Verify the SQL statement in the **Execute SQL** dialog box, and click **Execute**. |
   |**Delete row** |1. In the **Execution result** area, select the target row to delete and click **Delete row**.<br><br>2. (Optional) If you need to cancel this change, click **Reset**.<br><br>3. Click **Submit**. In the **Confirm whether the SQL is accurate and execute?**  dialog box, confirm that the SQL statement is correct, then click **SQL is valid. Execute now**. |
   |**Modify Row** |1. In the **Execution result** area, click to modify the row that needs to be changed<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe85b81933c53a1797d3293b2382da52.png) </span>icon.<br><br>2. In the **Edit field: Field name** dialog, modify the field information and click **OK**.<br><br>3. (Optional) If you need to cancel this change, click **Reset**.<br><br>4. Click **Submit**. In the **Confirm SQL accuracy and execute** dialog, verify that the SQL statement meets the requirements, then click **SQL is valid. Execute now**. |
   


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After a table is successfully queried, editing of the execution results is only supported for tables that meet the following conditions:</div>



* <div data-tips="true" data-tips-type="default">Single table query.</div>


* <div data-tips="true" data-tips-type="default">The table must have a primary key or a unique index in all columns.</div>


* <div data-tips="true" data-tips-type="default">The execution result is not queried through the table alias.</div>



<span id=".5Yig6Zmk6KGo"></span>
## **Delete a table**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A deleted table can not be recovered. In addition, deleting a table requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation.</div>



1. [Log on to the data interaction platform for RDS for PostgreSQL](https://docs.byteplus.com/en/docs/DBW/log-in-database-interaction-platform-for-PG).

2. On the top menu bar of the **Data interaction platform** page, click the icon after Database and select the target database.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fc8cdb512061347c970a02fd4daf5aa.jpeg) </span>icon after the database, select the target database.

3. In the visual area of the **Data interaction platform**, expand the **Table**, right\-click the target table, and select **Delete table**.

4. In the **Confirm to delete** input box of the **Delete table** dialog, re\-enter the table name and click **OK**.

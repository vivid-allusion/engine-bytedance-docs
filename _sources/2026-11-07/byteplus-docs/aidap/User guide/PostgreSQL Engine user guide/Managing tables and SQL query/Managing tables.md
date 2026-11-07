---
title: "Managing tables"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Managing_tables_user_guide"
---

This topic describes how to visually create, delete, and edit tables on the Database Workshop (DBW) console to manage the entire lifecycle of tables.

<span id="lor2Gc0b"></span>
## Function description

In the AIDAP Data Interaction Platform, there are three ways of table management. This topic takes table management as an example to describe how to visually create, delete, and edit tables through table management.


* You can create, query, edit, or delete tables by command. For more information, see [Command operations](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Command_operations).

* You can create, query, edit, or delete tables through the **SQL editor** operation area.

* You can visually create, query, edit, or delete tables through the **Table management** operation area.


Table query in SQL editing queries table contents using SQL commands. Table query in Table management performs visual query of table contents.

<span id="7vk1XbcK"></span>
## Prerequisites

Workspace, database, schema, and account have been created. For detailed operations, please refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace), [Creating a database](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_database), [Creating a schema](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Managing_schema?#5tgTpMZk), and [Creating an account](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_an_account).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The account you create must have the corresponding permissions for querying and modifying the corresponding database.</div>


<span id="yiVb8LQi"></span>
## Precautions

The creation, deletion, and other operations you perform may affect the online business operation. It is recommended to perform them during off\-peak hours.


|**Actions** |**Precautions** |
|---|---|
|**Create a table** |* Creating tables on system databases is not supported.<br><br>* When creating a table, the operations must comply with the PG syntax restrictions. |
|**Query a table** |* Querying tables on system databases is supported.<br><br>* Copying query results is supported, editing query results is not supported yet. |
|**Edit table (Basic information and table structure)** <br><br> |* Editing tables on system databases is not supported.<br><br>* Due to time constraints on DDL execution, large tables may fail to execute. Therefore, it is recommended that you do not make structural or index adjustments to large tables on the DBW console.<br><br>* Columns can not be modified if an index or foreign key is set. To adjust, delete the index or foreign key first, and then add the index or foreign key. |
|**Rename a table** |* Renaming tables on system databases is not supported.<br><br>* After renaming the table, you will not be able to access the table through the original table name. Please proceed with caution. |
|**Delete a table** |* Deleting tables in the system database is not supported.<br><br>* A deleted table can not be recovered. In addition, deleting a table requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation. |
|**Clear the table** |* Not supported yet to clear the table on the system database.<br><br>* Data in the table cannot be recovered after being cleared, handle with caution. |


<span id="FPTVTGLm"></span>
## Create a table


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span> **SQL query** in the center navigation bar on the page, then click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name, branch name, and database name on the top left of the page in turn to select the target workspace, target branch, and target database from the drop\-down list respectively to enter the **SQL query** page of the target database.

4. In the **SQL query** page's schema list, click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> in front of the target schema, expand the schema. You can create tables through either of the following two methods:

   * Method one: Right\-click the table under the target schema, then click **Create table**.

   * Method two: click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d578b34d80e5c7df4d90b257017379.png)<sub> </sub></span> on the right of the table under the target schema, select **Create table**.

5. On the pop\-up **Create table** tab, configure the following parameter information.

   1. Configure the basic information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Table name** |Custom table name. The rules for table names are as follows:<br><br><br>* The database name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Schema** |Select the target schema from the drop\-down list. |
      |**Owner** |Optional. Select the owner of the table from the drop\-down list. |
      |**Remarks** |Optional. Enter remarks for the table. Remarks. It is recommended to provide business\-related information. |
      

   2. On the **Column information** tab, click **Add column** to configure column information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Column name** |Custom column name. Naming rules:<br><br><br>* The column name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Type** |Select the attribute of the column from the drop\-down list. The following types are supported:<br><br><br>* **String**, including types of `char`, `varchar`, `text`, `citext`, `name`, `bytea`, `tsquery`, and `oid`,<br><br>* **Numeric**, including types of `smallint`, `integer`, `decimal`, `real`, `double`, `precision`, `smallserial`, `serial`, `bigserial`, `int2vector`, `geometry`, `geography`, `money`, `int4range`, `int8range`, `numrange`, `tsrange`, `datarange`, `bit`, `date`, `time`, `timestamp`, `interval`, `boolean`, `enum`, `point`, `line`, `lseg`, `box`, `path`, `polygon`, `circle`, `inet`, `cidr`, `xml`, `macaddr`, `json`, `jsonb`, `uuid`, `regproc`, `regprocedure`, `regoper`, `regoperator`, `regclass`, `regtype`, `regconfig`, and `regdictionary`. |
      |**Primary key** |Optional. Set whether to select the primary key as needed. When choosing to set a primary key, setting nullable is not supported. |
      |**Nullable** |Optional. Set whether to select Nullable as needed. Indicates whether NULL values can be inserted in this column. When Nullable is selected, setting a primary key is not supported. |
      |**Default value** |Optional. Set the default value. |
      |**Other configurations** |* **Validation rule**: Optional. Select a validation rule for the column from the drop\-down list.<br><br>* **Remarks**: Optional. Enter remarks for the column.<br><br>* **Array**: Optional. Set whether to check the array as needed. An array can hold multiple values of the same data type, like a list or collection. Check the box to select an array if you want to store multiple similar entries in a row. |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete a column, you can click the <strong>Delete icon</strong> to the left of this column.      </div>
      

   3. On the **Index information** tab, click **Add index** to configure index information, as shown in the following table.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Index name** |Custom index name. Naming rules:<br><br><br>* The index name is unique within the table.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
      |**Include column** |Select the columns to include from the drop\-down list box. Multiple selections are supported. |
      |**Index type** |Select an index type from the drop\-down list. The following types are supported:<br><br><br>* **index**: This index type represents a performance optimization tool. By creating an index on one or more columns of a table, you can retrieve data faster.<br><br>* **unique**: This index type represents a constraint that ensures all values in a specific column or combination are unique. This index helps with data consistency and integrity. |
      |**Index method** |Select an indexing method from the drop\-down list. The following options are currently supported:<br><br><br>* **btree**: Indicates that the index stores data in a `B+ Tree` structure.<br><br>* **gist**: Indicates a highly flexible index that can be used for various indexing styles.<br><br>* **Hash**: Indicates that the index can convert data values into unique hash codes using a hash function. This index can only be used for equality queries.<br><br>* **spgist**: Indicates that the index is a type that can use any non\-overlapping partitioning method, which can process point data and perform effective range lookups. |
      |**Concurrent?**  |Select whether to enable concurrency as needed. After being selected, normal read and write operations are allowed during index creation, reducing blocking time. |
      |**Remarks** |Optional. Enter remarks for the index. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete an index, you can click the <strong>Delete icon</strong> to the left of this column.      </div>
      

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
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete a foreign key, you can click the <strong>Delete icon</strong> to the left of this column.      </div>
      

   5. On the **Exclusive constraint** tab, click **Add exclusive constraint**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom exclusive constraint name. |
      |**Definition** |Click **Definition**, in the **Definition** dialog box, click **Add a row**, set **Field**, **Operator class**, **Sort**, **Null ordering**, **Operator**, and click **OK**. You can also click **Delete** to delete the added definition. |
      |**Access method** |Optional. Select an access method from the drop\-down list. Currently, **btree**, **gist**, **hash**, and **spgist** are supported. |
      |**Deferrable** |Optional. Check whether it can be delayed as needed. |
      |**Deferred** |Optional. Check the box to postpone as needed. |
      |**Remarks** |Optional. Enter remarks for the exclusive constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete an exclusive constraint, you can click the <strong>Delete icon</strong> to the left of the exclusive constraint.      </div>
      

   6. On the **Unique constraint** tab, click **Add unique constraint**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom unique constraint name. |
      |**Field** |From the drop\-down list, select the field. |
      |**Deferrable** |Optional. Check whether it can be delayed as needed. |
      |**Deferred** |Optional. Check the box to postpone as needed. |
      |**Remarks** |Optional. Enter remarks for the unique constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete a unique constraint, you can click the <strong>Delete icon</strong> to the left of the unique constraint.      </div>
      

   7. On the **Check constraint** tab, click **Add check**, as shown in the table below.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Name** |Custom check constraint name. |
      |**Check** |Check if it is a Boolean expression that defines the conditions that a column or combination of columns must meet. |
      |**Non\-inheritance** |Optional. Check if it is non\-inheritance as needed. When selected, this check constraint can only be applied to the current table and will not be applied to any subtables inherited from this table. |
      |**Do not verify** |Optional. Check whether not to validate as required. When checked, RDS for PostgreSQL will not check whether all rows already existing in the table meet the new check constraint. This will only apply the constraint to rows inserted or updated later. |
      |**Remarks** |Optional. Enter remarks for the check constraint. Remarks. It is recommended to provide business\-related information. |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When you need to delete a check constraint, you can click the <strong>Delete icon</strong> to the left of the check constraint.      </div>
      

5. Click **Submit**.

6. In the **SQL preview** dialog box, confirm the statement for creating a table.

7. Click **Execute**.


<span id="FWGvJq2n"></span>
## Edit table


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span>**SQL query**, then click the Workspace name, branch name, and the icon to the right of the database name in the top left corner of the page in sequence<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span>, select the target Workspace, target branch, and target database respectively in the pop\-up drop\-down list to enter the **SQL query** page of the target database.

4. In the **SQL query** page's schema list, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> before the target schema, expand the schema.

5. Under the target schema, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> before the table, expand the table.

6. In the expanded table list, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d578b34d80e5c7df4d90b257017379.png)<sub> </sub></span> after the target table, select **Edit table**.

7. In the popped\-up **Edit table** tab, after editing the table's **Basic information**, **Column information**, Index, Foreign keys, **Exclusive constraint**, **Unique constraint** or **Check constraint**, click **Submit**. For more information, refer to [Creating a table](https://docs.byteplus.com/en/docs/330/106664#FPTVTGLm).

8. In the **Execute SQL ** dialog box, confirm the statement to be executed.

9. Click **Execute**.


<span id="skdpzakG"></span>
## Query a table

In the Table management tab, click **Filter condition** to show or hide the where query condition of the table contents.


1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span> **SQL query** in the center navigation bar on the page, then click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name, branch name, and database name on the top left of the page in turn to select the target workspace, target branch, and target database from the drop\-down list respectively to enter the **SQL query** page of the target database.

4. In the **SQL query** page's schema list, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> before the target schema, expand the schema.

5. Under the target schema, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> before the table, expand the table.

6. In the expanded table list, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d578b34d80e5c7df4d90b257017379.png)<sub> </sub></span> after the target table, select **Query table**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Enter the table name to be queried in the Search table filter box and press Enter. Table names support fuzzy search.   </div>
   

7. In the popped\-up **SQL query** tab's SQL editor, enter the query statement to query the table contents. In the table in the execution result area below, you can view all results that meet the filter conditions.

   Copying query results is supported, editing query results is not supported now. At the same time, you can also manage the table, as shown in the following table:

   
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



<span id="TAltRzuw"></span>
## **Delete a table**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A deleted table can not be recovered. In addition, deleting a table requires the database to process a large number of files, which may block the processing of other transactions and degrade database performance. Exercise caution when performing this operation.</div>



1. Log in to the [AI Native BaaS for Supabase](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Go to the **SQL query** page of the target database. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_906ef41b4eb1b26873ff9c3cc9ddbc6d.png)<sub> </sub></span> **SQL query** in the center navigation bar on the page, then click the icon <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name, branch name, and database name on the top left of the page in turn to select the target workspace, target branch, and target database from the drop\-down list respectively to enter the **SQL query** page of the target database.

4. In the **SQL query** page's schema list, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span> before the target schema, expand the schema.

5. Under the target schema, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b624a5d69c2634d9e4c9ff0359f22c21.png)<sub> </sub></span>to expand the table.

6. In the expanded table list, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d578b34d80e5c7df4d90b257017379.png)<sub> </sub></span>after the target table and select **Delete table**.

7. In the **Confirm to delete** input box of the **Delete table** dialog, re\-enter the table name and click **OK**.

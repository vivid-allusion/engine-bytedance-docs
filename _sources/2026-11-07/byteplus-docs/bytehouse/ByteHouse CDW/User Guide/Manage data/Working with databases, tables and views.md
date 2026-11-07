---
title: "Working with databases, tables and views"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-databases-tables-and-views"
---

A database is a logical grouping of data. Each database contains many tables and views. Tables are where the data is stored, comprising structured rows and columns. Views are saved queries that depend on tables. When accessing the view, a query is executed in the background and results are returned. This article introduces how to manage databases and tables using both visualization and SQL commands.

<span id="ddba6796"></span>
## Database

Each database belongs to an account. You can only access databases that belong to their own account when they have permissions.

<span id="1e28316b"></span>
### Create database


<Tabs>
<Tab zoneid="YpN4OCd9QP" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. In the ByteHouse Console, click the **Database** tab.

2. Click the **New\>Create Database** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6697f6f190354238a24ada66930aa418~tplv-goo7wpa0wc-image.image) </span>

3. In the new database popup window, enter the database name and description.


</Tab>
<Tab zoneid="H7PME7MQY4" title="SQL">
<TabTitle>SQL</TabTitle>

You can run the following command to create a database in the **ByteHouse Console SQL Worksheet**.

```sql
CREATE DATABASE my_database01;
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Database names can only contain <strong>alphanumeric</strong> characters <code>a-z 0-9</code> and <strong>underline</strong> <code>_</code>. All names will be automatically converted to <strong>lowercase</strong>.</div>


<span id="c70cfc11"></span>
### **Set default database**

Once the default database is set, you do not need to specify the database name when performing query table operations; the system will automatically use the default database for queries.


<Tabs>
<Tab zoneid="NEN0SEuTUb" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse Console, click on the **Tenant Management** tab, click on the **Parameter Setting**, and view the default parameters.

2. Click the **Edit** button for the default database row.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e04eb0b074241a696d91d26a5383da2~tplv-goo7wpa0wc-image.image) </span>

3. Select the default database from the drop\-down list.

4. Click **Confirm**.


</Tab>
<Tab zoneid="Fo6fckHjxj" title="SQL">
<TabTitle>SQL</TabTitle>

You can run the following command to set the default database in the **ByteHouse Console SQL Worksheet**.

```SQL
SET DEFAULT DATABASE my_database01;
```


For example, if you set the default database to `my_database01`, and within `my_database01` there is a table named `demo_table`, you can query it like this:

```SQL
SELECT * FROM demo_table;
```


If you have not set a default database, you need to query using the following command:

```SQL
SELECT * FROM my_database01.demo_table;
```



</Tab>
</Tabs>


<span id="2d642e05"></span>
### Delete Database


<Tabs>
<Tab zoneid="lpP0hym01f" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse Console, click the **Database** tab. In the search bar, enter the target database name and click the **Search** button.

2. Click on the database name to enter the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fffe64d8ce2439cbefa45e8da3f9512~tplv-goo7wpa0wc-image.image) </span>

3. Click on the `...` in the current database management page. Button.

4. Click the **Delete Database** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67d4491f026c4306b0b4170323f135b0~tplv-goo7wpa0wc-image.image) </span>

5. In the popup window, confirm the database to be deleted by clicking **Confirm**, to delete the current database.


</Tab>
<Tab zoneid="bYRb9f53kP" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following command in the **ByteHouse Console \> SQL Worksheet** to delete the specified database.

```sql
DROP DATABASE my_database01;
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting the database will also delete all the tables in it.</div>


<span id="e3916eb2"></span>
## Table

A table is a place for storing data, and each table belongs to a database. You can create a table through different methods like visual pages, SQL commands, or [importing data](https://docs.byteplus.com/en/docs/bytehouse/docs-data-import-e8caa19b).

Tables in ByteHouse support configuration of different types of attributes.


|Name |Description |
|---|---|
|Table name |Required. Customize the table name. The naming rules are as follows:<br><br><br>* The name can only contain letters, numbers, and an underline "_".<br><br>* Up to 128 characters. |
|Description |Optional. Provide a custom description for calculation groups to help differentiate them in subsequent uses. |
|Engine |The type of engine determines the method of data storage and access. Currently, only support `CnchMergeTree`. By default, visualization\-based table creation uses `CnchMergeTree` and does not require configuration. |
|Order Key |Required. If a primary key is not specified, the column is used as the primary key. Key sorting is used to determine the actual storage method of data in the database. Users can specify up to 5 columns using key sorting. |
|Partition Key |Optional. Partition keys determine which data partition each row in the table belongs to, dividing a large table into smaller sections. When creating tables, you can define partitions using partition keys; reasonable partitioning can greatly reduce the amount of data that needs to be scanned during queries. ByteHouse supports setting partition keys as either time fields or non\-time fields, which you can specify as needed when creating tables. |
|Expire Time TTL |Optional. The specific duration of data retention can be set as needed if configured through the visual table creation process.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After setting the TTL expiration time, the system will automatically <strong>delete the table</strong> once the data exceeds the retention period.</div><br> |
|Unique key |Optional. Ensure that users can query the latest value of the unique key. |
|Bucketing key |Optional. For each table or partition, further divide into buckets by specifying a bucketing key (Cluster Key), hashing the data in the column for finer granularity division, thus improving query and sampling efficiency. |
|Primary key |Optional. A primary key is used to organize data files and impose constraints on the unique identification of each record in the data table. The primary key must contain "unique" values and cannot include "null" values. A data table can only have one primary key. |
|Sampling Key |Optionally defining a sampling key can partition a sample of the data. If specified, it must be included in the sorting key. The result of the sampling expression must be an unsigned integer. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Besides the sampling key, once the data table is created, sorting keys, partition keys, etc., cannot be changed, so configure them carefully.</div>


* <div data-tips="true" data-tips-type="warning">After creating the table, only the <strong>retention time</strong> can be updated from the table properties. Columns can still be added after creation.</div>



<span id="85f0f918"></span>
### Create Table

Tables are always created within the database. When a database is not specified, ByteHouse uses the default database according to the user's preference.


<Tabs>
<Tab zoneid="OjdB2x8AMU" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. In the ByteHouse console, click on the **Database** tab.

2. Click the  **+New\>Create table** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ce7aa6ec66749ae9957981763308e66~tplv-goo7wpa0wc-image.image) </span>

3. On the Create Table page, configure the table properties. You can refer to the descriptions in the aforementioned property table to configure the table properties.


</Tab>
<Tab zoneid="voI84f4yr3" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following example commands in the **ByteHouse Console\> SQL Worksheet** to create a table. You can replace the database and table names in the commands with the names of your target database and table. You can configure the table properties based on the descriptions in the aforementioned property table.

```sql
CREATE TABLE `test_db2`.`my_table` 
(
    `id` UInt64,
    `name` String,
    `started` DateTime
)
ENGINE=`CnchMergeTree()`
PRIMARY KEY `id`
ORDER BY `id`
PARTITION BY `toYYYYMMDD`(`started`); 
```


ByteHouse supports setting partition keys as time fields and non\-time fields and has designed different DDL commands based on field type validation. You can create tables using the following commands as needed.


* If you plan to set the partition key as a time field, such as day, month, year, etc., you can refer to the following commands to create tables.

   ```SQL
   CREATE TABLE `table_name`
   (
           `expr` type
   )
   ENGINE = CnchMergeTree
   PARTITION BY (toDate(toStartOfDay(toDate(`expr`))))
   ```
   

* If you plan to set the partition key as null, you can refer to the following commands to create tables.

   ```SQL
   CREATE TABLE `table_name`
   (
           `expr` type
   )
   ENGINE = CnchMergeTree
   PARTITION BY `expr`
   ```
   

* If you plan to set the partition key as custom, such as `toYYYYMM(`expr`)`, you can refer to the following commands to create tables.

   ```SQL
   CREATE TABLE `table_name`
   (
           `expr` type
   )
   ENGINE = CnchMergeTree
   PARTITION BY (toYYYYMM(`expr`))
   ```
   


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can refer to <a href="https://docs.byteplus.com/docs/bytehouse/bytehouse-table-creation-best-practice">ByteHouse table creation best practices</a> to learn more about table configuration.</div>


<span id="ed1ae270"></span>
### Modify Table


<Tabs>
<Tab zoneid="WpYrXE2RCa" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse console, click the **Databases** tab.

2. In the search bar, enter the target database name and click the **Search** button.

3. Click on **database name** to access the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe33f3b23e8546f1b312cb551d4ac0bd~tplv-goo7wpa0wc-image.image) </span>

4. Click on **table name** to access the current table management page.

5. Click the **Edit** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53f4c2f37c9c41ccbc83debecf7f4895~tplv-goo7wpa0wc-image.image) </span>

6. In the table editing page, you can change column configurations. The current visualization mode supports the following operations for modifying tables:

   * Add columns;

   * Delete columns not used as keys;

   * Modify columns not used as keys, supporting changes in column name, data type, default value, expression, comments, and nullable status.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a700828cfdc4e1682cd718b6e05a834~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to modify other column properties, you can refer to the SQL command method or <a href="https://docs.byteplus.com/docs/bytehouse/alter-statement">Alter statement (ALTER)</a> to alter the table.   </div>
   

7. After adjustments, click **Save Changes**, and the system will update the table as required.


</Tab>
<Tab zoneid="z2oLcWTYs7" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute ALTER commands in the ByteHouse c`ALTER commands in the ByteHouse console> SQL worksheet` to change table properties such as adding or deleting columns, adding comments, adjusting TTL expiration times, and modifying table names.


* Add columns, delete columns:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting columns used as keys is not supported.   </div>
   

   ```sql
   -- 添加列
   ALTER TABLE my_database01.my_table ADD COLUMN new_column UInt32;
   
   -- 删除列
   ALTER TABLE my_database01.my_table DROP COLUMN old_column UInt32;
   ```
   

* Add column comments:

   ```sql
   ALTER TABLE my_database01.my_table COMMENT COLUMN old_column 'my comment'
   ```
   

* Adjust TTL expiration times:

   ```sql
   -- 添加 TTL
   ALTER TABLE my_database01.my_table MODIFY TTL INTERVAL 3 DAY;
   
   -- 移除 TTL
   ALTER TABLE my_database01.my_table REMOVE TTL
   ```
   

* Modify table names:

   ```sql
   RENAME TABLE my_database01.my_table TO my_database01.new_table;
   ```
   


</Tab>
</Tabs>


<span id="7cdff4d0"></span>
### Clone Table

Cloning a table means creating a new table using the same schema and data as the **original table**.


<Tabs>
<Tab zoneid="LQSEHBSXAT" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse console, click on the **database** tab.

2. In the search bar, enter the name of the target database and click the **search** button.

3. Click on **Database Name** to enter the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe33f3b23e8546f1b312cb551d4ac0bd~tplv-goo7wpa0wc-image.image) </span>

4. Click on **Table Name** to enter the current table management page.

5. Click on `...` at the top right corner of the table management page. Button.

6. Click on the **Clone** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6dc056abb444345853ea27c7d26814a~tplv-goo7wpa0wc-image.image) </span>

7. On the clone table page, select the database where the new table will be placed, enter the table name, and fill in the table description as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1f8ff64921f4ca594f8de8266902e1d~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The naming rules for data tables are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Names can only contain letters, numbers, and underscores "_".   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A maximum of 128 characters.   </div>
   

8. After completing the form, click **OK** to clone the table. The system will automatically redirect to the newly created clone table page, where you can manage the table as needed.


</Tab>
<Tab zoneid="yBsQJwyvJO" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following commands in **ByteHouse Console\> SQL Worksheets** to clone a specified table.

```sql
CLONE TABLE orignal_db.orginal_tableINTO new_db.new_tableCOMMENT 'my newly cloned table'
```



</Tab>
</Tabs>


<span id="2afc156f"></span>
### Delete Table


<Tabs>
<Tab zoneid="MDhhOIuHix" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse console, click the **Database** tab.

2. In the search bar, enter the target database name and click the **Search** button.

3. Click on the **Database Name** to enter the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe33f3b23e8546f1b312cb551d4ac0bd~tplv-goo7wpa0wc-image.image) </span>

4. Click on the **Data Table Name** to enter the current data table management page.

5. Click on the `...` at the top right of the data table management page. Button.

6. Click the **Delete Data Table** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d412f8c509483984838699fc46022d~tplv-goo7wpa0wc-image.image) </span>

7. In the popup, confirm the data table to be deleted and click **OK** to delete the current data table.


</Tab>
<Tab zoneid="zSgyacAyeA" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following commands in the **ByteHouse Console\> SQL Worksheet** to delete a specified table.

```sql
DROP TABLE my_database01.my_table;
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The table cannot be deleted when there are views dependent on it. Before deleting a table, you must first delete the views that depend on it.</div>


<span id="05311fb5"></span>
## View

A view is a stored query. When accessing the view, it runs subsequent queries and displays data using the query results.

<span id="9f6b9860"></span>
### Create View


<Tabs>
<Tab zoneid="qBlCoO3wDb" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse console, click on the **Database** tab.

2. In the search bar, enter the target database name and click the **Search** button.

3. Click on the **Database Name** to enter the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe33f3b23e8546f1b312cb551d4ac0bd~tplv-goo7wpa0wc-image.image) </span>

4. Click the  **+View** button.

5. Click the **Create View** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92ade652d6764f89b6a88717ab8d96fb~tplv-goo7wpa0wc-image.image) </span>

6. On the view creation page, enter the view name, description, and the SQL statement you need to store.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">View names can only contain letters, numbers, and underscores "_", and support up to 128 characters.   </div>
   

7. Click **Create**, and the system will automatically create and display the view. You can view the column names and data preview on the view page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc29c3f8f76e407e958062b384f69cb6~tplv-goo7wpa0wc-image.image) </span>

   You can also click the DDL button on the page to view the SQL statement used to create the view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88b262454dc3480db09e154780effa0b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Vy5uB7yZCi" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following commands in the **ByteHouse Console\> SQL Worksheet** to create a view.

```sql
CREATE VIEW my_database01.my_view AS SELECT * FROM my_database01.my_table;
```



</Tab>
</Tabs>


<span id="e7987146"></span>
### Delete View


<Tabs>
<Tab zoneid="ygQBRlCqoy" title="Visualization">
<TabTitle>Visualization</TabTitle>

1. On the ByteHouse Console, click the **Database** tab.

2. In the search bar, enter the name of the target database and click the **search** button.

3. Click on the **Database Name** to enter the current database management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe33f3b23e8546f1b312cb551d4ac0bd~tplv-goo7wpa0wc-image.image) </span>

4. Click the **View** tab.

5. Click the **Delete** button in the view operation column to delete the current view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac7522250b5746ee95db078ba45a37c1~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="MMgLXMlxmQ" title="SQL">
<TabTitle>SQL</TabTitle>

You can execute the following commands in the **ByteHouse Control Console SQL Worksheet** to delete a specific view.

```sql
DROP VIEW my_database01.my_view;
```



</Tab>
</Tabs>

---
title: "SQL Worksheet"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-query-editor-and-worksheet"
---

The SQL worksheet is an SQL editor provided by the ByteHouse Cloud Data Warehouse Console. It supports writing and executing SQL queries, viewing results, and efficiently managing query results to improve data processing efficiency. This tutorial explains how to use SQL worksheets.

<span id="c7379740"></span>
# Function overview

The SQL worksheet page in ByteHouse Cloud Data Warehouse provides a feature\-rich interface for querying and analysis. You can use it to write and submit SQL queries, and view query results. On this page, you can perform DML, DDL, DCL, and other operations, execute multiple statements in a single run, save and manage worksheets, and add SQL parameter groups during execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4df98437d8b9451cb8351f9c56e1eb01~tplv-goo7wpa0wc-image.image) </span>

<span id="d76cc7cf"></span>
# Create and manage worksheets

ByteHouse SQL worksheets provide operations such as creating, naming, saving, sharing, archiving, deleting worksheets, and other operations.

<span id="f7a9eee8"></span>
## Create and name a worksheet

On the right side of the top navigation bar on the SQL worksheet page, click the + button to create a new worksheet. You can click the worksheet tab in the tab bar to assign a custom name to the worksheet (for example, `Sales analysis`). To modify the name of a worksheet that has already been set, click the worksheet name again to edit it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97e05843bb20492cb94519fc333178a7~tplv-goo7wpa0wc-image.image) </span>

<span id="43dbcb6f"></span>
## Save a worksheet

ByteHouse supports automatically saving the worksheet while you enter SQL statements. You can also click the **Save** button in the upper right corner to save the current worksheet.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9c1176443cb48a0ab18ef7347a64187~tplv-goo7wpa0wc-image.image) </span>

<span id="3e58d813"></span>
## Open a worksheet

After saving the worksheet, if you need to open a closed worksheet, click the **Saved worksheets** icon in the left sidebar, then click the worksheet name to open it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6991e9a7de49dbada35f8ac9778b8b~tplv-goo7wpa0wc-image.image) </span>

<span id="feb0dcbe"></span>
## Share worksheets

You can share a saved worksheet with a specified role, and users who have that role will be able to view the worksheet.

Click the **Share** button in the upper right corner of the worksheet, select the appropriate role in the **Share Worksheet** dialog box, and click **Share**. The worksheet will then be shared.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e50accb5d71439ea65091c1b5ab21c3~tplv-goo7wpa0wc-image.image) </span>

<span id="75b94dba"></span>
## Archive worksheets

You can create folders in saved worksheets and move worksheets into folders to make worksheet management easier.

**Operation steps**:


1. Click the **Saved worksheets**icon in the left sidebar. Click the **folder** icon. Create a folder.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d091fee02cb4deeb8f23675590d05a9~tplv-goo7wpa0wc-image.image) </span>

2. Hover over the worksheet name and click ... Click the **Moving to** button, select a folder, and then click **OK** to move the worksheet to the selected folder.

   You can also long\-press the worksheet name and drag the worksheet to the target folder to archive it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30c986f27083412aab9bce0d592422b2~tplv-goo7wpa0wc-image.image) </span>

3. (Optional) If you need to view the name of a folder that has already been set, hover the mouse over the folder name and click ... Button: Click **Rename** to modify the folder name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfdb21194987457d81ef9ed4f045c49d~tplv-goo7wpa0wc-image.image) </span>

4. Optional: If you need to delete a folder, hover over the folder name and click ... Click the **Delete** button, check **Delete All**, and click OK to delete the current folder.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b9991a4f4a4446b91c4372bd4278c18~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleting a folder will also <strong>delete all worksheets within that folder and its subfolders</strong>. This action is irreversible. Please proceed with caution.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you still need to use the worksheets in this folder, please move them to another folder according to steps 1\-2 before deleting the folder.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e410f3747624c09b7b27be13d8bbc87~tplv-goo7wpa0wc-image.image" width="361px" />   </div>
   

<span id="ba604c63"></span>
## Delete worksheets

Hover over the worksheet name and click ... Click the **Delete** button to delete the worksheet.

<span id="932edd7d"></span>
# Select a virtual warehouse

Before executing a query, you need to configure a virtual warehouse for the worksheet to obtain the corresponding computational resources.

In the top toolbar of the SQL worksheet page, click the virtual warehouse dropdown list to select a virtual warehouse for the current worksheet.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f913eee457e648829afb80703275eb4a~tplv-goo7wpa0wc-image.image) </span>

A green dot next to a virtual warehouse indicates that the virtual warehouse is running, while a gray dot means the virtual warehouse is currently paused. To use it, you can hover your mouse over the gray dot and click the **Start** button to start the virtual warehouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1117e2600ee142bf9ffca267468e6ab4~tplv-goo7wpa0wc-image.image) </span>

<span id="ea352646"></span>
# Select dialect

ByteHouse Cloud Data Warehouse supports three dialects: ANSI MySQL, ClickHouse SQL, and MySQL. You can click the language option to switch to your preferred dialect.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e1fb532b758421b953244becf860b95~tplv-goo7wpa0wc-image.image) </span>

<span id="67bb7483"></span>
# Select a database

Before executing a query, you can select the target database first. When executing subsequent queries, you can directly use the table name in the SQL statement without specifying the database name additionally.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45aba6d6ca3d425294857dc8d4e589ff~tplv-goo7wpa0wc-image.image) </span>

<span id="26fb5ddc"></span>
# Management queries

The query details and results displayed in the worksheet are valid only for the current user session. If you log out of the ByteHouse console interface and then log back in, the results from your previous session will no longer be displayed in the worksheet. However, you can view queries that have already been executed through the SQL history feature. For more details, see [Query history](https://docs.byteplus.com/docs/bytehouse/sql-audit).

<span id="c9fe9448"></span>
## Execute a query

After entering an SQL statement in the SQL editor, click **Run** to execute the query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/754ec1bcd2094dbd9f8d97bada0c520e~tplv-goo7wpa0wc-image.image) </span>

If you enter multiple SQL statements, the system will, by default, execute the statement you have selected. To execute all queries, select the **All queries** checkbox.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e89f1e97db5a41c6bc1f3c3138d881c3~tplv-goo7wpa0wc-image.image) </span>

<span id="852568b8"></span>
## Abort running queries

When a query is running, a new **Abort** button is added to the right of the Run button. Click this button to abort the running query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53298eda483e4c4aa659088a5baaad14~tplv-goo7wpa0wc-image.image) </span>

<span id="538289b4"></span>
## View query details

After the query is executed, you can view specific information in the **Query Results** section below the SQL editor.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de1188661a3c4e40bbfb289411e6b1fe~tplv-goo7wpa0wc-image.image) </span>

You can click the filter button in the results column to filter results as needed, or view results in ascending or descending order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/980caf5993414e8ea261e51a2187759c~tplv-goo7wpa0wc-image.image) </span>

<span id="0d5e4350"></span>
## Data visualization results

ByteHouse supports viewing data results as bar charts and line charts.

After the query is executed, you can set the chart type, X axis, and Y axis in **Data visualization** located below the SQL editor to display the query results in the form of a visual chart. An example of the visualization results is shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcff7fee7ba148b8bb21f7460ae195fd~tplv-goo7wpa0wc-image.image) </span>

<span id="10d7674d"></span>
## Remove query

When you perform too many queries, resulting in excessive page caching, you can delete query results to improve page load speed. You can view details of deleted query results in **Audit logs**.

Hover the mouse over a query result, click the x icon, then click **OK**. This will delete the current query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98f74166fe764379a5a4bc2f9ba0088e~tplv-goo7wpa0wc-image.image) </span>

<span id="b8e3c040"></span>
# Use SQL parameter groups

An SQL parameter group is a set of shortcut parameters provided when running SQL statements in the ByteHouse console. When executing queries in the SQL worksheet, you can select the required SQL parameter group, which will take effect within the session running in the ByteHouse console.

<span id="27d05e79"></span>
## Cautions


* SQL parameter groups are effective only in sessions running in the ByteHouse Console. Each sub\-user maintains their own shortcut parameters, which are not shared with others.

* When using, add with caution. It is recommended to use this at the Query level to avoid global system issues caused by improper parameter settings.

* ByteHouse does not validate parameters and parameter values set by users. After setting parameters, please ensure that the settings are correct. ByteHouse provides sample parameters and parameter values for your reference, which you can add as needed.

* The settings parameter configured in the SQL worksheet takes precedence over the SQL parameter group. That is, if you set the same parameter using both the settings parameter in the SQL worksheet and the SQL parameter group, but assign different values, ByteHouse will use the value specified in the settings parameter of the SQL worksheet.


<span id="09c476ed"></span>
## Create and use SQL parameter groups


1. Select **SQL Params**, click the checkbox next to the SQL parameter group, click + **Params**, and go to the page to create a new SQL parameter.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcd40b2c07254914ac78e09be65aa125~tplv-goo7wpa0wc-image.image) </span>

2. Customize the parameter group name and description, and specify the SQL parameter group in XML format.

   You can click **Params Demo** to view an example, copy and paste the sample into the SQL parameter group text box, and modify the parameter values according to your actual situation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a5f2961558d48069321aa1c34a4a10e~tplv-goo7wpa0wc-image.image) </span>

   **Parameter examples**

   ```XML
   <sql_parameters>
          <optimize_unique_table_write>false</optimize_unique_table_write>
          <max_insert_threads>0</max_insert_threads>
          <min_insert_block_size_bytes>1073710080</min_insert_block_size_bytes>
          <min_insert_block_size_rows>1048545</min_insert_block_size_rows>
          <max_partitions_per_insert_block>100</max_partitions_per_insert_block>
          <lake_commit_in_worker>true</lake_commit_in_worker>
          <lake_write_threads>4</lake_write_threads>
          <lake_write_max_file_size>1073741824</lake_write_max_file_size>
          <enable_plan_cache>false</enable_plan_cache>
          <match_name_ignore_case>false</match_name_ignore_case>
          <wait_runtime_filter_timeout>1000</wait_runtime_filter_timeout>
   </sql_parameters>
   ```
   

   **Parameter description**

   
   |Parameter items |Parameter description |Recommended value |
   |---|---|---|
   |optimize_unique_table_write |The import optimization switch for unique key tables using `INSERT SELECT`. It is recommended to enable this feature only in scenarios where the staging area is not enabled and `dedup_impl_version='dedup_in_txn_commit'`. |false |
   |max_insert_threads |It configures the thread pool size for write operations when Worker nodes execute `INSERT SELECT` requests. |0 |
   |min_insert_block_size_bytes |It controls the minimum size, in bytes, of data batch blocks in the `INSERT SELECT` operation. |1073710080 |
   |min_insert_block_size_rows |It controls the minimum number of rows in a batched data block during an `INSERT SELECT` operation. |1048545 |
   |max_partitions_per_insert_block |It limits the maximum number of parts that can be written within each block during a single `INSERT` operation. This value is typically limited by the product of the number of partitions and buckets in the data distribution. |100 |
   |lake_commit_in_worker |It controls whether to use Worker nodes to directly perform the commit operation when writing data to an external table. |true |
   |lake_write_threads |Thread pool size configuration for writing data to an external table. |4 |
   |lake_write_max_file_size |When configuring data writes to an external table, the maximum size of a single file is specified in bytes (byte). |1073741824 |
   |enable_plan_cache |It controls whether to enable the in\-memory query execution plan cache (query plan cache). |false |
   |match_name_ignore_case |It controls whether case sensitivity in SQL statements is ignored during parsing. |false |
   |wait_runtime_filter_timeout |It configures the wait time for building the runtime filter. The default is 1 second. If the construction is still not complete after the timeout, the system will ignore the runtime filter results. |1000 |
   

3. Click **OK** to create an SQL parameter group. You can click the selection box next to **SQL Params** to view the SQL parameter groups that have been created, or hover the mouse over a parameter group name to preview its contents.

4. (Optional) ByteHouse supports creating multiple parameter groups. You can continue to create them by following the steps above.

5. Select the checkbox next to the SQL parameter group, then click the desired parameter group name. The parameter group will be automatically added and used when executing SQL statements.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use the settings parameter in the SQL worksheet to set a parameter that already exists in the SQL parameter group, but assign it a different value, ByteHouse will override the group setting and use the value specified in the SQL worksheet.   </div>
   

<span id="bacf49ac"></span>
## Edit the SQL parameter group

Click the selection box next to **SQL Params**, hover over the parameter group name, and click the **Edit** button. You can modify the SQL parameter group name, description, and SQL parameter content as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/243a6805f8d347e28c3bbefd307ada16~tplv-goo7wpa0wc-image.image) </span>

<span id="313d0ebf"></span>
## Delete SQL parameter groups

Click the selection box next to **SQL Params**, hover the mouse over the parameter group name, click the **Delete** button, and, after confirmation, the current parameter group will be deleted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95da239a2d8d4f009efdcd03d11a6d81~tplv-goo7wpa0wc-image.image) </span>

<span id="9ad3347e"></span>
# Use the query analyzer

In addition to query details and results, ByteHouse also provides a query analysis tool that enables users to examine query statistical data, details, and various execution components of the query.

In the query results, click the query ID. The system will then navigate to the **History** page in **Audit logs** and automatically filter for that query ID. You can click the query ID to view SQL execution details, including the status of the query, the virtual warehouse used, execution time, execution plan, and other query details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84178eed76d4493191966810298ee584~tplv-goo7wpa0wc-image.image) </span>

<span id="c96bbc29"></span>
# Use the Data Object Browser

You can use the Object Browser to browse all data objects you have created or that have been shared with you, including databases, tables, views, external tables, and other data resources.

When the worksheet content changes, the lists of databases and other objects are refreshed automatically. You can also click the refresh button at the top of the object browser to immediately view changes to the object.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1da28c3c8c344106bd26a1d9811d0617~tplv-goo7wpa0wc-image.image) </span>


* **Databases and tables**

   You can view the databases and tables in the current cluster. You can hover your mouse over a table name to view the column information, table information, base table, and DDL. Alternatively, you can click the Insert button to the right of a database or table to insert them into the SQL editor.

* **External catalogs**

   You can view the databases and tables in external Catalogs that have been added. By hovering the mouse over a table name, you can view column information, table information, base table, and DDL. You can also click the Insert button to the right of a database or table to insert the database or table into the SQL editor.

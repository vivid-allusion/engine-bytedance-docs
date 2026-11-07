---
title: "Changing data capture (CDC) management"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/changing-data-capture-CDC-management"
---

Change data capture is used to record insertions, updates, and deletions applied to enabled tables, providing detailed information about changes. This article describes using stored procedures to turn data capture on or off for a specified database and usage examples.

<span id="prerequisite"></span>
## prerequisite

The SQL Server instance is connected and the target library status is Online. For more information, see [Connection instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

<span id="precautions"></span>
## Precautions


* Statements with transactions cannot perform insert operations.

* Performing change data capture statements against the system library or the rdsadmin library is not supported.

* Only the primary account supports performing on or off change data capture statements against the database.


<span id="turn-on-or-off-the-cdc"></span>
## Turn on or off the CDC.

Execute the following command to turn change data capture on or off.

```sql
Exec [msdb].[dbo].[rds_cdc_database] '@DBName',@Action;
```


The parameter description is as follows:


* `@DBName`: Represents the database name.

* `@Action`: Indicates whether change data capture is enabled, with the following values:

   * `1`: Indicates that change data capture is enabled.

   * `0`: Indicates that change data capture is turned off.


<span id="use-example"></span>
## use example

Below `@DBName` is `testDBName`, `@source_name` is `Table_1`, `@source_schema` is `dbo`, `@capture_instance` is `dbo_Table_1` as an example to introduce how to use CDC.


1. Execute the following command to enable change data capture CDC.

   ```sql
   Exec [msdb].[dbo].[rds_cdc_database] 'testDBName',1;
   ```
   

2. Execute the following command to create a change data capture task for the target database.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you first enable change data capture, you must execute the following command.   </div>
   

   ```sql
   EXEC [sys].[sp_cdc_add_job] @job_type = N'capture'; 
   EXEC [sys].[sp_cdc_add_job] @job_type = N'cleanup';
   ```
   

3. Execute the following command to enable change data capture for the target table.

   ```sql
   EXEC sys.sp_cdc_enable_table 
   @source_schema = 'dbo', -- source_schema default dbo 
          @source_name = 'Table_1', -- table_name 
          @capture_instance = NULL, -- capture_instance 
          @supports_net_changes = 0, -- supports_net_changes 
          @role_name = NULL -- role_name
   ```
   

4. Turn off change data capture for the target table.

   ```sql
   EXEC sys.sp_cdc_disable_table 
       @source_schema = N'dbo', 
       @source_name   = N'Table_1', 
       @capture_instance = N'dbo_Table_1'
   ```
   

   When a table with change capture enabled undergoes structural changes, such as adding or deleting partial columns, change data capture needs to be turned back on. The steps to restart are to turn off and then turn on the change data capture function.

5. Query for changes.

   For a table for which change data capture is enabled, you can query the table for specific changes by executing the following command.

   ```sql
   DECLARE @from_lsn binary(10), @to_lsn binary(10); 
   SET   @from_lsn = sys.fn_cdc_get_min_lsn('dbo_Table_1'); 
   SET   @to_lsn   = sys.fn_cdc_get_max_lsn(); 
   SELECT * FROM [cdc].[fn_cdc_get_all_changes_dbo_Table_1](@from_lsn, @to_lsn, 'all');
   ```

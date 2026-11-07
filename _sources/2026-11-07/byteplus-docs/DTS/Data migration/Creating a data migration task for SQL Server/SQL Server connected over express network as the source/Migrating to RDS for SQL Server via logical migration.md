---
title: "Migrating to RDS for SQL Server via logical migration"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_to_SQL_Server_connected_over_public_network_via_logical_migration"
---

This topic describes creating a task in the Database Transmission Service (DTS) console to migrate SQL Server from a public network to a public network.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A self\-managed instance and its database for RDS for SQL Server have been set up in the public network environment.

* When the access method of the database instance is public network and access restriction is enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27`.

   For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Confirm the network connectivity and service availability of the source and target databases before creating a data migration task.

* As CDC is enabled by default during the incremental migration phase, it is critical that before migration begins, the local disk hosting the source database has sufficient free space to accommodate the database to be migrated.

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (SQL Server)](https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


|**Type** |**Description** |
|---|---|
|Source database limits |* General limits:<br><br>   * Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>   * Tables to be migrated must contain a primary key or unique constraint, and the fields must be unique. Otherwise, duplicate data may occur in the target database.<br><br>   * If the migration objects are at the table level, then a single migration task supports a maximum of 1,000 tables. If the quantity limit is exceeded, it is recommended to split the tables to be migrated and create multiple tasks (create new tasks only after the previous one has completed).<br><br>   * A single migration task supports a maximum of 10 databases. Exceeding the quantity limit introduces risks of stability and performance issues. In such cases, it is recommended to split the tables to be migrated and create multiple tasks.<br><br>   * Do not perform write operations on the target database. Otherwise, data inconsistency may occur.<br><br>   * DTS does not migrate foreign keys from the source database to the target database, and as a result, operations such as cascading updates and deletes from the source will not be migrated.<br><br>   * The storage space of the target instance must be larger than the used storage space of the source instance.<br><br>   * Migration of data from read\-only instances is unsupported.<br><br>   * Column encryption during migration is unsupported.<br><br>   * Only RDS for SQL Server 2019 and 2022 instances are currently supported for migration.<br><br>   * Only tables are currently supported for migration (Views and triggers are not yet supported).<br><br>   * Configuring multiple migration tasks in the same table is unsupported.<br><br>   * During migration, do not switch to the primary, as this will cause the migration task to fail.<br><br>* Limits for schema or full migration:<br><br>   * During the table schema migration and full migration stages, do not perform DDL operations that change the database or table structure, or the data migration task will fail.<br><br>   * If only full data migration is performed, do not write new data to the source instance, or the source and target data will be inconsistent. To maintain real\-time data consistency, it is recommended to select schema migration, full migration, and incremental migration.<br><br>   * It supports selecting the table structure, data, and indexes of the table.<br><br>   * When migrating table structure, the functions `newid`, `getutcdate`, and `getdate` are supported as default values. When using these functions as default values, the target database also needs functions with the same functions.<br><br>   * It supports migrating columns with auto\-incrementing attributes.<br><br>   * Writing source database calculated columns to target database calculated columns is currently not supported, but writing source database calculated columns to target database ordinary columns is supported.<br><br>* Limits for incremental migration:<br><br>   * You need to enable data logs and set the instance backup mode to `Full`.<br><br>   * The `srvname` field of the `sys.sysservers` view must be consistent with the return value of the `SERVERPROPERTY` function.<br><br>   * The delete action for the following large data types is not supported: `IMAGE`, `TEXT`, and `NTEXT`.<br><br>   * The update action for the following large data types is not supported: `IMAGE`, `TEXT`, `NTEXT`, `varchar(max)`, `nvarchar(max)`, and `varbinary(max)`.<br><br>   * The source database does not support performing multiple add/drop column operations in succession (with intervals less than 10 minutes). Consecutive execution will cause the task to report an error.<br><br>   * Incremental changes to computed columns are unsupported.<br><br>   * Incremental migration is not supported if the source database instance is RDS for SQL Server 2019/2022 Web Edition.<br><br>   * As CDC is enabled by default during the incremental migration phase, it is critical that before migration begins, the local disk hosting the source database has sufficient free space to accommodate the database to be migrated.<br><br>   * During incremental migration, CDC data cleaning is performed every 24 hours to help maintain system stability and data consistency. |
|Other limits |* Currently, only RDS for SQL Server 2019 and 2022 instances are supported for migration. If you need to migrate from other versions or perform cross\-version migration, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br><br>* To ensure the accuracy of incremental data migration, DTS creates the trigger `volc_dts_cdc_sync_ddl` and the DDL storage table `volc_dts_cdc_ddl_history` in the source database.<br><br>* Prior to executing data migration, assess the performance of both the source and target database instances. It is also advised to perform the migration during off\-peak business hours. Otherwise, during full migration, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* Supported field types for migration tasks:<br><br>   * Supported field types include `TINYINT`, `SMALLINT`, `INT`, `BIGINT`, `DECIMAL`, `NUMERIC`, `FLOAT`, `REAL`, `BIT`, `DATE`, `SMALLDATETIME`, `DATETIME`, `DATETIME2`, `DATETIMEOFFSET`, `TIME`, `TIMESTAMP`, `CHAR`, `VARCHAR`, `NCHAR`, `NVARCHAR`, `BINARY`, `VARBINARY`, `NTEXT`, `TEXT`, and `UNIQUEIDENTIFIER`.<br><br>   * Unsupported field types include `CURSOR`, `ROWVERSION`, `SQL_VARIANT`, `GEOMETRY`, `GEOGRAPHY`, `HIERARCHYID`, `SMALLMONEY`, `MONEY`, `XML`, and `IMAGE`.<br><br>* Do not perform frequent DDL operations on the same table, as repeated DDL operations may cause DTS metadata update failures and risk transmission interruptions. The mitigation measures are as follows:<br><br>   * Perform DDL operations with intervals of 1 to 3 seconds.<br><br>   * Use the [Lock-free schema change tickets](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-structural-change-ticket-onlineddl-ticket-for-mysql) of Database Workshop (DBW). |


<span id=".5pSv5oyB5aKe6YeP6L-B56e755qELXNxbC3or63lj6U="></span>
## Supported SQL statements for incremental migration


|**Operation type** |**SQL statement** |
|---|---|
|DDL |ALTER TABLE |
|DML |INSERT, UPDATE, DELETE |


<span id=".5pWw5o2u5bqT6LSm5Y-35pyA5bCP5p2D6ZmQ562W55Wl"></span>
## Database account minimum permission policy


|**Database** |**Schema migration** |**Full migration** |**Incremental migration** |
|---|---|---|---|
|**Source database** |`db_owner` permissions |`db_owner` permissions |`sysadmin permissions` |
|**Target database** |* When the target database exists: `db_owner` permissions.<br><br>* When the target database does not exist: `create any database` permissions. |||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For how to grant account permissions, refer to <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account">Managing accounts</a>.</div>


<span id=".5pON5L2c5oyH5Y2X"></span>
## Operation guide


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Data migration list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the system generates a task named with <code>dts-</code> by default.</div><br> |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |**SQL Server** is selected by default. |
   ||**Access method** |Select **Public network SQL Server**. |
   ||**Migration method** |Select **Logical migration**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**Host address** |Enter the host address of the target instance. |
   ||**Port** |Enter the port number of the target instance. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **SQL Server**. |
   ||**Access method** |Select **BytePlus SQL Server**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**SQL Server instance** |Select RDS for SQL Server instance from the drop\-down list. You can search and select the target instance by instance ID or instance name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Support fuzzy search for selecting existing tag keys and tag values.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Create migration task** page, locate the **Configure migration object** wizard, and configure the following parameters.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**Migration type** ||Select the migration type as needed. Currently supported types are **Schema migration**, **Full migration**, and **Incremental migration**. including:<br><br><br>* If only full migration is required, select both **Schema migration** and **Full migration**.<br><br>* If online migration is needed, select **Schema migration**, **Full migration**, and **Incremental migration** simultaneously.<br><br>* When **Incremental migration** is not selected, do not write new data to the source database instance during data migration to ensure data consistency. |
   |**Migration object** ||Check the objects to migrate in the **Migration object** area. At the same time, you can filter and delete unnecessary targets in the **Selected object** area. The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Incremental migration does not automatically migrate newly added objects and their related changes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The migration object granularity can be either database or table. If tables are selected as the migration objects, other objects such as views, triggers, functions, or stored procedures will not be migrated to the target database.</div><br> |
   |**Advanced configuration** |**Error retry time** |If a migration task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not need to start the migration task immediately, click <strong>Save</strong> in the lower\-right corner of the page after configuring the migration object.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After saving, the task status will be <strong>To be started</strong>, and you can configure the migration task at a suitable time. For configuration methods, refer to <a href="https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task">Configuring a migration task</a>.   </div>
   

8. Click **Data validation configuration**.

9. On the **Create migration task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a migration task.<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data migration task.<br><br>* **Disable**: Do not configure data verification tasks when creating a data migration task. |
   |**Validation type** |DTS automatically generates validation types based on the database type and migration type, and does not support modification. For more information on validation types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
   |**Validation object** |Select the object to be verified as needed.<br><br><br>* **Consistent with the migration task**: The object to be verified matches the object to be migrated, meaning all migration objects are verified.<br><br>* **Custom**: Select the object to be verified as needed. |
   |**Startup settings** |Configure the timing of data verification in the migration task.<br><br><br>* **Automatic start**: The data verification task starts automatically along with the progress of the migration task. Automatic start occurs when full migration (if any) is complete and the delay of incremental migration is 0.<br><br>* **Manually start**: The data verification task does not start automatically with the migration task progress. You must manually start the data verification at the appropriate time. It is recommended to manually start data verification only after full migration (if any) is complete and the delay of incremental migration is 0. Otherwise, verification results may be inaccurate. |
   |**Billing type** |Currently, only **Pay\-as\-you\-go** is supported and can not be modified. |
   

10. Click **Pre\-check**.

11. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

12. On the **Create migration task** page, locate the **Pre\-check** wizard and perform the following operations based on the pre\-check results:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server">Pre\-check items (SQL Server)</a>.      </div>
      

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**. Then perform the following operations.

   * Click **Create and start a task**. After successfully creating the data migration task, data migration starts immediately.

   * Click **Create task**. After successfully creating the data migration task, you need to manually start data migration at the right time.


After successfully creating the data migration task, you can return to the DTS console to view the data migration task information on the data migration task list. For more information, refer to [Viewing migration tasks](https://docs.byteplus.com/en/docs/DTS/viewing_a_migration_task).

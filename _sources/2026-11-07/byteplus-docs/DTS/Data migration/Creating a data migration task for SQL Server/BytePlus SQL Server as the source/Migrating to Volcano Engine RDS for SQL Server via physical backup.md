---
title: "Migrating to Volcano Engine RDS for SQL Server via physical backup"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_to_Volcano_Engine_RDS_for_SQL_Server_via_physical_backup"
---

This topic describes how to create, through the physical backup method, automatic uploads of backup files from BytePlus RDS for SQL Server and restore them to BytePlus RDS for SQL Server on the Database Transmission Service (DTS) console.

<span id="DljlrqCI"></span>
## Prerequisites


* An instance for RDS for SQL Server has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance).

* Confirm the network connectivity and service availability of the source and target databases before creating a data migration task.

* Make sure that the available storage space of the target database instance is 1.5 times the total amount of the database to be restored. If the instance does not have enough storage space, increase the instance space. For details, refer to [Regular modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification).

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (SQL Server)](https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server).


<span id="Gm45RHVi"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* It is recommended to set the log backup frequency of the source BytePlus SQL Server instance to 30 minutes. Otherwise, the recovery speed will be slow.<br><br>* A single migration task supports a maximum of 10 databases. Exceeding the quantity limit introduces risks of stability and performance issues. In such cases, it is recommended to split the tables to be migrated and create multiple tasks.<br><br>* The database to be migrated does not exist in the BytePlus instance.<br><br>* The same target database can only be used for migration in one task.<br><br>* During migration, do not switch to the primary, as this will cause the migration task to fail. |
|Other limits |* Currently, only migration of backup files from lower versions to higher version database instances is supported. Migration of backup files from higher versions to lower versions is not supported. Version restrictions are as follows:<br><br>   * Database commercial version: It is recommended to upgrade from a lower version to a higher version, such as from Web Edition to Standard Edition to Enterprise Edition.<br><br>   * Database compatible version: For example, only Migration from SQL Server 2019 to SQL Server 2022 is supported. Migration from SQL Server 2022 to SQL Server 2019 is not supported.<br><br>* Before performing a database migration in a production environment, it is recommended that you first perform actual testing and evaluation in a development or test environment. If you need to run the assessment in a production environment, it is recommended to test during off\-peak hours to reduce the impact on your business.<br><br>* Migration of in\-memory tables, FileStream, and FileTables data fields is not supported.<br><br>* Filtering Database and table Migrations is not supported during the Migration process. |


<span id="5B27Q2mr"></span>
## Database version


|**Source database version** |**Target database version** |
|---|---|
|* Enterprise Edition (Developer)<br><br>* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* SQL Server 2019 Enterprise Edition<br><br>* SQL Server 2022 Enterprise Edition<br><br><br> |
|* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* SQL Server 2019 Standard Edition<br><br>* SQL Server 2022 Standard Edition<br><br><br> |
|* Web Edition<br><br>* Express Edition |* SQL Server 2019 Web Edition<br><br>* SQL Server 2022 Web Edition |


<span id="y3EIHUm7"></span>
## Database account minimum permission policy


|**Database** |**Permission type** |
|---|---|
|**Source database** |`db_owner` permissions |
|**Target database** |`db_owner` permissions |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For how to grant account permissions, refer to <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account">Managing accounts</a>.</div>


<span id="hdKvQHQh"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Data migration list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.



|**Type** |**Parameter** |**Description** |
|---|---|---|
|**Basic information** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
|**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **SQL Server**. |
||**Access method** |Select **BytePlus SQL Server**. |
||**Migration method** |Select **Physical backup**. |
||**SQL Server instance** |Select RDS for SQL Server instance from the drop\-down list. You can search and select the target instance by instance ID or instance name. |
||**Full backup set** |Select a physical backup (full backup) to be migrated from the drop\-down list. Each physical backup (full backup) set has a time identifier. You can select the most recent physical backup (full backup) based on the time identifier.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the most recent physical backup (full backup) is relatively old, it is recommended that you manually create a full backup for the source SQL Server, and select the most recent physical backup (full backup) for migration.</div><br> |
||**Database account** |Enter the database account of the source instance. |
||**Database password** |Enter the password corresponding to the database account of the source instance. |
||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Currently, only **SQL Server** is supported. No selection is required. |
||**Access method** |Currently, only **BytePlus SQL Server** is supported. No selection is required. |
||**SQL Server instance** |Select RDS for SQL Server instance from the drop\-down list. You can search and select the target instance by instance ID or instance name. |
||**Database account** |Enter the database account of the target instance. |
||**Database password** |Enter the password corresponding to the database account of the target instance. |
||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of volc:, such as Volc: or VOLC:.<br><br>* (Optional) Value<br><br>   * Supports any language, characters, numbers, spaces, or symbols (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |



6. Click **Next step: configure migration object**.

7. On the **Create migration task** page, locate the **Configure migration object** wizard, and configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Migration type** |**Full migration** and **incremental migration**, which are not editable.<br><br>DTS automatically identifies the selected full backup set and subsequent incremental backups, and then performs full migration and incremental migration. |
   |**Migration object** |Check the objects to migrate in the **Migration object** area. |
   

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   1. If the instances of the target databases are not modified, there is no need to restart the pre\-check.

   2. If you modify the target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Create migration task** page, locate the **Pre\-check** wizard and perform the following operations based on the pre\-check results:

   1. Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   2. Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server">Pre\-check items (SQL Server)</a>.      </div>
      

11. Click **Confirm order**.

12. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check ** I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**.

   * Click **Create and start a task**. After successfully creating the data migration task, data migration starts immediately.

   * Click **Create task**. After successfully creating the data migration task, you need to manually start data migration at the right time.


After successfully creating the data migration task, you can return to the DTS console to view the data migration task information on the data migration task list. For more information, refer to [Viewing migration tasks](https://docs.byteplus.com/en/docs/DTS/viewing_a_migration_task).

<span id="Shb3ZHjq"></span>
## Subsequent operations

<span id="ci9bBMGt"></span>
### Check whether the task is backed up normally

You can check whether the backup migration task is running properly in the following two ways:


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Data migration list** page, click the target task name.

5. On the target task details page, click **Task progress**.

6. On the **Task progress** tab, view the backup progress.


<span id="kOKw4QZm"></span>
### End data migration

The data migration task migrated to BytePlus SQL Server through physical backup will not end automatically. After the migration task ends, you need to manually end the data migration to restore the target database to be available.


1. Select the timing to end the data migration.

   1. At time T1 during the off\-peak hours of the business, pause writing data to the source end.

   2. Wait until the most recent incremental recovery time of the DTS migration task is later than time T1 (view the incremental recovery time in the task progress of the migration task).

2. Open database (end data migration).

   After completing the full and incremental data migration and before the business switchover, you need to manually open the target database to ensure that the business can read and write normally after the data switchover.

   1. Log on to the [DTS console](https://console.byteplus.com/dts).

   2. On the top menu bar, select the project and region.

   3. In the left navigation bar, click **Data migration**.

   4. On the **Migration task list** page, select  **...**  on the right of the target migration task.  **\> Open database**.

   5. In the confirmation box, click **OK**.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">After opening the database, the migration task can not be recovered. Proceed with caution.      </div>
      

3. Check whether the data of the source and target database are consistent.

4. Service switchover.

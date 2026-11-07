---
title: "Migrating to BytePlus RDS for SQL Server via physical backup (automatic backup)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_to_RDS_for_SQL_Server_via_physical_backup_automatic_backup"
---

This topic describes how to create, through the physical backup method, automatic uploads of backup files from SQL Server connected over express network and restore them to BytePlus RDS for SQL Server on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Set the source information as needed, as detailed below:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* An instance for RDS for SQL Server has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance).

* Make sure that the available storage space of the target database instance is 1.5 times the total amount of the database to be restored. If the instance does not have enough storage space, increase the instance space. For details, refer to [Regular modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification).

* Your account has been granted full read and write access to TOS, specifically `TOSFullAccess`.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When creating a data migration task via express network, the system creates several network cards by default in your selected VPC, and the network cards are mounted by default to the subnet you selected. The network card name format is `dts_shuttle_********`.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* A single migration task supports a maximum of 10 databases. Exceeding the quantity limit introduces risks of stability and performance issues. In such cases, it is recommended to split the tables to be migrated and create multiple tasks.<br><br>* The database to be migrated does not exist in the BytePlus instance.<br><br>* The same target database can only be used for migration in one task.<br><br>* During migration, do not switch to the primary, as this will cause the migration task to fail.<br><br>* Do not perform periodic full backups during the migration process. |
|Other limits |* Currently, only migration of backup files from lower versions to higher version database instances is supported. Migration of backup files from higher versions to lower versions is not supported. Version restrictions are as follows:<br><br>   * Database commercial version: It is recommended to upgrade from a lower version to a higher version, such as from Web Edition to Standard Edition to Enterprise Edition.<br><br>   * Database compatible version: For example, only migration from SQL Server 2012 to SQL Server 2019 is supported. Migration from SQL Server 2019 to SQL Server 2012 is not supported.<br><br>* The backup file name can not contain special characters, including `\\`, `/`, `:`, `*`, `?`, `"`, `<`, `>`, `\|`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `*`, `(`, `)`, `_`, `+`, `-`, and `=`.<br><br>* Before the backup data restoration to the Cloud is complete, do not delete the backup files from TOS. Otherwise, the migration to the Cloud may fail.<br><br>* The suffix of the backup file must be `bak`, `trn`, or `log`, as follows:<br><br>   * `bak`: Indicates a full backup file.<br><br>   * `trn` or `log`: Indicates a transaction log backup file.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the backup file does not have the above file suffix, the system may fail to correctly identify its type, which could affect subsequent operations.   </div><br>   <br><br>* Before performing a database migration in a production environment, it is recommended that you first perform actual testing and evaluation in a development or test environment. If you need to run the assessment in a production environment, it is recommended to test during off\-peak hours to reduce the impact on your business.<br><br>* Migration of in\-memory tables, FileStream, and FileTables data fields is not supported.<br><br>* Filtering Database and table Migrations is not supported during the Migration process. |


<span id=".5pWw5o2u5bqT54mI5pys"></span>
## Database version


|**Source database version** |**Target database version** |
|---|---|
|* Enterprise Edition (Developer)<br><br>* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* RDS for SQL Server 2019 Enterprise Edition<br><br>* RDS for SQL Server 2022 Enterprise Edition |
|* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* RDS for SQL Server 2019 Standard Edition<br><br>* RDS for SQL Server 2022 Standard Edition |
|* Web Edition<br><br>* Express Edition |* RDS for SQL Server 2019 Web Edition<br><br>* RDS for SQL Server 2022 Web Edition |


<span id=".5pWw5o2u5bqT6LSm5Y-35pyA5bCP5p2D6ZmQ562W55Wl"></span>
## Database account minimum permission policy


|**Database** |Permission type |
|---|---|
|**Source database** |`db_owner` permissions |
|**Target database** |`db_owner` permissions |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For how to grant account permissions, refer to <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account">Managing accounts</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65pWw5o2u6L-B56e75Lu75Yqh"></span>
### Step 1: Create a data migration task


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Data migration list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   |**Source database configuration** |**Instance type** |**SQL Server** is selected by default. |
   ||**Access method** |Select **SQL Server connected over express network**. |
   ||**Migration method** |Select **Physical backup**. |
   ||**Backup upload method** |Select **Automatic upload**. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **SQL Server**. |
   ||**Access method** |Select **BytePlus SQL Server**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**SQL Server instance** |Select RDS for SQL Server instance from the drop\-down list. You can search and select the target instance by instance ID or instance name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant IAM user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Create migration task** page, locate the **Configure migration object** wizard, and configure the parameters of **Migration object**. You can add up to 10 source and target databases.

   * **Source database**: Enter the database name to be migrated from the source end.

   * **Target database**: Enter the target database name.

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Create migration task** page, locate the **Pre\-check** wizard and perform the following operations based on the pre\-check results:

   1. Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   2. Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server">Pre\-check items (SQL Server)</a>.      </div>
      

11. Click **Create and start a task**.


<span id=".5q2l6aqk5LqM77ya5LiL6L295bel5YW3"></span>
### Step 2: Download the tool

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This tool is used to automatically upload data. It will occupy source database resources during the backup process. It is recommended to reserve enough storage space and perform a full backup during off\-peak hours.</div>


* <div data-tips="true" data-tips-type="tip">Currently, only 64\-bit Windows systems are supported.</div>



You can install the backup upload tool in the following two ways.


* Method 1: Click [Click download backup upload tool](https://dts-mssql-backup.tos-cn-beijing.volces.com/dtsBackupAgent.exe) to download the backup upload tool.

* Method 2: Download the backup upload tool through the DTS console.

   1. Log on to the [DTS console](https://console.byteplus.com/dts).

   2. On the top menu bar, select the project and region.

   3. In the left navigation bar, click **Data migration**.

   4. On the **Data migration list** page, click the target instance name.

   5. On the **Task information** tab of the target instance, click **Click to download** after **Backup upload method** in the **Source database information** area.

   6. In the **Download and start backup upload tool** dialog box, click **Click download backup upload tool** in the **Download address** area.


<span id=".5q2l6aqk5LiJ77ya5ZCv5Yqo5bel5YW3"></span>
### Step 3: Start the tool


1. Create a file directory named `dtsagent` in your SQL Server server, and copy the downloaded dtsBackupAgent tool to the `dtsagent` directory.

2. Create a `startParam.json` startup file in the file directory `dtsagent`.

3. Obtain the startup parameters in the DTS console.

   1. Log on to the [DTS console](https://console.byteplus.com/dts).

   2. On the top menu bar, select the project and region.

   3. In the left navigation bar, click **Data migration**.

   4. On the **Data migration list** page, click the target instance name.

   5. On the **Task information** tab of the target instance, click **Click to download** after **Backup upload method** in the **Source database information** area.

   6. In the **Download and start backup upload tool** dialog box, copy the **Startup parameter template**.

   7. Copy the startup parameters to the `startParam.json` file, and modify the content according to the parameter instructions.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The <code>taskId</code>, <code>tosEndpoint</code>, and <code>region</code> do not need to be modified. Modify other parameters as needed.      </div>
      

      ```sql
      {
                      "ak": "xx",
                      "sk": "xx",
                      "taskId": "xx",
                      "tosEndpoint": "tos-cn-chongqing-sdv.volces.com",
                      "region": "cn-chongqing-sdv",
                      "backupStartDate": "2025-04-02 15:44:00",
                      "backupDBList": "SQLTestDB",
                      "localBackupFileDir": "/home/wangzhengwei.0914/mssql_backup_dir",
                      "host": "10.37.53.253",
                      "port":  1433,
                      "username": "sa",
                      "password": "xx",
                      "biz": "FullAndRecurringLogBackup",
                      "logBackupInterval":  2,
                      "uploadRateMBLimit":  50
      }
      ```
      

      You can also directly copy the above parameter template content to the startup file and modify the content. The parameter instructions of the file content are shown in the following table:

      
      |**Parameter** |**Required?**  |**Description** |
      |---|---|---|
      |taskId |Yes |DTS task ID. |
      |ak |Yes |AccessKey ID of your BytePlus account. For details, refer to [API Access key management](https://docs.byteplus.com/en/docs/6257/64983).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Your account must have full read/write access to TOS, that is, <code>TOSFullAccess</code>. Uploading files will not take up your TOS resources.</div><br> |
      |sk |Yes |The SecretAccess Key of your BytePlus account. For detailed steps, refer to [API access key management](https://docs.byteplus.com/en/docs/6257/64983). |
      |tosEndpoint |Yes |The TOS domain name which is consistent with the region of the SQL Server instance connected over public network. For details, refer to [Region and Endpoint](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |
      |region |Yes |The region where the RDS for SQL Server instance is located. |
      |biz |Yes |Upload scenarios, which include:<br><br><br>* `OnlyUpload`: Indicates that the backup file and `Manifest` file are uploaded. This is suitable for existing full backup and periodic log backup tasks, and the database backup files need to be stored in the specified directory. In this scenario, DTS will not intrude on the source data and will reuse your existing backup files.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If non\-required parameters such as <code>host</code>, <code>port</code>, <code>username</code>, and <code>password</code> are not passed in your startup script, you need to configure the metadata file <code>Manifest</code> by yourself. Otherwise, the file upload will fail. For the procedure of configuring the <code>manifest</code> file, refer to <a href="https://docs.byteplus.com/en/docs/DTS/Migrating_to_RDS_for_SQL_Server_via_physical_backup_manual_upload#.5q2l6aqk5LiJ77ya5LiK5Lyg5aSH5Lu95YWD5pWw5o2u5paH5Lu2">Configuring the metadata file</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>FullAndRecurringLogBackup</code>: Indicates that full backup and periodic log backup are automatically performed, and backup files are uploaded. This is applicable when you do not have full backup and log backup tasks, or you do not want to perform too many manual operations. In this scenario, DTS will handle the entire process. You do not need to participate in the operations, nor maintain the backup metadata information.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>OnlyRecurringLogBackup</code>: Indicates that periodic log backups are automatically performed, and backup files are uploaded. It is applicable when the latest full backup already exists. In this scenario, the pressure and space occupation of the full backup on the source database can be reduced, and there is no need to maintain backup metadata information.</div><br> |
      |backupStartDate |Yes |The start time of the backup. The detailed description of this parameter is as follows:<br><br><br>* Wait time: If the backup is performed by the Agent, the Agent will wait until the time specified by `backupStartDate` before starting the backup.<br><br>* Back up immediately: if `backupStartDate` is earlier than the current time, the Agent will initiate a backup operation immediately after it is started. This means that if the specified backup start time has passed, the system will not wait for the set time, but will start backup scheduling immediately. |
      |backupDBList |Yes |List of backup databases. If there are multiple databases, separate them with commas (,). |
      |localBackupFileDir |Yes |Local address where the backup file is stored. If this address is not the machine directory where the SQL Server instance connected over public network is located, ensure that the file is in this directory and that the file is a complete backup file (not in transmission state). |
      |uploadRateMBLimit |No |The file migration rate. The default value is 50 MB. |
      |logBackupInterval |No |The interval of log backup. The unit is minutes, and the default value is 20 minutes. |
      |host |No |The host address used to connect to the SQL Server instance connected over public network. If a host address is specified, the system automatically pulls backup metadata after `backupStartDate`. |
      |port |No |The port used to connect to the SQL Server instance connected over public network. |
      |username |No |The username used to connect to the SQL Server instance connected over public network. |
      |password |No |The username password used to connect to the SQL Server instance connected over public network. |
      

4. Double\-click the `dtsBackupAgent.exe` file to start the tool.

   If it runs normally, a command terminal will be opened, and the `dtsBackupAgent.log` and `dtsBackupManifest.db` files will be generated. Do not delete the files during migration. If the script runs normally, a command terminal will be opened, and the `dtsBackupAgent.log` and `dtsBackupManifest.db` files will be generated. Do not delete the files during migration.


<span id=".5q2l6aqk5Zub77ya5qOA5p-l5Lu75Yqh5piv5ZCm5q2j5bi45aSH5Lu9"></span>
### Step 4: Check whether the task is backed up normally

You can check whether the backup migration task is running properly in the following two ways:


* Method 1: Check whether the task backup is running properly through logs. Check the `dtsBackupAgent.log` file in the `dtsagent` directory of your SQL Server server.

* Method 2: Check whether the task backup is running properly through the DTS console.

   1. Log on to the [DTS console](https://console.byteplus.com/dts).

   2. On the top menu bar, select the project and region.

   3. In the left navigation bar, click **Data migration**.

   4. On the **Data migration list** page, click the target task name.

   5. On the target task details page, click **Task progress**.

   6. On the **Task progress** tab, view the backup progress.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


1. At time T1 during the off\-peak hours of the business, pause writing data to the source end.

2. Wait until the most recent incremental recovery time of the DTS migration task is later than time T1.

3. Open the database. After completing the full and incremental data migration and before the business switchover, you need to manually open the target database to ensure that the business can read and write normally after the data cutover.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you open the database, you can not continue to perform the recovery. Proceed with caution.   </div>
   

4. Check whether the data of the source and target database are consistent.

5. Service switchover.


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

Q: Why is the backup file always in recovery?

A: The recovery may take a long time because the backup file to be recovered is large.

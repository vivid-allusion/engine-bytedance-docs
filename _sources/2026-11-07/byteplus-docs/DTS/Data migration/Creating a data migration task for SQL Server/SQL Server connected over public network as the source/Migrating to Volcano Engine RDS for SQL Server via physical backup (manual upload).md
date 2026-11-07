---
title: "Migrating to Volcano Engine RDS for SQL Server via physical backup (manual upload)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_to_RDS_for_SQL_Server_via_physical_backup_manual_upload"
---

This topic describes how to create, through the physical backup method, manual uploads of backup files from SQL Server connected over express network and restore them to BytePlus RDS for SQL Server on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|**Type** |**Description** |
|---|---|
|Source |* Download and install TOS Browser. For detailed steps, refer to [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3).<br><br>* Your account has been granted full read and write access to TOS, specifically `TOSFullAccess`.<br><br>* Set the source information as needed, as detailed below:<br><br>   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).<br><br>   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l). |
|Target |* A database instance has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance).<br><br>* Make sure that the available storage space of the target database instance is 1.5 times the total amount of the database to be restored. If the instance does not have enough storage space, increase the instance space. For details, refer to [Regular modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification). |
|others |* The local environment backup system is disabled.<br><br>* Given that the default locale of the RDS for SQL Server is English, it is recommended that you change it to Chinese for the convenience of subsequent operations. For detailed operations, refer to [How to modify the locale of SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-to-change-the-locale-of-rds-for-sql-server).<br><br>* Run the `DBCC CHECKDB` statement in the local database environment to ensure that there are no `allocation errors` and `consistency errors` in the database. And get the following normal execution result:<br><br>   ```sql```<br>```   ...```<br>```   CHECKDB found 0 allocation errors and 0 consistency errors in database 'xxx'.```<br>```   DBCC execution completed. If DBCC printed error messages, contact your system administrator.```<br>```   ```<br>    |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* A single migration task supports a maximum of 10 databases. Exceeding the quantity limit introduces risks of stability and performance issues. In such cases, it is recommended to split the tables to be migrated and create multiple tasks.<br><br>* The database to be migrated does not exist in the BytePlus instance.<br><br>* The storage space of the target instance must be larger than the used storage space of the source instance.<br><br>* Only one migration task can be in progress for the same target database.<br><br>* During migration, do not switch to the primary, as this will cause the migration task to fail. |
|Other limits |* Currently, only migration of backup files from lower versions to higher version database instances is supported. Migration of backup files from higher versions to lower versions is not supported. Version restrictions are as follows:<br><br>   * Database commercial version: It is recommended to upgrade from a lower version to a higher version, such as from Web Edition to Standard Edition to Enterprise Edition.<br><br>   * Database compatible version: For example, only migration from SQL Server 2012 to SQL Server 2019 is supported. Migration from SQL Server 2019 to SQL Server 2012 is not supported.<br><br>* The backup file name can not contain special characters, including `\\`, `/`, `:`, `*`, `?`, `\"`, `<`, `>`, `\|`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `*`, `(`, `)`, `_`, `+`, `-`, and `=`.<br><br>* Before the backup data restoration to the Cloud is complete, do not delete the backup files from TOS. Otherwise, the migration to the Cloud may fail.<br><br>* The suffix of the backup file must be `bak`, `trn`, or `log`, as follows:<br><br>   * `bak`: Indicates a full backup file.<br><br>   * `trn` or `log`: Indicates a transaction log backup file.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the backup file does not have the above file suffix, the system may fail to correctly identify its type, which could affect subsequent operations.   </div><br>   <br><br>* Before performing a database migration in a production environment, it is recommended that you first perform actual testing and evaluation in a development or test environment. If you need to run the assessment in a production environment, it is recommended to test during off\-peak hours to reduce the impact on your business.<br><br>* Do not perform periodic full backups during the migration process.<br><br>* Migration of in\-memory tables, FileStream, and FileTables data fields is not supported.<br><br>* Filtering Database and table Migrations is not supported during the Migration process. |


<span id=".5pWw5o2u5bqT54mI5pys"></span>
## Database version


|**Source database version** |**Target database version** |
|---|---|
|* Enterprise Edition (Developer)<br><br>* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* SQL Server 2019 Enterprise Edition<br><br>* SQL Server 2022 Enterprise Edition |
|* Standard Edition<br><br>* Web Edition<br><br>* Express Edition |* SQL Server 2019 Standard Edition<br><br>* SQL Server 2022 Standard Edition |
|* Web Edition<br><br>* Express Edition |* SQL Server 2019 Web Edition<br><br>* SQL Server 2022 Web Edition |


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

<span id=".5q2l6aqk5LiA77ya5Yib5bu66L-B56e75Lu75Yqh"></span>
### Step 1: Create a migration task


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
   ||**Backup upload method** |Select **Manual upload**. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **SQL Server**. |
   ||**Access method** |Select **BytePlus SQL Server**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**SQL Server instance** |Select RDS for SQL Server instance from the drop\-down list. You can search and select the target instance by instance ID or instance name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Supports fuzzy search for existing tag keys and tag values.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Create migration task** page, locate the **Configure migration object** wizard, and configure the parameters of **Migration object**. You can add up to 10 source and target databases.

   * **Source database**: Enter the database name to be migrated from the source end.

   * **Target database**: Enter the target database name.

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Create migration task** page, locate the **Pre\-check** wizard and perform the following operations based on the pre\-check results:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/pre-check-items-rds-for-sql-server">Pre\-check items (SQL Server)</a>.      </div>
      

11. Click **Create and start a task**.


<span id=".5q2l6aqk5LqM77ya5LiK5Lyg5aSH5Lu95paH5Lu2"></span>
### Step 2: Upload the backup file

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Your account must have full read/write access to TOS, that is, <code>TOSFullAccess</code>. Uploading files will not take up your TOS resources.</div>



1. Download and install TOS Browser. For detailed steps, refer to [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3).

2. After successfully installing TOS Browser, double\-click the TOS Browser icon to open the login screen.

3. On the TOS Browser login page, configure the following parameter information.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Endpoint** |1. Obtain the TOS Endpoint.<br><br>   1. Log on to the [DTS console](https://console.byteplus.com/dts).<br><br>   2. On the top menu bar, select the project and region.<br><br>   3. In the left navigation bar, click **Data migration**.<br><br>   4. On the **Data migration list** page, click the target task name.<br><br>   5. On the **Task information** tab, copy the **TOS Endpoint** information in the **Source database information** area.<br><br>2. In the TOS Browser logon interface, select **Custom** from the **Endpoint** drop\-down list.<br><br>3. Copy the obtained TOS Endpoint to the customized input box. |
   |**Access Key ID** |Fill in the AccessKey ID information of the account. |
   |**Secret Access Key** |Fill in the Secret Access Key information of the account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For specific steps on viewing AKSK information, refer to <a href="https://docs.byteplus.com/en/docs/6291/65568">Viewing AKSK information</a>.</div><br> |
   |**Access path** |1. Obtain the TOS access path.<br><br>   1. Log on to the [DTS console](https://console.byteplus.com/dts).<br><br>   2. On the top menu bar, select the project and region.<br><br>   3. In the left navigation bar, click **Data migration**.<br><br>   4. On the **Data migration list** page, click the target task name.<br><br>   5. On the **Task information** tab, copy the **TOS Bucket** information in the **Source database information** area.<br><br>2. Copy the obtained TOS Bucket to the access path input box. The format is: `tos://Tos Bucket`. |
   |**Remarks** |(Optional) It is used to set the remark name for login, which is convenient for account management. The instructions are as follows:<br><br><br>* A maximum of 30 characters is supported.<br><br>* It does not support starting with a hyphen (\-).<br><br>* If it is not filled in, the default is `-`. |
   |**Automatic login** |Optional. Log in automatically when you use the TOS Browser again. |
   

4. Click **Log in**.

5. On the TOS Browser page, click **Upload file**, select the data you want to migrate, and set the access permission of advanced settings for uploading files to **Inherit bucket**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the file access permission is not set to inherit bucket, the task migration will fail. For the procedure for modifying file access permissions, refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-modifying-the-file-access-permission">Modifying file access permissions</a>. If you can not modify the access permission of the uploaded file, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Inherit bucket indicates that the uploaded file object will inherit the bucket ACL, that is, the object's ACL policy will be consistent with the bucket ACL policy. For the relationship between object ACL and bucket ACL, refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-overview_4">Inheriting ACL settings from the bucket</a>.   </div>
   

6. Click **Upload**.


<span id=".5q2l6aqk5LiJ77ya5LiK5Lyg5aSH5Lu95YWD5pWw5o2u5paH5Lu2"></span>
### Step 3: Upload the backup metadata file


1. To obtain the metadata file, you can use the following two methods.

   * Manually edit the metadata file

      * Metadata file format

      ```sql
      <backup_set_id>,<database_name>,<type>,<physical_device_name>,<is_upload>
      ```
      

      The parameter descriptions are shown as follows:

      
      |**Parameter** |Required? |**Description** |
      |---|---|---|
      |backup_set_id |Yes |Increment ID. DTS will restore data in the order of IDs. |
      |database_name |Yes |Database name. |
      |type |Yes |Backup file type. The values are as follows:<br><br><br>* `D`: Full backup.<br><br>* `L`: Log backup. |
      |physical_device_name |Yes |The name of the backup file uploaded to the TOS. The TOS name must be unique. Or, it can be a Windows file path. The file name must be the same as the TOS file name. |
      |is_upload |Yes |Whether the upload is successful. The values are as follows:<br><br><br>* `Y`: Indicates that the upload is successful.<br><br>* `N`: Indicates that the upload is not successful. |
      |backup_start_date |No |The start time of the backup file. |
      |backup_finish_date |No |The end time of the backup file. |
      |first_lsn |No |The first log sequence number (LSN) in the backup set. |
      |last_lsn |No |The last log sequence number (LSN) in the backup set. |
      |checkpoint_lsn |No |Checkpoint log sequence number (LSN) during backup. |
      |database_backup_lsn |No |Backup LSN. |
      |backup_size |No |Backup file size. Unit: bytes. |
      |recovery_model |No |Backup mode. |
      

      * Example

      ```sql
      1,SQLTestDB,D,SQLTestDB_FULL.bak,Y
      2,SQLTestDB,L,SQLTestDB_Log1.bak,Y
      3,SQLTestDB,L,SQLTestDB_Log2.bak,Y
      ```
      

   * Automatically generate a metadata file

      1. Connect to the SQL Server instance connected over express network through SSMS.

      2. Obtain the metadata file

         Execute the following query command in the instance.

         ```sql
                         SELECT 
                                 backup_set_id,
                                 database_name, 
                                 type,
                                 physical_device_name,
                                 'Y' as is_upload,
                                 backup_start_date, 
                                 backup_finish_date, 
                                 first_lsn,
                                 last_lsn,
                                 checkpoint_lsn,
                                 database_backup_lsn,
                                 backup_size, 
                                 recovery_model
                         FROM msdb.dbo.backupset b
                         JOIN msdb.dbo.backupmediafamily m ON b.media_set_id = m.media_set_id
                         where database_name in ('<database_name>') and type in ('D','L')
                         and backup_start_date >= '<backup_start_date>'
                         ORDER BY backup_set_id ASC;
         ```
         

         When executing the above command, the following parameters need to be modified based on the actual situation:

         * `<database_name>` in `where database_name in ('<database_name>') and type in ('D','L')` is the actual database name.

         * `<back_start_date>` in `and backup_start_date >= '<backup_start_date>'` is the actual start date.

      3. Export the query result as a CSV file.

         1. The query results will be displayed on the **Results** tab. Right\-click any row in the window and select **Save Results As...** .

         2. In the pop\-up dialog box, select the directory and file name dts_backup_meta for saving the file, and select the file format as  **"CSV" (\*.csv)** .

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The saved metadata file name must be named dts_backup_meta, and the format must be <strong>"CSV" (\*.csv)</strong>.         </div>
         

         3. Click **Save**.

2. Upload the metadata file dts_backup_meta.csv to TOS Browser.

   1. Double\-click the TOS Browser icon. On the TOS Browser login page, configure the following parameter information.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Endpoint** |1. Obtain the TOS Endpoint.<br><br>   1. Log on to the [DTS console](https://console.byteplus.com/dts).<br><br>   2. On the top menu bar, select the project and region.<br><br>   3. In the left navigation bar, click **Data migration**.<br><br>   4. On the **Data migration list** page, click the target task name.<br><br>   5. On the **Task information** tab, copy the **TOS Endpoint** information in the **Source database information** area.<br><br>2. In the TOS Browser logon interface, select **Custom** from the **Endpoint** drop\-down list.<br><br>3. Copy the obtained TOS Endpoint to the customized input box. |
      |**Access Key ID** |Fill in the AccessKey ID information of the account. |
      |**Secret Access Key** |Fill in the Secret Access Key information of the account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For specific steps on viewing AKSK information, refer to <a href="https://docs.byteplus.com/en/docs/6291/65568">Viewing AKSK information</a>.</div><br> |
      |**Access path** |1. Obtain the TOS access path.<br><br>   1. Log on to the [DTS console](https://console.byteplus.com/dts).<br><br>   2. On the top menu bar, select the project and region.<br><br>   3. In the left navigation bar, click **Data migration**.<br><br>   4. On the **Data migration list** page, click the target task name.<br><br>   5. On the **Task information** tab, copy the **TOS Bucket** information in the **Source database information** area.<br><br>2. Copy the obtained TOS Bucket to the access path input box. The format is: `tos://Tos Bucket`. |
      |**Remarks** |(Optional) It is used to set the remark name for login, which is convenient for account management. The instructions are as follows:<br><br><br>* A maximum of 30 characters is supported.<br><br>* It does not support starting with a hyphen (\-).<br><br>* If it is not filled in, the default is `-`. |
      |**Automatic login** |Optional. Log in automatically when you use the TOS Browser again. |
      

   2. Click **Log in**.

   3. Click **Upload file** to upload the metadata CSV file to TOS Browser. You also need to set the access permission of the advanced settings for uploading files to **Inherit bucket**.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Inherit bucket indicates that the uploaded file object will inherit the bucket ACL, that is, the object's ACL policy will be consistent with the bucket ACL policy. For the relationship between object ACL and bucket ACL, refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-overview_4">Inheriting ACL settings from the bucket</a>.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the file access permission is not set to inherit bucket, the task migration will fail. For the procedure for modifying file access permissions, refer to <a href="https://docs.byteplus.com/en/docs/tos/docs-modifying-the-file-access-permission">Modifying file access permissions</a>. If you can not modify the access permission of the uploaded file, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.      </div>
      

   4. Click **Upload**.


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

<span id=".5Li65LuA5LmI5aSH5Lu95paH5Lu25LiA55u05Zyo5oGi5aSN5Lit77yf"></span>
#### Why is the backup file always in recovery?

The recovery may take a long time because the backup file to be recovered is large.

<span id=".5Lu75Yqh6L-B56e75aSx6LSl55qE5Y6f5Zug5piv5LuA5LmI77yf"></span>
#### What are the reasons for task migration failure?

When uploading a backup file, the file access permission is not set to inherit bucket. Inherit bucket indicates that the uploaded file object will inherit the bucket ACL, that is, the object's ACL policy will be consistent with the bucket ACL policy. For the procedure for modifying file access permissions, refer to [Modifying file access permissions](https://docs.byteplus.com/en/docs/tos/docs-modifying-the-file-access-permission).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you can not modify the access permission of the uploaded file, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div>

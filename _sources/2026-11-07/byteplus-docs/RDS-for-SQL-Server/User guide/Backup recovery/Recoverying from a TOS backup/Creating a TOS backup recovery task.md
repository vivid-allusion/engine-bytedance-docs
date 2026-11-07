---
title: "Creating a TOS backup recovery task"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-tos-backup-recovery-task"
---

This topic describes the steps to create a TOS backup recovery task.

<span id="background-information"></span>
## Background information

RDS for SQL Server supports convenient migration to cloud operations. Just upload the backup files of the self\-built database to the TOS (Torch Object Storage), and you can restore the backup files to the designated database through the TOS backup recovery function provided by RDS for SQL Server. TOS backup recovery function supports full recovery, differential recovery and log recovery to meet more business scenarios. The TOS backup recovery function adopts Microsoft's official backup recovery solution to strictly ensure stability and compatibility.

<span id="precautions"></span>
## Precautions


* Currently, recovery is only supported from backup sets that contain Microsoft SQL Server log files and SQL Server data files.

* If you need to perform differential recovery or log recovery, you need to restore the full backup it relies on first, and choose not to open the database, and then restore the differential or log backup on demand.

* When performing differential recovery or log recovery, it is necessary to ensure that the log sequence number (LSN) of the backup file is continuous, otherwise the recovery will fail.

* If the specified backup files contains multiple backup sets of the same type for databases with the same name, the recovery will be performed to the state of the latest backup set.

* If the original database contains F (Full\-text catalog), S (File stream, FileTable, or in\-memory OLTP container), recovery is not supported.

* During the TOS backup recovery process, the instance state is migrating.

* You can do the following for the instance in the migration:

   * Support viewing instance information in the migration.

   * Support manually backing up specified databases for instance in migration. For more information, see [Creating a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually).

   * Support backup files download for instance in migration. For details, see [Downloading data backup files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files) and [Downloading log backup files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-log-backups-files).

* The TOS backup recovery function adopts Microsoft's official backup recovery solution. It offers backward compatibility in recovery capabilities and supports recovery from backup files of the following versions:

   * Microsoft SQL Server 2022

   * Microsoft SQL Server 2019

   * Microsoft SQL Server 2017

   * Microsoft SQL Server 2016

   * Microsoft SQL Server 2014

   * Microsoft SQL Server 2012

   * Microsoft SQL Server 2008R2


<span id="prerequisite"></span>
## Prerequisite


* The bucket has been created in Torch Object Storage Service and the full backup files have been uploaded. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket) and [Uploading a file](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

* An instance of RDS for SQL Server has been created and is **in Running**, M**igrating** or R**ecovering**. For more information, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* The name of the database that needs to be restored from the backup file is already clear.

* (Optional)When the **Enable database** option is chosen in the cloud migration solution, the database will be automatically set to `Online` status, with the values of the below parameters also modified. To speed up the cloud migration process, we recommend you to manually adjust these parameters first:

   ```sql
   USE [master] 
   -- The database is set to read-write mode for easy reading and modification. 
   ALTER DATABASE [XXXX] SET READ_WRITE WITH NO_WAIT 
   GO 
   --Removed the automatic shutdown function of the database. In order to conserve system resources, some databases are automatically shut down when there is no active connection. 
   ALTER DATABASE [XXXX] SET AUTO_CLOSE OFF WITH NO_WAIT 
   GO 
   --The recovery mode of the database is set to full recovery mode. 
   ALTER DATABASE [XXXX] SET RECOVERY FULL WITH NO_WAIT 
   GO 
   --Allows multiple users to access the database simultaneously. 
   ALTER DATABASE [XXXX] SET MULTI_USER FULL WITH NO_WAIT
   ```
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can execute the following command to view the status of the database. This example uses the database <code>MyDatabase</code> as an example:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```sql
   SELECT name, user_access_desc, is_auto_close_on, recovery_model_desc 
   FROM sys.databases 
   WHERE name = 'MyDatabase'
   ```
      </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <code>user_access_desc</code> is <code>MULTI_USER</code>, <code>is_auto_close_on</code> is <code>0</code>, and <code>recovery_model_desc</code> is <code>FULL</code>, the database is configured correctly and no further action is required.   </div>
   

<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. In the left navigation bar, click **TOS backups** to enter the **TOS backup recovery list** page.

4. On the **TOS backup recovery list** page, click **Create recovery task** to enter the **Create recovery task** page.

5. On the **Create recovery task** page, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Recovery method |Defaults to **Self\-built TOS buckets** and does not support other selection. |
   |Bucket name |Required. The name of the TOS bucket that stores the backup files.<br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you are using the <strong>TOS backup recovery</strong> function for the first time, you need to click the <strong>Authorized</strong> on the right side of the bucket name drop\-down list.</div><br> |
   |Select backup |Required. Select the backup file to be restored.<br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only prefix search is supported. If the backup file is stored in a folder within the bucket, you need to enter the path of the file step by step. Display up to 20 matching results.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently only supports backing up files in <code>BAK</code>, <code>DIFF</code>, <code>TRN</code>, <code>LOG</code> formats.</div><br> |
   |Cloud migration solution |Required. You can choose to **Enable database** or ** Do** **not open the database**.<br><br><br>* **Enable database**: After the recovery is complete, the database automatically opens and becomes available. At this time, it is impossible to continue restoring log backups or differential backups to the database.<br><br>* **Do not open the database**: After the recovery is complete, the database remains in the recovery state, and you can continue to restore log backups or differential backups to the database. After the recovery is complete, you can also use stored procedures to modify the database state to Online. For more details, see [Modifying database state to online](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-database-status-to-online). |
   |Recovery type |Required. You can choose **Full recovery**, **Differential recovery**, **Log recovery**, and **Default recovery**.<br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <strong>Recovery type</strong> is selected <strong>Default recovery</strong>, it means that the database will be restored from the first full backup file by default. If you do not modify the database name (using the default setting):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the name duplicate an existing database name, the default name after recovery will be <code>database name + date</code>. </div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is no duplicate database name, the default name will be the original database name.</div><br> |
   |Select instance |Required. Select the target instance to restore to. You can search by instance name or instance ID. |
   |Database name to be restored |Set the following information on demand:<br><br><br>* **Original database name**: Fill in the name of the database to be restored, which must be consistent with the database name in the backup file. You can recover up to 20 databases at a time.<br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the <strong>Recovery type</strong> is selected as <strong>Default recovery</strong>, there is no need to configure the database name to be restored.   </div><br>   <br><br>* **New database name**: Customize the new database name. The new database name can be empty, if not set, it is the same as the original database name; if it is set, and the **Recovery type** selects **Full recovery** or **Default recovery**, then the new database name cannot be repeated with the existing database name. If the **Recovery type** selects **Differential recovery** or **Log recovery**, then the new database name must already exist. The naming conventions are as follows:<br><br>   * Begins with a letter and ends with a letter or number.<br><br>   * Length should be between 2 and 60 characters.<br><br>   * Consists of letters, numbers, and underscores (_), and letters are case\-insensitive.<br><br>   * Cannot use reserved words such as `master`, `msdb`, `model`, `tempdb`, `resource`, `rdsadmin`, `distribution`. |
   

6. Click **Submit.** 


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">During recovery, the instance is in <strong>Migrating</strong> state.</div>


<span id="next-steps"></span>
## Next steps

After the TOS backup file recovery task is completed and the database is opened, it is recommended to use the `DBCC CHECKDB` command to verify the integrity of the restored database. For specific commands, please refer to [DBCC CHECKDB (Transact-SQL) (Microsoft)](https://learn.microsoft.com/zh-cn/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql?spm=a2c6h.12873639.article-detail.4.11755196mF57jE&view=sql-server-ver16). After performing an integrity check, you will normally see the following results:

```sql
… 
CHECKDB found 0 allocation errors and 0 consisteency errors in database 'xx' 
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```


<span id="common-problem"></span>
## Common problem

If you encounter errors during the creation and execution of the recovery task, please refer to the following table for troubleshooting.


|**Error type** |**Possible reason** |**Solution** |
|---|---|---|
|Backup file validation failed |There is no recoverable database information in the backup file. |Verify the integrity of the backup file. If the backup file is damaged or the backup file does not contain the target database information, you need to regenerate the full backup file and upload the TOS, and then create the TOS backup recovery task. For information on how to upload files on TOS, see [Create a bucket ](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)and [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file). |
||When you select Full Recovery, the specified backup set contains a full\-text directory, file stream, FileTable, or in\-memory OLTP container. |Currently, recovery is only supported from backup sets that contain Microsoft SQL Server log files and SQL Server data files. If the backup set contains data stream files or full\-text catalog files, it cannot be used for recovery. In this case, you need to regenerate the backup file and upload the TOS, and then create the TOS backup recovery task. For information on how to upload files on TOS, see [Create a bucket ](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)and [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file). |
||When you select Full Recovery, the specified backup set does not contain Microsoft SQL Server log files or Microsoft SQL Server data files. |Currently, recovery is only supported from backup sets that contain Microsoft SQL Server log files and SQL Server data files. In this case, you need to regenerate the backup file and upload the TOS. For information on how to upload files on TOS, see [Create a bucket ](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)and [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file). |
||The backup file version is higher than the instance version. |Currently, recovery is supported from backup files of Microsoft SQL Server 2022 and earlier versions. However, there are limitations, restoring a backup file from a higher\-version instance to a lower\-version instance is not supported. Examples are as follows:<br><br><br>* If the backup file version is 2022 Enterprise Edition, it can only be restored to a 2022 Enterprise Edition instance.<br><br>* If the backup file version is 2022 Standard Edition, it can be restored to a 2022 Standard Edition or 2022 Enterprise Edition instance.<br><br>* If the backup file version is 2022 Web Edition, it can be restored to a 2022 Web Edition, 2022 Standard Edition, or 2022 Enterprise Edition instance.<br><br>* If the backup file version is 2019 Enterprise Edition, it can be restored to a 2019 Enterprise Edition or 2022 Enterprise Edition instance.<br><br>* If the backup file version is 2019 Standard Edition, it can be restored to a 2019 Standard Edition, 2019 Enterprise Edition, 2022 Standard Edition, or 2022 Enterprise Edition instance.<br><br>* If the backup file version is 2019 Web Edition, it can be restored to a 2019 Web Edition, 2019 Standard Edition, 2019 Enterprise Edition, 2022 Web Edition, 2022 Standard Edition, or 2022 Enterprise Edition instance. |
||Backup set integrity check failed. |Verify the integrity of the backup file. If the backup file is damaged, you need to regenerate the full backup file and upload the TOS, and then create the TOS backup recovery task. For information on how to upload files on TOS, see [Create a bucket ](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)and [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file). |
||An error was encountered while executing `DBCC CHECKDB`, indicating that the database may be corrupted in the local environment. |Restore to the cloud after fixing the local environment database error using the following command.<br><br>```java```<br>```DBCC CHECKDB (DBName, REPAIR_ALLOW_DATA_LOSS) WITH NO_INFOMSGS, ALL_ERRORMSGS;```<br><br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to perform a data backup before executing this command, otherwise the process of using this command to repair errors may result in data loss.</div><br> |
|The database does not exist |The database name entered is incorrect. There is no corresponding database information in the backup set. |1. Verify that the database name entered in the **database name to be restored** is correct.<br><br>2. Confirm that the uploaded backup file contains the target database.<br><br>3. Re\-upload the backup file.<br><br>4. Re\-create the TOS backup recovery task. |
|The database with the same name already exists |Full recovery, the database already exists and no overwrite is selected. |1. Verify that the database name entered in the **database name to be restored** is correct.<br><br>2. Change the option of **whether to overwrite recovery** in the TOS backup recovery task to **Yes**. |
|Lack of space |The instance free space does not meet the minimum space requirement for backup and recovery. |Expanding for instances. For more information about scaling, see [Change instance configuration](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/temporary-upgrade). |
|Failed to use differential backup file |Database state is not Restoring. |1. Use the corresponding full backup to recreate the TOS backup recovery task, and select the **cloud solution** to **not open the database**.<br><br>2. After the full recovery is completed, re\-use the differential backup file to create a TOS backup recovery task. |
||The differential backup does not match the target database. |Check that the differential backup file matches the target database. A database can only perform a differential restore once. After the differential restore is completed, only log restores can be performed subsequently. |
||The full recovery based on is a copyonly type. |After a full recovery based on a copyonly type of backup file, differential recovery is not allowed. |
||Differential backup file LSN continuity check failed. |Find differential backup files based on previous upload records to ensure LSN continuity. |
|Failed to backup file with log |Database state is not Restoring. |1. Use the corresponding full backup to recreate the TOS backup recovery task, and select the **cloud solution** to **not open the database**.<br><br>2. After the full recovery is completed, re\-use the log backup file to create a TOS backup recovery task. |
|Failed to restore using differential backup file |Differential backup failed during recovery. |Use the differential backup file to perform recovery in the local environment through SQL Server Management Studio:<br><br><br>* If successful, please [Submit a work order ](https://console.byteplus.com/workorder/create)for processing.<br><br>* If it fails, check the differential backup file. |
|Failed to restore using log backup file |Log backup failed during recovery. |Use the differential backup file to perform recovery in the local environment through SQL Server Management Studio:<br><br><br>* If successful, please [Submit a work order ](https://console.byteplus.com/workorder/create)for processing.<br><br>* If it fails, check the log backup file. |
|Backup file download failed |The TOS file does not exist. |Check the backup file at TOS and re\-upload the backup file. For information on how to upload files on TOS, see [Create a bucket ](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket)and [Upload files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file). |
||The file is too large and there is not enough space. |Expanding for instances. For more information about scaling, see [Change instance configuration](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/temporary-upgrade). |
|System error, please contact the administrator. |Unexpected situation, please contact the system admin. |Please [Submit a work order ](https://console.byteplus.com/workorder/create)for processing. |

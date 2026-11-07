---
title: "Upload incremental backup data from a local database to an RDS for SQL Server instance via TOS"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-incremental-backup-data-of-the-local-database-to-rds-for-sql-server-instance-through-tos"
---

RDS for SQL Server supports migrating local SQL Server data to the cloud through Object Storage TOS, which is suitable for scenarios such as data backup, disaster recovery, business expansion, development, and testing. This topic describes how to upload incremental backup data from a local database to an RDS for SQL Server instance via TOS.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Description

<span id=".6L-B56e75pa55qGI"></span>
### **Migration solutions**

RDS for SQL Server provides two solutions for migrating data to the cloud:


* Solution 1: Full backup to the cloud

   A full backup to the cloud allows for a one\-time data migration but requires extended service downtime. You need to upload the exported full backup file to Object Storage and then restore it to the target database instance.

* Solution 2: Full + incremental backup to the cloud

   The full + incremental backup method supports continuous data migration to the cloud. After completing the initial full backup, you can restore multiple incremental files to minimize service interruptions during the migration. An incremental restore typically requires multiple restore operations from incremental backups. After each restore, the target database will have an Importing status and will be unavailable for read/write operations. The database status changes to Running only after the final incremental backup restore is complete.


Cloud migration scenarios vary for databases of different sizes, as shown in the table below:


|**Service downtime duration** |**Size of database to be migrated (GiB)**  |**Recommended Solution** |
|---|---|---|
|30 min ~ 2 h |< 100 GiB |Solution 1 |
||≥ 100 GiB |Solution 2 |
|2 h ~ 4 h |< 200 GiB |Solution 1 |
||≥ 200 GiB |Solution 2 |
|4 h ~ 8 h |< 500 GiB |Solution 1 |
||≥ 500 GiB |Solution 2 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Solution 1 is suitable if your business can tolerate any amount of downtime.</div>


* <div data-tips="true" data-tips-type="tip">If your business cannot tolerate any downtime, the migration solutions in this document are not suitable.</div>



<span id=".6L-B56e75rWB56iL"></span>
### Migration Process

The following table shows an example migration process for a 100 GiB database from a local data center using full and incremental migration:


|**Cloud Migration Stage** |**Steps** |**Description** |
|---|---|---|
|Full Migration Stage |Preparations |Preparations include:<br><br><br>* Complete the CheckDB check in the database console.<br><br>* Disable the local backup system.<br><br>* Set the database to the FULL recovery model.<br><br>* Enable default backup compression. |
||Full database backup |Started a FULL Backup of the on\-premises database, which took approximately 30 minutes. The compressed backup is calculated at a 50% ratio. After completion, the backup file size will be approximately 50 GiB. |
||Upload a Full Backup to TOS |Uploading a 50 GiB backup file to a TOS Bucket at a public network speed of 10 MB/s takes about 2 hours. |
||Upload full backup files to the cloud |Start restoring the FULL Backup file in the RDS for SQL Server console, which takes approximately 1 hour. |
|Incremental stage |Back up and upload logs |Start the incremental database LOG backup to the cloud. The LOG backup is completed and uploaded to Object Storage TOS. Each LOG file is no larger than 200 MB, and the process takes about 20 minutes. |
||Cloud migration log backup file |The LOG Backup was restored to the cloud in approximately 10 minutes. |
||Repeat the two steps above. |Repeatedly perform LOG backups, upload them to object storage TOS, and incrementally migrate them to the cloud. This ensures that the final LOG backup file is as small as possible (under 200 MB). Stop local applications from writing to the database, perform another LOG backup, and then perform the final incremental migration to the cloud. |
|Enable database |Enable database |The final incremental upload of the log backup file is complete. This operation took 30 minutes, and the database is now being enabled. |
||Cloud migration complete |Bringing the database online takes only 1 minute if you choose to run database console operations asynchronously. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When performing an incremental migration to the cloud, you only need to stop application writes before the last LOG Backup, resulting in short application downtime. In this example, the last incremental LOG Backup migration to the cloud took about 31 minutes.</div>


<span id=".6L-B56e75pe26Ze0"></span>
### Migration Time

The phases of a complete backup migration are described in the following table:


|**Phase** |**Step** |**Description** |
|---|---|---|
|① |Export full and incremental database backup files. |The time required for this stage is primarily for generating the database backup file. This duration typically depends on the configuration and size of the source database. The specific time should be estimated based on the source database's configuration. |
|② |Upload Backup Files to a TOS Bucket |TOS does not have a speed limit. When you access TOS over the public network, your upload and download speeds are limited by your public network bandwidth. For example: if the public network bandwidth is 10 MB/s, the upload speed is 10 MB/s, assuming no other factors affect the network. |
|③ |Full recovery of the cloud migration task to the destination RDS for SQL Server via Object Storage TOS |The recovery speed is typically around 100 GiB/h. |
|④ |Use a TOS cloud migration task to incrementally restore data to the target RDS for SQL Server |Continuously upload locally generated incremental backups and restore them to the target instance. The restoration speed is typically around 100 GiB/h. |



* Migration duration = Duration of Phase ① + Duration of Phase ② + Duration of Phase ③ + Duration of Phase ④

* Business downtime = Time to perform the last incremental backup + Time to upload to TOS + Time to create a restore task from TOS


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only migrate backup files from an earlier version to a database instance of a later version. Migrating backup files from a later version to an earlier version is unsupported. The version restrictions are as follows:

   * Commercial database edition: Upgrade from a lower to a higher edition. For example, you can upgrade from Web Edition to Standard Edition, and then to Enterprise Edition.

   * Database compatible versions: For example, migration is only supported from SQL Server 2012 to SQL Server 2019, not from SQL Server 2012 to SQL Server 2019.

* Backup file names cannot contain special characters, including `\\`, `/`, `:`, `*`, `?`, `\"`, `<`, `>`, `|`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `*`, `(`, `)`, `_`, `+`, `-`, and `=`.

* Do not delete backup files from Object Storage TOS before the cloud data restore task is complete. Otherwise, the cloud migration will fail.

* The backup file extension must be `bak`, `diff`, `trn`, or `log`, as follows:

   * `bak`: Full backup.

   * `diff`: Differential backup.

   * `trn` or `log`: Transaction log backup.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a backup file does not have one of the above extensions, the system may not correctly identify the file type, which will affect subsequent operations.   </div>
   

* Before migrating a production database, first test and evaluate the process in a development or test environment. If you need to run an assessment in a production environment, test during off\-peak hours to minimize business impact.


<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios

Database migration to RDS for SQL Server is suitable for the following scenarios:


* **Data backup and disaster recovery**: RDS for SQL Server provides efficient backup and disaster recovery solutions. If hardware fails or data is accidentally damaged, you can restore data from cloud backups.

* **Business expansion**: If your business is expanding and needs more server and storage resources for your data, migrating to a cloud database can lower your hardware and maintenance costs. The cloud database can also scale elastically to meet business demands.

* **Real\-time services**: Cloud databases deliver efficient, high\-speed processing to support real\-time access and queries for large numbers of concurrent users, making them ideal for real\-time services.

* **Development and testing environments**: A cloud database provides an independent environment that is easy to build and manage, making it ideal for development and testing.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|Category |Description |
|---|---|
|TOS Object Storage |* TOS Object Storage is enabled. For more information, see [Enabling TOS Object Storage](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1#.5q2l6aqk5LiA77ya5byA6YCaLXRvcy3mnI3liqE=).<br><br>* Download and install TOS Browser. For detailed instructions, refer to [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3). |
|RDS for SQL Server |* A database instance has been created. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).<br><br>* The available storage space of the target database instance must be 1.5 times the total size of the database to be restored. If the instance's storage space is insufficient, increase it. For detailed operations, see [modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification) [modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification).<br><br>* Run the following command to set the database status to the full recovery model. This model records all transactions in the transaction log, enabling the recovery of all operations if a failure occurs.<br><br>   ```sql```<br>```   ALTER DATABASE [DBName] SET RECOVERY FULL WITH NO_WAIT;```<br>```   ```<br>   <br><br>* Run the following command to set the database's `AUTO_CLOSE` option to `OFF` and release all system resources used by the database:<br><br>   ```sql```<br>```   ALTER DATABASE [DBName] SET AUTO_CLOSE OFF WITH NO_WAIT;```<br>```   ```<br>    |
|Enable backup compression |Run the following code to view and enable default backup compression:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Backup compression is only supported for Standard and Enterprise Editions. It is unsupported for the Web Edition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Enabling default backup compression significantly increases CPU usage and prolongs the overall time required for a full backup. For more details, see <a href="https://learn.microsoft.com/zh-cn/sql/database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option?view=sql-server-ver17">Enable default backup compression in Microsoft SQL Server</a>.</div><br><br><br><br>```SQL```<br>```use master;```<br>```GO```<br>``` -- Check if compression is enabled. A value of 0 means it is disabled, and a value of 1 means it is enabled.```<br>```SELECT value```<br>```FROM sys.configurations```<br>```WHERE name = 'backup compression default';```<br>```GO```<br>```-- Set to enable compression by default. The web version will automatically ignore this option.```<br>```EXECUTE sp_configure 'backup compression default', 1;```<br>``````<br>```RECONFIGURE;```<br>```GO```<br> |
|Others |* The local environment backup system is disabled.<br><br>* Since the default language for RDS for SQL Server is English, we recommend changing it to Chinese to make future operations easier. For detailed instructions, see [How to Change the Language for SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-to-change-the-locale-of-rds-for-sql-server).<br><br>* Run the `DBCC CHECKDB` statement in the local database environment to ensure the database has no `allocation errors` or `consistency errors`. And you will get the following result for a successful execution:<br><br>   ```sql```<br>```   ...```<br>```   CHECKDB found 0 allocation errors and 0 consistency errors in database 'xxx'.```<br>```   DBCC execution completed. If DBCC printed error messages, contact your system administrator.```<br>```   ```<br>    |


<span id=".5q2l6aqk5LiA77ya5LiK5Lyg5pys5Zyw5pWw5o2u5bqT55qE5YWo6YeP5aSH5Lu95pWw5o2u6Iez5LqR5pWw5o2u5bqTLXNxbC1zZXJ2ZXIt54mI5a6e5L6L"></span>
## Step 1: Upload the full backup of your local database to an RDS for SQL Server instance

Before uploading incremental data, you must first upload a full backup. For detailed instructions, refer to [Upload the full backup of your local database to an RDS for SQL Server instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-full-backup-data-of-local-database-to-rds-for-sql-server-instance-through-tos).

<span id=".5q2l6aqk5LqM77ya5aSH5Lu95pys5Zyw5beu5byC5ZKM5pel5b-X5paH5Lu2"></span>
## Step 2: Back up local differential and log files

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before backing up local files, ensure that data writing is stopped. New data will not be backed up, which can cause data inconsistency.</div>



1. In the query editor of your local SQL Server database, run the following commands to back up differential and log data:

   * Differential backup

      ```sql
      BACKUP DATABASE [<db_name>] TO  DISK = N'<backup location, e.g. E:\backup\dbname_diff.bak' WITH DIFFERENTIAL, NOFORMAT, NOINIT,  NAME = N'<dbname>-Diff Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
      ```
      

   * Log backup

      ```sql
      BACKUP LOG [<db_name>] TO  DISK = N'<backup location, e.g. E:\backup\dbname_log.bak' WITH NOFORMAT, NOINIT,  NAME = N'<dbname>-Log Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
      ```
      

2. Rename the backup file to `DatabaseName_BackupType_Timestamp.bak`.


<span id=".5q2l6aqk5LiJ77ya5LiK5Lyg5pWw5o2u5bqT5aSH5Lu95paH5Lu2"></span>
## Step 3: Upload the database backup files


1. Create a Bucket

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If a bucket has already been created in Object Storage Service (TOS), check whether it meets the following requirements:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is in the same region as the RDS for SQL Server instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The bucket policy is set to Public Read.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The storage type is Standard Storage.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Server\-side encryption is disabled.   </div>
   

   1. Log in to the [Object Storage Service console](https://console.byteplus.com/tos).

   2. In the left navigation pane, click **Bucket List**. In the upper\-left corner of the page, click **Create Bucket**.

   3. Set the bucket parameters. The table below describes some of the parameters. Then, click **OK**.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Region** |It must be in the same region as the RDS for SQL Server instance. |
      |**Bucket policy** |Set to public\-read. This allows anyone to perform read operations on a bucket with public\-read permissions. |
      |**Default storage type** |Must be set to Standard storage. This storage type is suitable for frequent access. |
      |**Server\-side Encryption** |Set to None (no encryption). |
      

2. Upload database backup files

   1. Method 1: (Recommended) Upload files via TOS Browser

      * Log in to TOS Browser. To learn how to obtain your AK and SK, see [Get Access Key](https://docs.byteplus.com/en/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

      * On the **Bucket List** page, click the target bucket.

      * On the target bucket page, click **Upload File**.

      * On the **Upload File** panel, after uploading the file, click **OK**.

   2. Method 2: Upload files via the TOS console

      * Log in to the [TOS console](https://console.byteplus.com/tos).

      * In the left navigation pane, click **Bucket List**.

      * On the **bucket list** page, click the name of the target bucket.

      * On the **file list** page, click **Upload File**.

      * On the **Upload File** page, click **OK** after uploading the file.


<span id=".5q2l6aqk5Zub77ya5a-85YWl5beu5byC5oiW5pel5b-X5aSH5Lu95pWw5o2u"></span>
## Step 4: Import differential or log backup data

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you upload the full backup data, upload the differential or log backup data. Also, keep the following in mind when uploading differential or log backup databases:</div>



* <div data-tips="true" data-tips-type="tip">If you have multiple log backups, create a separate task for each one.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that each backup file is no larger than 500 MB, and preferably under 200 MB, to reduce the time for incremental migration to the cloud.</div>


* <div data-tips="true" data-tips-type="tip">Before generating the last log backup for upload, you must stop all write operations to the local database. Failure to do so may cause data inconsistency and other issues.</div>


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. In the left\-side navigation pane, click **TOS Backup and Restore List** to go to the **TOS Backup and Restore List** page.

4. On the **TOS Backup and Restore List** page, click **Create TOS Backup File Restore Task** to go to the **Create TOS Backup File Restore Task** page.

5. On the **Create TOS Backup File Restore Task** page, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Restore method |The default is a **Self\-built TOS bucket** and cannot be changed. |
   |Bucket name |The name of the TOS bucket for storing backup files. |
   |Select backup |Required. Select the backup file to restore.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports prefix search only. If the backup file is stored in a subfolder within the bucket, you must enter the file's full path. Displays up to 20 matching results.</div><br> |
   |Cloud migration solution |You can select **Enable database** or **Do not open the database**.<br><br><br>* Enable database: after the restoration is complete, the database automatically opens and becomes available. You can no longer restore log or differential backups to the database.<br><br>* Do not open the database: after the restoration is complete, the database remains in the recovering state. You can continue to restore log or differential backups to the database. After the restoration is complete, you can also use a stored procedure to change the database status to Online. For more information, see [Change the database status to Online](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-database-status-to-online). |
   |Recovery type |Select **Differential recovery** or **Log recovery**. |
   |Overwrite restore |Currently, you can only select **No**. |
   |Select instance |Select the target instance to restore to. You can search by instance name or instance ID. |
   |Database name to be recovered |Enter the name of the database to restore. The name must match the database name in the backup file. Restore up to 20 databases at a time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You do not need to configure this parameter when you select <strong>Default recovery</strong> as the <strong>Recovery type</strong>.</div><br> |
   


<span id=".5q2l6aqk5LqU77ya5p-l55yL5aSH5Lu95LiK5LqR6K6w5b2V"></span>
## Step 5: View cloud backup records

After the cloud backup operation is complete, you can view the TOS backup and restore tasks. For details, see [View TOS Backup and Restore Tasks](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/view-tos-backup-recovery-tasks).

<span id=".5q2l6aqk5YWt77ya6L-B56e75a6M5oiQ5ZCO6YWN572u5LqR5LiK5a6e5L6L55qE5Y-C5pWw"></span>
## Step 6: Configure the parameters of the cloud instance after migration

After migrating your local data to the cloud using TOS, you can also follow these practices to configure Login accounts, DBLink connections, and Agent Jobs to maintain consistency with your on\-premises experience.

<span id=".5Yib5bu6LWxvZ2luLei0puWPtw=="></span>
### Create Login accounts

A Login account is an instance\-level account for RDS for SQL Server, primarily used to manage your server and database permissions. You can use the following methods to create Login accounts with the same passwords and permissions as your on\-premises ones. The specific steps are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your account has SA permissions, we recommend prioritizing Method 1. When using this method, if other databases from the same on\-premises instance are later migrated to the cloud via TOS, their permissions will be automatically linked to the corresponding Login accounts. If your account does not have SA permissions, we recommend using Method 2.</div>



* Method 1 (Recommended): Create Login accounts using T\-SQL

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Use case: The account has SA permissions. Replay all SQL Logins from the source instance, including passwords and default languages.   </div>
   

   1. Log in to the local IDC instance and execute the following script command with SA permissions to get the creation script for the local instance's Login accounts:

      ```sql
      SELECT 'IF (SUSER_ID(N'+QUOTENAME(SP.name,'''')+') IS NULL) BEGIN CREATE LOGIN ' +QUOTENAME(SP.name)
      +' WITH PASSWORD = ' +CONVERT(NVARCHAR(MAX),SL.password_hash,1)+ ' HASHED,SID=' +CONVERT(NVARCHAR(MAX),SP.sid,1)
      +' ,DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[' +SP.default_language_name+ '] END;' as CreateLogin
      FROM sys.server_principals AS SP LEFT JOIN sys.sql_logins AS SL
      ON SP.principal_id = SL.principal_id
      WHERE SP.type ='S'
      AND SP.name NOT LIKE '##%##'
      AND SP.name NOT LIKE 'NT AUTHORITY%'
      AND SP.name NOT LIKE 'NT SERVICE%'
      AND SP.name NOT IN ('rdsadmin','rdsbackup','rdsmirror','public','sa','veyun_user')
      -- AND SP.name = N'user1'
      ```
      

      Expected output:

      ```sql
      IF (SUSER_ID('UserName') IS NULL) BEGIN CREATE LOGIN [UserName] WITH PASSWORD = {PassWord}... HASHED,SID={SID},CHECK_EXPIRATION = ON, CHECK_POLICY = ON, DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[English] END;
      ```
      

   2. Connect to the cloud instance through SSMS or Database Workshop (DBW). For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

   3. Execute the output from Step 1 to create the same Login account as the on\-premises instance.

* Method 2: Create Login accounts using T\-SQL

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Use case: The account does not have SA permissions. Replay SQL Logins from the source instance for a single database (excluding passwords and default languages).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Usage limitation: You must have <code>db_owner</code> permission for the database on the source instance.   </div>
   

   1. Log in to the local IDC instance and execute the following script command to get the creation script for the local instance's Login accounts:

      ```SQL
      USE [xxxxx]-- xxxxx is the database for replaying the login.
      GO
      SELECT 'IF (SUSER_ID(N'+QUOTENAME(SDP.name,'''')+') IS NULL) BEGIN CREATE LOGIN ' +QUOTENAME(SDP.name)
      +' WITH PASSWORD = N''Password123'',SID=' -- Password123 is an example. You can replace it with your desired password as needed.
      +CONVERT(NVARCHAR(MAX),SDP.sid,1)
      +' ,DEFAULT_DATABASE=[master]; END;' as CreateLogin
      FROM sys.database_principals AS SDP 
      WHERE SDP.type ='S'
      AND SDP.name NOT IN ('dbo','guest','INFORMATION_SCHEMA','sys', 'veyun_user')
      ```
      

      Expected output:

      ```sql
      IF (SUSER_ID(N'UserName') IS NULL) BEGIN CREATE LOGIN [UserName] WITH PASSWORD = {PassWord},SID={SID},DEFAULT_DATABASE=[master]; END;
      ```
      

   2. Connect to the cloud instance through SSMS or Database Workshop (DBW). For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

   3. Execute the output from Step 1 to create the same Login account as the on\-premises instance.

* Method 3: Create a Login account using the console

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Applicable scenario: A Login account exists for an instance on BytePlus, but its permissions differ from the source database.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Usage restrictions: The same operation must be performed for each database.   </div>
   

   1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

   2. Create the same Login account as the on\-premises instance. For detailed steps, refer to [Creating an account](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).

   3. Connect to the cloud instance through SSMS or Database Workshop (DBW). For details, see [Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-an-instance).

   4. Run the following script command in the target instance to associate the database user with the instance\-level Login, ensuring the account has the same permissions on the current database as it does on the local database.

   ```sql
   declare @DBName nvarchar(200)
   declare @Login_name nvarchar(200)
   declare @SQL nvarchar(MAX)
   set @Login_name = 'TestLogin7' -- Enter the login name and execute them one by one
   declare DBName_Cursor cursor for
   select quotename(name)from sys.databases where  database_id > 5 and state = 0
   and name not like '%$%'
   and name <> 'rdsadmin'
   open DBName_Cursor
   fetch next from DBName_Cursor into @DBName
   WHILE @@FETCH_STATUS= 0
   begin
   SET @SQL= N'    USE '+ (@DBName)+ '
   if exists(select top 1 1 from sys.sysusers where name = '''+ @Login_name +''')
   begin
   ALTER USER '+@Login_name+' with login = '+@Login_name+';
   end
   '
   print @SQL
   EXEC (@SQL)
   fetch next from DBName_Cursor into @DBName
   end
   close DBName_Cursor
   deallocate DBName_Cursor
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After completing the above operations, your cloud instance account will have the same permissions on the current database as it does on the local one.   </div>
   

<span id=".5Yib5bu6LWRibGluay3ov57mjqU="></span>
### Create a DBLink connection

SQL Server supports DBLink connections to interact with data on external instances. This allows you to query, sync, and compare data between different instances, including those of different database types. If you use this service on your local instance, the local DBLink connections will not automatically sync to the cloud instance after migration. You must manually sync them by following the instructions below:


* Method 1: Create a DBLink connection using T\-SQL

   1. Run the following command in the local database to get the DBLink name, data source, and other information.

      ```sql
      -- Get the basic information of the linked server
      SELECT 
          srv.name AS linked_server_name,
          srv.product AS server_product,
          srv.providername AS provider_name,
          srv.datasource AS data_source
      FROM 
          sys.servers AS srv
      WHERE 
          srv.is_linked = 1;
      
      -- Get the linked server login mapping information
      SELECT 
          lrmtsrv.name AS linked_server_name,
          lrmterr.locallogin AS local_login,
          lrmterr.useself AS uses_self,
          lrmterr.rmtuser AS remote_user,
          lrmterr.rmtpassword AS remote_password
      FROM 
          sys.linked_logins AS lrmterr
      JOIN 
          sys.servers AS lrmtsrv ON lrmterr.server_id = lrmtsrv.server_id
      WHERE 
          lrmtsrv.is_linked = 1;
      ```
      

   2. In your cloud database instance, create the same DBLink using the configuration from the previous step. For example:

      ```sql
      -- Example: Create a linked server in the cloud
      EXEC sp_addlinkedserver 
          @server = 'RemoteServer',    -- Linked server name
          @srvproduct = 'SQL Server',  -- Server product name
          @provider = 'SQLNCLI11',     -- Provider name
          @datasrc = 'RemoteServerNameOrIP'; -- Data source
      
      -- Set the login mapping for the linked server
      EXEC sp_addlinkedsrvlogin 
          @rmtsrvname = 'RemoteServer',
          @useself = 'FALSE',
          @locallogin = NULL,             -- Local login
          @rmtuser = 'remoteUsername',   -- Remote user
          @rmtpassword = 'remotePassword';-- Remote user password
      ```
      

* Method 1: Create a DBLink connection by connecting to the instance via SSMS.

   1. Get all DBLink connections on the local instance.

      1. Connect to the local database instance via SSMS.

      2. In the left navigation pane, select **Server Objects** \> **Linked Servers**.

      3. Find the target DBLink connection and press **Fn+F7**.

      4. In the new pop\-up window, create a script to copy all DBLink connections on the current instance.

   2. Create a DBLink connection in the cloud database.

      1. Connect to the cloud database instance using SSMS.

      2. In the left navigation pane, select **Server Objects** \> **Linked Servers**.

      3. Copy the DBLink script file from the local database instance to the cloud database instance.

      4. Modify the password for `@rmtpassword` and execute the script command. An example of the script command is as follows:

         The created script may contain many default system configurations. However, for each DBLink connection to run successfully, you only need to retain the following two key scripts. You must also re\-enter the account connection password.

         ```sql
         USE [master]
         GO
         
         /****** Object:  LinkedServer [AAAA]    Script Date: 2024/2/18 16:24:40 ******/
         EXEC master.dbo.sp_addlinkedserver @server = N'AAAA', @srvproduct=N'AAAA', @provider=N'SQLNCLI', @datasrc=N'PF2L1S4P-DMA\MSSQL_2019_STD'
          /* For security reasons the linked server remote logins password is changed with ### */
         EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'AAAA',@useself=N'False',@locallogin=NULL,@rmtuser=N'veyun_user',@rmtpassword='###'
         GO
         ```
         


<span id=".5Yib5bu6LWFnZW50LWpvYi3ov57mjqU="></span>
### Create an Agent Job connection

Agent Job, also known as the SQL Server Agent service, allows you to quickly create scheduled tasks in an instance for daily O&M and data processing. Therefore, you need to migrate the Jobs from your local instance to the cloud instance. The specific steps are as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Owner account for a new Job is crucial. In RDS for SQL Server, only the Job's Owner can see their own Job on the instance, while other Login accounts cannot see or operate it. Therefore, we recommend that all Jobs share the same Owner account for easier management.</div>



1. Get the script file for the Jobs on the local instance.

   1. Connect to the local database instance via SSMS.

   2. In the left navigation pane, select **SQL Server Agent** \> **Jobs**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29b64efb7dfb20eb1f3534c4da622d1c.png) </span>

   3. Press **Fn+F7**. On the **Object Explorer Details** page, select all Jobs, then right\-click and select **Script Job as** \> **Create To** \> **New Query Window**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a735477c64e9b06e37d3b90c480ea467.png) </span>

   4. In the pop\-up window, copy the T\-SQL to create a script and note the following information:

      * Modify the Owner account for each Job. For example: `@owner_login_name=N'veyun_user'`.

      * Modify the instance name for each Job. For example: `@server=N'Instance IP'`, `@server_name = N'Instance IP'`.

2. Create Jobs script commands in the cloud instance.

   1. Connect to the cloud database instance using SSMS.

   2. In the left navigation pane, select **SQL Server Agent** \> **Jobs**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_54cdb0f449570ad31517f13c118255f5.png) </span>

   3. Press **Fn+F7**. On the **Object Explorer Details** page, select all Jobs, then right\-click and select **Script Job as** \> **Create To** \> **New Query Window**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a71398179f2243c11dcba7c44e7116.png) </span>

   4. In the pop\-up window, copy the Jobs script commands from the local instance.

---
title: "Upload full backup data from a local database to an RDS for SQL Server instance via TOS"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/upload-full-backup-data-of-local-database-to-rds-for-sql-server-instance-through-tos"
---

RDS for SQL Server supports migrating local SQL Server data to the cloud via object storage TOS. This is applicable for scenarios such as data backup, disaster recovery, business expansion, development, and testing. This topic describes how to upload full backup data from a local database to an RDS for SQL Server instance via TOS.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Description

<span id=".6L-B56e75pa55qGI"></span>
### **Migration Solutions**

RDS for SQL Server provides two solutions for migrating data to the cloud:


* Solution 1: Full backup cloud migration

   Full backup cloud migration allows for a one\-time data migration but requires extended service downtime. You need to upload the exported full backup file to object storage and then restore it to the target database instance.

* Solution 2: Full + incremental backup cloud migration

   Full + incremental backup cloud migration allows for continuous data migration. After completing the initial full backup, you can restore multiple incremental files to minimize service downtime during the migration. Incremental restore typically requires restoring multiple incremental backups. After each restore, the target database will be in the Importing status and cannot be read from or written to. The database will change to the Running status only after the final incremental backup is restored.


Cloud migration scenarios for databases of different sizes vary. For details, see the following table:


|**Service interruption duration** |**Size of the database to be migrated (GiB)**  |**Recommended solution** |
|---|---|---|
|30 min ~ 2 h |< 100 GiB |Solution 1 |
||≥ 100 GiB |Solution 2 |
|2 h ~ 4 h |< 200 GiB |Solution 1 |
||≥ 200 GiB |Solution 2 |
|4 h ~ 8 h |< 500 GiB |Solution 1 |
||≥ 500 GiB |Solution 2 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Solution one is applicable if your business can tolerate any length of downtime.</div>


* <div data-tips="true" data-tips-type="tip">If your business cannot tolerate any length of downtime, the migration solutions described in this document are not suitable.</div>



<span id=".6L-B56e75rWB56iL"></span>
### Migration process

This example describes the process of migrating a 100 GiB database from a local data center using a full and incremental migration method. For details, see the following table:


|**Cloud migration phase** |**Step** |**Description** |
|---|---|---|
|Full phase |Preparations |Preparations include:<br><br><br>* Complete the CheckDB check from the database console.<br><br>* Disable the local backup system.<br><br>* Set the database recovery model to FULL.<br><br>* Enable default backup compression. |
||Full database backup |Start a full backup of the offline database. This takes about 30 minutes. Assuming a 50% compression ratio, the backup file size is approximately 50 GiB after completion. |
||Upload the full backup to TOS. |Uploading a 50 GiB backup file to a TOS Bucket at a public network speed of 10 MB/s takes about 2 hours. |
||Upload full backup files to the cloud |Start restoring the FULL Backup file in the RDS for SQL Server console. The process takes approximately 1 hour. |
|Enable database |Cloud migration complete |Complete the database go\-live. If you choose to perform database console operations asynchronously, the process is faster and takes about 1 minute. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, migrating 100 GiB of data to the cloud using a full backup requires approximately 3 hours and 31 minutes of application downtime.</div>


<span id=".6L-B56e75pe26Ze0"></span>
### Migration Time

The following table describes the stages of a complete backup migration:


|**Phase** |**Step** |**Description** |
|---|---|---|
|① |Export database full backup files |The time spent in this stage is mainly for generating the database backup file. The duration depends on the configuration and size of the source database, which you will need to estimate. |
|② |Upload backup files to a TOS bucket |TOS has no speed limit. When you access TOS over the public network, your upload and download speeds are limited by your public network bandwidth. For example, with a public network bandwidth of 10 MB/s, the upload speed is 10 MB/s, provided no other factors affect the network. |
|③ |Fully restore to the target RDS for SQL Server instance via a cloud migration task using Object Storage Service (TOS). |The restore speed is typically around 100 GiB/h. |



* Migration Duration = Stage ① Duration + Stage ② Duration + Stage ③ Duration

* Service Downtime = Uploading to Object Storage TOS + Creating an Object Storage TOS restore task


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only migrate backup files from an older version to a newer database instance. Migrating backup files from a newer version to an older version is not supported. The version restrictions are as follows:

   * Commercial database versions: we recommend migrating from a lower to a higher version, such as from Web Edition to Standard Edition and then to Enterprise Edition.

   * Compatible database version: For example, migration is only supported from SQL Server 2012 to SQL Server 2019, but not from SQL Server 2019 to SQL Server 2012.

* Backup file names cannot contain special characters, including `\\`, `/`, `:`, `*`, `?`, `\"`, `<`, `>`, `|`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `*`, `(`, `)`, `_`, `+`, `-`, and `=`.

* Before the cloud migration task is complete, do not delete the backup files on Object Storage TOS. Otherwise, the migration will fail.

* The backup file extension must be `bak`, `diff`, `trn`, or `log`, as follows:

   * `bak`: Full backup file.

   * `diff`: Differential backup file.

   * `trn` or `log`: Transaction log backup file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the backup file extension is not in the specified format, the system may not correctly identify the file type, affecting subsequent operations.   </div>
   

* If the `BAK` backup file size exceeds 5 GiB, use the [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3) graphical management tool or the [tosutil](https://docs.byteplus.com/en/docs/tos/overview) command\-line tool to upload it.

* Before migrating a production database, we recommend that you first perform tests and evaluations in a development or testing environment. If you need to run an assessment in a production environment, test it during off\-peak hours to reduce the business impact.


<span id=".6YCC55So5Zy65pmv"></span>
## Applicable scenarios

RDS for SQL Server database migration is applicable to the following scenarios:


* **Data backup and disaster recovery**: Cloud databases provide efficient backup and disaster recovery solutions. You can restore data from cloud backups in case of hardware failure or accidental data damage.

* **Business expansion**: If your business is expanding and requires more servers and storage resources to handle your data needs, migrating to a cloud database can lower hardware and operational costs. A cloud database can also scale elastically based on your business requirements.

* **Real\-time services**: Cloud databases provide efficient and fast processing capabilities, supporting real\-time access and queries from a large number of concurrent users. This makes them highly suitable for scenarios requiring real\-time business support.

* **Development and test environments**: A cloud database provides an independent environment that is easy to build and manage, making it ideal for development and testing.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


|Category |Description |
|---|---|
|Object Storage TOS |* TOS has been activated. For more information, see [Activate TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1#.5q2l6aqk5LiA77ya5byA6YCaLXRvcy3mnI3liqE=).<br><br>* Download and install TOS Browser. For detailed instructions, see [TOS Browser](https://docs.byteplus.com/en/docs/tos/Overview3). |
|RDS for SQL Server |* A database instance has been created. For detailed operations, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).<br><br>* The target database instance must have available storage space of at least 1.5 times the total size of the database to be restored. If the storage space is insufficient, increase the instance's storage space. For detailed instructions, see [modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification) [modification of specification](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/regular-modification-of-specification).<br><br>* Run the following command to set the database to the full recovery model. This model logs all transactions in the transaction log, allowing for the recovery of all operations in case of a failure.<br><br>   ```sql```<br>```   ALTER DATABASE [DBName] SET RECOVERY FULL WITH NO_WAIT;```<br>```   ```<br>   <br><br>* Run the following command to set the database's `AUTO_CLOSE` option to `OFF` to release all system resources it uses:<br><br>   ```sql```<br>```   ALTER DATABASE [DBName] SET AUTO_CLOSE OFF WITH NO_WAIT;```<br>```   ```<br>    |
|Enable backup compression |Run the following code to view and enable default backup compression:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Backup compression is only supported for Standard and Enterprise Editions. It is unsupported for the Web Edition.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Enabling default backup compression significantly increases CPU usage and prolongs the overall time for a full backup. For more information, see <a href="https://learn.microsoft.com/zh-cn/sql/database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option?view=sql-server-ver17">Enable default backup compression in Microsoft SQL Server</a>.</div><br><br><br><br>```SQL```<br>```use master;```<br>```GO```<br>``` -- Checks if compression is currently enabled. A value of 0 means disabled; a value of 1 means enabled.```<br>```SELECT value```<br>```FROM sys.configurations```<br>```WHERE name = 'backup compression default';```<br>```GO```<br>```-- Sets compression as enabled by default. The web version will automatically ignore this option.```<br>```EXECUTE sp_configure 'backup compression default', 1;```<br>``````<br>```RECONFIGURE;```<br>```GO```<br> |
|Others |* The on\-premises backup system has been disabled.<br><br>* Since the default language of RDS for SQL Server is English, change it to Chinese to simplify future operations. For detailed instructions, see [How to change the language setting of SQL Server](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/how-to-change-the-locale-of-rds-for-sql-server).<br><br>* Run the `DBCC CHECKDB` statement in your local database environment to ensure that the database has no `allocation errors` or `consistency errors`. A normal execution returns the following result:<br><br>   ```SQL```<br>```   ...```<br>```   CHECKDB found 0 allocation errors and 0 consistency errors in database 'xxx'.```<br>```   DBCC execution completed. If DBCC printed error messages, contact your system administrator.```<br>```   ```<br>    |


<span id=".5q2l6aqk5LiA77ya5aSH5Lu95pys5Zyw5paH5Lu2"></span>
## Step 1: Back up local files

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Stop writing data before backing up local files. New data will not be backed up, which can lead to data inconsistency.</div>



1. In the query editor of your on\-premises SQL Server database, run the following command to back up all data:

   ```sql
   BACKUP DATABASE [<db_name>] TO  DISK = N'<backup location, e.g. E:\backup\dbname.bak' WITH NOFORMAT, NOINIT,  NAME = N'<dbname>-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
   ```
   

2. Rename the backup file to `DatabaseName_BackupType_Timestamp.bak`.


<span id=".5q2l6aqk5LqM77ya5LiK5Lyg5pWw5o2u5bqT5aSH5Lu95paH5Lu2"></span>
## Step 2: Upload the database backup file


1. Create a bucket

   1. Log on to the [Object Storage Service console](https://console.byteplus.com/tos).

   2. In the left\-side navigation pane, click **Bucket List**, then click **Create Bucket** in the upper\-left corner of the page.

   3. Set the bucket parameters as described in the table below, and then click **OK**.

      
      |**Parameter** |**Description** |
      |---|---|
      |**Region** |It must be in the same region as the RDS for SQL Server instance. |
      |**Bucket policy** |Must be set to public read. This allows anyone to read from buckets with public read permissions. |
      |**Default storage type** |Must be set to Standard storage. This storage type is suitable for frequent access. |
      |**Server\-side encryption** |Must be set to None and unencrypted. |
      

2. Upload database backup files

   * Method 1: (Recommended) Upload files using TOS Browser

      1. Log in to TOS Browser. For instructions on obtaining your AK and SK, see [Obtain Access Key](https://docs.byteplus.com/en/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

      2. On the **Bucket List** page, click the target bucket.

      3. On the target bucket page, click **Upload File**.

      4. On the **Upload File** page, upload the file and click **Upload**.

   * Method 2: Upload files using the Object Storage TOS console

      1. Log in to the [Object Storage console](https://console.byteplus.com/tos).

      2. In the left navigation pane, click **Bucket List**.

      3. On the **Bucket List** page, click the name of the target bucket.

      4. On the **File List** page, click **Upload File**.

      5. On the **Upload File** page, click **OK** after uploading the file.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If the size of a <code>BAK</code> backup file exceeds 5 GiB, upload it using the <a href="https://docs.byteplus.com/en/docs/tos/Overview3">TOS Browser</a> graphical management tool or the <a href="https://docs.byteplus.com/en/docs/tos/overview">tosutil</a> command\-line tool.         </div>
         

<span id=".5q2l6aqk5LiJ77ya5Yib5bu65YWo6YeP5pWw5o2u5LiK5LqR5Lu75Yqh"></span>
## Step 3: Create a full data cloud migration task


1. Log on to the [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper\-left corner of the top menu bar, select the project and region of the instance.

3. In the left navigation pane, click **TOS Backup and Recovery List** to go to the **TOS Backup and Recovery List** page.

4. On the **TOS Backup and Recovery List** page, click **Create TOS Backup File Restore Task** to go to the **Create TOS Backup File Restore Task** page.

5. On the **Create TOS Backup File Restore Task** page, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Restore method |By default, a **self\-built TOS bucket** is used and cannot be changed. |
   |Bucket name |Name of the TOS bucket storing the backup files. |
   |Select backup |Required. Select the backup file to restore.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only prefix search is supported. If the backup file is in a subfolder within the bucket, enter the complete file path. Displays a maximum of 20 matching results.</div><br> |
   |Cloud migration solution |You can select **Enable database** or **Do not open the database**.<br><br><br>* Enable database: After the restoration is complete, the database is automatically enabled and available. You cannot continue restoring log or differential backups to the database.<br><br>* Do not open the database: After the restoration is complete, the database remains in the recovering state. You can continue to restore log or differential backups to the database. After the restoration is complete, you can also use a stored procedure to modify the database status to Online. For more information, see [Modify the Database Status to Online](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/editing-database-status-to-online). |
   |Recovery type |Select **Full recovery**. |
   |Overwrite and restore? |Currently, only **No** is supported. |
   |Select instance |Select the target instance to restore to. You can search by instance name or instance ID. |
   |Database name to be recovered |Enter the database name to be recovered. It must match the database name in the backup file. You can restore a maximum of 20 databases at a time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you select <strong>Default recovery</strong> for <strong>Recovery type</strong>.</div><br> |
   

6. Click **Submit**.


<span id=".5q2l6aqk5Zub77ya5p-l55yL5aSH5Lu95LiK5LqR6K6w5b2V"></span>
## Step 4: View cloud backup tasks

After completing the cloud backup, you can view the TOS backup and restore tasks. For detailed instructions, see [View TOS backup and restore tasks](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/view-tos-backup-recovery-tasks).

<span id=".5q2l6aqk5LqU77ya6L-B56e75a6M5oiQ5ZCO6YWN572u5LqR5LiK5a6e5L6L55qE5Y-C5pWw"></span>
## Step 5: Configure instance parameters after migration

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

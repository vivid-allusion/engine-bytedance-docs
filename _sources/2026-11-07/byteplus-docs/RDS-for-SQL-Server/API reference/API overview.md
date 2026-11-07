---
title: "API overview"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/api-references"
---

This topic lists the APIs for RDS for SQL Server.

<span id=".5YWo5bGA"></span>
## Global


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeRegions) |Call the DescribeRegions API to view the list of supported regions. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailabilityzones) |Call the DescribeAvailabilityZones API to query availability zones. |


<span id=".5a6e5L6L"></span>
## Instance management


|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance) |Call the CreateDBInstance API to create an instance. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances) |Call the DescribeDBInstances API to query the instance list. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail) |Call the DescribeDBInstanceDetail API to query instance details. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletedbinstance) |Call the DeleteDBInstance API to delete an instance. |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancespecs) |Call the DescribeDBInstanceSpecs API to query instance specification codes. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restartdbinstance) |Calls the RestartDBInstance API to restart an instance. |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbinstancename) |Call the ModifyDBInstanceName API to modify the instance name. |
|[ModifyDBFailover](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbfailover) |Call the ModifyDBFailover API to manually switch the primary and secondary nodes. |


<span id=".5aSH5Lu9"></span>
## Account management


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/CreateDBAccount_-_Create_an_account?lang=en) |Call the CreateDBAccount API to create a database account. |
|[ModifyDBAccountStatus](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyDBAccountStatus_-_Modify_the_status_of_an_instance_account?lang=en) |Call the ModifyDBAccountStatus operation to enable or disable an instance account. |
|[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/GrantDBAccountPrivilege_-_Grant_privileges_to_an_account?lang=en) |Call the GrantDBAccountPrivilege API to grant privileges to a database account. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DeleteDBAccount_-_Delete_an_account?lang=en) |Call DeleteDBAccount to delete a database account. |
|[RevokeDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/RevokeDBAccountPrivilege_-_Revoke_account_privileges?lang=en) |Call the RevokeDBAccountPrivilege operation to revoke privileges from a database account. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeDBAccounts_-_Query_accounts?lang=en) |Call the DescribeDBAccounts API to query database accounts. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ResetDBAccount_-_Reset_a_database_account_password?lang=en) |Call the ResetDBAccount operation to reset a database account password. |


<span id="d0rK7YF0"></span>
## Allowlist management


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createAllowList?lang=en) |Call the CreateAllowList API to create an allowlist. |
|[DescribeInstanceAllowLists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeInstanceAllowLists?lang=en) |Call the DescribeInstanceAllowLists API to query the allowlists associated with an instance. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyAllowList?lang=en) |Call the ModifyAllowList API to modify the allowlist of an instance. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DisAssociateAllowList?lang=en) |Call the DisassociateAllowList API to disassociate an instance from an allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowLists?lang=en) |Call the DescribeAllowLists API to query allowlists. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowListDetail?lang=en) |Call the DescribeAllowListDetail API to query the details of an allowlist. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/AssociateAllowList?lang=en) |Call the AssociateAllowList API to associate an allowlist with an instance. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DeleteAllowList?lang=en) |Call the DeleteAllowList API to delete the allowlist. |


<span id="iOuPL71f"></span>
## Backup and recovery


|**API** |**Description** |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createbackup) |Call the CreateBackup API to create a backup set. |
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloadbackup) |Call the DownloadBackup API to download full physical backup files. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackups?lang=en) |Call the DescribeBackups API to view the list of backup sets. |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifybackuppolicy) |Call the ModifyBackupPolicy API to modify the backup information of the instance. |
|[DeleteBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletebackup) |Call the DeleteBackup API to delete the backup files of an instance. |
|[DescribeBackupDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail) |Call the DescribeBackupDetail API to query the details of a backup file. |
|[DescribeCrossBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describecrossbackuppolicy) |Call the DescribeCrossBackupPolicy API to view the cross\-regional backup policy. |
|[DescribeAvailableCrossRegion](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailablecrossregion) |Call the DescribeAvailableCrossRegion API to view destination regions for cross\-regional backups. |
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restoretoexistedinstance) |Call the RestoreToExistedInstance API to restore data to an existing instance at the database level. |
|[ModifyCrossBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifycrossbackuppolicy) |Call the ModifyCrossBackupPolicy API to modify a cross\-regional backup policy. |


<span id=".5oGi5aSN"></span>
## Back up to cloud


|**API** |**Description** |
|---|---|
|[CreateTosRestore](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createtosrestore) |Call the CreateTosRestore API to restore backup files from object storage TOS to an instance to migrate data to the cloud. |
|[DescribeTosRestoreTasks](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretasks) |Call the DescribeTosRestoreTasks API to query the list of tasks for uploading instance backup data to the cloud. |
|[DescribeTosRestoreTaskDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretaskdetail) |Call the DescribeTosRestoreTaskDetail API to query details about uploading instance backup data to the cloud. |


<span id=".5Y-C5pWw"></span>
## Data security


|**API** |**Description** |
|---|---|
|[DescribeDBInstanceTDE](https://docs.volcengine.com/docs/6899/1703441) |Call the DescribeDBInstanceTDE API to query the TDE status of an instance. |
|[ModifyDBInstanceTDE](https://docs.volcengine.com/docs/6899/1703501) |Call the ModifyDBInstanceTDE API to modify the TDE configuration of an instance. |
|[DownloadSSLCertificate](https://docs.volcengine.com/docs/6899/2488935) |Call the DownloadSSLCertificate API to download the instance's SSL CA certificate. |
|[DescribeDBInstanceSSL](https://docs.volcengine.com/docs/6899/2488936) |Call the DescribeDBInstanceSSL API to view the SSL information of an instance. |
|[ModifyDBInstanceSSL](https://docs.volcengine.com/docs/6899/2488938) |Call the ModifyDBInstanceSSL API to modify the SSL configuration of an instance. |


<span id="silvwvPS"></span>
## Parameter management


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstanceparameters) |Call the DescribeDBInstanceParameters API to query instance parameters. |

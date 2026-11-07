---
title: "API History"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/API_History"
---

This topic summarizes the API changes for RDS for SQL Server.


<Tabs>
<Tab zoneid="ZusRRE4XxA" title="2026">
<TabTitle>2026</TabTitle>

<span id="phCvlzRI"></span>
## May 2026


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeDBInstanceSSL_-_Query_Instance_SSL_Configuration) |2026\-05\-29 |New API. Call the DescribeDBInstanceSSL API to view the SSL information of an instance. |* [Set up SSL encryption](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/setting-ssl-encryption?lang=en)<br><br>* [Update SSL certificate](https://docs.volcengine.com/docs/6899/2432750?lang=zh) |
|[DownloadSSLCertificate](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DownloadSSLCertificate_-_Download_an_SSL_certificate) |2026\-05\-29 |New API. Call the DownloadSSLCertificate API to download the instance's SSL CA certificate. ||
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyDBInstanceSSL_-_Modify_the_SSL_configuration_of_an_instance) |2026\-05\-29 |New API. Call the ModifyDBInstanceSSL API to modify the SSL configuration of the instance. ||
|[DescribeDBInstanceTDE](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeDBInstanceTDE)<br><br> |2026\-05\-29 |New API. Call the DescribeDBInstanceTDE API to query the TDE status of an instance. |[Enable transparent data encryption (TDE).](https://docs.volcengine.com/docs/6899/1676531?lang=zh) |
|[ModifyDBInstanceTDE](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyDBInstanceTDE) |2026\-05\-29 |New API. Call the ModifyDBInstanceTDE API to modify the TDE configuration of an instance. ||


<span id="jT6xNuRc"></span>
## March 2026


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/CreateDBAccount_-_Create_an_account?lang=en) |2026\-03\-27 |New API. Call the CreateDBAccount API to create a database account. |[Create and manage accounts](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account?lang=en) |
|[ModifyDBAccountStatus](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyDBAccountStatus_-_Modify_the_status_of_an_instance_account?lang=en) |2026\-03\-27 |New API. Call the ModifyDBAccountStatus operation to enable or disable an instance account. ||
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DeleteDBAccount_-_Delete_an_account?lang=en) |2026\-03\-27 |New API. Call DeleteDBAccount to delete a database account. ||
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeDBAccounts_-_Query_accounts?lang=en) |2026\-03\-27 |New API. Call the DescribeDBAccounts API to query database accounts. ||
|[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/GrantDBAccountPrivilege_-_Grant_privileges_to_an_account?lang=en) |2026\-03\-27 |New API. Call the GrantDBAccountPrivilege API to grant privileges to a database account. |[Modify account permissions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifying-account-permissions?lang=en) |
|[RevokeDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/RevokeDBAccountPrivilege_-_Revoke_account_privileges?lang=en) |2026\-03\-27 |New API. Call the RevokeDBAccountPrivilege operation to revoke privileges from a database account. ||
|[ResetDBAccount](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ResetDBAccount_-_Reset_a_database_account_password?lang=en) |2026\-03\-27 |New API. Call the ResetDBAccount operation to reset a database account password. |[Reset account password](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/resetting-account-password?lang=en) |



</Tab>
<Tab zoneid="Hv0xpEtYbr" title="2025">
<TabTitle>2025</TabTitle>

<span id="Qnk7MtAk"></span>
## May 2025


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletedbinstance) |2025\-05\-28 |New API. Call the DeleteDBInstance API to delete an instance. |* [Delete a pay-as-you-go instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-pay-as-you-go-instance)<br><br>* [Unsubscribing from yearly or monthly subscription instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/unsubscribing-subscription-instance) |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancespecs) |2025\-05\-28 |New API. Call the DescribeDBInstanceSpecs API to query instance specification codes. |[View instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details) |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restartdbinstance) |2025\-05\-28 |New API. Calls the RestartDBInstance API to restart an instance. |[Restart an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/restart-instance) |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbinstancename) |2025\-05\-28 |New API. Call the ModifyDBInstanceName API to modify the instance name. |None |
|[ModifyDBFailover](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifydbfailover) |2025\-05\-28 |New API. Call the ModifyDBFailover API to manually switch the primary and secondary nodes. |[Switch to primary node](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/switching-master-node) |
|[ModifyCrossBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifycrossbackuppolicy) |2025\-05\-28 |New API. Call the ModifyCrossBackupPolicy API to modify a cross\-regional backup policy. |[Customize backup policy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy) |
|[DescribeCrossBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describecrossbackuppolicy) |2025\-05\-28 |New API. Call the DescribeCrossBackupPolicy API to view the cross\-regional backup policy. |[Customize backup policy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy) |
|[DescribeAvailableCrossRegion](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailablecrossregion) |2025\-05\-28 |New API. Call the DescribeAvailableCrossRegion API to view destination regions for cross\-regional backups. |[View backups](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-backup-details) |


<span id="hxVOpbnl"></span>
## March 2025


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|DescribeTosRestoreTasks |2025\-03\-26 |Updated API. The `RestoreTaskId` parameter is added to the request of the DescribeTosRestoreTasks API. |[DescribeTosRestoreTasks](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretasks) |
|ModifyBackupPolicy |2025\-03\-26 |Updated API. Added the LogBackupInterval parameter to the ModifyBackupPolicy API request. |[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifybackuppolicy) |
|DownloadBackup |2025\-03\-26 |Updated API. The request type for the DownloadBackup API has changed to a Sync request. |[DownloadBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloadbackup) |
|DescribeDBInstances |2025\-03\-26 |Updated API. The `Value` parameter in the `TagFilters` data structure returned by the `DescribeDBInstances` API is changed to the `Values` parameter. |[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances) |



</Tab>
<Tab zoneid="iG5nfi3agc" title="2024">
<TabTitle>2024</TabTitle>

<span id="0lgRKsQ3"></span>
## September 2024


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|[DescribeBackupDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail) |2024\-10\-10 |New API. Call the DescribeBackupDetail API to query the details of a backup file. |[DescribeBackupDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail) |
|[CreateBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createbackup) |2024\-10\-10 |Updated API. Added the instanceId parameter to the CreateBackup API response. |[Create a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually) |
|[DeleteBackup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deletebackup) |2024\-10\-10 |Updated API. Adds the InstanceId and BackupId parameters to the response of the DeleteBackup API. |[Delete a manual data backup file](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-manual-data-backup-files) |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modifybackuppolicy) |2024\-10\-10 |Updated API. The response for the ModifyBackupPolicy API now includes the InstanceId parameter. |[Customize backup policy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy) |
|* [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail)<br><br>* [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances)<br><br>* [CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance) |2024\-10\-10 |Updated API. Adds more values for the ServerCollation return parameter, which specifies the instance character set. |* [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)<br><br>* [View instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-instance-details) |


<span id="2l6Twnss"></span>
## January 2024


|**API** |**Release time** |**Change log** |**Associated feature** |
|---|---|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance) |2024\-01\-03 |Updated API. Added the ZoneId and SubnetId parameters to the CreateDBInstance API. Supports deploying the primay and secondary nodes of an instance across availability zones. |* [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)<br><br>* [Restore to a new instance from a backup set](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovery-to-new-instances-by-using-backup-set)<br><br>* [Restore to a new instance by point in time](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/recovering-to-new-instance-by-time-point)<br><br>* [Rebuild an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/rebuilding-instance) |



</Tab>
</Tabs>

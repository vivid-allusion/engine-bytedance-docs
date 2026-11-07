---
title: "API overview"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/api_overview_1"
---

This topic summarizes the Open APIs for RDS for MySQL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In a single region, the rate limit for calling an RDS for MySQL API is 20 times per second for each BytePlus account. If this limit is exceeded, the API request execution will fail and an <code>AccountFlowLimitExceeded</code> error will be prompted.</div>


* <div data-tips="true" data-tips-type="tip">The timeout for RDS for MySQL API calls is 30 seconds.</div>



<span id="DXZ5oQj0"></span>
## Global management


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/docs/RDS_for_MySQL/describeregions) |Call the DescribeRegions API to view the list of regions. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/docs/RDS_for_MySQL/describeavailabilityzones) |Call the DescribeAvailabilityZones API to view the list of availability zones. |


<span id="MJTXBaRk"></span>
## Managing instances


|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/createdbinstance1) |Call the CreateDBInstance API to create an instance. |
|[DescribeDBInstances](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstances) |Call the DescribeDBInstances API to view the instance list. |
|[DescribeDBInstanceAttribute](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBInstanceAttribute) |Call the DescribeDBInstanceAttribute API to query the attributes of the instance. |
|[DescribeDBInstanceEndpoints](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints) |Call the DescribeDBInstanceEndpoints API to query the list of connection addresses of the instance. |
|[DescribeResourceUsage](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeResourceUsage) |Call the DescribeResourceUsage API to query the resource usage of the instance. |
|[DescribeDBInstanceChargeDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBInstanceChargeDetail) |Call the DescribeDBInstanceChargeDetail API to query the billing information of the instance. |
|[DescribeDBInstanceHAConfig](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBInstanceHAConfig) |Call the DescribeDBInstanceHAConfig API to query the high availability configuration of the instance. |
|[DescribeDBDisasterRecoveryInstances](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBDisasterRecoveryInstances) |Call the DescribeDBDisasterRecoveryInstances API to query the disaster recovery instance information of the instance. |
|[DescribeDBProxy](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBProxy) |Call the DescribeDBProxy API to query the proxy configuration of the instance. |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstancespecs) |Call the DescribeDBInstanceSpecs API to query the supported specifications for MySQL. |
|[DescribeDBInstancePriceDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstancepricedetail) |Call the DescribeDBInstancePriceDetail API to query the price details of the MySQL instance. |
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of an instance. |
|[ModifyDBInstanceName](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancename) |Call the ModifyDBInstanceName API to modify the instance name. |
|[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancemaintenancewindow) |Call the ModifyDBInstanceMaintenanceWindow API to modify the maintenance window of an instance. |
|[ModifyDBNodeTemporarySpec](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbnodetemporaryspec) |Call the ModifyDBNodeTemporarySpec API to temporarily upgrade the configuration of an instance. |
|[ModifyDBNodeSpec](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbnodespec) |Call the ModifyDBNodeSpec API to modify the node specifications of an instance. |
|[CreateDBNodes](https://docs.byteplus.com/docs/RDS_for_MySQL/createdbnodes) |Call the CreateDBNodes API to add nodes to an instance. |
|[DeleteDBNodes](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedbnodes) |Call the DeleteDBNodes API to remove nodes from an instance. |
|[ModifyDBInstanceSyncMode](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancesyncmode) |Call the ModifyDBInstanceSyncMode API to modify the data synchronization mode of an instance. |
|[ModifyDBInstanceType](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancetype) |Call the ModifyDBInstanceType API to modify the instance type of a specified MySQL instance. |
|[SwitchDBInstanceHA](https://docs.byteplus.com/docs/RDS_for_MySQL/switchdbinstanceha) |Call the SwitchDBInstanceHA API to manually switch the primary and secondary nodes of a specified MySQL instance. |
|[MigrateToOtherZone](https://docs.byteplus.com/docs/RDS_for_MySQL/migratetootherzone) |Call the MigrateToOtherZone API to migrate nodes of a specified instance to another availability zone within the same region. |
|[RestartDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/restartdbinstance1) |Call the RestartDBInstance API to restart an instance. |
|[RebuildDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/rebuilddbinstance) |Call the RebuildDBInstance API to rebuild an instance using the backup of a deleted instance. |
|[DeleteDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedbinstance1) |Call the DeleteDBInstance API to delete an instance. |
|[DescribeTagsByResource](https://docs.byteplus.com/docs/RDS_for_MySQL/describetagsbyresource) |Call the DescribeTagsByResource API to query tags for one or more MySQL instances. |
|[AddTagsToResource](https://docs.byteplus.com/docs/RDS_for_MySQL/addtagstoresource) |Call the AddTagsToResource API to bind tags to one or more MySQL instances. |
|[RemoveTagsFromResource](https://docs.byteplus.com/docs/RDS_for_MySQL/removetagsfromresource) |Call the RemoveTagsFromResource API to unbind tags from one or more MySQL instances. |
|[DescribeDBInstanceEngineMinorVersions](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstanceengineminorversions) |Call the DescribeDBInstanceEngineMinorVersions API to query the upgradable minor kernel versions of an instance. |
|[UpgradeDBInstanceEngineMinorVersion](https://docs.byteplus.com/docs/RDS_for_MySQL/upgradedbinstanceengineminorversion) |Call the UpgradeDBInstanceEngineMinorVersion API to upgrade the minor kernel version of an instance. |
|[ModifyDBInstanceAutoUpgradeEngineMinorVersion](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstanceautoupgradeengineminorversion) |Call the ModifyDBInstanceAutoUpgradeEngineMinorVersion API to modify the upgrade strategy for the instance's kernel minor version. |
|[CreateDrDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/createdrdbinstance) |Call the CreateDrDBInstance API to create a disaster recovery instance for the specified instance. |
|[SwitchDrInstanceToMaster](https://docs.byteplus.com/docs/RDS_for_MySQL/switchdrinstancetomaster) |Call the SwitchDrInstanceToMaster API to promote a disaster recovery instance to a primary instance. |
|[RebuildDrInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/rebuilddrinstance) |Call the RebuildDrInstance API to rebuild disaster recovery instance data. |
|[DescribeDisasterRecoveryRegions](https://docs.byteplus.com/docs/RDS_for_MySQL/describedisasterrecoveryregions) |Call the DescribeDisasterRecoveryRegions API to view the list of regions where disaster recovery instances can be created. |
|[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancedeletionprotectionpolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy API to set the deletion protection feature for an instance. |
|[UpgradeDBInstanceEngineMajorVersionPrecheck](https://docs.byteplus.com/docs/RDS_for_MySQL/UpgradeDBInstanceEngineMajorVersionPrecheck) |Call the UpgradeDBInstanceEngineMajorVersionPrecheck API to pre\-check the instance before upgrading to a major version. |
|[DescribeUpgradeEngineMajorVersionPrecheckResult](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeUpgradeEngineMajorVersionPrecheckResult) |Call the DescribeUpgradeEngineMajorVersionPrecheckResult API to query the pre\-check results of upgrading the major kernel version of the instance. |
|[UpgradeDBInstanceEngineMajorVersion](https://docs.byteplus.com/docs/RDS_for_MySQL/UpgradeDBInstanceEngineMajorVersion) |Call the UpgradeDBInstanceEngineMajorVersion API to upgrade the major kernel version of an instance. |
|[StopDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/stopdbinstance) |Call the StopDBInstance API to pause the instance. |
|[StartDBInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/startdbinstance) |Call the StartDBInstance API to start the stopped instance. |
|[DescribeDBInstanceNodes](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstancenodes) |Call the DescribeDBInstanceNodes API to query the detailed information of instance nodes. |
|[DescribeDBProxyPriceDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbproxypricedetail) |Call the DescribeDBProxyPriceDetail API to query the billing information of the database proxy service for an instance. |
|[CreateDBBlueGreenInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/CreateDBBlueGreenInstance) |Call the CreateDBBlueGreenInstance API to create a blue\-green deployment for an instance. |
|[DescribeDBBlueGreenInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBBlueGreenInstance) |Call the DescribeDBBlueGreenInstance API to query the blue\-green deployment information for the instance. |
|[SwitchDBPrecheckBlueGreen](https://docs.byteplus.com/docs/RDS_for_MySQL/SwitchDBPrecheckBlueGreen) |Call the SwitchDBPrecheckBlueGreen API to initiate a pre\-check for a blue\-green deployment switch. |
|[DescribeDBSwitchBlueGreenPrecheck](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBSwitchBlueGreenPrecheck) |Call the DescribeDBSwitchBlueGreenPrecheck API to query the pre\-check result of the blue\-green switch. |
|[DescribeDBBlueGreenDifferences](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeDBBlueGreenDifferences) |Call the DescribeDBBlueGreenDifferences API to query the differences between the blue and green instances in a blue\-green deployment. |
|[SwitchDBBlueGreen](https://docs.byteplus.com/docs/RDS_for_MySQL/SwitchDBBlueGreen) |Call the SwitchDBBlueGreen API to switch the blue\-green deployment. |
|[RebuildDBGreenInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/RebuildDBGreenInstance) |Call the RebuildDBGreenInstance API to rebuild the green instance in a blue\-green deployment. |
|[DeleteDBBlueGreenRelation](https://docs.byteplus.com/docs/RDS_for_MySQL/DeleteDBBlueGreenRelation) |Call the DeleteDBBlueGreenRelation API to delete the blue\-green deployment. |


<span id="TzcPTr8m"></span>
## Managing connections


|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/docs/RDS_for_MySQL/createdbendpoint) |Call the CreateDBEndpoint API to create a connection endpoint (Endpoint). |
|[ModifyDBEndpoint](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbendpoint) |Call the ModifyDBEndpoint API to modify an endpoint. |
|[ModifyDBEndpointAddress](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbendpointaddress) |Call the ModifyDBEndpointAddress API to modify the prefix or port of a connection address. |
|[ModifyDBEndpointDNS](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbendpointdns) |Call the ModifyDBEndpointDNS API to modify the resolution method of a private network address. |
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/docs/RDS_for_MySQL/createdbendpointpublicaddress) |Call the CreateDBEndpointPublicAddress API to create a public address. |
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedbendpointpublicaddress) |Call the DeleteDBEndpointPublicAddress API to delete a public address. |
|[DescribeDBProxyConfig](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbproxyconfig) |Call the DescribeDBProxyConfig API to query the database proxy information of a specified MySQL instance. |
|[ModifyDBProxyConfig](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbproxyconfig) |Call the ModifyDBProxyConfig API to modify the connection pool mode of a specified MySQL instance. |
|[DeleteDBEndpoint](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedbendpoint) |Call the DeleteDBEndpoint API to delete an Endpoint. |
|[DescribeReadOnlyNodeDelay](https://docs.byteplus.com/docs/RDS_for_MySQL/describereadonlynodedelay) |Call the DescribeReadOnlyNodeDelay API to query the delayed replication configuration of a read\-only node. |
|[ModifyReadOnlyNodeDelayReplicationTime](https://docs.byteplus.com/docs/RDS_for_MySQL/modifyreadonlynodedelayreplicationtime) |Call the ModifyReadOnlyNodeDelayReplicationTime API to configure the delayed replication feature for a read\-only node. |
|[ModifyDBProxy](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbproxy) |Call the ModifyDBProxy API to enable or disable the database proxy feature. |
|[ModifyDBProxySpec](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbproxyspec) |Call the ModifyDBProxySpec API to modify the proxy configuration of an instance. |
|[ModifyDBInstanceGlobalReadOnly](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstanceglobalreadonly) |Call the ModifyDBInstanceGlobalReadOnly API to enable or disable the global read\-only feature for an instance. |
|[CreateDiagnosticsTask](https://docs.byteplus.com/docs/RDS_for_MySQL/creatediagnosticstask) |Call the CreateDiagnosticsTask API to perform connection diagnostics for an instance. |
|[DescribeDiagnosticsInfos](https://docs.byteplus.com/docs/RDS_for_MySQL/describediagnosticsinfos) |Call the DescribeDiagnosticsInfos API to query the connection diagnostic results of an instance. |
|[RemoveDiagnosticsEntity](https://docs.byteplus.com/docs/RDS_for_MySQL/removediagnosticsentity) |Call the RemoveDiagnosticsEntity API to remove connection diagnostic records for an instance. |
|[AddDiagnosticsEntity](https://docs.byteplus.com/docs/RDS_for_MySQL/adddiagnosticsentity) |Call the AddDiagnosticsEntity API to add diagnostic items for connection diagnostics to an instance. |
|[ModifyDBEndpointConnectionMode](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbendpointconnectionmode) |Call the ModifyDBEndpointConnectionMode API to modify the type of the connection endpoint. |


<span id="Owvl1Nsa"></span>
## Managing accounts


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/docs/RDS_for_MySQL/createdbaccount) |Call the CreateDBAccount API to create a database account. |
|[DeleteDBAccount](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedbaccount) |Call the DeleteDBAccount API to delete an account. |
|[ResetDBAccount](https://docs.byteplus.com/docs/RDS_for_MySQL/resetdbaccount) |Call the ResetDBAccount API to reset the account password. |
|[DescribeDBAccounts](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbaccounts) |Call the DescribeDBAccounts API to view the account list. |
|[DescribeDBAccountTableColumnInfo](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbaccounttablecolumninfo) |Call the RevokeDBAccountPrivilege API to revoke permissions from a database account. |
|[ModifyDBAccountHost](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbaccounthost) |Call the ModifyDBAccountHost API to modify the IP address from which a regular database account can access the database. |
|[ModifyDBAccountDescription](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbaccountdescription1) |Call the ModifyDBAccountDescription API to modify the description information of an account. |
|[GrantDBAccountPrivilege](https://docs.byteplus.com/docs/RDS_for_MySQL/grantdbaccountprivilege) |Call the GrantDBAccountPrivilege API to grant database privileges to a specified database account. |
|[RevokeDBAccountPrivilege](https://docs.byteplus.com/docs/RDS_for_MySQL/revokedbaccountprivilege) |Call the RevokeDBAccountPrivilege API to revoke permissions from a database account. |


<span id="ol5ftEnz"></span>
## Managing databases


|API |Description |
|---|---|
|[CreateDatabase](https://docs.byteplus.com/docs/RDS_for_MySQL/createdatabase1) |Call the CreateDatabase API to create a database. |
|[DeleteDatabase](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedatabase1) |Call the DeleteDatabase API to delete a database. |
|[DescribeDatabases](https://docs.byteplus.com/docs/RDS_for_MySQL/describedatabases) |Call the DescribeDatabases API to view the database list. |
|[GrantDatabasePrivilege](https://docs.byteplus.com/docs/RDS_for_MySQL/grantdatabaseprivilege) |Call the GrantDatabasePrivilege API to add authorized database accounts for the specified database. |
|[RevokeDatabasePrivilege](https://docs.byteplus.com/docs/RDS_for_MySQL/revokedatabaseprivilege) |Call the RevokeDatabasePrivilege API to revoke authorization from a database account. |
|[ModifyDatabaseDescription](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydatabasedescription1) |Call the ModifyDatabaseDescription API to modify the description of a database. |


<span id="DNMJmsM9"></span>
## Security encryption


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/docs/RDS_for_MySQL/describeallowlists1) |Call the DescribeAllowLists API to view the allow list. |
|[DescribeAllowListDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/describeallowlistdetail1) |Call the DescribeAllowListDetail API to view the details of an allowlist. |
|[CreateAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/createallowlist1) |Call the CreateAllowList API to create an allowlist. |
|[ModifyAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/modifyallowlist1) |Call the ModifyAllowList API to modify an allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/deleteallowlist1) |Call the DeleteAllowList API to delete an allowlist. |
|[AssociateAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/associateallowlist1) |Call the AssociateAllowList API to bind an allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/disassociateallowlist1) |Call the DisassociateAllowList API to unbind an allowlist. |
|[SyncAllowList](https://docs.byteplus.com/docs/RDS_for_MySQL/syncallowlist) |Call the SyncAllowList API to synchronize the IPs of security groups bound to the allowlist. |
|[UpgradeAllowListVersion](https://docs.byteplus.com/docs/RDS_for_MySQL/upgradeallowlistversion1) |Call the UpgradeAllowListVersion API to upgrade the version of an allowlist. |
|[DescribeDBInstanceSSL](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstancessl) |Call the DescribeDBInstanceSSL API to query the SSL settings of a specified MySQL instance. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancessl) |Call the ModifyDBInstanceSSL API to modify the SSL configuration of a specified MySQL instance. |
|[DownloadSSLCertificate](https://docs.byteplus.com/docs/RDS_for_MySQL/downloadsslcertificate) |Call the DownloadSSLCertificate API to download the SSL certificate of a specified MySQL instance. |
|[DescribeDBInstanceTDE](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstancetde) |Call DescribeDBInstanceTDE to query the enabled/disabled state of the transparent data encryption function of an instance. |
|[ModifyDBInstanceTDE](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstancetde) |Call the ModifyDBInstanceTDE API to enable the Transparent Data Encryption (TDE) feature for an instance. |
|[DescribeNonWhiteSessionList](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeNonWhiteSessionList) |Call the DescribeNonWhiteSessionList API to query the non\-allowlisted sessions of an instance. |
|[CleanNonWhiteSession](https://docs.byteplus.com/docs/RDS_for_MySQL/CleanNonWhiteSession) |Call the CleanNonWhiteSession API to clear the non\-allowlist sessions of an instance. |


<span id="NA8kAr4S"></span>
## Backup and recovery


|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/docs/RDS_for_MySQL/createbackup1) |Call the CreateBackup API to create a backup. |
|[DescribeBackups](https://docs.byteplus.com/docs/RDS_for_MySQL/describebackups) |Call the DescribeBackups API to query the data backup list. |
|[ModifyBackupName](https://docs.byteplus.com/docs/RDS_for_MySQL/ModifyBackupName) |Call the ModifyBackupName API to modify the name of a data backup first. |
|[DescribeBinlogFiles](https://docs.byteplus.com/docs/RDS_for_MySQL/describebinlogfiles) |Call the DescribeBinlogFiles API to query Binlog backup files. |
|[ModifyBackupPublicAccessPolicy](https://docs.byteplus.com/docs/RDS_for_MySQL/modifybackuppublicaccesspolicy) |Call the ModifyBackupPublicAccessPolicy API to modify the public network download policy for instance backups. |
|[DownloadBackup](https://docs.byteplus.com/docs/RDS_for_MySQL/downloadbackup) |Call the DownloadBackup API to download a backup. |
|[GetBackupDownloadLink](https://docs.byteplus.com/docs/RDS_for_MySQL/getbackupdownloadlink) |Call the GetBackupDownloadLink API to obtain the backup download link. |
|[RestoreToNewInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/restoretonewinstance) |Call the RestoreToNewInstance API to restore data to a new instance. |
|[RestoreToExistedInstance](https://docs.byteplus.com/docs/RDS_for_MySQL/restoretoexistedinstance) |Call the RestoreToExistedInstance API to restore data to an existing database instance. |
|[DescribeRecoverableTime](https://docs.byteplus.com/docs/RDS_for_MySQL/describerecoverabletime1) |Call the DescribeRecoverableTime API to view the recoverable time range. |
|[DescribeBackupPolicy](https://docs.byteplus.com/docs/RDS_for_MySQL/describebackuppolicy) |Call the DescribeBackupPolicy API to query the backup policy of a specified instance. |
|[ModifyBackupPolicy](https://docs.byteplus.com/docs/RDS_for_MySQL/modifybackuppolicy) |Call the ModifyBackupPolicy API to modify the backup policy of an instance. |
|[CreateBinlogBackup](https://docs.byteplus.com/docs/RDS_for_MySQL/createbinlogbackup) |Call the CreateBinlogBackup API to create a log backup. |
|[DeleteDataBackup](https://docs.byteplus.com/docs/RDS_for_MySQL/deletedatabackup) |Call the DeleteDataBackup API to delete manually created data backups. |
|[ModifyBackupEncryptionPolicy](https://docs.byteplus.com/docs/RDS_for_MySQL/ModifyBackupEncryptionPolicy) |Call the ModifyBackupEncryptionPolicy API to modify backup encryption settings. |
|[DescribeBackupEncryptionStatus](https://docs.byteplus.com/docs/RDS_for_MySQL/describebackupencryptionstatus) |Call the DescribeBackupEncryptionStatus API to query the backup encryption policy of an instance. |
|[DescribeBackupDecryptionKey](https://docs.byteplus.com/docs/RDS_for_MySQL/describebackupdecryptionkey) |Call the DescribeBackupDecryptionKey API to query the encryption key for a backup. |
|[DescribeBackupStats](https://docs.byteplus.com/docs/RDS_for_MySQL/describebackupstats) |Call the DescribeBackupStats API to query the storage space usage information of backup files for an instance. |
|[DescribeDeletedDBInstances](https://docs.byteplus.com/docs/RDS_for_MySQL/describedeleteddbinstances) |Call the DescribeDeletedDBInstances API to query the list of deleted instances. |


<span id="6k0Q8D9i"></span>
## Managing parameters


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query instance parameters. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/docs/RDS_for_MySQL/modifydbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify instance parameters. |
|[DescribeDBInstanceParametersLog](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbinstanceparameterslog) |Call the DescribeDBInstanceParametersLog API to query the parameter modification history of an instance. |
|[CreateParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/createparametertemplate1) |Call the CreateParameterTemplate API to create a parameter template. |
|[ModifyParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/modifyparametertemplate1) |Call the ModifyParameterTemplate API to modify a parameter template. |
|[CopyParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/copyparametertemplate1) |Call the CopyParameterTemplate API to copy a parameter template. |
|[DeleteParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/deleteparametertemplate1) |Call the DeleteParameterTemplate API to delete a parameter template. |
|[DescribeParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/describeparametertemplate1) |Call the DescribeParameterTemplate API to query the details of a specified parameter template. |
|[ListParameterTemplates](https://docs.byteplus.com/docs/RDS_for_MySQL/listparametertemplates1) |Call the ListParameterTemplates API to query the parameter template list of a MySQL instance. |
|[DescribeApplyParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/describeapplyparametertemplate1) |Call the DescribeApplyParameterTemplate API to query parameter changes when applying a specific parameter template to a specified MySQL instance. |
|[SaveAsParameterTemplate](https://docs.byteplus.com/docs/RDS_for_MySQL/saveasparametertemplate1) |Call the SaveAsParameterTemplate API to save the parameter configuration of a specified instance as a parameter template. |
|[DescribeDBNodeParameterDifferences](https://docs.byteplus.com/docs/RDS_for_MySQL/describedbnodeparameterdifferences) |Call the DescribeDBNodeParameterDifferences API to query the parameter differences between nodes of an instance. |


<span id="1cXrWSRE"></span>
## Managing tasks


|API |Description |
|---|---|
|[DescribeTasks](https://docs.byteplus.com/docs/RDS_for_MySQL/describetasks) |Call the DescribeTasks API to query tasks. |
|[DescribeTaskDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/describetaskdetail) |Call the DescribeTaskDetail API to query task details. |
|[ModifyTask](https://docs.byteplus.com/docs/RDS_for_MySQL/modifytask) |Call the ModifyTask API to edit the task. |


<span id="CI4ExZsA"></span>
## Event management


|API |Description |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/docs/RDS_for_MySQL/describeplannedevents) |Call the DescribePlannedEvents API to query operation and maintenance events. |
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/docs/RDS_for_MySQL/modifyplannedeventexecutetime) |Call the ModifyPlannedEventExecuteTime API to postpone the execution time of a maintenance event. |


<span id="hlzgIEtk"></span>
## Logs


|API |Description |
|---|---|
|[DescribeFailoverLogs](https://docs.byteplus.com/docs/RDS_for_MySQL/describefailoverlogs) |Call the DescribeFailoverLogs API to query the primary\-secondary switchover logs of a MySQL instance. |


<span id="XHNsgkRL"></span>
## Resource plan management


|API |Description |
|---|---|
|[DescribeResourcePackageDetail](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeResourcePackageDetail) |Call the DescribeResourcePackageDetail API to query the detailed usage information of the resource plan. |
|[CreateResourcePackage](https://docs.byteplus.com/docs/RDS_for_MySQL/CreateResourcePackage) |Call the CreateResourcePackage API to create a resource plan. |
|[ListResourcePackages](https://docs.byteplus.com/docs/RDS_for_MySQL/ListResourcePackages) |Call the ListResourcePackages API to query resource plans. |
|[DescribeResourcePackagePrice](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeResourcePackagePrice) |Call the DescribeResourcePackagePrice API to query the purchase price of a resource plan. |
|[DescribeResourcePackageSpec](https://docs.byteplus.com/docs/RDS_for_MySQL/DescribeResourcePackageSpec) |Call the DescribeResourcePackageSpec API to query the specifications of resource plans. |


&nbsp;

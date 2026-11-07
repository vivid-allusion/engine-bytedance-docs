---
title: "API overview"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/api_references"
---

This topic summarizes the APIs available in RDS for PostgreSQL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a single region, the API flow control limit of RDS for PostgreSQL is 20 times/second, that is, a single BytePlus account cannot call a single API interface more than 20 times per second. If this limit is exceeded, the API request execution will fail and an <code>AccountFlowLimitExceeded</code> error will be prompted.</div>


<span id=".5YWo5bGA"></span>
## Global


|API |Note |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions) |Call the DescribeRegions API to query the list of available regions. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) |Call the DescribeAvailabilityZones API to query the list of availability zones (AZs). |


<span id=".5a6e5L6L566h55CG"></span>
## Managing instances


|API |Note |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance) |Call CreateDBInstance API to create an instance. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstances) |Call the DescribeDBInstances API to query a list of instances. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) |Call DescribeDBInstanceDetail API to query instance details. |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) |Call the DescribeDBInstanceSpecs API to query instance specifications available for sale. |
|[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedetail) |Call the DescribeDBInstancePriceDetail API to query instance price details. |
|[DescribeDBInstancePriceDifference](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedifference) |Call the DescribeDBInstancePriceDifference API to query instance price difference. |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancename) |Call the ModifyDBInstanceName API to modify the instance name. |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec) |Call the ModifyDBInstanceSpec API to modify instance configurations. |
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing type of an instance. |
|[ModifyDBInstanceAvailabilityZone](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceavailabilityzone) |Call the ModifyDBInstanceAvailabilityZone API to migrate nodes from one AZ to another AZ in the same region. |
|[AddTagsToResource](https://docs.byteplus.com/en/docs/RDS_for_PG/addtagstoresource) |Call the AddTagsToResource API to add tags to an instance. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/RDS_for_PG/removetagsfromresource) |Call the RemoveTagsFromResource API to remove tags from an instance. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restartdbinstance) |Call the RestartDBInstance API to restart an instance. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbinstance) |Call the DeleteDBInstance API to delete an instance. |
|[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceMaintenanceWindow) |Call the ModifyDBInstanceMaintenanceWindow API to modify the maintenance window of an instance. |


<span id=".5pWw5o2u5bqT566h55CG"></span>
## Managing databases


|API |Note |
|---|---|
|[CreateDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/createdatabase) |Call the CreateDatabase API to create a database. |
|[DescribeDatabases](https://docs.byteplus.com/en/docs/RDS_for_PG/describedatabases) |Call the DescribeDatabases API to query a list of databases. |
|[ModifyDatabaseOwner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydatabaseowner) |Call the ModifyDatabaseOwner API to modify the database owner. |
|[CloneDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneDatabase) |Call the CloneDatabase API to clone an existing database. |
|[DeleteDatabase](https://docs.byteplus.com/en/docs/RDS_for_PG/deletedatabase) |Call the DeleteDatabase API to delete a database. |


<span id=".6LSm5Y-3566h55CG"></span>
## Managing accounts


|API |Note |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/RDS_for_PG/createdbaccount) |Call the CreateDBAccount API to create an account. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbaccounts) |Call the DescribeDBAccounts API to query a list of accounts. |
|[ModifyDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbaccountprivilege) |Call the ModifyDBAccountPrivilege API to modify the database account permissions. |
|[RevokeDBAccountPrivilege](https://docs.byteplus.com/en/docs/RDS_for_PG/revokedbaccountprivile) |Call the RevokeDBAccountPrivilege API to revoke authorization to database accounts. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/RDS_for_PG/resetdbaccount) |Call the ResetDBAccount API to reset the account password. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbaccount) |Call the DeleteDBAccount API to delete an account. |


<span id=".c2NoZW1hLeeuoeeQhg=="></span>
## Managing schemas


|API |Note |
|---|---|
|[CreateSchema](https://docs.byteplus.com/en/docs/RDS_for_PG/createschema) |Call the CreateSchema API to create a schema. |
|[DescribeSchemas](https://docs.byteplus.com/en/docs/RDS_for_PG/describeschemas) |Call the DescribeSchemas API to query a list of schemas. |
|[ModifySchemaOwner](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyschemaowner) |Call the ModifySchemaOwner API to modify the schema owner. |
|[DeleteSchema](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteschema) |Call the DeleteSchema API to delete a schema. |


<span id=".6L-e5o6l566h55CG"></span>
## Managing connections


|API |Note |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_PG/createdbendpoint) |Call the CreateDBEndpoint API to create an endpoint for the specified instance. |
|[ModifyDBEndpointName](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointname) |Call the ModifyDBEndpointName API to modify the connection endpoint name. |
|[ModifyDBInstanceConfig](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceconfig) |Call the ModifyDBInstanceConfig API to set whether to enable the global read\-only mode for the instance. |
|[ModifyDBEndpointReadWeight](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadweight) |Call the ModifyDBEndpointReadWeight API to modify the read weight distribution mode and custom weight ratio of an endpoint. |
|[ModifyDBEndpointReadWriteFlag](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwriteflag) |Call the ModifyDBEndpointReadWriteFlag API to enable or disable read\-write separation. |
|[ModifyDBEndpointReadWriteDelayThreshold](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointreadwritedelaythreshold) |Call the ModifyDBEndpointReadWriteDelayThreshold API to modify the read\-only latency threshold of an endpoint. |
|[ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointaddress) |Call the ModifyDBEndpointAddress API to modify the instance address. |
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbendpoint) |Call the CreateDBEndpointPublicAddress API to create a public address. |
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/RDS_for_PG/createdbendpointpublicaddress) |Call the DeleteDBEndpointPublicAddress API to delete a public endpoint address. |
|[DescribeDBInstanceProxyParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceProxyParameters) |Call the DescribeDBInstanceProxyParameters API to query the connection parameter configuration after read\-write separation is enabled on the default endpoint of an instance. |
|[ModifyDBEndpointProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBEndpointProxyConfig) |Call the ModifyDBEndpointProxyConfig API to modify the number of read/write separation proxy connections for the connection endpoint. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbendpointpublicaddress) |Call the DeleteDBEndpoint API to delete a connection endpoint. |


<span id=".5Y-C5pWw566h55CG"></span>
## Managing parameters


|API |Note |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query instance parameters. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify instance parameters. |
|[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstanceparame) |Call the DescribeDBInstanceParametersLog API to query the modification history of an instance parameter. |
|[DescribeDBEngineVersionParameters](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBEngineVersionParameters) |Call the DescribeDBEngineVersionParameters API to query the list of parameters supported for a specified database engine version. |
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CreateParameterTemplate) |Call the CreateParameterTemplate API to create a parameter template. |
|[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates) |Call the ListParameterTemplates API to query the parameter templates of the account in the current region. |
|[DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate) |Call the DescribeParameterTemplate API to query the details of the parameter template. |
|[DescribeApplyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeApplyParameterTemplate) |Call the DescribeApplyParameterTemplate API to query the parameter changes after applying the parameter template (only query, not actually apply). |
|[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/SaveAsParameterTemplate) |Call the SaveAsParameterTemplate API to export the current parameter configuration of the instance as a parameter template. |
|[CloneParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneParameterTemplate) |Call the CloneParameterTemplate API to clone the parameter template. |
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyParameterTemplate) |Call the ModifyParameterTemplate API to modify a parameter template. |
|[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteParameterTemplate) |Call the DeleteParameterTemplate API to delete a parameter template. |


<span id=".5aSH5Lu95LiO5oGi5aSN"></span>
## Backup and recovery


|API |Note |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/createbackup) |Call the CreateBackup API to create a data backup. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups) |Call the DescribeBackups API to query a list of backups. |
|[DescribeDetachedBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describedetachedbackups) |Call the DescribeDetachedBackups API to query the backup of a deleted instance. |
|[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_PG/describerecoverabletime) |Call the DescribeRecoverableTime API to query the time range for data recovery from an instance backup. |
|[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackuppolicy) |Call the DescribeBackupPolicy API to query the backup policy. |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/RDS_for_PG/modifybackuppolicy) |Call the ModifyBackupPolicy API to modify the backup policy. |
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) |Call the DownloadBackup API to download a backup. |
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink) |Call the GetBackupDownloadLink API to obtain the download link of the backup. |
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance) |Call the RestoreToNewInstance API to restore data to a new instance. |
|[RestoreToExistedInstance](https://docs.byteplus.com/en/docs/RDS_for_PG/RestoreToExistedInstance) |Call the RestoreToExistedInstance API to restore data to an existing instance. |
|[DeleteBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteBackup) |Call the DeleteBackup API to delete the data backup. |
|[DescribeSlots](https://docs.byteplus.com/en/docs/RDS_for_PG/describeslots) |Call the DescribeSlots API to query the replication slots of the instance. |
|[DeleteSlot](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteslot) |Call the DeleteSlot API to delete the replication slot. |
|[DescribeWALLogBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeWALLogBackups) |Call the DescribeWALLogBackups API to obtain the list of backed\-up WAL logs for the specified instance. |


<span id=".5pel5b-X566h55CG"></span>
## Logs


|API |Note |
|---|---|
|[DescribeFailoverLogs](https://docs.byteplus.com/en/docs/RDS_for_PG/describefailoverlogs) |Call the DescribeFailoverLogs API to query the primary/secondary switchover log of the instance. |


<span id=".5LqL5Lu2566h55CG"></span>
## Event management


|API |Note |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents) |Call the DescribePlannedEvents API to query the operation and maintenance events in the current region. |
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyPlannedEventExecuteTime) |Call the ModifyPlannedEventExecuteTime API to modify the execution time of operation and maintenance events. |


<span id=".5pWw5o2u5a6J5YWo"></span>
## Data security


|API |Note |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists) |Call the DescribeAllowLists API to query the allowlists list in a specific region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the allowlist details. |
|[CreateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist) |Call the CreateAllowList API to create an allowlist. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/modifyallowlist) |Call the ModifyAllowList API to modify the allowlist. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/associateallowlist) |Call the AssociateAllowList API to associate an allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociateallowlist) |Call the DisassociateAllowList API to disassociate an allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteallowlist) |Call the DeleteAllowList API to delete an allowlist. |
|[UnifyNewAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/unifynewallowlist) |Call the UnifyNewAllowList API to merge some allowlists of multiple instances into a new allowlist. |
|[UpgradeAllowListVersion](https://docs.byteplus.com/en/docs/6438/1257396) |Call the UpgradeAllowListVersion API to upgrade the version of an allowlist. |
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeDBInstanceSSL) |Call the DescribeDBInstanceSSL API to query the SSL settings of the specified instance. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceSSL) |Call the ModifyDBInstanceSSL interface to modify the SSL configuration of the specified instance. |
|[DownloadSSLCertificate](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadSSLCertificate) |Call the DownloadSSLCertificate API to download the SSL certificate of the specified instance. |


<span id=".5Lu75Yqh566h55CG"></span>
## Managing tasks


|API |Note |
|---|---|
|[DescribeTasks](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeTasks) |Call the DescribeTasks API to query tasks. |
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask) |Call the ModifyTask API to edit the task. |

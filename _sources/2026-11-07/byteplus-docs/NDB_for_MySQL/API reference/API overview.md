---
title: "API overview"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/API_overview_1"
---

This article summarizes the APIs provided by NDB for MySQL.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a single region, the API rate limit for NDB for MySQL is 20 calls per second. That is, a single BytePlus account cannot call a single API more than 20 times per second. If this limit is exceeded, the API request execution fails and an <code>AccountFlowLimitExceeded</code> error is reported.</div>


<span id="v1（2022-01-01）"></span>
## v1（2022\-01\-01）

<span id=".5YWo5bGA"></span>
### Global


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions) |Call the DescribeRegions to query the available geographical resources of the instance. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones) |Call the DescribeAvailabilityZones to query the Availability Zone resources supported by the instance in the current region. |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceSpecs) |Call DescribeDBInstanceSpecs to query the node specification code supported by the availability zone. |


<span id=".5a6e5L6L566h55CG"></span>
### Managing instances


|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance) |Call the CreateDBInstance to create a new instance. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) |Call the DescribeDBInstances to query the instance list. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail to query the instance details. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBInstance) |Call the DeleteDBInstance API to delete an instance. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestartDBInstance) |Call the RestartDBInstance to restart the instance. |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceName) |Call ModifyDBInstanceName to modify the instance name. |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceChargeType) |Call the ModifyDBInstanceChargeType API to modify the instance's billing method. |
|[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceDeletionProtectionPolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy interface to enable or disable the instance deletion protection function. |
|[ModifyDBNodeConfig](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBNodeConfig) |Call the ModifyDBNodeConfig interface to set the priority of the specified node to be selected as the primary node during primary node switching. |
|[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceMaintenanceWindow) |Call the ModifyDBInstanceMaintenanceWindow API to modify the maintenance window of an instance. |
|[ChangeMaster](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ChangeMaster) |Calls the ChangeMaster API to switch the primary node. |
|[DescribeDBInstanceVersion](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceVersion) |Call the DescribeDBInstanceVersion API to query the version of the target instance. |
|[DescribeStoragePayablePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeStoragePayablePrice) |Call the DescribeStoragePayablePrice API to query the storage price. |
|[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstancePriceDetail) |Call the DescribeDBInstancePriceDetail API to query the price details for a specified instance configuration. |
|[DescribeExistDBInstancePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeExistDBInstancePrice) |Call the DescribeExistDBInstancePrice to query the price details of an existing instance. |
|[ModifyDBInstanceStorageType](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceStorageType) |Call the ModifyDBInstanceStorageType API to modify the storage type. |
|[ModifyConnectionPersistence](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyConnectionPersistence) |Call the ModifyConnectionPersistence API to enable or disable connection persistence for the instance. |


<span id=".5qCH562-566h55CG"></span>
### Managing tags


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/NDB_for_MySQL/AddTagsToResource) |Call the AddTagsToResource to associate tags to one or more instances. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RemoveTagsFromResource) |Call the RemoveTagsFromResource to disassociate tags from one or more instances. |


<span id=".6L-e5o6l566h55CG"></span>
### Managing connections


|API |Description |
|---|---|
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpointPublicAddress) |Call the CreateDBEndpointPublicAddress to enable public network access for instance. |
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpointPublicAddress) |Call the DeleteDBEndpointPublicAddress to disable the public network access function. |
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint) |Call the CreateDBEndpoint to create a connection endpoint for instance. |
|[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) |Call the ModifyDBEndpoint to modify the connection endpoint. |
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint) |Call the DescribeDBEndpoint to query the details of the instance connection endpoint. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpoint) |Call the DeleteDBEndpoint to delete the connection endpoint. |
|[ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointAddress) |Call the ModifyDBEndpointAddress API to modify the connection address port or prefix. |
|[ModifyDBEndpointDNS](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointDNS) |Call the ModifyDBEndpointDNS API to modify the resolution method of a private network address. |


<span id=".5pWw5o2u5bqT"></span>
### Database


|API |Description |
|---|---|
|[CreateDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase) |Call the CreateDatabase to create the database. |
|[DescribeDatabases](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases) |Call the DescribeDatabases to query the database list. |
|[DeleteDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDatabase) |Call DeleteDatabase to delete the database. |
|[ModifyDatabaseDescription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDatabaseDescription) |Call the ModifyDatabaseDescription API to modify the description of a database. |


<span id=".6LSm5Y-3"></span>
### Account


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount) |Call the CreateDBAccount to create a database account. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBAccount) |Call the DeleteDBAccount to delete the database account. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) |Call the DescribeDBAccounts to query the account information of the instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ResetDBAccount) |Call the ResetDBAccount to change the account password. |
|[ResetAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ResetAccount) |Call the ResetAccount interface to reset the permissions of the super account to its initial state. |
|[ModifyDBAccountDescription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBAccountDescription) |Call ModifyDBAccountDescription to modify the account description information. |
|[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege) |Calling the GrantDBAccountPrivilege gives the account permissions on the specified database. |
|[RevokeDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RevokeDBAccountPrivilege) |Call RevokeDBAccountPrivilege to revoke permissions to the database for the account. |


<span id=".5a6J5YWo"></span>
### Safety


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RevokeDBAccountPrivilege) |Call the CreateAllowList to create a new allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists) |Call the DescribeAllowLists to query all allowlist information in the specified area under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail) |Call the DescribeAllowListDetail to query the detailed information of the allowlist. |
|[DescribeInstanceAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeInstanceAllowLists) |Call DescribeInstanceAllowLists to query the allowlist information associated with the instance. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyAllowList) |Call the ModifyAllowList to modify the allowlist information. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/AssociateAllowList) |Call the AssociateAllowList to associate the instance to the allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DisassociateAllowList) |Call the DisassociateAllowList to disassociate the instance from the allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteAllowList) |Call the DeleteAllowList to delete the allowlist. |


<span id=".5aSH5Lu95oGi5aSN"></span>
### Backup recovery


|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateBackup) |Call the CreateBackup to manually create a data backup. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups) |Call the DescribeBackups to query the backup file list of the instance. |
|[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackupPolicy) |Call the DescribeBackupPolicy to query the instance data backup policy. |
|[DeleteBackup](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteBackup) |Call the DeleteBackup to delete the instance manual backup file. |
|[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyBackupPolicy) |Call the ModifyBackupPolicy to modify the data backup policy of the instance. |
|[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime) |Call the DescribeRecoverableTime to query the recoverable time range for instance backups. |
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreToNewInstance) |Call the RestoreToNewInstance to restore the backup data of an existing instance to a new instance. |
|[DescribeRecoverableTables](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTables) |Call the DescribeRecoverableTables to query the recoverable libraries and tables of the instance. |
|[RestoreTable](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreTable) |Call the RestoreTable to restore the historical database and table of the instance to the original instance. |


<span id=".5Y-C5pWw566h55CG"></span>
### Managing parameters


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameters) |Call the DescribeDBInstanceParameters to query the instance parameter list. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceParameters) |Call the ModifyDBInstanceParameters to modify instance parameters. |
|[DescribeParameterTemplates](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplates) |Call the DescribeParameterTemplates to query the parameter template list. |
|[DescribeParameterTemplateDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplateDetail) |Call DescribeParameterTemplateDetail to query parameter template details. |
|[CreateParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateParameterTemplate) |Call the CreateParameterTemplate to create a parameter template. |
|[ApplyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ApplyParameterTemplate) |Call the ApplyParameterTemplate to apply the parameter template. |
|[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteParameterTemplate) |Call the DeleteParameterTemplate to delete the parameter template. |
|[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/SaveAsParameterTemplate) |Call the SaveAsParameterTemplate saves the parameter configuration of the instance as a parameter template. |
|[DescribeDBInstanceParameterChangeHistory](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameterChangeHistory) |Call the DescribeDBInstanceParameterChangeHistory interface to query the parameter modification history of an instance. |
|[DescribeModifiableParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeModifiableParameters) |Call the DescribeModifiableParameters API to query the modifiable parameter list. |
|[CopyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CopyParameterTemplate) |Call the CopyParameterTemplate API to copy a specified parameter template to a new parameter template. |
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyParameterTemplate) |Call the ModifyParameterTemplate API to modify a parameter template. |


<span id=".6K6h5YiS5YaF5LqL5Lu2"></span>
### Planned events


|API |Description |
|---|---|
|[DescribeScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeScheduleEvents) |Call the DescribeScheduleEvents API to view the scheduled events of the current account. |
|[CancelScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CancelScheduleEvents) |Call the CancelScheduleEvents to cancel pending scheduled events. |
|[ModifyScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyScheduleEvents) |Call the ModifyScheduleEvents to modify the execution time of the event to be executed. |


<span id="G4FVPqBT"></span>
## v2（2024\-01\-01）

<span id="K7wZCYfg"></span>
### Managing instances


|API |Description |
|---|---|
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |

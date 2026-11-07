---
title: "SDK overview"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/SDK_Overview"
---

To improve ease of use and scalability and meet the needs of more business scenarios, NDB for MySQL provides three versions of SDK: Go, Python, and Java. After installing the SDK locally, you can develop based on the OpenAPI provided by NDB for MySQL.

<span id=".c2RrLeWIl-ihqA=="></span>
## SDK list

The corresponding download links for the three versions of the SDK are shown in the table below.


|Language |Download address |User guide |
|---|---|---|
|Go |[Go SDK](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/main/service/vedbm) |[Go SDK download and installation](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_go) |
|Python |[Python SDK](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/main/byteplussdkvedbm) |[Python SDK download and installation](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Downloading_and_installing_SDK_python) |
|Java |[Java SDK](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-vedbm) |[Java SDK download and installation](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Download_and_installation_java) |


<span id=".YXBpLeWIl-ihqA=="></span>
## API list

The current three versions of the SDK include the following OpenAPI.


|Classification |Action |Description |Version |
|---|---|---|---|
|Global |[DescribeRegions](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRegions) |Call the DescribeRegions to query the available geographical resources of the instance. |2022\-01\-01 |
||[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones) |Call the DescribeAvailabilityZones to query the Availability Zone resources supported by the instance in the current region. |2022\-01\-01 |
||[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceSpecs) |Call DescribeDBInstanceSpecs to query the node specification code supported by the availability zone. |2022\-01\-01 |
|Managing instances |[CreateDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance) |Call the CreateDBInstance to create a new instance. |2022\-01\-01 |
||[DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) |Call the DescribeDBInstances to query the instance list. |2022\-01\-01 |
||[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) |Call the DescribeDBInstanceDetail to query the instance details. |2022\-01\-01 |
||[DeleteDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBInstance) |Call the DeleteDBInstance to delete a pay\-as\-you\-go instance. |2022\-01\-01 |
||[RestartDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestartDBInstance) |Call the RestartDBInstance to restart the instance. |2022\-01\-01 |
||[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceName) |Call ModifyDBInstanceName to modify the instance name. |2022\-01\-01 |
||[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |2022\-01\-01 |
||[ModifyDBNodeConfig](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBNodeConfig) |Call the ModifyDBNodeConfig interface to set the priority of the specified node to be selected as the primary node during primary node switching. |2022\-01\-01 |
||[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceDeletionProtectionPolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy interface to enable or disable the instance deletion protection function. |2022\-01\-01 |
||[ModifyDBInstanceMaintenanceWindow](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceMaintenanceWindow) |Call ModifyDBInstanceMaintenanceWindow to modify the maintenance window of the instance. |2022\-01\-01 |
||[ChangeMaster](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ChangeMaster) |Call ChangeMaster to switch the primary node. |2022\-01\-01 |
||[DescribeDBInstanceVersion](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceVersion) |Call the DescribeDBInstanceVersion to query the version of the target instance. |2022\-01\-01 |
||[DescribeStoragePayablePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeStoragePayablePrice) |Call DescribeStoragePayablePrice to query the storage price. |2022\-01\-01 |
||[DescribeDBInstancePriceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstancePriceDetail) |Call the DescribeDBInstancePriceDetail to query the price details of the specified instance configuration. |2022\-01\-01 |
||[DescribeExistDBInstancePrice](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeExistDBInstancePrice) |Call DescribeExistDBInstancePrice to query the price details of an existing instance. |2022\-01\-01 |
|Connectivity |[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpointPublicAddress) |Call the CreateDBEndpointPublicAddress to enable public network access for instance. |2022\-01\-01 |
||[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpointPublicAddress) |Call the DeleteDBEndpointPublicAddress to disable the public network access function. |2022\-01\-01 |
||[CreateDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpoint) |Call the CreateDBEndpoint to create a connection endpoint for instance. |2022\-01\-01 |
||[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBEndpoint) |Call the ModifyDBEndpoint to modify the connection endpoint. |2022\-01\-01 |
||[ModifyDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpoint) |Call the DescribeDBEndpoint to query the details of the instance connection endpoint. |2022\-01\-01 |
||[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBEndpoint) |Call the DeleteDBEndpoint to delete the connection endpoint. |2022\-01\-01 |
||[ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointAddress) |Call ModifyDBEndpointAddress to modify the endpoint address port or prefix. |2022\-01\-01 |
||[ModifyDBEndpointDNS](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBEndpointDNS) |Call the ModifyDBEndpointDNS to modify the resolution method of the private network address. |2022\-01\-01 |
|Managing tags |[AddTagsToResource](https://docs.byteplus.com/en/docs/NDB_for_MySQL/AddTagsToResource) |Call the AddTagsToResource to associate tags to one or more instances. |2022\-01\-01 |
||[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RemoveTagsFromResource) |Call the RemoveTagsFromResource to disassociate tags from one or more instances. |2022\-01\-01 |
|Database |[CreateDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDatabase) |Call the CreateDatabase to create the database. |2022\-01\-01 |
||[DescribeDatabases](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDatabases) |Call the DescribeDatabases to query the database list. |2022\-01\-01 |
||[DeleteDatabase](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDatabase) |Call DeleteDatabase to delete the database. |2022\-01\-01 |
||[ModifyDatabaseDescription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDatabaseDescription) |Call the ModifyDatabaseDescription to modify the description information of the database. |2022\-01\-01 |
|Account |[CreateDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount) |Call the CreateDBAccount to create a database account. |2022\-01\-01 |
||[DeleteDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBAccount) |Call the DeleteDBAccount to delete the database account. |2022\-01\-01 |
||[DescribeDBAccounts](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBAccounts) |Call the DescribeDBAccounts to query the account information of the instance. |2022\-01\-01 |
||[ResetDBAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ResetDBAccount) |Call the ResetDBAccount to change the account password. |2022\-01\-01 |
||[ResetAccount](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ResetAccount) |Call the ResetAccount interface to reset the permissions of the super account to its initial state. |2022\-01\-01 |
||[ModifyDBAccountDescription](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBAccountDescription) |Call ModifyDBAccountDescription to modify the account description information. |2022\-01\-01 |
||[GrantDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/GrantDBAccountPrivilege) |Calling the GrantDBAccountPrivilege gives the account permissions on the specified database. |2022\-01\-01 |
||[RevokeDBAccountPrivilege](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RevokeDBAccountPrivilege) |Call RevokeDBAccountPrivilege to revoke permissions to the database for the account. |2022\-01\-01 |
|Safety |[CreateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RevokeDBAccountPrivilege) |Call the CreateAllowList to create a new allowlist. |2022\-01\-01 |
||[DescribeAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists) |Call the DescribeAllowLists to query all allowlist information in the specified area under the current account. |2022\-01\-01 |
||[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail) |Call the DescribeAllowListDetail to query the information of the allowlist bound to the instance. |2022\-01\-01 |
||[DescribeInstanceAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeInstanceAllowLists) |Call DescribeInstanceAllowLists to query the allowlist information associated with the instance. |2022\-01\-01 |
||[ModifyAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyAllowList) |Call the ModifyAllowList to modify the allowlist information. |2022\-01\-01 |
||[AssociateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/AssociateAllowList) |Call the AssociateAllowList to associate the instance to the allowlist. |2022\-01\-01 |
||[DisassociateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DisassociateAllowList) |Call the DisassociateAllowList to disassociate the instance from the allowlist. |2022\-01\-01 |
||[DeleteAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteAllowList) |Call the DeleteAllowList to delete the allowlist. |2022\-01\-01 |
|Parameters |[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameters) |Call the DescribeDBInstanceParameters to query the instance parameter list. |2022\-01\-01 |
||[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceParameters) |Call the ModifyDBInstanceParameters to modify instance parameters. |2022\-01\-01 |
||[DescribeParameterTemplates](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplates) |Call the DescribeParameterTemplates to query the parameter template list. |2022\-01\-01 |
||[DescribeParameterTemplateDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeParameterTemplateDetail) |Call DescribeParameterTemplateDetail to query parameter template details. |2022\-01\-01 |
||[CreateParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateParameterTemplate) |Call the CreateParameterTemplate to create a parameter template. |2022\-01\-01 |
||[ApplyParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ApplyParameterTemplate) |Call the ApplyParameterTemplate to apply the parameter template. |2022\-01\-01 |
||[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteParameterTemplate) |Call the DeleteParameterTemplate to delete the parameter template. |2022\-01\-01 |
||[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/SaveAsParameterTemplate) |Call the SaveAsParameterTemplate saves the parameter configuration of the instance as a parameter template. |2022\-01\-01 |
||[DescribeDBInstanceParameterChangeHistory](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameterChangeHistory) |Call the DescribeDBInstanceParameterChangeHistory to query the parameter modification history of the instance. |2022\-01\-01 |
||[DescribeModifiableParameters](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeModifiableParameters) |Call the DescribeModifiableParameters to query the modifiable parameter list. |2022\-01\-01 |
|Backups |[CreateBackup](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateBackup) |Call the CreateBackup to manually create a data backup. |2022\-01\-01 |
||[DescribeBackups](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups) |Call the DescribeBackups to query the backup file list of the instance. |2022\-01\-01 |
||[DescribeBackupPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackupPolicy) |Call the DescribeBackupPolicy to query the instance data backup policy. |2022\-01\-01 |
||[DeleteBackup](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteBackup) |Call the DeleteBackup to delete the instance manual backup file. |2022\-01\-01 |
||[ModifyBackupPolicy](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyBackupPolicy) |Call the ModifyBackupPolicy to modify the data backup policy of the instance. |2022\-01\-01 |
||[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime) |Call the DescribeRecoverableTime to query the recoverable time range for instance backups. |2022\-01\-01 |
||[RestoreToNewInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreToNewInstance) |Call the RestoreToNewInstance to restore the backup data of an existing instance to a new instance. |2022\-01\-01 |
||[RestoreTable](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreTable) |Call the RestoreTable to restore the historical database and table of the instance to the original instance. |2022\-01\-01 |
|Planned events |[DescribeScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeScheduleEvents) |Call the DescribeScheduleEvents API to view the scheduled events of the current account. |2022\-01\-01 |
||[CancelScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/CancelScheduleEvents) |Call the CancelScheduleEvents to cancel pending scheduled events. |2022\-01\-01 |
||[ModifyScheduleEvents](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyScheduleEvents) |Call the ModifyScheduleEvents to modify the execution time of the event to be executed. |2022\-01\-01 |

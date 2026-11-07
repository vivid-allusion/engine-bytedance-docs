---
title: "API overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/api-overview"
---

This topic summarizes the APIs provided by Document Database for MongoDB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a single region, the API flow control limit of Document Database for MongoDB is 20 times per second. One BytePlus account cannot call a single API more than 20 times per second. If the limit is exceeded, the API request will fail, and the error <code>AccountFlowLimitExceeded</code> will be reported.</div>


<span id="#vQIf8zma"></span>
## Region and availability zone


|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/mongodb/describeregions) |Call the DescribeRegions API to query the available region resource list of MongoDB. |
|[DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones) |Call the DescribeAvailabilityZones API to query the list of availability zone resources of MongoDB in the specified region. |


<span id=".5a6e5L6L566h55CG"></span>
## Instance management


|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |Call the CreateDBInstance API to create a MongoDB instance. |
|[DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) |Call the DescribeNodeSpecs API query the list of node specifications supported by MongoDB. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |Call the DescribeDBInstances API to query the basic information of the MongoDB instance. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query the detailed information of the target MongoDB instance. |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancespec) |Call the ModifyDBInstanceSpec API to modify the configuration of the target MongoDB instance (such as node specification or storage capacity). |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancename) |Call the ModifyDBInstanceName API to modify instance name of target MongoDB instance. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/mongodb/restartdbinstance) |Call the RestartDBInstance API to restart the target MongoDB instance. |
|[SwitchDBMaster](https://docs.byteplus.com/en/docs/mongodb/switchdbmaster) |Call the SwitchDBMaster API to manually switch the roles of primary and secondary nodes of target MongoDB instance. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/mongodb/deletedbinstance) |Call the DeleteDBInstance API to delete a specified MongoDB instance. |


<span id=".5qCH562-566h55CG"></span>
## Tag management


|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/mongodb/addtagstoresource) |Call the AddTagsToResource API to associate tags with the target MongoDB instance. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/mongodb/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate tags from the target MongoDB instance. |


<span id=".6K6h6LS5566h55CG"></span>
## Billing management


|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify billing method of target MongoDB instance. |


<span id=".6LSm5Y-3566h55CG"></span>
## Account management


|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/mongodb/createdbaccount) |Call the CreateDBAccount API to create an account for a specified MongoDB instance. |
|[DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) |Call the DescribeDBAccounts API to query list of accounts for target MongoDB instance. |
|[UpdateDBAccountPrivilege](https://docs.byteplus.com/en/docs/mongodb/updatedbaccountprivilege) |Call the UpdateDBAccountPrivilege API to modify the privileges or account description of a specified account in the target MongoDB instance. |
|[ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) |Call the ResetDBAccount API to modify password of specified account or reset the permissions of the root account to its initial state for target MongoDB instance. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/mongodb/deletedbaccount) |Call the DeleteDBAccount API to delete the specified account in the target MongoDB instance. |


<span id=".6L-e5o6l566h55CG"></span>
## Connection management


|API |Description |
|---|---|
|[CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) |Call the CreateDBEndpoint API to create a connection address for the target MongoDB instance. |
|[DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) |Call the DescribeDBEndpoint API to query address information in target instance. |
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint) |Call the DeleteDBEndpoint API to delete specified address in target MongoDB instance. |
|[ModifyDBEndpointPort](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport) |Call the ModifyDBEndpointPort interface to modify port number of connection address corresponding to target MongoDB instance. |
|[ModifyDBEndpointPrivateDNSVisibility](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointprivatednsvisibility) |Call the ModifyDBEndpointPrivateDNSVisibility API to enable or disable public network resolution function for target MongoDB instance. |


<span id=".5aSH5Lu95LiO5oGi5aSN"></span>
## Backup and recovery


|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/mongodb/createbackup) |Call the CreateBackup API to manually create backup for target MongoDB instance. |
|[DescribeDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/describedbinstancebackuppolicy) |Call the DescribeDBInstanceBackupPolicy API to query automatic backup policy of target MongoDB instance. |
|[ModifyDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackuppolicy) |Call the ModifyDBInstanceBackupPolicy API to modify the automatic backup policy of the target MongoDB instance. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) |Call the DescribeBackups API to query backup file list of target MongoDB instance. |
|[ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) |Call the ModifyDBInstanceBackupURL API to obtain the download address of the specified backup file in the target MongoDB instance. |
|[DescribeDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl) |Call the DescribeDBInstanceBackupURL API to query information such as acquisition progress, download URL, and validity period of the download URL of specified backup file in target MongoDB instance. |
|[DescribeRecoverableTime](https://docs.byteplus.com/en/docs/mongodb/describerecoverabletime) |Call the DescribeRecoverableTime API to query the recoverable time range of backup files in the target MongoDB instance. |
|[RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) |Call the RestoreToNewInstance API to restore instance data to new instance according to backup file or time point. |


<span id=".55m95ZCN5Y2V566h55CG"></span>
## Allowlist management


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) |Call the CreateAllowList API to create a new IP allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/mongodb/modifyallowlist) |Call the ModifyAllowList API to modify the target allowlist settings (such as the name of the allowlist, IP address in the allow list, whether to set it as the default allowlist, etc.). |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/mongodb/associateallowlist) |Call AssociateAllowList API to associate the target instance to the specified IP allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target MongoDB instance from the specified IP allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/mongodb/deleteallowlist) |Call the DeleteAllowList API to delete the target allowlist. |


<span id=".c3NsLeWKoOWvhg=="></span>
## SSL encryption


|API |Description |
|---|---|
|[DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/describedbinstancessl) |Call the DescribeDBInstanceSSL interface to query the SSL encryption settings of the target MongoDB instance, including whether the function has been enabled, the expiration time of the SSL certificate, and other information. |
|[ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancessl) |Call the ModifyDBInstanceSSL API to change the SSL encryption settings of the target MongoDB instance, including enabling/disabling the encryption function, or updating the SSL certificate validity period. |


<span id=".5Y-C5pWw566h55CG"></span>
## Parameter management


|API |Description |
|---|---|
|[DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) |Call the DescribeDBInstanceParameters API to query list of parameters supported by target MongoDB instance. |
|[ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifydbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify specified parameters of target MongoDB instance. |
|[DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameterslog) |Call the DescribeDBInstanceParametersLog API to query parameter modification history of target MongoDB instance within specified time. |
|[ModifyMultiDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifymultidbinstanceparameters) |Call the ModifyDBInstanceParameters API to modify specified parameters of target MongoDB instance. |


<span id=".5pel5b-X566h55CG"></span>
## Log management


|API |Description |
|---|---|
|[DescribeNormalLogs](https://docs.byteplus.com/en/docs/mongodb/describenormallogs) |Call the DescribeNormalLogs API to query the running log or error log information of the target MongoDB instance within the specified time period. |
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/mongodb/describeslowlogs) |Call the DescribeSlowLogs API to query the slow log information of the target MongoDB instance within the specified time. |

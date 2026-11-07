---
title: "API changelog"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/api-history"
---

This topic summarizes the changelog of API of Document Database for MongoDB for your reference.

<span id=".XzIwMjYt5bm0LTEwLeaciA=="></span>
## October 2026


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|9OZmLs">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |2026\-10\-12 |Added `RsMemberState` field to response parameters, used to display the node's status in the replica set. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|TiDWFr">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||||


<span id=".XzIwMjYt5bm0LTA3LeaciA=="></span>
## July 2026


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|qnoQpg">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2026\-07\-21 |Request parameter `DBEngineVersion` newly supports the value of `MongoDB_8_3` for creating MongoDB 8.3 instances.<br><br>Added `MongotSpec` field to request parameters to specify Mongot node specifications when creating instances |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|6zgTMG">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||The request parameter `DBEngineVersion` now supports the `MongoDB_8_3` value, for filtering MongoDB 8.3 instances.<br><br>Add the `MongotInfos` field to the response parameters to display Mongot node information. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|jNejzQ">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||Add the `MongotInfos` field to the response parameters to display Mongot node information. |[Managing read-only nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes?lang=en) |
|<span data-api-tag="update\|3xPvl4">更新</span> [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) ||Added `MongotNodeSpecs` structure to response parameters to display the Mongot node spec list. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |


<span id=".XzIwMjYt5bm0LTAzLeaciA=="></span>
## March 2026


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|Gncwug">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2026\-03\-31 |Request parameter `DBEngineVersion` newly supports the value of `MongoDB_7_0` for creating MongoDB 7.0 instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|QFOsv4">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||Request parameter `DBEngineVersion` newly supports the value of `MongoDB_7_0` for filtering out MongoDB 7.0 instances. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |


<span id=".XzIwMjUt5bm0LTExLeaciA=="></span>
## November 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|X0gW34">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2025\-11\-27 |Added `Port` field to request parameter to set the private network address port number for new instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|VUXCk1">更新</span> [RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) ||Added `Port` field to request parameters to set the private network address port number for recovered new instance. |* [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |
|<span data-api-tag="update\|893cvR">更新</span> [DescribeDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl) ||Added `PrivateDownloadLink` field to response parameters, which displays the private network download address of backup file. |[Managing backup files](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file) |


<span id=".XzIwMjUt5bm0LTA5LeaciA=="></span>
## September 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|IjywJ8">更新</span> [CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) |2025\-09\-25 |Added `ObjectIds` and `AllShard` to request parameters to batch create connection addresses for multiple or all Shards. |* [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address)<br><br>* [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address) |


<span id=".XzIwMjUt5bm0LTA4LeaciA=="></span>
## August 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|UsVCFm">新增</span> [ModifyDBEndpointPort](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointport) |2025\-08\-28 |Added new API to modify port number of connection address for target MongoDB instance. |[Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports) |
|<span data-api-tag="add\|lE2yNA">新增</span> [ModifyDBEndpointPrivateDNSVisibility](https://docs.byteplus.com/en/docs/mongodb/modifydbendpointprivatednsvisibility) ||Added new API to enable or disable public network resolution for target MongoDB instance. |[Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/mongodb/set-public-network-resolution) |


<span id=".XzIwMjUt5bm0LTA2LeaciA=="></span>
## June 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|fm6gcc">新增</span> [ModifyDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackuppolicy) |2025\-06\-26 |Added new API to modify the automatic backup policy of target MongoDB instance. |[Modifying automatic backup policy](https://docs.byteplus.com/en/docs/mongodb/automatic-backup) |
|<span data-api-tag="update\|awKr1Z">更新</span> [ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype) |2025\-06\-03 |* Request parameter `ChargeType` supports more values, enabling billing type conversion between pay\-as\-you\-go instances and subscription instances.<br><br>* The `PeriodUnit` and `Period` request parameters are now required only when `ChargeType` is `Prepaid`. |* [Switching to subscription](https://docs.byteplus.com/en/docs/mongodb/switch-to-subscription)<br><br>* [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/switch-to-pay-as-you-go) |


<span id=".XzIwMjUt5bm0LTA0LeaciA=="></span>
## April 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|qh7fWr">更新</span> [CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) |2025\-04\-28 |Added the `AllowListCategory` field to request parameters to set the type of new allowlists. |[Creating an allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist) |
|<span data-api-tag="update\|U2GJ8j">更新</span> [ModifyAllowList](https://docs.byteplus.com/en/docs/mongodb/modifyallowlist) ||Added `AllowListCategory` field to request parameters for modifying the allowlist type. |[Editing an allowlist](https://docs.byteplus.com/en/docs/mongodb/edit-allowlist) |
|<span data-api-tag="update\|21UqD5">更新</span> [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) ||* Added `AllowListCategory` field to request parameters to filter default allowlists.<br><br>* Added `AllowListCategory` field to response parameters to display the allowlist type. |[Allowlist management](https://docs.byteplus.com/en/docs/mongodb/manage-allowlists) |
|<span data-api-tag="update\|7HrU8Q">更新</span> [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) ||Added `AllowListCategory` field to response parameters to display the allowlist type. ||
|<span data-api-tag="update\|TlTSrS">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) ||Added `ConfigServerNodeSpec` and `ConfigServerStorageSpaceGB` fields to request parameters, which specify the ConfigServer's node specification and storage space when creating new sharding cluster instance. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|2jZn5f">更新</span> [RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) ||* Added `ConfigServerNodeSpec` and `ConfigServerStorageSpaceGB` fields to request parameters to specify node specifications and storage space for the ConfigServer of new sharding cluster instances after recovery.<br><br>* Added `Tags` field to request parameters to associate tags with new instances after recovery. |* [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |
|<span data-api-tag="update\|mSxZY7">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||Request parameter `TagFilters` field is deprecated and replaced by the newly added `FilterByTags` field for filtering instances by tags. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |


<span id=".XzIwMjUt5bm0LTAyLeaciA=="></span>
## February 2025


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|HWGRyG">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2025\-02\-10 |Optimized the value constraint conditions for request parameter `SuperAccountPassword`, adding validation interception for multiple weak passwords. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|ksaNIE">更新</span> [RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) |||* [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |
|<span data-api-tag="update\|Tbznw0">更新</span> [CreateDBAccount](https://docs.byteplus.com/en/docs/mongodb/createdbaccount) ||Optimized value restrictions for the request parameter `AccountPassword`, adding verification and interception for multiple weak passwords. |[Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account) |
|<span data-api-tag="update\|z81xCa">更新</span> [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) |||* [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password)<br><br>* [Resetting root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account) |


<span id=".XzIwMjQt5bm0LTEyLeaciA=="></span>
## December 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|qaWyqc">更新</span> [ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) |2024\-12\-30 |Optimized the value constraint conditions for request parameter `BackupId`, no longer restricting the backup object to be data backup (that is `BackupObject` value is `Data`). |[Managing backup files](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file) |
|<span data-api-tag="add\|HjLXxI">新增</span> [CreateDBAccount](https://docs.byteplus.com/en/docs/mongodb/createdbaccount) |2024\-12\-03 |Added new API to create account for target MongoDB instance. |[Creating account](https://docs.byteplus.com/en/docs/mongodb/create-account) |
|<span data-api-tag="add\|HxiVwy">新增</span> [UpdateDBAccountPrivilege](https://docs.byteplus.com/en/docs/mongodb/updatedbaccountprivilege) ||Added new API to modify privileges or description of specified account in target MongoDB instance. |[Modifying account privileges](https://docs.byteplus.com/en/docs/mongodb/modifying_account_privileges) |
|<span data-api-tag="add\|8fwknp">新增</span> [DeleteDBAccount](https://docs.byteplus.com/en/docs/mongodb/deletedbaccount) ||Added new API to delete specified account in target MongoDB instance. |[Deleting account](https://docs.byteplus.com/en/docs/mongodb/delete_account) |
|<span data-api-tag="add\|uqvm4O">新增</span> [ModifyMultiDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifymultidbinstanceparameters) ||Added new API to modify multiple parameters of target MongoDB instance. |[Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter) |


<span id=".XzIwMjQt5bm0LTEwLeaciA=="></span>
## October 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|wxPVXH">更新</span> [DescribeDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/describedbinstancebackuppolicy) |2024\-10\-17 |The response parameter `DataFullBackupTime` has been changed from UTC+8 time to UTC time. |[Automatic backup](https://docs.byteplus.com/en/docs/mongodb/automatic-backup) |
|<span data-api-tag="update\|aBcZ9d">更新</span> [CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) ||Added `ProjectName` field to request parameters to specify the allowlist's project. |[Creating an allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist) |
|<span data-api-tag="update\|kecZDU">更新</span> [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) ||* Added `ProjectName` field to request parameters to filter allowlist information for the specified project.<br><br>* Added `ProjectName` field to `AllowLists` structure of response parameters, which is used to display the project to which the allowlist belongs. |[Allowlist management](https://docs.byteplus.com/en/docs/mongodb/manage-allowlists) |
|<span data-api-tag="update\|FzW0UU">更新</span> [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) ||Added `ProjectName` field to response parameters to display the project of the allowlist, and added `ProjectName` field `AssociatedInstances` struct to display the project of the instance. ||


<span id=".XzIwMjQt5bm0LTA5LeaciA=="></span>
## September 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|JdNcxm">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2024\-09\-09 |Request parameter `DBEngineVersion` newly supports values of `MongoDB_4_2` and `MongoDB_6_0` for creating MongoDB 4.2 and 6.0 instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |


<span id=".XzIwMjQt5bm0LTA4LeaciA=="></span>
## August 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|egeuXa">新增</span> [DescribeSlowLogs](https://docs.byteplus.com/en/docs/mongodb/describeslowlogs) |2024\-08\-15 |Added new API to query slow log information of target MongoDB instance within specified time. |[Querying slow logs](https://docs.byteplus.com/en/docs/mongodb/query-slow-log) |
|<span data-api-tag="add\|Epa4Qg">新增</span> [DescribeNormalLogs](https://docs.byteplus.com/en/docs/mongodb/describenormallogs) ||Added new API to query operating logs or error logs of target MongoDB instance within specified time. |* [Querrying error logs](https://docs.byteplus.com/en/docs/mongodb/query-error-log)<br><br>* [Querying running logs](https://docs.byteplus.com/en/docs/mongodb/query-running-log) |
|<span data-api-tag="update\|9Y9Wox">更新</span> [DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) ||* Request parameter `AccountName` allows more values for querying details of non\-root accounts.<br><br>* Added `AuthDB` to request parameters to filter accounts belonging to specified database.<br><br>* The `AccountType` in the `Accounts` structure of the response parameter supports more values for returning different types of accounts.<br><br>* Added `AuthDB`, `CreateTime`, `ModifyTime`, and `AccountDesc` fields to response parameters, which are used to display the database to which the instance belongs, account creation time, update time, and account description, respectively. |[Viewing account details](https://docs.byteplus.com/en/docs/mongodb/viewing_account_information) |
|<span data-api-tag="update\|owQKNs">更新</span> [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) ||Added `AuthDB` and `ResetDBAccount` fields to request parameters to specify database an account belongs to and whether to reset root account permissions to their initial state. |* [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password)<br><br>* [Resetting root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account) |


<span id=".XzIwMjQt5bm0LTA2LeaciA=="></span>
## June 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|D9Ka6k">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2024\-06\-24 |* Added `NodeAvailabilityZone` field to request parameters to specify read\-only node information for new instances, including the number of read\-only nodes and their availability zone.<br><br>* Request parameter `DBEngineVersion` newly supports value of `MongoDB_4_4` for creating MongoDB 4.4 instances. |[Create Instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|UyS5ab">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||Added `ReadOnlyNodeNumber` field to response parameters to display the number of read\-only nodes in the instance. |* [Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance)<br><br>* [Managing read-only nodes](https://docs.byteplus.com/en/docs/mongodb/managing_read_only_nodes) |
|<span data-api-tag="update\|nePEgI">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||* Added `ReadOnlyNodeNumber` field to response parameters to display the number of read\-only nodes in the instance.<br><br>* The `NodeRole` field in the `Nodes` structure of response parameters, newly supports the value of `ReadOnly`, used to distinguish between primary, secondary, hidden, and read\-only node roles in replica set instances or Shard nodes in sharding cluster instances. ||
|<span data-api-tag="update\|WVvdAl">更新</span> [RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) ||Added `NodeAvailabilityZone` field to request parameters to configure read\-only node settings. |* [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |
|<span data-api-tag="update\|1t5ijj">更新</span> [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) ||The `AddressType` field in `DBAddresses` structure of response parameters newly supports value of `ReadOnly`, used to display connection address information for read\-only nodes in the instance. |[Introduction to connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction) |


<span id=".XzIwMjQt5bm0LTA0LeaciA=="></span>
## April 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|ljIS3Q">新增</span> [CreateBackup](https://docs.byteplus.com/en/docs/mongodb/createbackup) |2024\-04\-25 |Added new API to manually create backups for target MongoDB instances. |[Manual backup](https://docs.byteplus.com/en/docs/mongodb/manual-backup) |
|<span data-api-tag="add\|ZJq9lC">新增</span> [DescribeDBInstanceBackupPolicy](https://docs.byteplus.com/en/docs/mongodb/describedbinstancebackuppolicy) ||Added new API to query automatic backup policy of target MongoDB instance. |[Automatic backup](https://docs.byteplus.com/en/docs/mongodb/automatic-backup) |
|<span data-api-tag="add\|Jr6xPT">新增</span> [DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) ||Added new API to query backup set list of target MongoDB instance. |[Managing backup files](https://docs.byteplus.com/en/docs/mongodb/manage-backup-file) |
|<span data-api-tag="add\|nTYnQ4">新增</span> [ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) ||Added new API to retrieve specified backup files from target MongoDB instance. ||
|<span data-api-tag="add\|r87xr3">新增</span> [DescribeDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl) ||Added new API to query download address information for specified backup file under target MongoDB instance. ||
|<span data-api-tag="add\|7docaO">新增</span> [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/mongodb/describerecoverabletime) ||Added new API to query recoverable time range of backup files in target MongoDB instance. |[Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |
|<span data-api-tag="add\|hVOQbQ">新增</span> [RestoreToNewInstance](https://docs.byteplus.com/en/docs/mongodb/restoretonewinstance) ||Added new API to restore instance data to new instance according to backup file or time point. |* [Recovery from backup files](https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file)<br><br>* [Recovery by point in time](https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point) |


<span id=".XzIwMjQt5bm0LTAzLeaciA=="></span>
## March 2024


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|wKoKRx">更新</span> [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones) |2024\-03\-25 |Request parameter `RegionId` changed from optional to required. |[Service endpoints](https://docs.byteplus.com/en/docs/mongodb/request-structure#9TeFSOVO) |


<span id=".XzIwMjMt5bm0LTA2LeaciA=="></span>
## June 2023


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|wZoiM5">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) |2023\-06\-05 |* Added `PrivateEndpoint` field to response parameters to display string information of instance's private network connection address.<br><br>* The `NodeRole` field in response parameters newly supports the `Hidden` value, used to distinguish between primary, secondary, and hidden node roles. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|GCnKT9">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||Added `PrivateEndpoint` field to response parameters to display string information of instance's private network connection address. ||
|<span data-api-tag="add\|KJjkdc">新增</span> [SwitchDBMaster](https://docs.byteplus.com/en/docs/mongodb/switchdbmaster) ||Added new API to manually switch primary and secondary nodes of target MongoDB instance. |[Switching primary node](https://docs.byteplus.com/en/docs/mongodb/switch-primary-node) |


<span id=".XzIwMjMt5bm0LTA0LeaciA=="></span>
## April 2023


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|LKkUVv">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2023\-04\-12 |Request parameter `DBEngineVersion` newly supports the value of `MongoDB_5_0` for creating MongoDB 5.0 instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|IF1y5t">更新</span> [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) ||Added `ConfigServerNodeSpecs` structure to response parameters to display ConfigServer node spec list. |[Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification) |


<span id=".XzIwMjMt5bm0LTAzLeaciA=="></span>
## March 2023


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|FzSib4">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) |2023\-03\-07 |Added `StorageType` field to response parameters to display instance's storage type. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|EklgNi">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||||


<span id=".XzIwMjMt5bm0LTAxLeaciA=="></span>
## January 2023


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|EVHXBc">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2023\-01\-16 |Added `Tags` field to request parameters to associate tags with new instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|JZMEO3">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||* Added `TagFilters` structure to request parameters to filter instances associated with the corresponding tags.<br><br>* Added `Tags` structure to response parameters to display tags associated with the instance. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|q4iHMu">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||* Added `ZoneId` field to `Nodes`, `ConfigServers`, and `Mongos` structures in response parameters to display availability zone where the corresponding instance or component node is located.<br><br>* Added `Tags` structure to response parameters to display tags associated with the instance. ||
|<span data-api-tag="add\|Yll0HS">新增</span> [AddTagsToResource](https://docs.byteplus.com/en/docs/mongodb/addtagstoresource) ||Added new API to associate a tag with target MongoDB instance. |[Associating or adding tag](https://docs.byteplus.com/en/docs/mongodb/associate-tag) |
|<span data-api-tag="add\|jbCky1">新增</span> [RemoveTagsFromResource](https://docs.byteplus.com/en/docs/mongodb/removetagsfromresource) ||Added new API to disassociate tags for one or more instances. |[Disassociating or deleting tag](https://docs.byteplus.com/en/docs/mongodb/disassociate-tag) |


<span id=".XzIwMjIt5bm0LTExLeaciA=="></span>
## November 2022


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|cdvJJV">新增</span> [DescribeDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/describedbinstancessl) |2022\-11\-03 |Added new API to query SSL encryption settings of target MongoDB instance, including whether feature is enabled and SSL certificate expiration time. |[Setting SSL encryption](https://docs.byteplus.com/en/docs/mongodb/setup-ssl) |
|<span data-api-tag="add\|uqnqK3">新增</span> [ModifyDBInstanceSSL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancessl) ||Added new API to modify SSL encryption settings for target MongoDB instance, including enabling or disabling encryption, or updating SSL certificate validity period. ||


<span id=".XzIwMjIt5bm0LTA4LeaciA=="></span>
## August 2022


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|fNfAAm">新增</span> [DescribeDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameters) |2022\-08\-03 |Added new API to query the list of supported parameters of target MongoDB instance. |[Supported parameters](https://docs.byteplus.com/en/docs/mongodb/supported-parameter) |
|<span data-api-tag="add\|7RnWuF">新增</span> [ModifyDBInstanceParameters](https://docs.byteplus.com/en/docs/mongodb/modifydbinstanceparameters) ||Added new API to modify specified parameters of target MongoDB instance. |[Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter) |
|<span data-api-tag="add\|tOdn2j">新增</span> [DescribeDBInstanceParametersLog](https://docs.byteplus.com/en/docs/mongodb/describedbinstanceparameterslog) ||Added new API to query parameter modification history of target MongoDB instance within specified period. |[Viewing parameter modification history](https://docs.byteplus.com/en/docs/mongodb/view-parameter-modification-history) |


<span id=".XzIwMjIt5bm0LTA3LeaciA=="></span>
## July 2022


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|K8gDtj">更新</span> [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancespec) |2022\-07\-04 |Added `ShardNumber` and `MongosNodeNumber` fields to request parameters to modify the number of shards or Mongos nodes for sharding cluster instances. |* [Modifying Mongos node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config)<br><br>* [Modifying shard configuration](https://docs.byteplus.com/en/docs/mongodb/modify-shard-config) |


<span id=".XzIwMjIt5bm0LTA1LeaciA=="></span>
## May 2022


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="update\|k0w8kj">更新</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) |2022\-05\-31 |Added `ProjectName` field to request parameters to specify project to which the instance belongs. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="update\|I4RwX8">更新</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||Added `ProjectName` field to response parameters to display the project to which the instance belongs. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="update\|PKGlHS">更新</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||||
|<span data-api-tag="update\|GBCuna">更新</span> [CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) ||Added `EipIds` field to request parameters to associate with EIP when applying for public network address. |* [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address)<br><br>* [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address) |
|<span data-api-tag="update\|cGeWPs">更新</span> [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) ||* Added `EipId` field to response parameters to display EIP information associated with the instance's public network connection address.<br><br>* Added `SubnetId` field to response parameters to display instance's subnet information. |[Introduction to connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction) |
|<span data-api-tag="update\|5qvSgf">更新</span> [DeleteDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint) ||Added `MongosNodeIds` field to request parameter to specify Mongos node IDs whose public network connection addresses need to be released. |[Releasing public address](https://docs.byteplus.com/en/docs/mongodb/release-public-address) |


<span id=".XzIwMjIt5bm0LTA0LeaciA=="></span>
## April 2022


|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|<span data-api-tag="add\|ZsNpgt">新增</span> [DescribeRegions](https://docs.byteplus.com/en/docs/mongodb/describeregions) |2022\-04\-12 |Added new API to query available regional resource information for MongoDB. |[Service endpoints](https://docs.byteplus.com/en/docs/mongodb/request-structure#9TeFSOVO) |
|<span data-api-tag="add\|9Upgny">新增</span> [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/mongodb/describeavailabilityzones) ||Added new API to query the list of availability zone resources of MongoDB in specified region. ||
|<span data-api-tag="add\|EjuPId">新增</span> [CreateDBInstance](https://docs.byteplus.com/en/docs/mongodb/createdbinstance) ||Added new API to create MongoDB instances. |[Creating instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) |
|<span data-api-tag="add\|8HRbDI">新增</span> [DescribeNodeSpecs](https://docs.byteplus.com/en/docs/mongodb/describenodespecs) ||Added new API to query supported node specifications for creating MongoDB instances. |[Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification) |
|<span data-api-tag="add\|Z2xfcL">新增</span> [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) ||Added new API to query basic information of one or more MongoDB instances. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="add\|iBNXjr">新增</span> [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/mongodb/describedbinstancedetail) ||Added new API to query detailed information of target MongoDB instance. ||
|<span data-api-tag="add\|t8vESJ">新增</span> [RestartDBInstance](https://docs.byteplus.com/en/docs/mongodb/restartdbinstance) ||Added new API to restart target MongoDB instance. |[Restart instance](https://docs.byteplus.com/en/docs/mongodb/restart-instance) |
|<span data-api-tag="add\|6910iD">新增</span> [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancespec) ||Added new API to modify the configuration of the target MongoDB instance (such as node specification or storage capacity). |* [Modifying replica set instance configuration](https://docs.byteplus.com/en/docs/mongodb/modify-replica-set-instance-spec)<br><br>* [Modifying Mongos node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config)<br><br>* [Modifying shard configuration](https://docs.byteplus.com/en/docs/mongodb/modify-shard-config)<br><br>* [Modifying ConfigServer node configuration](https://docs.byteplus.com/en/docs/mongodb/modify-configserver-config) |
|<span data-api-tag="add\|nonSIU">新增</span> [ModifyDBInstanceName](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancename) ||Added new API to modify instance name of target MongoDB instance. |[Viewing instance information](https://docs.byteplus.com/en/docs/mongodb/view-instance) |
|<span data-api-tag="add\|nzT2qc">新增</span> [DeleteDBInstance](https://docs.byteplus.com/en/docs/mongodb/deletedbinstance) ||Added new API to delete target MongoDB instance. |[Deleting pay-as-you-go instance](https://docs.byteplus.com/en/docs/mongodb/delete-instance) |
|<span data-api-tag="add\|GHt2rH">新增</span> [ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancechargetype) ||Added new API to modify billing type of target MongoDB instance. |* [Switching to subscription](https://docs.byteplus.com/en/docs/mongodb/switch-to-subscription)<br><br>* [Switching to pay-as-you-go](https://docs.byteplus.com/en/docs/mongodb/switch-to-pay-as-you-go) |
|<span data-api-tag="add\|IZfzde">新增</span> [ResetDBAccount](https://docs.byteplus.com/en/docs/mongodb/resetdbaccount) ||Added new API to reset password of specified account in target MongoDB instance. |* [Resetting password](https://docs.byteplus.com/en/docs/mongodb/reset-password)<br><br>* [Resetting root account](https://docs.byteplus.com/en/docs/mongodb/reset-root-account) |
|<span data-api-tag="add\|X4gQ2s">新增</span> [DescribeDBAccounts](https://docs.byteplus.com/en/docs/mongodb/describedbaccounts) ||Added new API to query account information in target MongoDB instances. |[Viewing account details](https://docs.byteplus.com/en/docs/mongodb/viewing_account_information) |
|<span data-api-tag="add\|7B4ovY">新增</span> [CreateDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/createdbendpoint) ||Added new API to create connection address for target MongoDB instance. |* [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address)<br><br>* [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address) |
|<span data-api-tag="add\|sR8XP8">新增</span> [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) ||Added new API to query connection address information of target MongoDB instance. |[Introduction to connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction) |
|<span data-api-tag="add\|bCD82g">新增</span> [DeleteDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/deletedbendpoint) ||Added new API to delete connection address of target MongoDB instance. |[Releasing private address](https://docs.byteplus.com/en/docs/mongodb/release-private-address) |
|<span data-api-tag="add\|Pz6SkR">新增</span> [CreateAllowList](https://docs.byteplus.com/en/docs/mongodb/createallowlist) ||Added new API to create target IP allowlist. |[Creating an allowlist](https://docs.byteplus.com/en/docs/mongodb/create-allowlist) |
|<span data-api-tag="add\|6oZpWE">新增</span> [DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) ||Added new API to query all IP allowlist information for specified region under current account. |[Allowlist management](https://docs.byteplus.com/en/docs/mongodb/manage-allowlists) |
|<span data-api-tag="add\|BaMWvs">新增</span> [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) ||Added new API to query detailed information of target allowlist, including IP addresses and details of associated instances. ||
|<span data-api-tag="add\|wMG0ZR">新增</span> [ModifyAllowList](https://docs.byteplus.com/en/docs/mongodb/modifyallowlist) ||Added new API to modify target allowlist information (such as allowlist name and IP allowlist address). |[Editing an allowlist](https://docs.byteplus.com/en/docs/mongodb/edit-allowlist) |
|<span data-api-tag="add\|PMUPjm">新增</span> [AssociateAllowList](https://docs.byteplus.com/en/docs/mongodb/associateallowlist) ||Added new API to associate target MongoDB instance with specified IP allowlist. |[Associating instances and allowlists](https://docs.byteplus.com/en/docs/mongodb/associate-allowlist) |
|<span data-api-tag="add\|6QQDwc">新增</span> [DisassociateAllowList](https://docs.byteplus.com/en/docs/mongodb/disassociateallowlist) ||Added new API to disassociate target MongoDB instance from specified IP allowlist. |[Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/mongodb/disassociate-allowlist) |
|<span data-api-tag="add\|CgPwwK">新增</span> [DeleteAllowList](https://docs.byteplus.com/en/docs/mongodb/deleteallowlist) ||Added new API to delete target allowlist. |[Deleting allowlist](https://docs.byteplus.com/en/docs/mongodb/delete-allowlist) |


&nbsp;

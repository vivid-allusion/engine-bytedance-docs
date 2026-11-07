---
title: "API changelog"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/api-changelog"
---

This topic summarizes the changelog of API of Cache for Redis for your reference.

## October 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribePlannedEventImpactDetail](https://docs.byteplus.com/en/docs/redis/DescribePlannedEventImpactDetail) |2026\-10\-15 |New API. |[Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event) |
|新增 Public struct \- ImpactSummary ||Added new public struct. |* [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) |
|新增 Public struct \- PlannedEventImpactDetail |||* [DescribePlannedEventImpactDetail](https://docs.byteplus.com/en/docs/redis/DescribePlannedEventImpactDetail) |
|新增 Public structure \- ImpactItem ||||
|新增 Public Struct \- ImpactNode ||||
|更新Public Struct \- PlannedEventInfo ||Added parameters ExeEndTime, ExeStartTime, and ImpactSummary. |* [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) |

## August 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [DescribeBackupPlan](https://docs.byteplus.com/en/docs/redis/describebackupplan) |2026\-08\-05 |Update the value range for the BackupType return parameter. |[Automatic backup](https://docs.byteplus.com/en/docs/redis/automatic-backup) |

## July 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [SyncAllowList](https://docs.byteplus.com/en/docs/redis/SyncAllowList) |2026\-07\-22 |New API. |[Synchronizing security group](https://docs.byteplus.com/en/docs/redis/synchronizing_the_security_group) |
|新增 [DescribeTasks](https://docs.byteplus.com/en/docs/redis/DescribeTasks) |||[Task management](https://docs.byteplus.com/en/docs/redis/task-management) |
|新增 [ApplyParameterGroup](https://docs.byteplus.com/en/docs/redis/ApplyParameterGroup) |||[Applying parameter template](https://docs.byteplus.com/en/docs/redis/apply-parameter-template) |
|新增 [DescribeClientSessionSnapshot](https://docs.byteplus.com/en/docs/redis/DescribeClientSessionSnapshot) |||[Instance sessions](https://docs.byteplus.com/en/docs/redis/instance-session) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) ||Updated the length limit for request parameter Password. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |
|更新 [CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) ||* Updated the value range for the request parameter RoleName, adding the `NotWrite` value.<br><br>* Updated the length limit for request parameter Password. |[Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account) |
|更新 [ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) ||* Updated the length limit for request parameter Password.<br><br>* Updated the value range for the request parameter RoleName, adding the `NotWrite` value. ||
|更新 [DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) ||Updated the description for the response parameter Commands, adding an explanation for the `NotWrite` role. |[Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command) |
|更新 [DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) ||Updated the description of the `Categories` return parameter, adding an explanation for the `NotWrite` role. ||
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added new return parameter Modules. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |

## May 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeDBInstanceSlots](https://docs.byteplus.com/en/docs/redis/DescribeDBInstanceSlots) |2026\-05\-28 |New API. |[Slot distribution view](https://docs.byteplus.com/en/docs/redis/Slot_distribution_view) |
|新增 [DescribeFatLogs](https://docs.byteplus.com/en/docs/redis/DescribeFatLogs) |||[Querying fatlog](https://docs.byteplus.com/en/docs/redis/query-fat-log) |
|新增 [CreateBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/createbluegreendeployment) ||Added an API for creating blue\-green deployment tasks. |[Upgrading major versions using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment) |
|新增 [DescribeBlueGreenDeployments](https://docs.byteplus.com/en/docs/redis/describebluegreendeployments) ||Add API to query blue\-green deployment task details for the target Redis instance ||
|新增 [SwitchoverBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/switchoverbluegreendeployment) ||Added new API to perform blue/green deployment switch for the target Redis instance. ||
|新增 [DeleteBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/deletebluegreendeployment) ||||
|更新 [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) ||Added parameter `Action` to the PlannedEvents data structure as a response parameter. |[Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event) |
|更新 [DescribeHotKeys](https://docs.byteplus.com/en/docs/redis/describehotkeys) ||Added the `ActionType` parameter to the HotKey data structure, which is a response parameter. |[Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) ||The Backups data structure, a return parameter, now includes the new parameter `BackupProgress`. |[Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup) |

## April 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeDBEngineVersions](https://docs.byteplus.com/en/docs/redis/describedbengineversions) |2026\-04\-13 |Added new API to query list of minor versions supported by Redis major versions. |[Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version) |
|新增 [ModifyDBInstanceMinorVersion](https://docs.byteplus.com/en/docs/redis/modifydbinstanceminorversion) ||Added new API to upgrade target Redis instance to specified minor version. ||
|新增 [EnableDBInstanceHA](https://docs.byteplus.com/6293/2245715) ||Added new API to switch Redis single node instance to primary\-secondary instance. |[Switching to primary-secondary instance](https://docs.byteplus.com/en/docs/redis/switch_to_high_availability_instance) |
|更新 [SwitchOver](https://docs.byteplus.com/en/docs/redis/switchover) ||Added `TargetPrimaryNodeIds` field to request parameters, compatible with the existing `TargetPrimaryNodeId` field, which can be used to batch switch primary nodes for multiple shards. |[Executing failover manually](https://docs.byteplus.com/en/docs/redis/switch-primary-node-manually) |

## January 2026

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DeleteAllClientSession](https://docs.byteplus.com/en/docs/redis/deleteallclientsession) |2026\-01\-29 |Added new API to terminate all sessions in target Redis instance. |[Instance sessions](https://docs.byteplus.com/en/docs/redis/instance-session) |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added `BlueGreenRole` field to response parameters to display the instance's blue\-green deployment role. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) ||||

## December 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [InterruptKeyScanJob](https://docs.byteplus.com/en/docs/redis/interruptkeyscanjob) |2025\-12\-22 |Added new API to cancel specified expired key clear task. |[Canceling expired key clear task](https://docs.byteplus.com/en/docs/redis/cancel_expired_key_cleanup_task) |
|更新 [ModifyBackupPlan](https://docs.byteplus.com/en/docs/redis/modifybackupplan) ||Request parameter `Active` has been changed from required to optional, with a default value of `false`. |[Automatic backup](https://docs.byteplus.com/en/docs/redis/automatic-backup) |

## November 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [TestFailoverDBInstanceZone](https://docs.byteplus.com/en/docs/redis/testfailoverdbinstancezone) |2025\-11\-24 |Added new API to simulate availability zone\-level failover for target Redis instance. |[Failover](https://docs.byteplus.com/en/docs/redis/failover) |
|新增 [TestShutDownDBInstanceNodes](https://docs.byteplus.com/en/docs/redis/testshutdowndbinstancenodes) ||Added new API to simulate a specified server or proxy node failover for target Redis instance. |[Multi-availability-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution) |
|更新 [DescribeDBInstanceBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard) |2025\-11\-05 |Added `AdditionalWriteBandwithPerShard` and `AdditionalReadBandwidthPerShard` fields to response parameters, replacing the original `AdditionalBandwidthPerShard` field, to display the instance's additional write and read bandwidth, respectively. |[Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth) |
|更新 [ModifyDBInstanceAdditionalBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/modifydbinstanceadditionalbandwidthpershard) ||Added `AdditionalWriteBandwidth` and `AdditionalReadBandwidth` fields to request parameters, compatible with the original `AdditionalBandwidth` field, to set instance's additional write and additional read bandwidth, respectively. ||

## September 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [ModifyDBInstancePrivateDNSVisibility](https://docs.byteplus.com/en/docs/redis/modifydbinstanceprivatednsvisibility) |2025\-09\-24 |Added new API to enable or disable public network resolution for target Redis instances. |[Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/redis/set-public-network-resolution) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) ||Added `PrivatePort` field to response parameters to display the port number of the instance's private network address |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |

## August 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) |2025\-08\-26 |The character length limit for request parameter `AllowListName` has been changed from 32 to 128. |[Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) |||[Editing an allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist) |

## July 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [CreateKeyScanJob](https://docs.byteplus.com/en/docs/redis/createkeyscanjob) |2025\-07\-16 |Added new API to create expired key clear task for target Redis instance. |[Expired key management](https://docs.byteplus.com/en/docs/redis/Expired_key_management) |
|新增 [DescribeKeyScanJobs](https://docs.byteplus.com/en/docs/redis/describekeyscanjobs) ||Added new API to query the list of key clear tasks for target Redis instance within the specified time period. ||

## June 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) |2025\-06\-24 |The maximum value of request parameter `PageSize` increased from 100 to 1000. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |||[Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup) |
|更新 [DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |||[Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter) |
|更新 [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) |||[Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event) |
|更新 [DescribeBigKeys](https://docs.byteplus.com/en/docs/redis/describebigkeys) ||The upper limit for the time interval between `QueryStartTime` and `QueryEndTime` in request parameters has been increased from 1 hour to 24 hours. |[Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) |

## May 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/redis/modifyplannedeventexecutetime) |2025\-05\-27 |Added new API to modify the execution time of planned system maintenance events. |[Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time) |
|新增 [ExecutePlannedEvent](https://docs.byteplus.com/en/docs/redis/executeplannedevent) ||Added new API to immediately execute the scheduled event. |[Executing planned event](https://docs.byteplus.com/en/docs/redis/execute-planned-event) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) ||Request parameter `ShardCapacity` newly supports the value of `512`, used to create Redis instance with node specification of 512 MiB. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |
|更新 [ModifyDBInstanceShardCapacity](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity) ||The request parame`ter ShardCapa`city newly supports the value` of` 512, used to change the instance' single\-shard capacity to 512 MiB. |[Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) |
|更新 [CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress) ||Added `Port` field to request parameters to set the port number for public network addresses. |[Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address) |
|更新 [ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) ||The `NewPort` field in request parameters removes restrictions on public network addresses, allowing modification of the public network address port number. |* [Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address)<br><br>* [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port)<br><br>* [Upgrading domain suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix) |

## April 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/redis/describedbinstancespecs) |2025\-04\-22 |Added new API to query the list of instance specifications supported by Redis. |[Product specifications](https://docs.byteplus.com/en/docs/redis/product-specification) |

## March 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeHotKeys](https://docs.byteplus.com/en/docs/redis/describehotkeys) |2025\-03\-19 |Added new API to query the details of hot keys for target Redis instances within a specified time range. |[Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis) |
|新增 [ModifyMaintenanceTime](https://docs.byteplus.com/en/docs/redis/modifymaintenancetime) ||Added new API to modify the maintenance period of target Redis instance. |[Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period) |
|新增 [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) ||Added new API to query the planned events of target Redis instance within specified time range. |[Viewing planned event](https://docs.byteplus.com/en/docs/redis/manage-planned-event) |
|更新 [ModifyDBInstanceShardCapacity](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity) ||Added `ReserveAdditionalBandwidth` optional field to request parameters, which allows to set whether to retain the instance's additional bandwidth when changing node specifications. |[Modifying node specifications](https://docs.byteplus.com/en/docs/redis/modify-node-spec) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) ||Adjusted password rules for request parameter `Password`, increasing the maximum password length from 30 to 32 characters. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |
|更新 [CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) |||[Creating account](https://docs.byteplus.com/en/docs/redis/manage-account) |
|更新 [ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) |||* [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password)<br><br>* [Managing accounts](https://docs.byteplus.com/en/docs/redis/manage-account#.5ZCO57ut5pON5L2c) |
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) ||Added `ProjectName` field to request parameters to specify the allowlist's project. |[Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) |
|更新 [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) ||* Added `ProjectName` field to request parameters to filter allowlist information for the specified project.<br><br>* Added `ProjectName` field to `AllowLists` structure of response parameters, which is used to display the project to which the allowlist belongs. |[Allowlist management](https://docs.byteplus.com/en/docs/redis/manage-allowlists) |
|更新 [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) ||* Added `ProjectName` and `AssociatedInstanceNum` fields to response parameters to display the project to which the allowlist belongs and the total number of associated instances, respectively.<br><br>* Added `ProjectName` field to `AssociatedInstances` structure of response parameters to display the project to which the instance belongs. ||
|更新 [ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) ||Added `UpgradeRegionDomain` field to request parameters, which can be used to upgrade the domain suffix of the connection address. |* [Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address)<br><br>* [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port)<br><br>* [Upgrading domain suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix) |

## February 2025

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [CreateDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointdirectlinkaddress) |2025\-02\-13 |Added new API to apply for direct connection addresses for target Redis instances. |[Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) |
|新增 [DeleteDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointdirectlinkaddress) ||Added new API to release the direct connection address for target Redis instance. |[Releasing direct connection address](https://docs.byteplus.com/en/docs/redis/release-direct-connection-address) |
|新增 [CreateParameterGroup](https://docs.byteplus.com/en/docs/redis/createparametergroup) ||Added new API to create parameter templates. |[Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template) |
|新增 [DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) ||Added new API to query basic information of parameter templates under the current account and region. |[Parameter template management](https://docs.byteplus.com/en/docs/redis/parameter-template-overview) |
|新增 [DescribeParameterGroupDetail](https://docs.byteplus.com/en/docs/redis/describeparametergroupdetail) ||Added new API to query detailed information of target parameter group. ||
|新增 [ModifyParameterGroup](https://docs.byteplus.com/en/docs/redis/modifyparametergroup) ||Added new API to modify the parameter template information (such as parameter template name, description, and parameter values in the template). |[Editing parameter template](https://docs.byteplus.com/en/docs/redis/edit-parameter-template) |
|新增 [DeleteParameterGroup](https://docs.byteplus.com/en/docs/redis/deleteparametergroup) ||Added new API to delete target parameter template. |[Deleting parameter template](https://docs.byteplus.com/en/docs/redis/delete-parameter-template) |
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) ||Added `NoAuthMode` and `ParameterGroupId` fields to request parameters, which can be used to enable password\-free accessand associate specified parameter templates for new instances. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |

## December 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeDBInstanceBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard) |2024\-12\-26 |Added new API to query the single shard bandwidth details of target Redis, including default bandwidth and additional bandwidth. |[Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth) |
|更新 [ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) ||Added `AccountStatus` field to response parameters, to display the account status. |[Managing accounts](https://docs.byteplus.com/en/docs/redis/manage-account#.5ZCO57ut5pON5L2c) |
|更新 [CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) ||Changed request type from synchronous request to asynchronous request. |[Creating account](https://docs.byteplus.com/en/docs/redis/manage-account) |
|更新 [ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) |||* [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password)<br><br>* [Managing accounts](https://docs.byteplus.com/en/docs/redis/manage-account#.5ZCO57ut5pON5L2c) |
|更新 [DeleteDBAccount](https://docs.byteplus.com/en/docs/redis/deletedbaccount) |||[Managing accounts](https://docs.byteplus.com/en/docs/redis/manage-account#.5ZCO57ut5pON5L2c) |
|更新 [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) ||Added `IPAddress` and `IPSegment` fields to request parameters to filter allowlists that meet the corresponding IP address or address segment conditions. |[Allowlist management](https://docs.byteplus.com/en/docs/redis/manage-allowlists) |

## November 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) |2024\-11\-28 |Added new API to query the list of commands supported by a specified command category in target Redis instance. |[Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command) |
|新增 [DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) ||Added new API to query details of command categories supported by target Redis instance. ||
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added `ConfigureNodes` structure to response parameters to display availability zone information for all nodes in the instance. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) ||* Request parameter `AllowList` has been changed from required to optional.<br><br>* Added `SecurityGroupBindInfos` structure to request parameters to specify associated security groups when creating new allowlist. |[Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) ||Added `SecurityGroupBindInfos` structure to request parameters to specify associated security groups when modifying the allowlist. |[Editing an allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist) |
|更新 [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) ||Added `SecurityGroupBindInfos` structure to response parameters to display information about security groups associated with the allowlist. |[Allowlist management](https://docs.byteplus.com/en/docs/redis/manage-allowlists) |
|更新 [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) ||||

## October 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) |2024\-10\-24 |The `RegionIds`, `PageNumber`, and `PageSize` fields in request parameters have been changed from required to optional. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) ||Added the `AllowListCategory` field to request parameters to set the type of new allowlists. |[Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) ||Added `AllowListCategory` field to request parameters for modifying the allowlist type. |[Editing an allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist) |
|更新 [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) ||* Added `QueryDefault` field to request parameters to filter default allowlists.<br><br>* Added `AllowListCategory` field to response parameters to display the allowlist type. |[Allowlist management](https://docs.byteplus.com/en/docs/redis/manage-allowlists) |
|更新 [DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) ||Added `AllowListCategory` field to response parameters to display the allowlist type. ||

## September 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) |2024\-09\-12 |* Request parameter `InstanceId` has changed from supporting fuzzy search to exact search.<br><br>* The default value of request parameter `ServiceType` has changed to `Basic`.<br><br>* Added `PrivateAddress`, `VIP`, and `VIPv6` fields to `Instances` structure in response parameter, which are used to display the instance's private network address domain name and the corresponding IPv4 and IPv6 address information. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added `VIPv6` field to `VisitAddrs` structure of response parameters to display the IPv6 address information for the instance connection address. ||
|更新 [DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) ||* Added `BackupPointId` field to request parameters to filter backups that meet the corresponding conditions.<br><br>* Changed the structure name `InstanceDetail` to `InstanceInfo` in response parameters, and the following modifications have been made to this structure:<br><br>   * Deleted the `AutoRenew` and `UsedCapacity` fields.<br><br>   * Original `VpcInfo` structure (which contained the `ID` and `Name` fields for VPC) has been deleted and replaced by the new `VpcId` field.<br><br>   * Field name `ShardCount` changed to `ShardNumber`.<br><br>   * The data type of `ShardCapacity` has been changed from Integer to Double. |[Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup) |

## August 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [ModifyDBInstanceMaxConn](https://docs.byteplus.com/en/docs/redis/modifydbinstancemaxconn) |2024\-08\-08 |Added new API to modify the maximum number of connections per shard for target Redis instance. |[Modifying maximum connections](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number) |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added `MaxConnections` field to response parameters to display the current maximum number of connections per shard of the instance. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) ||The request parameter `AllowListName` field has been changed from required to optional. |[Editing an allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist) |

## July 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [ModifyDBInstanceAdditionalBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/modifydbinstanceadditionalbandwidthpershard) |2024\-07\-10 |Added `OrderNO` field to response parameters to display the order ID generated by modifying additional bandwidth. |[Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth) |

## June 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) |2024\-06\-13 |Request parameter `EngineVersion` newly supports the value of `7.0`, which is used to create Redis version 7.0 instances. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |

## May 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|新增 [ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) |2024\-05\-09 |Added new API to modify the domain name or port number of a specified connection address in target Redis instance. |* [Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address)<br><br>* [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port)<br><br>* [Upgrading domain suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix) |

## April 2024

|API |Release time |Change records |Relevant functions |
|---|---|---|---|
|更新 [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) |2024\-04\-11 |Request parameter `Password` has been changed from required to optional. |[Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) |
|更新 [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) ||Added `ServiceType` field to request parameters to filter instances that meet the corresponding conditions. |[Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance) |
|更新 [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) ||Added `VIP` field to `VisitAddrs` structure of response parameters to display the IPv4 address information for the instance connection address. ||

---
title: "API overview"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/api-overview"
---

This topic summarizes the APIs provided by Cache for Redis.

> **tip**

> In a single region, the API flow control limit of Cache for Redis is 20 times per second. One BytePlus account cannot call a single API more than 20 times per second. If the limit is exceeded, the API request will fail, and the error `AccountFlowLimitExceeded` will be reported.

## Region and availability zone

|API |Description |
|---|---|
|[DescribeRegions](https://docs.byteplus.com/en/docs/redis/describeregions) |Call the DescribeRegions API to query the list of regions available for Cache for Redis. |
|[DescribeZones](https://docs.byteplus.com/en/docs/redis/describezones) |Call the DescribeZones API to query the list of availability zones available for Cache for Redis in a specified region. |

## Instance management

|API |Description |
|---|---|
|[CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance) |Call the CreateDBInstance API to create Redis instance. |
|[DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/redis/describedbinstancespecs) |Call the DescribeDBInstanceSpecs API to query the list of instance specifications supported by Redis. |
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) |Call the DescribeDBInstances API to query basic information about Redis instances. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query details about the target Redis instance. |
|[DescribeDBInstanceShards](https://docs.byteplus.com/en/docs/redis/describedbinstanceshards) |Call the DescribeDBInstanceShards API to query details about Server nodes in each shard of the target Redis instance. |
|[DescribeNodeIds](https://docs.byteplus.com/en/docs/redis/describenodeids) |Call the DescribeNodeIds API to query the list of all Proxy and Server node IDs in the target Redis instance. |
|[DescribeDBInstanceSlots](https://docs.byteplus.com/en/docs/redis/DescribeDBInstanceSlots) |Call the DescribeDBInstanceSlots API to query the slot allocation of each shard under the target Redis instance. |
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/redis/modifydbinstancename) |Call the ModifyDBInstanceName API to modify an instance name. |
|[ModifyDBInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/redis/modifydbinstancedeletionprotectionpolicy) |Call the ModifyDBInstanceDeletionProtectionPolicy API to enable or disable the instance deletion protection. |
|[ModifyDBInstanceAZConfigure](https://docs.byteplus.com/en/docs/redis/modifydbinstanceazconfigure) |Call the ModifyDBInstanceAZConfigure to modify the availability zone of a specified instance. |
|[ModifyMaintenanceTime](https://docs.byteplus.com/en/docs/redis/modifymaintenancetime) |Call the ModifyMaintenanceTime API to modify the maintenance period of target Redis instance. |
|[RestartDBInstance](https://docs.byteplus.com/en/docs/redis/restartdbinstance) |Call the RestartDBInstance API to restart target Redis instance. |
|[RestartDBInstanceProxy](https://docs.byteplus.com/en/docs/redis/restartdbinstanceproxy) |Call the RestartDBInstanceProxy API to restart one or more proxy nodes in a specified Redis instance. |
|[SwitchOver](https://docs.byteplus.com/en/docs/redis/switchover) |Call the SwitchOver API to perform primary\-secondary node switchover for a specified instance. |
|[FlushDBInstance](https://docs.byteplus.com/en/docs/redis/flushdbinstance) |Call the FlushDBInstance API to clear all business data in the target Redis instance. |
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/redis/deletedbinstance) |Call the DeleteDBInstance API to delete target Redis instance. |
|[DescribeDBEngineVersions](https://docs.byteplus.com/en/docs/redis/describedbengineversions) |Call the DescribeDBEngineVersions API to query the list of minor versions supported by each Redis major version. |
|[ModifyDBInstanceMinorVersion](https://docs.byteplus.com/en/docs/redis/modifydbinstanceminorversion) |Call the ModifyDBInstanceMinorVersion API to upgrade target Redis instance to specified minor version. |
|[CreateBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/createbluegreendeployment) |Call the CreateBlueGreenDeployment API to create blue\-green deployment task for target Redis instance. |
|[DescribeBlueGreenDeployments](https://docs.byteplus.com/en/docs/redis/describebluegreendeployments) |Call the DescribeBlueGreenDeployments API to query details about blue\-green deployment tasks of the target Redis instance. |
|[SwitchoverBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/switchoverbluegreendeployment) |Call the SwitchoverBlueGreenDeployment API to perform blue\-green deployment switch for target Redis instance. |
|[DeleteBlueGreenDeployment](https://docs.byteplus.com/en/docs/redis/deletebluegreendeployment) |Call the DeleteBlueGreenDeployment API to cancel the blue\-green deployment task for the target Redis instance. |

## Changing instance configuration

|API |Description |
|---|---|
|[IncreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/increasedbinstancenodenumber) |Call the IncreaseDBInstanceNodeNumber API to increase the number of single shard nodes for target Redis instance. |
|[DecreaseDBInstanceNodeNumber](https://docs.byteplus.com/en/docs/redis/decreasedbinstancenodenumber) |Call the DecreaseDBInstanceNodeNumber API to reduce the number of single\-shard nodes for the target Redis instance. |
|[ModifyDBInstanceShardCapacity](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardcapacity) |Call the ModifyDBInstanceShardCapacity API to modify the single shard memory of target Redis instance. |
|[ModifyDBInstanceShardNumber](https://docs.byteplus.com/en/docs/redis/modifydbinstanceshardnumber) |Call the ModifyDBInstanceShardNumber API to modify the number of shards of the target Redis instance. |
|[EnableShardedCluster](https://docs.byteplus.com/en/docs/redis/enableshardedcluster) |Call the EnableShardedCluster API to change an instance with sharding cluster disabled to an instance with sharding cluster enabled. |
|[EnableDBInstanceHA](https://docs.byteplus.com/en/docs/redis/enabledbinstanceha) |Call the EnableDBInstanceHA API to change the Redis single\-node instance to the primary and backup instances. |

## Tag management

|API |Description |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/redis/addtagstoresource) |Call the AddTagsToResource API to associate tags with target Redis instance. |
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/redis/describetagsbyresource) |Call the DescribeTagsByResource API to query tags bound to the target Redis instance. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/redis/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate tags for one or more instances. |

## Billing management

|API |Description |
|---|---|
|[ModifyDBInstanceChargeType](https://docs.byteplus.com/en/docs/redis/modifydbinstancechargetype) |Call the ModifyDBInstanceChargeType API to modify the billing method of the target instance. |

## Backup and recovery

|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/redis/createbackup) |Call the CreateBackup API to create backup manually for a specified Redis instance. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |Call the DescribeBackups API to query the backup set list of the target Redis instance. |
|[DescribeBackupPlan](https://docs.byteplus.com/en/docs/redis/describebackupplan) |Call the DescribeBackupPlan API to query the automatic backup policy of the target Redis instance, including the backup type, backup cycle, and expected time of the next backup. |
|[ModifyBackupPlan](https://docs.byteplus.com/en/docs/redis/modifybackupplan) |Call the ModifyBackupPlan API to modify the automatic backup settings of specified Redis instance, including backup cycle, automatic backup enable or disable, and other settings. |
|[DescribePitrTimeWindow](https://docs.byteplus.com/en/docs/redis/describepitrtimewindow) |Call the DescribePitrTimeWindow API to query the recoverable time range supported by the target Redis instance for point\-in\-time recovery. |
|[DescribeBackupPointDownloadUrls](https://docs.byteplus.com/en/docs/redis/describebackuppointdownloadurls) |Call the DescribeBackupPointDownloadUrls API to query the download address of the specified backup file in the target Redis instance. |
|[StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) |Call the StartContinuousBackup API to enable data flashback for target Redis instance. |
|[StopContinuousBackup](https://docs.byteplus.com/en/docs/redis/stopcontinuousbackup) |Call the StopContinuousBackup API to disable data flashback for a specified instance. |
|[RestoreDBInstance](https://docs.byteplus.com/en/docs/redis/restoredbinstance) |Call the RestoreDBInstance API to restore the data in a backup set to the original Redis instance. |

## Parameter management

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the list of parameters supported by the target Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the parameter configuration of target Redis instance. |
|[CreateParameterGroup](https://docs.byteplus.com/en/docs/redis/createparametergroup) |Call the CreateParameterGroup API to create a parameter template. |
|[DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) |Call the DescribeParameterGroups API to query basic information about parameter templates under the current account and region. |
|[DescribeParameterGroupDetail](https://docs.byteplus.com/en/docs/redis/describeparametergroupdetail) |Call the DescribeParameterGroupDetail API to query details about the target parameter template. |
|[ModifyParameterGroup](https://docs.byteplus.com/en/docs/redis/modifyparametergroup) |Call the ModifyParameterGroup API to modify the parameter template information (such as parameter template name, description, and parameter values in the template). |
|[ApplyParameterGroup](https://docs.byteplus.com/en/docs/redis/ApplyParameterGroup) |Call the ApplyParameterGroup API to apply the parameter template to the instance. |
|[DeleteParameterGroup](https://docs.byteplus.com/en/docs/redis/deleteparametergroup) |Call the DeleteParameterGroup API to delete the target parameter template. |

## Connection management

|API |Description |
|---|---|
|[ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode) |Call the ModifyDBInstanceVpcAuthMode API to enable or disable password\-free access. |
|[ModifyDBInstanceSubnet](https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet) |Call the ModifyDBInstanceSubnet API to modify  VPC or subnet for target Redis instance. |
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress) |Call the CreateDBEndpointPublicAddress API to create the public address for target Redis instance (enable Internet access for an instance). |
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointpublicaddress) |Call the DeleteDBEndpointPublicAddress API to release the public connection address of the target Redis instance, that is, to disable public access. |
|[CreateDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointdirectlinkaddress) |Call the CreateDBEndpointDirectLinkAddress API to apply for a direct connection address for target Redis instance. |
|[DeleteDBEndpointDirectLinkAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointdirectlinkaddress) |Call the DeleteDBEndpointDirectLinkAddress API to release the direct connection address of the target Redis instance. |
|[DescribeDBInstanceBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/describedbinstancebandwidthpershard) |Call the DescribeDBInstanceBandwidthPerShard API to query the single\-shard bandwidth details of the target Redis, including default bandwidth and additional bandwidth. |
|[ModifyDBInstanceAdditionalBandwidthPerShard](https://docs.byteplus.com/en/docs/redis/modifydbinstanceadditionalbandwidthpershard) |Call the ModifyDBInstanceAdditionalBandwidthPerShard API to modify the single shard bandwidth for target Redis instance. |
|[ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) |Call the ModifyDBInstanceVisitAddress API to modify the address or port number of the target connection address of the specified instance. |
|[ModifyDBInstanceMaxConn](https://docs.byteplus.com/en/docs/redis/modifydbinstancemaxconn) |Call the ModifyDBInstanceMaxConn API to modify the maximum number of connections per shard of the specified Redis instance. |
|[ModifyDBInstancePrivateDNSVisibility](https://docs.byteplus.com/en/docs/redis/modifydbinstanceprivatednsvisibility) |Call the ModifyDBEndpointPrivateDNSVisibility API to enable or disable the public network resolution function for the target Redis instance. |

## Account management

|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) |Call the CreateDBAccount API to create an account for target Redis instance. |
|[ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) |Call the ListDBAccount API to query the information of specified accounts or all accounts for a Redis instance, including the account name and account role. |
|[ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) |Call the ModifyDBAccount API to modify the information of a specified account, including the account role, password, and description. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/redis/deletedbaccount) |Call the DeleteDBAccount API to delete the specified account from the target Redis instance. |
|[DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) |Call the DescribeDBInstanceAclCommands API to query the list of commands supported by the specified command category in target Redis instance. |
|[DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) |Call the DescribeDBInstanceAclCategories API to query the command categories supported by target Redis instance. |

## Allowlist management

|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) |Call the CreateAllowList API to create a new IP address allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query the IP allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query details about the target allowlist, including IP addresses and details about bound instances. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) |Call the ModifyAllowList API to modify the setting of a target allowlist (allowlist name, allowlist IP address, etc.). |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/redis/associateallowlist) |Call the AssociateAllowList API to associate the target instance to the specified IP address allowlist. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/redis/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target Redis instance from the specified IP allowlist. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/redis/deleteallowlist) |Call the DeleteAllowList API to delete the target IP allowlist. |
|[SyncAllowList](https://docs.byteplus.com/en/docs/redis/SyncAllowList) |Call the SyncAllowList API to synchronize the IP addresses of the security groups bound in the allowlist. |

## Log management

|API |Description |
|---|---|
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/redis/describeslowlogs) |Call the DescribeSlowLogs API to query slow log details of the target Redis instance within a specified time range. |
|[DescribeFatLogs](https://docs.byteplus.com/en/docs/redis/DescribeFatLogs) |Call the DescribeFatLogs API to query Fatlog log details of Server or Proxy nodes in the target Redis instance within a specified time range. |

## Event management

|API |Description |
|---|---|
|[DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) |Call the DescribePlannedEvents API to query scheduled events of the target Redis instance within a specified time range. |
|[DescribePlannedEventImpactDetail](https://docs.byteplus.com/en/docs/redis/DescribePlannedEventImpactDetail) |Call the DescribePlannedEventImpactDetail API to query impact information about planned events. |
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/redis/modifyplannedeventexecutetime) |Call the ModifyPlannedEventExecuteTime API to modify the execution time of planned system maintenance events. |
|[ExecutePlannedEvent](https://docs.byteplus.com/en/docs/redis/executeplannedevent) |Call the ExecutePlannedEvent API to immediately execute the scheduled event. |

## Performance analysis

|API |Description |
|---|---|
|[DescribeBigKeys](https://docs.byteplus.com/en/docs/redis/describebigkeys) |Call the DescribeBigKeys API to query large key details of the target Redis instance within a specified time range. |
|[DescribeHotKeys](https://docs.byteplus.com/en/docs/redis/describehotkeys) |Call the DescribeHotKeys API to query hot key details of the target Redis instance within a specified time range. |
|[CreateKeyScanJob](https://docs.byteplus.com/en/docs/redis/createkeyscanjob) |Call the CreateKeyScanJob API to create expired key cleanup task for the target Redis instance. |
|[DescribeKeyScanJobs](https://docs.byteplus.com/en/docs/redis/describekeyscanjobs) |Call the DescribeKeyScanJobs API to query the list of expired key cleanup tasks of the target Redis instance within a specified time range. |
|[InterruptKeyScanJob](https://docs.byteplus.com/en/docs/redis/interruptkeyscanjob) |Call the InterruptKeyScanJob API to cancel specified expired key cleanup task. |
|[DescribeClientSessionSnapshot](https://docs.byteplus.com/en/docs/redis/DescribeClientSessionSnapshot) |Call the DescribeClientSessionSnapshot API to query the client session snapshot of the instance within the specified time window. |
|[DeleteAllClientSession](https://docs.byteplus.com/en/docs/redis/deleteallclientsession) |Call the DeleteAllClientSession API to terminate all sessions in the target Redis instance. |

## Failure drills

|API |Description |
|---|---|
|[TestFailoverDBInstanceZone](https://docs.byteplus.com/en/docs/redis/testfailoverdbinstancezone) |Call the TestFailoverDBInstanceZone API to simulate an availability zone\-level failover for target Redis instance. |
|[TestShutDownDBInstanceNodes](https://docs.byteplus.com/en/docs/redis/testshutdowndbinstancenodes) |Call the TestShutDownDBInstanceNodes API to simulate the failover of the specified Server or Proxy nodes for the target Redis instance. |

## Task center

|API |Description |
|---|---|
|[DescribeTasks](https://docs.byteplus.com/en/docs/redis/DescribeTasks) |Call the DescribeTasks API to query tasks. |

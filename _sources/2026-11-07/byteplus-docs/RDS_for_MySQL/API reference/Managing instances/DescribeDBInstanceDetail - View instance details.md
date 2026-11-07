---
title: "DescribeDBInstanceDetail - View instance details"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail"
---

Call the DescribeDBInstanceDetail API to view instance details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API is deprecated. Use the following APIs to query instance information:


* [DescribeDBInstanceAttribute](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceAttribute): call the DescribeDBInstanceAttribute API to query the attributes of an instance.

* [DescribeDBInstanceEndpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceEndpoints): call the DescribeDBInstanceEndpoints API to query the list of instance connection endpoints.

* [DescribeResourceUsage](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourceUsage): call the DescribeResourceUsage API to query the resource usage of an instance.

* [DescribeDBInstanceChargeDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceChargeDetail): Call the DescribeDBInstanceChargeDetail API to query the billing information of the instance.

* [DescribeDBInstanceHAConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceHAConfig): Call the DescribeDBInstanceHAConfig API to query the high availability configuration of the instance.

* [DescribeDBDisasterRecoveryInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBDisasterRecoveryInstances): Call the DescribeDBDisasterRecoveryInstances API to query the disaster recovery instance information of the instance.

* [DescribeDBProxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBProxy): Call the DescribeDBProxy API to query the proxy configuration of the instance.


<span id=".6LCD6K-V"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-cf0c1a52\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BasicInfo |Object of [BasicInfoObject](https://docs.byteplus.com/en/docs/40/15520#basicinfoobject) |Refer to the Sample response. |Basic information of the instance. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/40/15520#chargedetailobject) |Refer to the Sample response. |Payment method. |
|Endpoints |Array of [EndpointObject](https://docs.byteplus.com/en/docs/40/15520#endpointobject) |Refer to the Sample response. |Instance connection information. |
|Nodes |Array of [NodeObject](https://docs.byteplus.com/en/docs/40/15520#nodeobject) |Refer to the Sample response. |Instance node information. |
|ProxyDetail |Object of [ProxyInfoObject](https://docs.byteplus.com/en/docs/40/15520#proxyinfoobject) |Refer to the Sample response. |Configuration of the database proxy for the instance. |
|DisasterRecoveryInstances |Array of [DisasterRecoveryInstance](https://docs.byteplus.com/en/docs/40/15520#disasterrecoveryinstance) |Refer to the Sample response. |Information about the disaster recovery instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The primary instance returns this field.</div><br> |


<span id="basicinfoobject"></span>
### BasicInfoObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AllowListVersion |String |V2 |Allowlists version. |
|AutoUpgradeMinorVersion |String |Auto |The upgrade policy for the kernel minor version of the instance. Values:<br><br><br>* `Auto`: automatic.<br><br>* `Manual`: manual. |
|CreateTime |String |2022\-01\-01T10:10:10Z |The local time when the instance was created. |
|CurrentKernelVersion |String |MySQL 8.0.32_20240415 |Kernel minor version of the instance. |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|DataSyncMode |String |Async |Data synchronization method:<br><br><br>* `SemiSync`: semisynchronous.<br><br>* `Async`: asynchronous. |
|DeletionProtection |String |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yes.<br><br>* `Disabled`: no. Default value. |
|InstanceId |String |mysql\-66347599\*\*\*\* |Instance ID. |
|InstanceName |String |Test instance |Instance name. |
|InstanceStatus |String |Running |Instance state, values:<br><br><br>* `Creating`: creating.<br><br>* `Running`: running.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: modifying.<br><br>* `Restoring`: recovering.<br><br>* `Error`: error.<br><br>* `Upgrading`: upgrading.<br><br>* `Released`: recycling.<br><br>* `Recycled`: recycled.<br><br>* `MasterChanging`: primary node switching.<br><br>* `TDEUpdating`: TDE modifying.<br><br>* `Closed`: shut down.<br><br>* `Maintaining`: maintaining.<br><br>* `CreateFailed`: failed to create.<br><br>* `Closing`: Shutting down.<br><br>* `SSLUpdating`: SSL modifying.<br><br>* `AllowListMaintaining`: Allowlist modifying.<br><br>* `Unknown`: Unknown.<br><br>* `ProxyCreating`: Proxy is enabling.<br><br>* `ProxyDeleting`: Proxy is disabling.<br><br>* `ChargeTypeChanging`: billing method changing.<br><br>* `NetWorkChanging`: Network changing. |
|InstanceType |String |DoubleNode |Instance type. Values:<br><br><br>* `DoubleNode`, double node type.<br><br>* `MultiNode`, multiple node type. |
|LowerCaseTableNames |String |true |Whether table names are case sensitive. The default value is `true`. Values:<br><br><br>* `false`: table names are stored in their original case and are case\-sensitive.<br><br>* `true`: table names are stored in lowercase and are not case\-sensitive. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/40/15520#maintenancewindowobject) |Refer to the sample. |Specifies the maintenance window for the instance during instance creation. This field is optional. If not specified, it defaults to 18:00Z\-21:59Z UTC (02:00\-05:59 Beijing time) every day of the week. |
|Memory |Integer |2 |Memory size. Unit: GiB. |
|NodeNumber |String |2 |Number of nodes. |
|NodeSpec |String |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ProjectName |String |Test |Affiliated project. |
|RegionId |String |cn\-beijing |Region ID, use [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions) to query the available region list. Use this parameter to specify the region for creating the instance. |
|StorageSpace |Long |200 |The storage space for the instance. Unit: GiB. |
|StorageType |String |LocalSSD |The storage type of the instance. Value is `LocalSSD`, which is local SSD disk. |
|StorageUse |Double |4.14 |Instance storage space used. Unit: GiB. |
|SubnetId |String |subnet\-3rf442t6a54w016nf3pg9\*\*\*\* |Subnet ID. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/15520#tagobject) |Refer to the sample. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when tags are associated with the instance.</div><br> |
|TimeZone |String |UTC + 08: 00 |Time zone |
|UpdateTime |String |2022\-01\-01T10:10:10Z |Instance update local time. |
|VCPU |Integer |1 |CPU size. For example: 1 indicates 1U. |
|VpcId |String |vpc\-3rebt5uf5fr405zsk2if9\*\*\*\* |Proprietary network (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|DrDtsTaskId |String |df5a93434880466cb8422b2db93d\*\*\*\* |The ID of the DTS data synchronization task for the synchronization link between the primary and disaster recovery instances. |
|MasterRegion |String |cn\-shanghai |The region where the primary instance of the disaster recovery instance is located. |
|DrDtsTaskName |String |Disaster recovery instance test link |The name of the DTS data synchronization task for the synchronization link between the primary instance and the disaster recovery instance. |
|DrDtsTaskStatus |String |Running |The state of the data synchronization link in the DTS data synchronization task between the primary instance and the disaster recovery instance. |
|MasterInstanceId |String |mysql\-ce48081d\*\*\*\* |The ID of the primary instance of the disaster recovery instance. |
|MasterInstanceName |String |Disaster recovery primary instance |The name of the primary instance of the disaster recovery instance. |
|DrSecondsBehindMaster |Integer |1 |The data synchronization latency between the primary instance and the disaster recovery instance. |
|EngineType |String |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>InnoDB</code>.</div><br> |
|NewNodeSpec |String | |General\-purpose instance specification. The new specification code is rds.mysql.d1.xxcxxg. |


<span id="maintenancewindowobject"></span>
### MaintenanceWindowObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DayKind |String |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeek |Array of String |["Monday","Tuesday"] |Specifies the day(s) of the week for the maintenance window. Valid values are `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, and `Sunday`. You can select more than one day. If this value is not specified or is empty, it defaults to all seven days of the week. |
|MaintenanceTime |String |22:00Z\-02:00Z |The maintenance window for the instance. Format: `HH:mmZ-HH:mmZ` (UTC time). |


<span id="tagobject"></span>
### TagObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |tagkey |The key of the instance tag. The rules for the tag key are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with any case form of `volc:`.<br><br>* The tag key must be 1 to 128 characters in length. |
|Value |String |tagvalue |The value of the instance tag. The rules for setting the tag value are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length, which means the tag value can be empty. |


<span id="chargedetailobject"></span>
### ChargeDetailObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AutoRenew |Boolean |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal. |
|ChargeEndTime |String |2025\-08\-22T15:59:59.000Z |Billing end time for the subscription instance (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is empty for pay\-as\-you\-go instances.</div><br> |
|ChargeStartTime |String |2025\-07\-22T13:10:15.000Z |The billing start time of the instance (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ChargeStatus |String |Normal |Billing state of the instance. Values:<br><br><br>* `Normal`: normal.<br><br>* `Overdue`: overdue.<br><br>* `Overdue`: waiting for payment. |
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|OverdueReclaimTime |String |2025\-08\-29T15:59:59.000Z |The estimated UTC release time after the instance is shut down due to overdue payments (pay\-as\-you\-go) or expiration (subscription). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|OverdueTime |String |2025\-08\-23T04:00:00.000Z |The time in UTC when the instance is shut down due to overdue payments (pay\-as\-you\-go) or expiration (subscription). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|Period |Integer |1 |Subscription duration in a prepaid scenario.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When this parameter is used as a request parameter, the default value is <code>1</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When PeriodUnit is<code> Year</code>, Period ranges from 1 to 3.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When PeriodUnit is <code>Month</code>, Period ranges from 1 to 9.</div><br> |
|PeriodUnit |String |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When this parameter is used as a request parameter, the default value is <code>Month</code>.</div><br> |
|TempModifyStartTime |String |2022\-01\-01T10:10:10.000Z |Start time of the temporary upgrade (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned for an instance that is not in a temporary upgrade period.</div><br> |
|TempModifyEndTime |String |2022\-01\-01T10:10:09.000Z |Restoration time of temporary upgrade (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned for an instance that is not in a temporary upgrade period.</div><br> |


<span id="endpointobject"></span>
### EndpointObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Addresses |Array of [AddressObject](https://docs.byteplus.com/en/docs/40/15520#addressobject) |Refer to the Sample response. |Address list. |
|AutoAddNewNodes |String |Enable |When the endpoint type is read/write or read\-only, setting whether the new node joins automatically is supported. Values:<br><br><br>* `Enable`: automatically join<br><br>* `Disable`: do not automatically join (default). |
|ConnectionInfoTags |Array of String |["Default"] |Connection endpoint tag. |
|ConnectionMode |String |Proxy |Connection endpoint type. Values:<br><br><br>* `Proxy`: proxy endpoint.<br><br>* `Direct`: direct endpoint.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the database proxy of the instance is enabled, the value can be <code>Proxy</code> or <code>Direct</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the database proxy of the instance is disabled, the value can only be <code>Direct</code>.</div><br><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the status of the database proxy of the instance.</div><br> |
|ConnectionPoolType |String |Direct |The connection pool type of the proxy endpoint. Values:<br><br><br>* `Transaction`: transaction\-level connection pool. Default value.<br><br>* `Direct`: direct connection mode. |
|Description |String |This is a description of the connection endpoint. |Description of the connection endpoint. |
|EnableReadOnly |String |Enable |Whether global read\-only is enabled. Valid values:<br><br><br>* `Enable`: enabled.<br><br>* `Disable`: disabled. |
|EnableReadWriteSplitting |String |Enable |Whether read/write separation is enabled, value:<br><br><br>* `Enable`: enabled.<br><br>* `Disable`: disabled. |
|EnableConnectionPersistent |Boolean |false |Whether to enable connection persistence. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|EndpointId |String |mysql\-050b3e08\*\*\*\* |Instance ID. |
|EndpointName |String |Customize connection endpoint |Instance endpoint name. |
|EndpointType |String |Custom |Endpoint type. The value is `Custom`, which indicates a customized endpoint. |
|IdleConnectionReclaim |Boolean |true |Indicates whether the Wait_timeout feature is enabled.<br><br><br>* `true`: enabled.<br><br>* `false`: disabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the proxy endpoint returns this field.</div><br> |
|ImplicitTransSplit |Boolean |false |Indicates whether to enable transaction splitting. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the proxy endpoint returns this field.</div><br> |
|MasterNodeRouting |Boolean |false |Specifies whether to enable primary node routing. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the proxy endpoint returns this field.</div><br> |
|MasterProtectorTimeout |Integer |60 |Overload protection timeout. Value range: an integer from 60 to 7,200, in seconds.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the proxy endpoint returns this field.</div><br> |
|MultiStatementsMode |String |Loose |The Multi\-Statements mode of the proxy endpoint. Values:<br><br><br>* `Strict`: strict mode. Default value.<br><br>* `Loose`: loose mode. |
|OverloadProtection |Boolean |false |Whether overload protection is enabled. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only the proxy endpoint returns this field.</div><br> |
|ReadOnlyNodeDistributionType |String |LoadSchedule |Read weight distribution mode. This parameter is required when read/write separation is set to `true`. As a request parameter for the CreateDBEndpoint and ModifyDBEndpoint APIs, the value range is as follows:<br><br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment.<br><br>   As a response parameter for the DescribeDBInstanceDetail API, the value range is as follows:<br><br>* `Default`: automatic assignment based on specification weights.<br><br>* `Custom`: custom weight assignment.<br><br>* `RoundRobin`: round robin scheduling.<br><br>* `LoadSchedule`: load scheduling.<br><br>* `RoundRobinCustom`: round robin scheduling with custom weights.<br><br>* `RoundRobinAuto`: round robin scheduling with automatic weight assignment. |
|ReadOnlyNodeMaxDelayTime |Integer |40 |The latency threshold for the read\-only node. The value can be an integer from 1 to 3,600. The default value is 30. The unit is seconds. |
|ReadOnlyNodeWeight |Array of [NodeWeightObject](https://docs.byteplus.com/en/docs/40/15520#nodeweightobject) |Refer to the Sample response. |Node list configured for the connection endpoint and corresponding read\-only weights. |
|ReadWriteMode |String |ReadOnly |Read/Write mode:<br><br><br>* `ReadWrite`: read/write.<br><br>* `ReadOnly`: read\-only. |


<span id="addressobject"></span>
### AddressObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DNSVisibility |Boolean |false |* `false`: BytePlus private network resolution (default).<br><br>* `true`: BytePlus private and public network resolution. |
|Domain |String |mysql1d797b6f\*\*\*\*.rds.ivolces.com |Connection domain name. |
|EipId |String |eip\-13g6t81tglmgw3n6nu4vt\*\*\*\* |ID of EIP, valid only for Public Address. |
|IPAddress |String |10. ** *.* ** .3 |IP address. |
|InternetProtocol |String |IPv4 |IP protocol version. Value is `IPv4`. |
|NetworkType |String |Private |Network address type, values are:<br><br><br>* `Private`: private network connection address.<br><br>* `Public`: public network connection address. |
|Port |String |3306 |Port. |
|SubnetId |String |subnet\-2bzr8zdx5o8ao2dx0efq4\*\*\*\* |Subnet ID, valid for private addresses only. |
|EipLocked |Boolean |false |Whether the EIP for the connection endpoint is shut down due to arrears. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |


<span id="nodeweightobject"></span>
### NodeWeightObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|NodeId |String |mysql\-050b3e08\*\*\*\*\-2 |Read\-only node requires passing in NodeId; primary node does not require it. |
|NodeType |String |Primary |Node type.<br><br><br>* `Primary`: primary node.<br><br>* `ReadOnly`: read\-only node. |
|Weight |Integer |100 |The read weight of the node, increasing by 100, with a maximum value of 10000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Weights cannot all be set to 0.</div><br> |


<span id="nodeobject"></span>
### NodeObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CreateTime |String |2024\-10\-29T08:45:28.000Z |The creation time of the node (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|DelayReplicationTime |Long |1000 |The replication delay for a read\-only node ranges from 0 to 604,800, and the unit is seconds. |
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|Memory |Integer |2 |Memory size. Unit is GiB. |
|NodeId |String |mysql\-h441603c\*\*\*\*\-01 |Node ID. |
|NodeSpec |String |rds.mysql.d1.n.2c4g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|NodeStatus |String |Running |Node status, with values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `Error`: error. |
|NodeType |String |Primary |Node type. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node. |
|RegionId |String |cn\-beijing |Region ID, use [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions) to query the available region list. Use this parameter to specify the region for creating the instance. |
|SyncDelay |Long |28 |The delay between the node and the primary node. The unit is milliseconds (ms). |
|UpdateTime |String |2024\-10\-31T08:45:28.000Z |The local update time of the node (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|VCPU |Integer |1 |CPU cores of the node. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |


<span id="proxyinfoobject"></span>
### ProxyInfoObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DBProxyStatus |String |Shutdown |The state of the database proxy for the instance. Values:<br><br><br>* `Creating`: proxy is enabling.<br><br>* `Running`: the database proxy is running.<br><br>* `Shutdown`: the database proxy is closed.<br><br>* `Deleting`: the database proxy is disabling. |
|ProxyResourceInfo |Object of [ProxyResourceInfo](https://docs.byteplus.com/en/docs/40/15520#proxyresourceinfo) |Refer to the Sample response. |Resource information of the database proxy service for the instance. |


<span id="proxyresourceinfo"></span>
### ProxyResourceInfo


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|CurrentProxyCpuNum |Integer |2 |The current number of cores for the database proxy service of the instance. |
|MaxProxyCpuNum |Integer |1024 |The maximum number of cores that can be configured for the database proxy service. |
|MinProxyCpuNum |Integer |2 |The minimum number of cores that can be configured for the database proxy service. |


<span id="disasterrecoveryinstance"></span>
### DisasterRecoveryInstance


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DtsTaskId |String |9c0c17a0b82f460b87b338d1db8d\*\*\*\* |The ID of the synchronization task between the primary instance and the disaster recovery instance. |
|DtsTaskName |String |TestTask |The name of the synchronization task between the primary instance and the disaster recovery instance. |
|DtsTaskStatus |String |Running |The state of the synchronization task between the primary and disaster recovery instances. |
|InstanceId |String |mysql\-6c7c35fb\*\*\*\* |The ID of the disaster recovery instance. |
|InstanceName |String |DrInstance\-test |Disaster recovery instance name |
|Region |String |cn\-shanghai |Region of the disaster recovery instance. |
|SecondsBehindMaster |Integer |0 |Latency between the disaster recovery instance and the primary instance. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-66347599****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024111814372900D9621B68C57432A544-ba24ec",
        "Action": "DescribeDBInstanceDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "BasicInfo": {
            "AllowListVersion": "v2",
            "BackupAuditLogSize": 0,
            "BackupBinLogSize": 397089974,
            "BackupChargeStatus": "Normal",
            "BackupDataSize": 99443762,
            "BackupErrorLogSize": 63567,
            "BackupFreeQuotaSize": 20,
            "BackupLogSize": 397321976,
            "BackupSlowLogSize": 168435,
            "BackupUse": 0.42,
            "BasicBackupBinlogSize": 390123374,
            "BasicBackupDataSize": 49721881,
            "CreateTime": "2024-10-29T08:45:27.000Z",
            "CurrentKernelVersion": "MySQL 5.7.32_20240615",
            "DBEngine": "Mysql",
            "DBEngineVersion": "MySQL_5_7",
            "DataSyncMode": "SemiSync",
            "InnerVersion": "",
            "InstanceId": "mysql-66347599****",
            "InstanceName": "测试实例",
            "InstanceStatus": "Running",
            "InstanceType": "DoubleNode",
            "IsLatestVersion": false,
            "LowerCaseTableNames": "1",
            "MaintenanceWindow": {
                "DayKind": "Week",
                "DayOfWeek": [
                    "Monday"
                ],
                "MaintenanceTime": "18:00Z-21:59Z"
            },
            "Memory": 1,
            "NodeNumber": "2",
            "NodeSpec": "rds.mysql.d1.n.1c1g",
            "PrimaryDBAccount": "",
            "ProjectName": "default",
            "RegionId": "cn-beijing",
            "ServerCollation": "",
            "ServiceArea": null,
            "ShardNumber": 0,
            "StorageAuditLogSize": 4096,
            "StorageBinLogSize": 29985723,
            "StorageDataSize": 4415339996,
            "StorageErrorLogSize": 53675,
            "StorageLogSize": 30131720,
            "StorageSlowLogSize": 88226,
            "StorageSpace": 20,
            "StorageType": "LocalSSD",
            "StorageUse": 4.3,
            "SubnetId": "subnet-rrot9xdj3j0gv0x57gv****",
            "TimeZone": "UTC +08:00",
            "UpdateTime": "",
            "VCPU": 1,
            "VpcId": "vpc-rrot7em3x05cv0x58dx****",
            "ZoneId": "cn-beijing-a"
        },
        "ChargeDetail": {
            "AutoRenew": false,
            "ChargeEndTime": "",
            "ChargeStartTime": "2024-10-29T08:45:31.000Z",
            "ChargeStatus": "Normal",
            "ChargeType": "PostPaid",
            "Number": 1,
            "OverdueReclaimTime": "2200-01-15T16:00:00.000Z",
            "OverdueTime": "",
            "Period": 1,
            "PeriodUnit": "Month"
        },
        "Endpoints": [
            {
                "Address": [
                    {
                        "DNSVisibility": false,
                        "Domain": "mysql66347599****.rds.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.6",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-rrot9xdj3j0gv0x57gv****"
                    }
                ],
                "Addresses": [
                    {
                        "DNSVisibility": false,
                        "Domain": "mysql66347599****.rds.ivolces.com",
                        "EipId": "",
                        "IPAddress": "192.***.***.6",
                        "IPv6Address": "",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "Port": "3306",
                        "SubnetId": "subnet-rrot9xdj3j0gv0x57gv****"
                    }
                ],
                "AutoAddNewNodes": "Enable",
                "ConnectionMode": "Proxy",
                "ConnectionPoolType": "Transaction",
                "Description": "",
                "EnableReadOnly": "Disable",
                "EnableReadWriteSplitting": "Disable",
                "EndpointId": "mysql-66347599****-cluster",
                "EndpointName": "",
                "EndpointProxyPort": "3679",
                "EndpointType": "Cluster",
                "IdleConnectionReclaim": false,
                "ReadOnlyNodeDistributionType": "Default",
                "ReadOnlyNodeMaxDelayTime": 30,
                "ReadOnlyNodeWeight": [
                    {
                        "NodeId": "",
                        "NodeType": "Primary",
                        "Weight": 100
                    }
                ],
                "ReadWriteMode": "ReadWrite"
            }
        ],
        "Nodes": [
            {
                "CreateTime": "2024-10-29T08:45:28.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-66347599****",
                "Memory": 1,
                "NodeId": "mysql-66347599****-m64c5-0",
                "NodeSpec": "rds.mysql.d1.n.1c1g",
                "NodeStatus": "Running",
                "NodeType": "Primary",
                "RegionId": "cn-beijing",
                "ShardId": "",
                "SubInstanceId": "mysql-66347599****-m64c5",
                "SyncDelay": 0,
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            },
            {
                "CreateTime": "2024-10-29T08:45:29.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-66347599****",
                "Memory": 1,
                "NodeId": "mysql-66347599****-s7fc0-0",
                "NodeSpec": "rds.mysql.d1.n.1c1g",
                "NodeStatus": "Running",
                "NodeType": "Secondary",
                "RegionId": "cn-beijing",
                "ShardId": "",
                "SubInstanceId": "mysql-66347599****-s7fc0",
                "SyncDelay": 137,
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-beijing-a"
            }
        ],
        "ProxyDetail": {
            "Charged": true,
            "DBProxyStatus": "Running",
            "ProxyResourceInfo": {
                "CurrentProxyCpuNum": 2,
                "MaxProxyCpuNum": 1024,
                "MinProxyCpuNum": 2
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

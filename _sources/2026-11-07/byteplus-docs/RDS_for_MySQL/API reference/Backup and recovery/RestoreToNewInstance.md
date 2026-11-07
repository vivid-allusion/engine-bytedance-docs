---
title: "RestoreToNewInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/restoretonewinstance"
---

Call the RestoreToNewInstance API to restore data to a new instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Restoring a single availability zone instance to a multiple availability zone instance, or a multiple availability zone instance to a single availability zone instance, is not supported.

* Cross\-major\-version instance restoration is not supported. For example: Restore a MySQL 5.7 instance to a MySQL 8.0 instance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestoreToNewInstance&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|SrcInstanceId |String |Yes |mysql\-603e30e6\*\*\*\* |ID of the source instance to which the backup file belongs. |
|BackupId |String |No |2b18d7e970c442caae05be478a9e\*\*\*\* |Backup file ID. You can query the BackupID by calling [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Either this parameter or the RestoreTime parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can select a backup set of a physical or logical backup to restore. When restoring from a logical backup, only the table structures and content of all non\-system databases in the backup can be restored to the new instance.</div><br> |
|RestoreTime |String |No |2022\-01\-01T10:10:10Z |Any point in time within the retention cycle of the original instance backup, in the `yyyy-MM-ddTHH:mm:ssZ format `(UTC time). You can call [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describerecoverabletime1) to check if restoration to this point in time is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You must specify either this parameter or the BackupId parameter.</div><br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/15435#nodeinfoobject) |Yes |See the request example. |The specifications of the instance. There is exactly 1 primary node, exactly 1 standby node, and 0 to 10 optional read\-only nodes. |
|StorageType |String |Yes |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: Local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br>* `CloudESSD_HighPerf`: high performance cloud disk.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When InstanceType is set to SingleNode, the StorageType can only be <code>CloudESSD_FlexPL</code>, <code>CloudESSD_PL0</code>, or <code>CloudESSD_HighPerf</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code>, the storage type cannot be changed.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">f the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code>, <code>CloudESSD_FlexPL</code>, or <code>CloudESSD_HighPerf</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|StorageSpace |Integer |No |100 |The storage space for the instance. Value range: [Size of the original instance's storage space, the maximum storage space for the new instance primary node specification]. The unit is GiB, with a step size of 10 GiB. The default value is the size of the source instance space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on the value range of storage space corresponding to each specification, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications">Product specifications</a>.</div><br> |
|VpcId |String |Yes |vpc\-2d70di2hrnbpc58ozfdx9\*\*\*\* |Virtual private cloud (VPC) ID. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Shared VPCs are not supported.</div><br> |
|SubnetId |String |Yes |subnet\-2d70dj20bob9c58ozfek6\*\*\*\* |Subnet ID. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) and specify the VpcId and ZoneId (the Availability zone of the primary node or secondary node) to query for available subnets. |
|Port |Integer |No |3306 |The private network address port for the default_endpoint. The value range of the port number is 1,000\-65,534, and the default value is 3,306.<br><br>When a new connection endpoint is created or a new address is enabled, the private network address port of the default_endpoint is configured as the default port in real time. |
|AllowListIds |Array of String |No |[<br><br>"acl\-a29be2559dc4406883d358892b90\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Allowlists ID. To associate multiple allowlists, separate the allowlist IDs with a comma (,). An instance can be associated with up to 100 allowlists.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you use the RestoreToNewInstance API to restore to a new instance, the allowlists of the original instance are not associated with the new instance by default. If needed, before calling this API, you can call <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1">DescribeAllowLists</a> to query the allowlists associated with the original instance and write them to this field. Alternatively, after restoring to the new instance, you can call <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/associateallowlist1">AssociateAllowList</a> to associate allowlists with the new instance.</div><br> |
|InstanceName |String |No |Name123 |Instance name. The naming rules for the instance name are as follows:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* Length must be between 1 and 128. |
|DBParamGroupId |String |No |mysql\-sys\-6013c7b8f7ef\*\*\*\* |Parameter templates ID. The default value is the default parameter template for the database engine version. |
|ProjectName |String |No |Test |Affiliated project. |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/40/15435#chargeinfoobject) |Yes |See the request example. |Payment method. |
|InstanceTags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/15435#tagobject) |No |[<br><br>{<br><br>"Key":"key1",<br><br>"Value":"value1"<br><br>},<br><br>{<br><br>"Key":"key2",<br><br>"Value":"value2"<br><br>}<br><br>] |Instance tag.<br><br><br>* Each MySQL instance can be associated with a maximum of 50 tags.<br><br>* You can add a maximum of 20 tags at a time. |
|AutoStorageScalingConfig |Object of [AutoStorageScalingConfig](https://docs.byteplus.com/en/docs/40/15435#autostoragescalingconfig) |No |See the request example. |Automatic scale\-out configuration. |
|DeletionProtection |String |No |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. Default value. |
|TableMeta |Array of [TableMeta](https://docs.byteplus.com/en/docs/40/15435#tablemeta) |No | |Specifies the databases and tables information to restore during databases and tables recovery.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specify this parameter only when restoring data from specified databases and tables.</div><br> |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/15435#proxynodecustom) |No |See the request example. |The proxy configuration of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This field is required when the original instance of the backup is a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This field does not take effect when the original instance of the backup is a double\-node instance.</div><br> |
|EnableExternalReplication |Boolean |No |false |Whether to enable native replication. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This setting applies only when InstanceType is set to <code>SingleNode</code>.</div><br> |
|PrivateIpAddress |String |No |192.168.xxx.xxx |The IP address of the default endpoint of the instance in the specified virtual private cloud and subnet.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is not set, an IP address within the specified virtual private cloud and subnet is automatically assigned to the default endpoint of the instance.</div><br> |
|AutoUpgradeMinorVersion |String |No |Auto |The upgrade policy for the kernel minor version of the instance. Values:<br><br><br>* `Auto`: automatic. When a new kernel minor version is released, the instance is automatically upgraded to the latest kernel version during the configured [Maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period?lang=en).<br><br>* `Manual`: manual. When a new kernel version is released, you need to manually upgrade to the latest kernel version in the console. For details, refer to [Manually upgrading the instance kernel version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version?lang=en).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If an instance's kernel minor version exceeds its maintenance cycle, the system temporarily ignores the upgrade policy and automatically upgrades the kernel minor version.</div><br> |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is optional for the DescribeDBInstancePriceDetail API.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add a node by calling the CreateDBNodes API, you can set this parameter only to <code>ReadOnly</code> for a double\-node instance or <code>Secondary</code> for a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A double\-node instance consists of one primary node, one secondary node, and 0 to 10 optional read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A multiple\-node instance consists of one primary node, and at least one and up to eight secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.</div><br> |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of the secondary node must be the same as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If StorageType is set to <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>, only the general type can be passed for NodeSpec.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nodes of an instance can be distributed across a maximum of three availability zones.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During a single configuration change, you can add or delete nodes in up to three availability zones.</div><br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: add.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding a node (CreateDBNodes), this field can only be <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the configuration, this parameter can only be set to <code>Modify</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This value has no actual meaning when set to <code>Delete</code>.</div><br> |


<span id="chargeinfoobject"></span>
### ChargeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|AutoRenew |Boolean |No |true |Specifies whether to enable Due Automatic renewal for prepaid instances. Range:<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.</div><br> |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios. Range:<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.</div><br> |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. The value range of this parameter depends on the value of PeriodUnit:<br><br><br>* When PeriodUnit is `Month`, Period ranges from 1 to 9.<br><br>* When PeriodUnit is `Year`, Period ranges from 1 to 3.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.</div><br> |
|Number |Integer |No |1 |The number of instances to purchase. Value range: 1~50. Default value: 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the RestoreToNewInstance and RestoreToCrossRegionInstance APIs, only a value of 1 is supported for this parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Specifying a name for each instance is not supported for batch creation. For batch instance creation:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you specify a name in the `InstanceName` parameter, a serial number is appended to the name for each instance.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you do not specify a name in the `InstanceName` parameter, the instance ID is used as the instance name.</div><br> |


<span id="tagobject"></span>
### TagObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |tagkey |The key of the instance tag. The rules for the tag key are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with any case form of `volc:`.<br><br>* The tag key must be 1 to 128 characters in length. |
|Value |String |No |tagvalue |The value of the instance tag. The rules for setting the tag value are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length, which means the tag value can be empty. |


<span id="autostoragescalingconfig"></span>
### AutoStorageScalingConfig


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|EnableStorageAutoScale |Boolean |Yes |true |Specifies whether to enable automatic expansion for the storage space. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When StorageConfig is used as a request parameter, if EnableStorageAutoScale is set to <code>false</code>, the StorageThreshold and StorageUpperBound parameters are optional.</div><br> |
|StorageThreshold |Integer |Yes |20 |The percentage of available storage space that triggers automatic scale\-out. The value range is 10 to 50, with a default value of 10. The unit is %. |
|StorageUpperBound |Integer |Yes |3000 |The upper limit of storage space for automatic scale\-out. The lower limit of this field is the `instance storage space + 20 GiB`, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specifications, in GiB. For more information about the range of storage space values that can be selected for different specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ScalingDetectNode |String |No |MasterNode |The range of nodes to check for automatic expansion. Values:<br><br><br>* `MasterNode`: primary node.<br><br>* `MasterSlaveNodes`: primary and secondary nodes.<br><br>* `AllNodes`: all nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>MasterNode</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a multiple\-node instance, setting this parameter to <code>MasterSlaveNodes</code> or <code>AllNodes</code> has the same effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single\-node instance, setting this parameter to <code>MasterNode</code>, <code>MasterSlaveNodes</code>, or <code>AllNodes</code> has the same effect.</div><br> |


<span id="tablemeta"></span>
### TableMeta


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|DBName |String |Yes |testdb1 |Specifies the database to restore. |
|NewDBName |String |No |testdb2 |Rename the database name. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reserved words, including root and admin. Refer to the [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords) for forbidden reserved words.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you only restore tables, this parameter can be the same as <code>DBName</code>.</div><br> |
|Table |Array of [Table](https://docs.byteplus.com/en/docs/40/15435#table) |No |[<br><br>{<br><br>"TableName" : "table1",<br><br>"NewTableName" : "table2"<br><br>}<br><br>] |Specifies the table to restore.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this value is empty, the entire database specified by the <code>DBName</code> parameter is restored.</div><br> |


<span id="table"></span>
### Table


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|TableName |String |Yes |table1 |Specifies the table to restore. |
|NewTableName |String |No |table2 |Rename the table name. Naming rules are as follows:<br><br><br>* The name must be unique.<br><br>* 2 to 64 characters in length.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* It cannot contain certain reserved words, including root and admin. Refer to the [List of forbidden keywords](https://apihub.bytedance.net/project/2544/branch/dev-1724929119/6313/66162) for forbidden reserved words. |


<span id="proxynodecustom"></span>
### ProxyNodeCustom


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Range:<br><br><br>* Maximum: 1,024.<br><br>* The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>* The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-e7fda57b\*\*\*\* |The Instance ID of the new instance after restoration. |
|OrderId |String |Order709899242175681\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RestoreToNewInstance&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "SrcInstanceId": "mysql-603e30e6****",
    "BackupId": "9671e15707ca44a1b9d8c8fc3e9f****",
    "NodeInfo": [
        {
            "NodeType": "Primary",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.mysql.1c2g"
        },
        {
            "NodeType": "Secondary",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.mysql.1c2g"
        }
    ],
    "StorageType": "LocalSSD",
    "SubnetId": "subnet-2gcy3ey5i9reo50ztyzo6****",
    "VpcId": "vpc-3jhamu8itr5ds3pncmf9q****",
    "AllowListIds": [
        "acl-3929ba6fd27049e88ee772dc7b46****"
    ],
    "Port": 3306,
    "InstanceName": "备份恢复样例",
    "ChargeInfo": {
        "ChargeType": "PostPaid"
    },
    "InstanceTags": [
        {
            "Key": "key1",
            "Value": "value1"
        },
        {
            "Key": "key2",
            "Value": "value2"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202305081052028E9DB7D3AD66FA6FFCE0",
        "Action": "RestoreToNewInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-cd8ae4ca****",
        "OrderId": "Order7230637470966354220"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

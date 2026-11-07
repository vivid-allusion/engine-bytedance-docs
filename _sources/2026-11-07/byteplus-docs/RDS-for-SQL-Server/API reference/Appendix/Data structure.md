---
title: "Data structure"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure"
---

This topic describes the data structures used in the RDS for SQL Server APIs.

<span id="addressobject"></span>
## AddressObject


|Name |Type |Sample |Description |
|---|---|---|---|
|DNSVisibility |Bool |false |Specifies whether to enable private\-to\-public network resolution. The valid values are as follows:<br><br><br>* `true`: Enables private\-to\-public network resolution.<br><br>* `false`: Disables private\-to\-public network resolution. |
|Domain |String |mssqldab1be87\*\*\*\*.rds\-mssql.ivolces.com |Connection domain. |
|EipId |String |eip\-5go6uulm687473inqk15\*\*\*\* |The ID of the EIP, which is only valid for public network addresses. |
|IPAddress |String |10.1.2.3 |IP address. |
|NetworkType |String |Private |Network address type. Possible values:<br><br><br>* `Private`: Private network type.<br><br>* `Public`: Public network type. |
|Port |String |1433 |Port. |
|SubnetId |String |subnet\-2bzup883l93402dx0efe1\*\*\*\* |The subnet ID, which is valid only for private network addresses. |


<span id="dpMbmtgp"></span>
## AllowListObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|AllowListCategory |String |Ordinary |The allowlist type. The valid values are as follows:<br><br><br>* `Ordinary`: Ordinary allowlist.<br><br>* `Default`: Default allowlist. |
|AllowListDesc |String |DTS internal white list |Remarks for the allowlist. |
|AllowListIPNum |Integer |1 |The total number of IP addresses (or address ranges) in the allowlist. |
|AllowListId |String |acl\-f0b3a98402144871ae22d3ef\*\*\*\*\*\* |The allowlist IDs. |
|AllowListName |String |dts_internal_for_EndpointVolcMSSQL |Allowlist name. |
|AllowListType |String |IPv4 |The type of IP address in the allowlist. Only the IPv4 address type is supported. |
|AssociatedInstanceNum |Integer |1 |The total number of instances bound to the allowlist. |
|ProjectName |String |default |Project name. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfoObject](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#securitygroupbindinfo) |```json```<br>```[```<br>```    {```<br>```        "BindMode":```<br>```        "IngressDirectionIp",```<br>```        "IpList": [```<br>```            "10.1.1.2/32",```<br>```            "10.1.1.1/32"```<br>```        ],```<br>```        "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******",```<br>```        "SecurityGroupName": "Default"```<br>```    }```<br>```]```<br> |A list of security groups associated with the allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the allowlist contains associated security groups.</div><br> |


<span id="dlWrOqbg"></span>
## AssociatedInstanceObject


|Name |Type |Sample |Description |
|---|---|---|---|
|InstanceId |String |mssql\-04a9110\*\*\*\*\* |The ID of the instance bound to the current allowlist. |
|InstanceName |String |mssql\-04a9110\*\*\*\*\* |The name of the instance associated with the current allowlist. |
|VPC |String |vpc\-b8pzuqn05yio28j06j\*\*\*\*\* |The ID of the VPC to which the instance belongs. |
|IsLatest |Bool |true |Whether to sync the latest allowlist IPs. |
|InstanceStatus |String |Running |The status of the instance. The valid values are:<br><br><br>* `Running`: Running.<br><br>* `Creating`: Creating.<br><br>* `Deleting`: Deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: changing.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Error`: Error. |
|ProjectName |String |default |The project to which the instance belongs. |


<span id="S67hABYd"></span>
## BackupDatabaseDetailObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|BackupType |String |Full |Backup type. The values are as follows:<br><br><br>* `Full`: Full backup.<br><br>* `Diff`: Differential backup. |
|BackupFileName |String |backup/mssql\-bbe31c86\*\*\*\*/D/1692648480\-master\-D\-06bf4b6a4313495c9debd28bf3ab\*\*\*\*.bak |Backup file name. |
|BackupFileSize |Long |1048576 |The size of the backup file in bytes. |
|BackupStartTime |String |2023\-08\-22T08:17:14.000Z |The start time of the backup. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC time). |
|BackupEndTime |String |2023\-08\-22T08:17:14.000Z |The end time of the backup. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC time). |
|DatabaseName |String |testname |Database name. |
|BackupDownloadLinkInner |String |https://\*\*\*\*\* |Private network download link.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before obtaining the private network download link, you need to call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloadbackup">DownloadBackup</a> API to get the full physical backup file.</div><br> |
|BackupDownloadLinkEIP |String |https://\*\*\*\*\* |Public download link for the backup.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before getting the public download link for the backup, you need to call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloadbackup">DownloadBackup</a> API to obtain the full physical backup file.</div><br> |
|LinkExpiredTime |String |2023\-05\-11T02:55:44.000Z |The expiration time of the download link, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC). |
|DownloadProgress |Integer |10 |The preparation progress of the backup file, in percent. |
|DownloadStatus |String |Success |Backup file preparation status. Values:<br><br><br>* `Success`: Preparation complete.<br><br>* `Failed`: Preparation failed.<br><br>* `Running`: Preparing.<br><br>* `NotDownload`: Not downloaded. |


<span id="backupmetaobject"></span>
## BackupMetaObject


|**Name** |**Type** |**Required** |**Sample** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |dbname |The database name of the backup. |


<span id="backupsinfoobject"></span>
## BackupsInfoObject


|Name |Type |Sample |Description |
|---|---|---|---|
|BackupEndTime |String |2023\-04\-17T18:48:00.000Z |The end time of the backup. The time is in UTC and follows the yyyy\-MM\-ddTHH:mm:sssZ format. |
|BackupFileSize |Long |5129555 |The size of the backup file in bytes. |
|BackupId |String |8d4ce0cbd1d643cc8287cedbf421\*\*\*\* |The backup ID. |
|BackupMethod |String |Physical |Backup method. The valid values are:<br><br><br>* `Logical`: Logical backup.<br><br>* `Physical`: Physical backup.<br><br>* `Snapshot`: Snapshot backup. |
|BackupStartTime |String |2023\-04\-17T18:48:00.000Z |The backup start time, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC time). |
|BackupStatus |String |Success |Status. The possible values are:<br><br><br>* `Success`: The backup is successful.<br><br>* `Failed`: The backup failed.<br><br>* `Running`: The backup is in progress. |
|BackupType |String |Full |Backup type. Value:<br><br><br>* `Full`: Full backup.<br><br>* `Diff`: Differential backup. |
|CreateType |String |System |The creation type. The value can be:<br><br><br>* `System`: System.<br><br>* `User`: User. |
|DownloadProgress |Integer |10 |The preparation progress of the backup file in `%`. |
|DownloadStatus |String |Success |The preparation status of the backup file. Values:<br><br><br>* `Success`: Preparation complete.<br><br>* `Failed`: Preparation failed.<br><br>* `Running`: Preparing.<br><br>* `NotDownload`: Not downloaded. |
|BackupDatabaseDetail |Array of BackupDatabaseDetailObject |[BackupDatabaseDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure?lang=en#S67hABYd) |Backup information.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned when you call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describebackupdetail">DescribeBackups</a> API to view the backup sets of an RDS for SQL Server instance.</div><br> |
|MaintenanceTime |String |22:00Z\-02:59Z |The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time). |


<span id="basicinfoobject"></span>
## BasicInfoObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|BackupUse |Folat |1.42 |The backup space used by the instance. Unit: GiB. |
|CreateTime |String |2023\-12\-26T02:32:36.000Z |The time when the instance was created. |
|DBEngineVersion |String |SQLServer_2019_Std |Compatible versions. The values are as follows:<br><br><br>* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.<br><br>* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.<br><br>* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition. |
|InnerVersion |String |15.0.4335.1 |Minor version information. |
|InstanceId |String |mssql\-dab1be87\*\*\*\* |Instance ID. |
|InstanceName |String |Instance example |The instance name. |
|InstanceStatus |String |Running |The status of the instance. The valid values are:<br><br><br>* `Running`: Running.<br><br>* `Creating`: Creating.<br><br>* `Deleting`: Deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: changing.<br><br>* `PrimaryChanging`: Primary node is switching.<br><br>* `Error`: Error. |
|InstanceType |String |HA |Instance type. The values are as follows:<br><br><br>* `HA`: Indicates the High Availability type.<br><br>* `Basic`: Indicates the single\-node edition type.<br><br>* `Cluster`: Cluster type.<br><br>* `ReadOnly`: A read\-only instance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code>, <code>InstanceType</code> can be <code>HA</code> or <code>Basic</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code>, <code>InstanceType</code> can be <code>Cluster</code>, <code>Basic</code>, or <code>ReadOnly</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code>, <code>InstanceType</code> can be <code>Basic</code>.</div><br> |
|Memory |Integer |16 |Memory size in GiB. |
|NodeSpec |String |rds.mssql.ee.ha.x8.4c32g |The primary node specification. |
|ProjectName |String |Test |Project. |
|RegionId |String |cn\-beijing |Region ID. |
|ServerCollation |String |Chinese_PRC_CS_AS |The default instance character set collation is `Chinese_PRC_CI_AS`. The supported character sets are as follows:<br><br><br>* `Latin1_General_CI_AS`<br><br>* `Latin1_General_CS_AS`<br><br>* `SQL_Latin1_General_CP1_CI_AS`<br><br>* `SQL_Latin1_General_CP1_CS_AS`<br><br>* `Chinese_PRC_CI_AS`<br><br>* `Chinese_PRC_CS_AS`<br><br>* `Chinese_PRC_BIN`<br><br>* `Japanese_CI_AS`<br><br>* `Japanese_CS_AS`<br><br>* `Chinese_Taiwan_Stroke_CI_AS`<br><br>* `Chinese_Taiwan_Stroke_CS_AS`<br><br>* `Thai_CI_AS` |
|SlowQueryEnable |String |false |Indicates whether the slow query log is enabled. The values are as follows:<br><br><br>* `true`: The slow query log is enabled.<br><br>* `false`: The slow query log is disabled. |
|SlowQueryTime |String |1 |The threshold for the slow query log. The value ranges from 1 to 10. Unit: seconds (s). |
|StorageSpace |Integer |200 |Total instance storage space. Unit: GiB. |
|StorageType |String |ESSDPL1 |The storage type of the instance. A value of `ESSDPL1` indicates Extreme Speed SSD PL1. |
|StorageUse |Float |1.85 |The storage space used by the instance. Unit: GiB. |
|SubnetId |String |subnet\-rroau2hdn1mov0x57f7\*\*\*\* |The subnet ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When two subnets are returned separated by a semicolon (;), the primary and secondary nodes are deployed in different availability zones. By default, the first is the primary node subnet, and the second is the standby node subnet.</div><br> |
|TimeZone |String |China Standard Time |Time zone. |
|UpdateTime |String |2024\-01\-03T07:15:08.000Z |The time when the instance was updated. |
|VCPU |Integer |4 |CPU size. For example, 1 indicates 1 core. |
|VpcId |String |vpc\-13g2qkkzntfy83n6nu4z1\*\*\*\* |Virtual private cloud (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |The availability zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When two availability zones are returned separated by a semicolon (;), the primary and secondary nodes are deployed in different availability zones. By default, the first is the primary node subnet, and the second is the secondary node subnet.</div><br> |
|ReadOnlyNumber |Integer |1 |The number of read\-only instances. |
|PrimaryInstanceId |String |mssql\-e75beddc\*\*\*\* |Master instance ID. |
|Tags |Array of TagsObject |{<br><br>"Key":"key", "Value":"value"<br><br>} |Instance tags. For more information, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#tagfilterobject). |


<span id="chargedetailobject"></span>
## ChargeDetailObject


|Name |Type |Sample |Description |
|---|---|---|---|
|AutoRenew |Bool |false |Specifies whether to enable auto\-renewal for prepaid instances.<br><br><br>* `true`: Auto\-renewal (Default).<br><br>* `false`: No auto\-renewal. |
|ChargeStartTime |String |2023\-02\-03T06:16:03.000Z |The billing start time in the yyyy\-MM\-ddTHH:mm:sssZ format (UTC). |
|ChargeEndTime |String |2023\-03\-02T15:59:59.000Z |The billing expiration time in yyyy\-MM\-ddTHH:mm:sssZ format (UTC). |
|ChargeStatus |String |Normal |Billing status. Possible values:<br><br><br>* `Normal`: the instance is normal.<br><br>* `Overdue`: The instance is overdue.<br><br>* `Unpaid`: The instance is awaiting payment. |
|ChargeType |String |PostPaid |Payment type. Possible values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription. |
|OverdueReclaimTime |String |2023\-03\-09T15:59:59.000Z |The estimated release time when suspended due to an overdue payment. The format is yyyy\-MM\-ddTHH:mm:sssZ (UTC time). |
|OverdueTime |String |2023\-03\-03T04:00:00.000Z |The time when the instance is suspended due to an overdue payment, in yyyy\-MM\-ddTHH:mm:sssZ format (UTC). |
|Period |Integer |1 |The subscription duration for prepaid instances. Default value: `1`. |
|PeriodUnit |String |Month |The billing cycle for prepaid instances.<br><br><br>* `Month`: Indicates a monthly subscription (default).<br><br>* `Year`: A yearly subscription. |


<span id="chargeinfoobject"></span>
## ChargeInfoObject


|Name |Type |Required |Sample |Description |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Possible values:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Subscription. |
|AutoRenew |Bool |No |true |Specifies whether to enable automatic renewal in a prepaid scenario. This parameter can be set when `ChargeType` is `Prepaid`.<br><br><br>* `true`: Enables automatic renewal (default value).<br><br>* `false`: Disables automatic renewal. |
|PeriodUnit |String |No |Month |The purchase period for prepaid plans. This parameter can be set when `ChargeType` is `Prepaid`.<br><br><br>* `Month`: A monthly subscription (default).<br><br>* `Year`: A yearly subscription. |
|Period |Integer |No |1 |The subscription duration for prepaid instances. This parameter is required when `ChargeType` is set to `Prepaid`. |
|Number |Integer |No |1 |The number of instances to purchase. Default value: `1` The value range is [1,10]. |


<span id="connectioninfo"></span>
## ConnectionInfo


|Name |Type |Sample |Description |
|---|---|---|---|
|Address |Array of AddressObject |[AddressObject](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#addressobject) |The address information. |
|Description |String |Null |The description. |
|EndpointId |String |mssql\-dab1be87\*\*\*\*\-primary |The endpoint ID. |
|EndpointName |String |Primary connection endpoint |The name of the endpoint. |
|EndpointType |String |Primary |Endpoint type. The values are as follows:<br><br><br>* `Primary`: The primary node endpoint.<br><br>* `ROCluster`: The read\-only cluster endpoint.<br><br>* `RO`: Read\-only node endpoint. |


<span id="databaseobject"></span>
## DatabaseObject


|**Name** |**Type** |**Required** |**Sample** |**Description** |
|---|---|---|---|---|
|DBName |String |Yes |test |Original database name. |
|NewDBName |String |No |test_bak |The new name for the database. Naming rules are as follows:<br><br><br>* Start with a letter and end with a letter or digit.<br><br>* The length must be between 2 and 60 characters.<br><br>* Consists of letters, numbers, and underscores (_), and is case\-insensitive.<br><br>* You can not use reserved words, such as `master`, `msdb`, `model`, `tempdb`, `resource`, `rdsadmin`, and `distribution`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When calling the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createtosrestore">CreateTosRestore</a> API to create a TOS backup recovery task, note the following information:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is not configured, the original database name is used by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When this parameter is set and <code>BackupType</code> is <code>Full</code>, the new database name cannot be the same as an existing database name. If <code>BackupType</code> is <code>Diff</code> or <code>LOG</code>, the new database name must already exist.</div><br> |


<span id="dbstatusobject"></span>
## DBStatusObject


|Name |Type |Sample |Description |
|---|---|---|---|
|DBName |String |AdventureWorks2016 |Database name. |
|Enable |Boolean |ture |The transparent data encryption status of the database. Possible values:<br><br>`true`: The database is encrypted.<br><br>`false`: The database is not encrypted. |


<span id="instancesinfoobject"></span>
## InstancesInfoObject


|Name |Type |Sample |Description |
|---|---|---|---|
|ChargeDetail |ChargeDetailObject |[ChargeDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#chargedetailobject) |The billing method. |
|CreateTime |String |2023\-04\-04T07:04:21.000Z |The time when the instance was created, in yyyy\-MM\-ddTHH:mm:ss.sZ format (UTC). |
|DBEngineVersion |String |SQLServer_2019_Std |Compatible versions. The values are as follows:<br><br><br>* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.<br><br>* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.<br><br>* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition. |
|InstanceId |String |mssql\-dab1be87\*\*\*\* |Instance ID. |
|InstanceName |String |Instance example |The instance name. |
|InstanceStatus |String |Running |The status of the instance. The valid values are:<br><br><br>* `Running`: Running.<br><br>* `Creating`: Creating.<br><br>* `Deleting`: Deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: changing.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Error`: Error. |
|InstanceType |String |HA |Instance type. The values are as follows:<br><br><br>* `HA`: Indicates the High Availability type.<br><br>* `Basic`: Indicates the single\-node edition type.<br><br>* `Cluster`: Cluster type.<br><br>* `ReadOnly`: A read\-only instance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code>, <code>InstanceType</code> can be <code>HA</code> or <code>Basic</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code>, <code>InstanceType</code> can be <code>Cluster</code>, <code>Basic</code>, or <code>ReadOnly</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code>, <code>InstanceType</code> can be <code>Basic</code>.</div><br> |
|NodeDetailInfo |Array of NodeDetailInfoObject |[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail?lang=zh#.6L-U5Zue56S65L6L) |Instance node information. |
|NodeSpec |String |rds.mssql.ee.ha.x8.4c32g |The primary node specification. |
|Port |String |1433 |The instance's private network port. |
|ProjectName |String |Test |Project. |
|RegionId |String |cn\-beijing |The region ID. You can call [DescribeRegions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeRegions) to query for available regions. This parameter specifies the region where the instance is created. |
|ServerCollation |String |Chinese_PRC_CS_AS |The default instance character set collation is `Chinese_PRC_CI_AS`. The supported character sets are as follows:<br><br><br>* `Latin1_General_CI_AS`<br><br>* `Latin1_General_CS_AS`<br><br>* `SQL_Latin1_General_CP1_CI_AS`<br><br>* `SQL_Latin1_General_CP1_CS_AS`<br><br>* `Chinese_PRC_CI_AS`<br><br>* `Chinese_PRC_CS_AS`<br><br>* `Chinese_PRC_BIN`<br><br>* `Japanese_CI_AS`<br><br>* `Japanese_CS_AS`<br><br>* `Chinese_Taiwan_Stroke_CI_AS`<br><br>* `Chinese_Taiwan_Stroke_CS_AS`<br><br>* `Thai_CI_AS` |
|StorageSpace |Integer |200 |Total instance storage space. Unit: GiB. |
|StorageType |String |ESSDPL1 |The storage type of the instance. The value is `ESSDPL1`. |
|SubnetId |String |subnet\-2bzup883l93402dx0efe1\*\*\*\* |The subnet ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When two subnets are returned separated by a semicolon (;), the primary and secondary nodes are deployed in different availability zones. By default, the first is the primary node subnet, and the second is the standby node subnet.</div><br> |
|TimeZone |String |China Standard Time |Time zone. |
|VpcId |String |vpc\-2d5xeur6hiscg58ozfcuq\*\*\*\* |Virtual private cloud (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |The availability zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When two availability zones are returned separated by a semicolon (;), the primary and secondary nodes are deployed in different availability zones. By default, the first is the primary node subnet, and the second is the secondary node subnet.</div><br> |
|InstanceCategory |String |Primary |The instance type. Valid values are as follows:<br><br><br>* `Primary`: The primary instance.<br><br>* `ReadOnly`: Read only instance. |
|ReadOnlyNumber |Integer |1 |The number of read\-only instances. |
|PrimaryInstanceId |String |mssql\-e75beddc\*\*\*\* |Master instance ID. |
|Tags |Array of TagsObject |{<br><br>"Key":"key", "Value":"value"<br><br>} |Instance tags. For more information, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#tagfilterobject). |
|MaintenanceTime |String |22:00Z\-02:59Z |The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time). |


<span id="instancespecobject"></span>
## InstanceSpecObject


|Name |Type |Sample |Description |
|---|---|---|---|
|DBEngineVersion |String |SQLServer_2019_Std |Compatible versions. The values are as follows:<br><br><br>* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.<br><br>* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.<br><br>* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition. |
|Generation |String |Generation1 |The instance specification generation. The following values are available:<br><br><br>* `Generation1`: Type I.<br><br>* `Generation2`: Type II.<br><br>* `Generation3`: Type III. |
|InstanceType |String |HA |Instance type. The values are as follows:<br><br><br>* `HA`: Indicates the High Availability type.<br><br>* `Basic`: Indicates the single\-node edition type.<br><br>* `Cluster`: Cluster type.<br><br>* `ReadOnly`: A read\-only instance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code>, <code>InstanceType</code> can be <code>HA</code> or <code>Basic</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code>, <code>InstanceType</code> can be <code>Cluster</code>, <code>Basic</code>, or <code>ReadOnly</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code>, <code>InstanceType</code> can be <code>Basic</code>.</div><br> |
|Memory |Integer |16 |Memory size in GiB. |
|SpecCode |String |rds.mssql.ee.std.d2.2c4g |Instance specification code. |
|SpecFamily |String |Exclusive |The instance specification family. The following values are available:<br><br><br>* `Exclusive`: Exclusive Type.<br><br>* `General`: General Type. |
|SpecSaleType |String |SPLA |The instance specification type. A value of `SPLA` indicates a normal specification. |
|SpecStatus |String |Normal |The status of the specification in the availability zone. The possible values are as follows:<br><br><br>* `Normal`: The specification is available for purchase.<br><br>* `Unsupported`: The specification is not supported in the availability zone and is not for sale.<br><br>* `Sold out`: Indicates that the item is sold out. |
|VCPU |Integer |16 |CPU size. For example, 1 indicates 1 core. |
|ZoneId |String |cn\-beijing\-a |The availability zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When two availability zones are returned separated by a semicolon (;), the primary and secondary nodes are deployed in different availability zones. By default, the first is the primary node subnet, and the second is the secondary node subnet.</div><br> |


<span id="instanceparametersobject"></span>
## InstanceParametersObject


|Name |Type |Sample |Description |
|---|---|---|---|
|CheckingCode |String |[10\-3000] |Parameter value range. |
|ForceModify |Bool |false |Indicates whether the running value of the parameter can be modified.<br><br><br>* `true`: The running value of the parameter can be modified.<br><br>* `false`: The running value of the parameter cannot be modified. |
|ForceRestart |Bool |false |Indicates whether the instance must be restarted for the modified parameter to take effect.<br><br><br>* `true`: Indicates that the instance must be restarted for the modified parameter to take effect.<br><br>* `false`: Indicates that the instance does not need to be restarted. |
|ParameterDefaultValue |String |1 |The default value for the parameter in the parameter template used by the instance. |
|ParameterDescription |String |Database Mail XPs option. The Database Mail XPs option enables database mail on this server. |Parameter description. |
|ParameterName |String |automatic soft\-NUMA disabled |Parameter name. |
|ParameterType |String |Integer |The parameter type. The value can be:<br><br><br>* `String`<br><br>* `Integer`<br><br>* `Boolean`<br><br>* `List`<br><br>* `Float` |
|ParameterValue |String |1 |Indicates the value of the parameter. |


<span id="nodedetailinfoobject"></span>
## NodeDetailInfoObject


|Name |Type |Sample |Description |
|---|---|---|---|
|CreateTime |String |2024\-01\-02T11:17:33.000Z |The creation time of the node. |
|InstanceId |String |mssql\-93420fe2\*\*\*\* |Instance ID. |
|Memory |Integer |8 |Memory size in GiB. |
|NodeId |String |mssql\-dab1be87\*\*\*\*\-0 |Node ID |
|NodeSpec |String |rds.mssql.se.ha.d4.4c16g |Node specification. |
|NodeStatus |String |Running |The status of the node. Possible values are:<br><br><br>* `Running`: Running.<br><br>* `Creating`: Creating.<br><br>* `Deleting`: Deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: changing.<br><br>* `MasterChanging`: primary node switching.<br><br>* `Error`: Error. |
|NodeType |String |Primary |Node type. Possible values:<br><br><br>* `Primary`: The primary node endpoint.<br><br>* `ReadOnly`: The read only node endpoint.<br><br>* `Secondary`: The secondary node endpoint. |
|RegionId |String |cn\-beijing |Region ID. |
|UpdateTime |String |2024\-01\-03T09:34:55.000Z |The update time of the node. |
|VCPU |Integer |4 |CPU size. For example, 1 indicates 1 core. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|NodeIP |String |192.168.\*\*\*.\*\*\* |Node IP. |


<span id="regionobject"></span>
## RegionObject


|Name |Type |Sample |Description |
|---|---|---|---|
|RegionId |String |cn\-beijing |Region ID. |
|RegionName |String |cn\-beijing |Region name. |


<span id="restoretaskdetailobject"></span>
## RestoreTaskDetailObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RestoreFileName |String |copyonly_log.bak |Restore file name. |
|RestoreFileSize |String |202394112 |Size of the restored file in bytes. |
|RestoreStartTime |String |2023\-05\-11T02:55:38.000Z |The recovery start time in yyyy\-MM\-ddTHH:mm:sssZ (UTC) format. |
|RestoreEndTime |String |2023\-05\-11T02:55:44.000Z |Recovery end time. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC time). |
|BackupType |String |Full |Recovery type. The values are as follows:<br><br><br>* `Full`: Full recovery.<br><br>* `Diff`: Differential recovery.<br><br>* `Log`: Log recovery.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>BackupType</code> parameter is set to <code>Full</code> and <code>DBName</code> is not set, it is a Default recovery.</div><br> |
|DBName |String |testdb |Database name. |
|NewDBName |String |newtestdb |The new database name after modification. |
|RestoreDesc |String |Restoration successful |Recovery details. |


<span id="restoretaskobject"></span>
## RestoreTaskObject


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|RestoreTaskId |String |90 |Restore task ID. |
|InstanceId |String |mssql\-bbe31c86\*\*\*\* |Instance ID. |
|InstanceName |String |testname |The instance name. |
|TaskStartTime |String |2023\-08\-22T09:51:00.000Z |Task start time. Format: yyyy\-MM\-ddTHH:mm:sssZ (UTC). |
|TaskEndTime |String |2023\-08\-22T09:50:45.000Z |The end time of the task. The format is yyyy\-MM\-ddTHH:mm:sssZ (UTC time). |
|TaskStatus |String |Failed |Task status. The possible values are as follows:<br><br><br>* `NoStart`: Indicates that the task is not started.<br><br>* `Running`: The task is running.<br><br>* `Success`: The task was successful.<br><br>* `Failed`: The task failed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For failed restore tasks, some databases may have been successfully restored. You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describetosrestoretaskdetail">DescribeTosRestoreTaskDetail</a> interface for more details.</div><br> |
|TaskType |String |OpenDB |Task type. The possible values are:<br><br><br>* `OpenDB`: Open the database.<br><br>* `NotOpenDB`: Do not open the database. |
|IsReplace |Boolean |false |A value of `false` indicates that existing databases on the target instance are not overwritten during the restore. |
|RestoreType |String |Full |Recovery type. The values are as follows:<br><br><br>* `Full`: Indicates full recovery.<br><br>* `Diff`: Differential recovery.<br><br>* `LOG`: Indicates log recovery. |
|TaskDesc |String |Restore file verification failed. |Task backup description. |


<span id="securitygroupbindinfo"></span>
## SecurityGroupBindInfo


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|BindMode |String |IngressDirectionIp |Security group association mode. The valid values are:<br><br><br>* `IngressDirectionIp`: Ingress IP. Allows database access from IP addresses specified as source addresses in the security group's ingress rules for TCP and ALL protocols. Security groups configured as source addresses are ignored.<br><br>* `AssociateEcsIp`: Associate ECS IP. Allows the ECS within the security group to access the database. Currently, only the IP information import of the main network interface card is supported.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required in the request.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information about security group association mode, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist">Create an allowlist</a>.</div><br> |
|IpList |Array of string |```json```<br>```[```<br>```    "10.1.1.2/32",```<br>```    "10.1.1.1/32"```<br>```]```<br> |List of IPs in the associated security group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is optional.</div><br> |
|SecurityGroupId |String |sg\-30up5lo07p7nk7r2qr0\*\*\*\*\*\* |Associated security group ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required in the request.</div><br> |
|SecurityGroupName |String |Default |Associated security group name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is optional.</div><br> |


<span id="tagfilterobject"></span>
## TagFilterObject


|Name |Type |Required |Sample |Description |
|---|---|---|---|---|
|Key |String |Yes |abc |The tag key for the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The number of tags in a single query can not exceed 10. An AND relationship is applied when multiple keys are passed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Duplicate tag keys are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Tag keys cannot be empty.</div><br> |
|Values |Array of String |No |["1", "2", "8"] |When multiple tag values are passed in for an instance tag, they shall be separated by English commas (,) with the values in an OR logical relationship.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is specified, the key must be specified first.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is not specified, all tag values for the same tag key are queried.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for tags with an empty tag value.</div><br> |


<span id="tagsobject"></span>
## TagsObject


|**Parameter** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|Key |String |Yes |Tag key information. The configuration specifications are as follows:<br><br><br>* Supports characters in any language, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>* Case\-sensitive, and the length is 1 \- 128 characters.<br><br>* Use the Unicode format encoded with UTF\-8.<br><br>* Keys starting with `volc:` in any format, such as `Volc:` or `VOLC:`, are not supported.<br><br>* You can set up to 20 at a time, without duplicates. |key1 |
|Value |String |No |The value of the tag. The configuration specifications are as follows:<br><br><br>* Supports characters in any language, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>* Case\-sensitive, with a length of 0 to 256 characters.<br><br>* Use the Unicode format encoded with UTF\-8. |value1 |


<span id="zonesobject"></span>
## ZonesObject


|Name |Type |Sample |Description |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |
|ZoneName |String |cn\-beijing\-a |Availability zone name. |
|Description |String |China North 2 (Beijing) \- Availability Zone A |The name of the region and availability zone. |

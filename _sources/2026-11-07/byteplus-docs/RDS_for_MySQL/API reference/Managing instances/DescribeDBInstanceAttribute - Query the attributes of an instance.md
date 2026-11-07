---
title: "DescribeDBInstanceAttribute - Query the attributes of an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceAttribute"
---

Call the DescribeDBInstanceAttribute API to query the attributes of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceAttribute&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DBInstanceAttribute |Object of [DBInstanceAttribute](https://docs.byteplus.com/en/docs/40/61045#dbinstanceattribute) |Refer to the Sample response. |Instance attributes. |


<span id="dbinstanceattribute"></span>
### DBInstanceAttribute


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AllowListVersion |String |v2 |Instance allowlist version. |
|AutoUpgradeMinorVersion |String |Auto |The upgrade policy for the kernel minor version of the instance. Values:<br><br><br>* `Auto`: automatic.<br><br>* `Manual`: manual. |
|CreateTime |String |2025\-07\-23T03:40:54.000Z |Instance creation time (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|CurrentKernelVersion |String |MySQL 5.7.32_20250615 |The current kernel minor version of the instance. |
|DBEngineVersion |String |MySQL_5_7 |Instance compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|DeletionProtection |String |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. |
|HasDisasterRecoveryInstances |Boolean |false |Whether the instance has a disaster recovery instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|HasGreenInstance |Boolean |false |Whether the instance is in a blue\-green deployment. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |
|InstanceId |String |mysql\-f83edc2e\*\*\*\* |Instance ID. |
|InstanceName |String |Test instance |Instance name. |
|InstanceStatus |String |Running |Instance status. Values:<br><br><br>* `Creating`: creating.<br><br>* `Running`: running.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: modifying.<br><br>* `Restoring`: recovering.<br><br>* `Error`: error.<br><br>* `Upgrading`: upgrading.<br><br>* `Released`: recycling.<br><br>* `Recycled`: recycled.<br><br>* `MasterChanging`: primary node switching.<br><br>* `TDEUpdating`: TDE modifying.<br><br>* `Closed`: shut down.<br><br>* `Maintaining`: maintaining.<br><br>* `CreateFailed`: failed to create.<br><br>* `Closing`: Shutting down.<br><br>* `SSLUpdating`: SSL modifying.<br><br>* `AllowListMaintaining`: Allowlist modifying.<br><br>* `Unknown`: Unknown.<br><br>* `ProxyCreating`: Proxy is enabling.<br><br>* `ProxyDeleting`: Proxy is disabling.<br><br>* `ChargeTypeChanging`: billing method changing.<br><br>* `NetWorkChanging`: Network changing. |
|InstanceType |String |DoubleNode |Instance type. Values:<br><br><br>* `DoubleNode`, Double node type.<br><br>* `MultiNode`, multiple node type. |
|LowerCaseTableNames |String |false |Specifies whether table names are case sensitive. Values:<br><br><br>* `false`: table names are stored in their original case and are case\-sensitive.<br><br>* `true`: table names are stored in lowercase and are not case\-sensitive. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/40/61045#maintenancewindowobject) |Refer to the Sample response. |The maintenance window for the instance. |
|Memory |Integer |2 |The memory size of the instance. The unit is GiB. |
|NodeNumber |String |2 |Number of nodes. |
|NodeSpec |String |rds.mysql.d1.n.1c1g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ProjectName |String |default |The project to which the instance belongs. |
|RegionId |String |cn\-beijing |The region ID of the instance. |
|StorageSpace |Long |200 |The storage space for the instance. The unit is GiB. |
|StorageType |String |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br>* `CloudESSD_HighPerf`: high performance cloud disk. |
|SubnetId |String |subnet\-11wfw1cvzttds40yrhcx1\*\*\*\* |The ID of the subnet that the instance uses. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/61045#tagobject) |[<br><br>{<br><br>"Key": "Key1",<br><br>"Value": "Value1"<br><br>},<br><br>{<br><br>"Key": "Key2",<br><br>"Value": "Value2"<br><br>}<br><br>] |Instance tag. |
|TimeZone |String |UTC +08:00 |The time zone of the instance. |
|UpdateTime |String |2025\-07\-24T13:40:54.000Z |The local time when the instance is updated. |
|VCPU |Integer |1 |CPU cores of the instance. |
|VpcId |String |vpc\-3ezxu117lv18g72200rro\*\*\*\* |The ID of the instance's virtual private cloud. |
|ZoneId |String |cn\-guangzhou\-a |The ID of the availability zone where the primary instance node resides. |
|EngineType |String |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>InnoDB</code>.</div><br> |


<span id="maintenancewindowobject"></span>
### MaintenanceWindowObject


|Parameter |Type |Example |Description |
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


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceAttribute&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "202507241406442EEEFDBA9025ACFAD59A-fdf98c",
        "Action": "DescribeDBInstanceAttribute",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "DBInstanceAttribute": {
            "AllowListVersion": "v2",
            "AutoUpgradeMinorVersion": "Auto",
            "CreateTime": "2025-07-23T03:40:54.000Z",
            "CurrentKernelVersion": "MySQL 5.7.32_20250615",
            "DBEngineVersion": "MySQL_5_7",
            "DeletionProtection": "Enabled",
            "HasDisasterRecoveryInstances": false,
            "HasGreenInstance": true,
            "InstanceId": "mysql-f83edc2e****",
            "InstanceName": "测试实例",
            "InstanceStatus": "Updating",
            "InstanceType": "DoubleNode",
            "LowerCaseTableNames": "1",
            "MaintenanceWindow": {
                "DayKind": "Week",
                "DayOfWeek": [
                    "Monday",
                    "Tuesday",
                    "Wednesday",
                    "Thursday",
                    "Friday",
                    "Saturday",
                    "Sunday"
                ],
                "MaintenanceTime": "18:00Z-21:59Z"
            },
            "Memory": 1,
            "NodeNumber": "4",
            "NodeSpec": "rds.mysql.d1.n.1c1g",
            "ProjectName": "default",
            "RegionId": "cn-guangzhou",
            "StorageSpace": 100,
            "StorageType": "LocalSSD",
            "SubnetId": "subnet-3rf442t6a54w016nf3pg9****",
            "Tags": [
                {
                    "Key": "Key1",
                    "Value": "Value1"
                },
                {
                    "Key": "Key2",
                    "Value": "Value2"
                }
            ],
            "TimeZone": "UTC +08:00",
            "UpdateTime": "",
            "VCPU": 1,
            "VpcId": "vpc-3ezxu117lv18g72200rro****",
            "ZoneId": "cn-guangzhou-a"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

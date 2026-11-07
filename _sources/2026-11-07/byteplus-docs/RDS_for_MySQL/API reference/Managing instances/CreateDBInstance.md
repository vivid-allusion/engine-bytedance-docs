---
title: "CreateDBInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbinstance1"
---

## Request type

Asynchronous request.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|DBEngineVersion |String |Yes |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|InstanceType |String |No |DoubleNode |Instance type for the green instance. Values:<br><br><br>* `DoubleNode`, Double node type.<br><br>* `MultiNode`, multiple node type.<br><br>* `SingleNode`, Single node type.<br><br><br>> **tip**<br><br><br><br>* > If the blue instance is a single\-node type, you can select a single\-node or double\-node type for the green instance.<br><br><br>* > If the blue instance is a double\-node type, you can select a double\-node or multiple\-node type for the green instance.<br><br><br>* > If the blue instance is a multiple\-node type, you can only select the multiple\-node type for the green instance.<br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/15528#nodeinfoobject) |Yes |[<br><br>    {<br><br>        "NodeType": "Primary",<br><br>        "ZoneId": "cn\-beijing\-a",<br><br>        "NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "Secondary",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"ZoneId": "cn\-beijing\-a",<br><br>"NodeSpec": "rds.mysql.1c2g"<br><br>}<br><br>] |Node configuration of the instance. |
|StorageType |String |Yes |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br>* `CloudESSD_HighPerf`: high performance cloud disk.<br><br><br>> **tip**<br><br><br><br>* > The StorageType parameter is required if you set the StorageSpace parameter.<br><br><br>* > When InstanceType is set to SingleNode, the StorageType can only be `CloudESSD_FlexPL`, `CloudESSD_PL0`, or `CloudESSD_HighPerf`.<br><br><br>* > This parameter has different value ranges for different APIs. The rules are as follows:<br><br><br>   * > When used as a request parameter in the following APIs, StorageType can only be `LocalSSD`.<br><br><br>      * > RestoreToCrossRegionInstance<br><br><br>      * > RestoreToNewInstanceFromUserTos<br><br><br>* > When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:<br><br><br>   * > If the original instance storage type is `LocalSSD`, the storage type cannot be changed.<br><br><br>   * > f the original instance storage type is `CloudESSD_PL0`, the value can be `CloudESSD_PL0`, `CloudESSD_FlexPL`, or `CloudESSD_HighPerf`.<br><br><br>      > The related APIs are:<br>      <br><br>      * > RebuildDBInstance<br><br><br>      * > RestoreToNewInstance<br><br><br>      * > ModifyDBNodeSpec<br> |
|StorageSpace |Integer |Yes |100 |Different storage types and specifications have different storage space value ranges. For detailed information on storage space value ranges, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). The unit is GiB, and the step size is 10 GiB. |
|VpcId |String |Yes |vpc\-2d70di2hrnbpc58ozfdx9\*\*\*\* |Virtual private cloud (VPC) ID. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query.<br><br>> **tip**<br><br><br>> Shared VPCs are not supported.<br> |
|SubnetId |String |Yes |subnet\-2d70dj20bob9c58ozfek6\*\*\*\* |Subnet ID. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) and specify the VpcId and ZoneId (the Availability zone of the primary node or secondary node) to query for available subnets. |
|InstanceName |String |No |Name123 |Instance name. The naming rules for the instance name are as follows:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* The length must be 1 to 128 characters.<br><br><br>> **tip**<br><br><br><br>* > If left blank, the instance ID will be used as the instance name by default.<br><br><br>* > You can create up to 50 RDS for MySQL instances in a batch. For batch creation,<br><br><br>   * > If you do not enter the instance name, all instances created in a batch will use their instance IDs as their instance names.<br><br><br>   * > If you enter the instance name, a sequence number will be automatically added after the instance name. If you specify the instance name as "test_instance", create three in a batch, and the names of these three instances will be "test_instance\-1", "test_instance\-2", and "test_instance\-3" respectively.<br><br><br>   * > Support for specifying ordered instance names for instances using a specific syntax, which is `name_prefix [begin_number, bits] name_suffix`. If you specify the instance name as "NamePrefix_[0,2]Name_Suffix", create 3 in batches, and the names of these 3 instances will be "Name_Prefix00Name_Suffix", "Name_Prefix01Name_Suffix" and "Name_Prefix02Name_Suffix" respectively. For more details, see [Rules for setting ordered instance names](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Batch_setting_ordered_instance_names).<br> |
|SuperAccountName |String |No |Test1 |Super account name. If this parameter is not specified, a super account will not be created. The naming rules for the super account name are as follows:<br><br><br>* The account name must be 2 to 32 characters long.<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* It consists of letters, digits, underscores (_), or hyphens (\-).<br><br>* The name can not contain certain reserved words and forbidden keywords. For all forbidden keywords, refer to [List of forbidden keywords](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_forbidden_keywords).<br><br>* The account name must be unique within the instance. |
|SuperAccountPassword |String |No |Test@123456 |Password for the super account. The password must meet the following requirements:<br><br><br>* The length is 8~32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* Special characters are `!#$%&()*+,-.=?@^_\|/`. |
|LowerCaseTableNames |String |No |1 |Specifies whether table names are case sensitive. The default value is 1. The backend ignores case. Value range:<br><br><br>* `0`: table names are stored in their original case and are case\-sensitive.<br><br>* `1`: Table names are stored in lowercase and are not case\-sensitive. |
|DBTimeZone |String |No |UTC +08:00 |Time zone. Supports UTC\-12:00 to +13:00. The default value is the time zone of the Region. |
|DBParamGroupId |String |No |mysql\-sys\-6013c7b8f7ef\*\*\*\* |Parameter templates ID. The default value is the default parameter template for the database engine version. |
|ProjectName |String |No |Test |The project to which the instance belongs. If you need to specify a project when it is created, you must ensure that the project already exists. You can query the project list by calling the ListProjects API, or create a new project by calling the CreateProject API. |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/40/15528#chargeinfoobject) |Yes |{<br><br>"ChargeType": "PostPaid"<br><br>} |Payment method. |
|AllowListIds |Array of String |No |[<br><br>"acl\-a29be2559dc4406883d358892b90\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Allowlists ID. To associate multiple allowlists, separate the allowlist IDs with a comma (,). An instance can be associated with up to 100 allowlists. |
|Port |Integer |No |3306 |The private network address port for the default_endpoint. The value range of the port number is 1,000\-65,534, and the default value is 3,306. When you create a new connection endpoint or enable a new address, the private network address port of the default endpoint is configured as the default port. |
|InstanceTags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/15528#tagobject) |No |[{"Key":"key", "Value":"value"}] |Instance tag.<br><br><br>* Each MySQL instance can be associated with a maximum of 50 tags.<br><br>* You can add a maximum of 20 tags at a time. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/40/15528#maintenancewindowobject) |No |{<br><br>"DayKind": "Week",<br><br>"DayOfWeek": [ ,<br><br>"Monday",<br><br>"Tuesday",<br><br>"Wednesday",<br><br>"Thursday",<br><br>"Friday",<br><br>"Saturday",<br><br>"Sunday"<br><br>]<br><br>"MaintenanceTime": "18:00Z\-21:59Z"<br><br>} |Specifies the maintenance window for the instance during instance creation. This field is optional. If not specified, it defaults to 18:00Z\-21:59Z UTC (02:00\-05:59 Beijing time) every day of the week. |
|DeletionProtection |String |No |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. Default value. |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/15528#proxynodecustom) |No |See the request example. |The proxy configuration of the instance.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when InstanceType is set to `MultiNode`.<br><br><br>* > This parameter does not take effect when InstanceType is set to `DoubleNode` or `SingleNode`.<br> |
|EnableExternalReplication |Boolean |No |false |Whether to enable native replication. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br>> **tip**<br><br><br>> This configuration is valid only when InstanceType is set to `SingleNode`.<br> |
|EngineType |String |No |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br>> **tip**<br><br><br>> When used as a request parameter, the default value is `InnoDB`.<br> |
|PrivateIpAddress |String |No |192.168.xxx.xxx |The IP address of the default endpoint of the instance in the specified virtual private cloud and subnet.<br><br>> **tip**<br><br><br>> If this parameter is not set, an IP address within the specified virtual private cloud and subnet is automatically assigned to the default endpoint of the instance.<br> |
|AutoStorageScalingConfig |Object of [AutoStorageScalingConfig](https://docs.byteplus.com/en/docs/40/15528#autostoragescalingconfig) |No |See the request example. |Automatic scale\-out configuration. |
|AutoUpgradeMinorVersion |String |No |Auto |The upgrade policy for the kernel minor version of the instance. Values:<br><br><br>* `Auto`: automatic. When a new kernel minor version is released, the instance is automatically upgraded to the latest kernel version during the configured [Maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period?lang=en).<br><br>* `Manual`: manual. When a new kernel version is released, you need to manually upgrade to the latest kernel version in the console. For details, refer to [Manually upgrading the instance kernel version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version?lang=en).<br><br><br>> **tip**<br><br><br>> If an instance's kernel minor version exceeds its maintenance cycle, the system temporarily ignores the upgrade policy and automatically upgrades the kernel minor version.<br> |
|PasswordPolicy |Object of [PasswordPolicy](https://docs.byteplus.com/en/docs/40/15528#passwordpolicy) |No |See the request example. |Custom password policy. |

### NodeInfoObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br>> **tip**<br><br><br>> This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.<br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br>> **tip**<br><br><br><br>* > This parameter is optional for the DescribeDBInstancePriceDetail API.<br><br><br>* > When you add a node by calling the CreateDBNodes API, you can set this parameter only to `ReadOnly` for a double\-node instance or `Secondary` for a multiple\-node instance.<br><br><br>* > A double\-node instance consists of one primary node, one secondary node, and 0 to 10 optional read\-only nodes.<br><br><br>* > A multiple\-node instance consists of one primary node, and at least one and up to eight secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.<br> |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br>> **tip**<br><br><br><br>* > The specification of the secondary node must be the same as that of the primary node.<br><br><br>* > The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.<br><br><br>* > If StorageType is set to `CloudESSD_FlexPL` or `CloudESSD_PL0`, only the general type can be passed for NodeSpec.<br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br>> **tip**<br><br><br><br>* > The nodes of an instance can be distributed across a maximum of three availability zones.<br><br><br>* > During a single configuration change, you can add or delete nodes in up to three availability zones.<br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: Add node.<br><br>* `Modify`: Modify the node configuration.<br><br><br>> **tip**<br><br><br><br>* > When adding a node (CreateDBNodes), this field can only be `Create`.<br><br><br>* > When you modify the configuration, this parameter can only be set to `Modify`.<br><br><br>* > This value has no actual meaning when set to `Delete`.<br> |

### ChargeInfoObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|AutoRenew |Boolean |No |true |Specifies whether to enable Due Automatic renewal for prepaid instances. Range:<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal.<br><br><br>> **tip**<br><br><br><br>* > This parameter is required when the value of ChargeType is PrePaid.<br><br><br>* > This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.<br> |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios. Range:<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year.<br><br><br>> **tip**<br><br><br><br>* > This parameter is required when the value of ChargeType is PrePaid.<br><br><br>* > This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.<br> |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. The value range of this parameter depends on the value of PeriodUnit:<br><br><br>* When PeriodUnit is `Month`, Period ranges from 1 to 9.<br><br>* When PeriodUnit is `Year`, Period ranges from 1 to 3.<br><br><br>> **tip**<br><br><br><br>* > This parameter is required when the value of ChargeType is PrePaid.<br><br><br>* > This parameter is not required when the value of ChargeType is PostPaid. Even if parameters are passed in, the system will automatically ignore them and the configuration will not take effect.<br> |
|Number |Integer |No |1 |The number of instances to purchase. Value range: 1~50. Default value: 1.<br><br>> **tip**<br><br><br><br>* > For the RestoreToNewInstance and RestoreToCrossRegionInstance APIs, only a value of 1 is supported for this parameter.<br><br><br>* > Specifying a name for each instance is not supported for batch creation. For batch instance creation:<br><br><br>   * > If you specify a name in the `InstanceName` parameter, a serial number is appended to the name for each instance.<br><br><br>   * > If you do not specify a name in the `InstanceName` parameter, the instance ID is used as the instance name.<br> |

Call the CreateDBInstance API to create an instance.

### TagObject

|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |tagkey |The key of the instance tag. The rules for the tag key are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with any case form of `volc:`.<br><br>* The tag key must be 1 to 128 characters in length. |
|Value |String |No |tagvalue |The value of the instance tag. The rules for setting the tag value are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length, which means the tag value can be empty. |

### MaintenanceWindowObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|DayKind |String |No |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeek |Array of String |No |["Monday","Tuesday"] |Specifies the day(s) of the week for the maintenance window. Valid values are `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, and `Sunday`. You can select more than one day. If this value is not specified or is empty, it defaults to all seven days of the week. |
|MaintenanceTime |String |No |22:00Z\-02:00Z |The maintenance window for the instance. Format: `HH:mmZ-HH:mmZ` (UTC time). |

### ProxyNodeCustom

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Range:<br><br><br>* Maximum: 1,024.<br><br>* The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>* The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`. |

### AutoStorageScalingConfig

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|EnableStorageAutoScale |Boolean |Yes |true |Indicates whether to enable automatic expansion of storage space. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br>> **tip**<br><br><br>> When StorageConfig is used as a request parameter, if EnableStorageAutoScale is set to `false`, the StorageThreshold and StorageUpperBound parameters are optional.<br> |
|StorageThreshold |Integer |Yes |20 |The percentage of available storage space that triggers automatic scale\-out. The value range is 10 to 50, with a default value of 10. The unit is %. |
|StorageUpperBound |Integer |Yes |3000 |The upper limit of storage space for automatic scale\-out. The lower limit of this field is the `instance storage space + 20 GiB`, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specifications, in GiB. For more information about the range of storage space values that can be selected for different specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ScalingDetectNode |String |No |MasterNode |The range of nodes to check for automatic expansion. Values:<br><br><br>* `MasterNode`: primary node.<br><br>* `MasterSlaveNodes`: primary and secondary nodes.<br><br>* `AllNodes`: all nodes.<br><br><br>> **tip**<br><br><br><br>* > When used as a request parameter, the default value is `MasterNode`.<br><br><br>* > For a multiple\-node instance, setting this parameter to `MasterSlaveNodes` or `AllNodes` has the same effect.<br><br><br>* > For a single\-node instance, setting this parameter to `MasterNode`, `MasterSlaveNodes`, or `AllNodes` has the same effect.<br> |

### PasswordPolicy

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|Enabled |Boolean |Yes |true |Whether to enable the custom password policy. Values:<br><br><br>* `true`: Enabled.<br><br>* `false` (Default value): Disabled. |
|PolicyLevel |String |No |MEDIUM |Password strength level. Values are as follows:<br><br><br>* `LOW` (Default value): Low strength. Only the password length is verified. The password can be set as needed provided the length requirement is met.<br><br>* `MEDIUM`: Medium strength. The password length is verified, and the password must contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br>* `STRONG`: High strength. The password length is verified, and the password must contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > Since specifying a dictionary file is not supported currently, the verification rules for `MEDIUM` (medium strength) and `STRONG` (high strength) are the same.<br> |
|MinLength |Integer |No |8 |The minimum length of the password. The default value is 8, and the value range is 8~256.<br><br>> **tip**<br><br><br>> This parameter is required only when the `Enabled` parameter is set to `true`.<br> |
|NumberCount |Integer |No |1 |The number of digits that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of the `MinLength`, `MixedCaseCount` and `SpecialCharCount` parameters.<br> |
|MixedCaseCount |Integer |No |1 |The minimum number of uppercase letters and lowercase letters that the password must contain respectively. The default value is 1, and the value range is 0~256. For example, when this parameter is set to 2, the password must contain at least 2 uppercase letters and 2 lowercase letters, meaning a total of at least 4 letters.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of the `MinLength`, `NumberCount`, and `SpecialCharCount` parameters.<br> |
|SpecialCharCount |Integer |No |1 |The number of special characters that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when the `Enabled` parameter is set to `true`.<br><br><br>* > The configurable range of this parameter is dynamically adjusted based on the current values of `MinLength`, `NumberCount`, and `MixedCaseCount`.<br> |

## Response parameter

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|InstanceId |String |mysql\-06f13c93\*\*\*\* |Instance ID. |
|OrderId |String |Order709899242175681\*\*\*\* |Order ID. |

## Sample

### Sample request

```json
POST /?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBEngineVersion": "MySQL_5_7",
    "NodeInfo": [
        {
            "NodeType": "Primary",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.mysql.1c2g"
        },
        {
            "NodeType": "Secondary",
            "ZoneId": "cn-beijing-b",
            "NodeSpec": "rds.mysql.1c2g"
        }
    ],
    "StorageType": "LocalSSD",
    "StorageSpace": 20,
    "SubnetId": "subnet-2gcy3ey5i9reo50ztyzo6****",
    "VpcId": "vpc-3jhamu8itr5ds3pncmf9q****",
    "AllowListIds": [
        "acl-3929ba6fd27049e88ee772dc7b46****"
    ],
    "Port": 3306,
    "InstanceName": "测试样例",
    "ChargeInfo": {
        "ChargeType": "PostPaid",
        "Number": 1
    },
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
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230508104043BEB227FB****F73A1436",
        "Action": "CreateDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-06f13c93****",
        "OrderId": "Order7230634971667632428"
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

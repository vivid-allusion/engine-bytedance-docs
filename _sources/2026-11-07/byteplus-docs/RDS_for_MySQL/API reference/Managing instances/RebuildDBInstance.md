---
title: "RebuildDBInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/rebuilddbinstance"
---

Call the RebuildDBInstance API to rebuild an instance using the backup of a deleted instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-0f1a2a9a\*\*\*\* |Instance ID. |
|ProjectName |String |No |default |The name of the project to which the instance belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If not set, the rebuilt instance is assigned to the <strong>Default project</strong>, and the value <code>default</code> is used.</div><br> |
|RequestSource |String |No |EventType_Web |The source of the request. Values:<br><br><br>* `EventType_Web`: From the Web.<br><br>* `EventType_OpenAPI`: From Open API. |
|BackupId |String |No |2b18d7e970c442caae05be478a9e\*\*\*\* |Backup file ID. |
|StorageType |String |No |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|StorageSpace |Integer |No |100 |The storage space for the instance. Value range: [Size of the original instance's storage space, the maximum storage space for the new instance primary node specification]. The unit is GiB, with a step size of 10 GiB. The default value is the size of the source instance space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on the value range of storage space corresponding to each specification, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications">Product specifications</a>.</div><br> |
|VpcId |String |No |vpc\-2d70di2hrnbpc58ozfdx9\*\*\*\* |Virtual private cloud (VPC) ID. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Shared VPCs are not supported.</div><br> |
|InstanceName |String |No |TestInstance |Instance name. The naming rules for the instance name are as follows:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* Length must be between 1 and 128.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If not set, the rebuilt instance is named using the original instance ID.</div><br> |
|DBParamGroupId |String |No |mysql\-sys\-6013c7b8f7ef\*\*\*\* |Parameter templates ID. The default value is the default parameter template for the database engine version. |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/40/15517#chargeinfoobject) |No |See the request example. |Payment method. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/15517#nodeinfoobject) |No |See the request example. |The specifications of the instance. There is exactly 1 primary node, exactly 1 standby node, and 0 to 10 optional read\-only nodes. |
|SubnetId |String |No |subnet\-2d70dj20bob9c58ozfek6\*\*\*\* |Subnet ID. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) and specify the VpcId and ZoneId (the Availability zone of the primary node or secondary node) to query for available subnets. |
|InstanceTags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/15517#tagobject) |No |See the request example. |Instance tag.<br><br><br>* Each MySQL instance can be associated with a maximum of 50 tags.<br><br>* You can add a maximum of 20 tags at a time. |
|AllowListIds |Array of String |No |[<br><br>"acl\-a29be2559dc4406883d358892b90\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Allowlist ID. To associate multiple allowlists, separate the allowlist IDs with a comma (,). An instance can be associated with up to 100 allowlists.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you use the RebuildDBInstance API to restore to a new instance, the allowlists of the original instance are not associated with the new instance by default. After the instance rebuild is completed, you can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/associateallowlist1">AssociateAllowList</a> API to associate allowlists with the new instance.</div><br> |
|Port |Integer |No |3307 |The private network address port for the default_endpoint. The value range of the port number is 1,000\-65,534, and the default value is 3,306.<br><br>When a new connection endpoint is created or a new address is enabled, the private network address port of the default_endpoint is configured as the default port in real time. |
|AutoStorageScalingConfig |Object of [AutoStorageScalingConfig](https://docs.byteplus.com/en/docs/40/15517#autostoragescalingconfig) |No |See the request example. |Automatic scale\-out configuration. |
|DeletionProtection |String |No |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. Default value. |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/15517#proxynodecustom) |No |See the request example. |The proxy configuration of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This field is required when the original instance of the backup is a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This field does not take effect when the original instance of the backup is a double\-node instance.</div><br> |
|PrivateIpAddress |String |No |192.168.xxx.xxx |The IP address of the default endpoint of the instance in the specified virtual private cloud and subnet. |


<span id="chargeinfoobject"></span>
### ChargeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|AutoRenew |Boolean |No |true |Specifies whether to enable Due Automatic renewal for prepaid instances. Range:<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid.</div><br> |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios. Range:<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid.</div><br> |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. The value range of this parameter depends on the value of PeriodUnit:<br><br><br>* When PeriodUnit is `Month`, Period ranges from 1 to 9.<br><br>* When PeriodUnit is `Year`, Period ranges from 1 to 3.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of ChargeType is PrePaid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is PostPaid.</div><br> |
|Number |Integer |No |1 |The number of instances to purchase. Value range: 1~50. Default value: 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the RestoreToNewInstance and RestoreToCrossRegionInstance APIs, only a value of 1 is supported for this parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Specifying a name for each instance is not supported for batch creation. For batch instance creation:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you specify a name in the `InstanceName` parameter, a serial number is appended to the name for each instance.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you do not specify a name in the `InstanceName` parameter, the instance ID is used as the instance name.</div><br> |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|Parameter |Type |Required? |Sample value |Description |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is optional for the DescribeDBInstancePriceDetail API.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add a node by calling the CreateDBNodes API, you can set this parameter only to <code>ReadOnly</code> for a double\-node instance or <code>Secondary</code> for a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A double\-node instance consists of one primary node, one secondary node, and 0 to 10 optional read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A multiple\-node instance consists of one primary node, and at least one and up to eight secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.</div><br> |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of the secondary node must be the same as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If StorageType is set to <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>, only the general type can be passed for NodeSpec.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nodes of an instance can be distributed across a maximum of three availability zones.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During a single configuration change, you can add or delete nodes in up to three availability zones.</div><br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: add.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding a node (CreateDBNodes), this field can only be <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the configuration, this parameter can only be set to <code>Modify</code>.</div><br> |


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
|EnableStorageAutoScale |Boolean |Yes |true |Indicates whether to enable automatic scale\-out for the instance. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When StorageConfig is used as a request parameter, if EnableStorageAutoScale is set to <code>false</code>, the StorageThreshold and StorageUpperBound parameters are optional.</div><br> |
|StorageThreshold |Integer |Yes |20 |The percentage of available storage space that triggers automatic scale\-out. The value range is 10 to 50, with a default value of 10. The unit is %. |
|StorageUpperBound |Integer |Yes |3000 |The upper limit of storage space for automatic scale\-out. The lower limit of this field is the `instance storage space + 20 GiB`, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specifications, in GiB. For more information about the range of storage space values that can be selected for different specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ScalingDetectNode |String |No |MasterNode |The range of nodes to check for automatic expansion. Values:<br><br><br>* `MasterNode`: primary node.<br><br>* `MasterSlaveNodes`: primary and secondary nodes.<br><br>* `AllNodes`: all nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>MasterNode</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a multiple\-node instance, setting this parameter to <code>MasterSlaveNodes</code> or <code>AllNodes</code> has the same effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single\-node instance, setting this parameter to <code>MasterNode</code>, <code>MasterSlaveNodes</code>, or <code>AllNodes</code> has the same effect.</div><br> |


<span id="proxynodecustom"></span>
### ProxyNodeCustom


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Range:<br><br><br>* Maximum: 1,024.<br><br>* For a multiple\-node instance,<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For a double\-node instance,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-e7fda57b\*\*\*\* |The ID of the rebuilt instance. |
|OrderId |String |Order709899242175681\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RebuildDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlk****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c****
{
    "InstanceId": "mysql-05aeaf44fe2f",
    "BackupId": "34c5f835570c4eab85ed5ecb4f583820",
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
    "StorageSpace": 110,
    "AutoStorageScalingConfig": {
        "EnableStorageAutoScale": true,
        "StorageThreshold": 20,
        "StorageUpperBound": 300
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
        "RequestId": "2023080920015509344927A18EDA8CBB20",
        "Action": "RebuildDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-0f1a2a9a****",
        "OrderId": "Order726528840890330****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

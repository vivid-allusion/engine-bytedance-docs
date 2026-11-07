---
title: "CreateDBBlueGreenInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/CreateDBBlueGreenInstance"
---

Call the CreateDBBlueGreenInstance API to create a blue\-green deployment for an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* MySQL 8.4 instances do not support creating blue\-green deployments.

* The blue instance state must be Running.

* Disaster recovery instances do not support creating blue\-green deployments.

* If an instance is already bound to a blue\-green deployment relationship (i.e. a green instance exists), you cannot create another green instance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBBlueGreenInstance&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-54fc7408\*\*\*\* |The ID of the blue instance in the blue\-green deployment. |
|DBEngineVersion |String |Yes |MySQL_8_0 |Compatible version for the green instance. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0. |
|InstanceType |String |No |DoubleNode |Instance type for the green instance. Values:<br><br><br>* `DoubleNode`, Double node type.<br><br>* `MultiNode`, multiple node type.<br><br>* `SingleNode`, single node type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a single\-node type, you can select a single\-node or double\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a double\-node type, you can select a double\-node or multiple\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a multiple\-node type, you can only select the multiple\-node type for the green instance.</div><br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/61054#nodeinfoobject) |Yes |See the request example. |Specifications of the green instance in a blue\-green deployment. |
|StorageType |String |Yes |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|StorageSpace |Integer |Yes |100 |Storage space of the green instance in a blue\-green deployment. The value must be greater than or equal to the storage space of the blue instance. |
|InstanceName |String |No |Test instance\-green |Green instance name. The naming rules for the instance name are as follows:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* Length must be between 1 and 128.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no name is specified for the green instance, it will be named <code>${blue instance name}-green-${uuid6}</code> by default. The name will be truncated if longer than 128 characters.</div><br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/40/61054#chargeinfoobject) |Yes |See the request example. |Billing configuration of the green instance in a blue\-green deployment. |
|DeletionProtection |String |No |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. Default value. |
|DBParamGroupId |String |No |mysql\-0cfb0b83d64a\*\*\*\* |The ID of the parameter template applied to the green instance in a blue\-green deployment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue and green instances share the same compatible database version and this parameter is not specified, the green instance inherits the parameter settings of the blue instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue and green instances have different compatible database versions, this parameter is required.</div><br> |
|MinorVersion |String |No |MySQL 5.7.32_20250615 |The kernel minor version of the green instance in a blue\-green deployment. The value can be the kernel minor version of the blue instance or the latest kernel version. |
|SubnetId |String |No |subnet\-3rf442t6a54w016nf3pg9\*\*\*\* |Subnet ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is not specified, the same subnet as the blue instance is used.</div><br> |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/61054#proxynodecustom) |No |See the request example. |Number of proxy cores for the green instance in the blue\-green deployment.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The proxy feature of the green instance is enabled by default to match the blue instance. If the proxy feature is enabled on the blue instance, the number of proxy cores on the green instance defaults to that of the blue instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the database proxy of the blue instance is disabled, setting the <code>CpuNum</code> parameter to a value greater than 0 will automatically enable the database proxy for the green instance. The specified value will serve as the number of CPU cores allocated to the proxy service.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the database proxy of the blue instance is enabled, setting the <code>CpuNum</code> parameter to 0 will disable the database proxy for the green instance.</div><br> |
|PrivateIpAddress |String |No |192.168.xxx.xxx |The IP address of the default endpoint of the instance in the specified virtual private cloud and subnet. |
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


<span id="proxynodecustom"></span>
### ProxyNodeCustom


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Values are as follows:<br><br><br>* Value range: Upper limit 1024.<br><br>* For a multiple\-node instance,<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For a double\-node instance,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-1252c254\*\*\*\* |The ID of the green instance in the blue\-green deployment. |
|OrderId |String |Order2180000035163379202 |Order number. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDBBlueGreenInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-54fc7408****",
    "DBEngineVersion": "MySQL_5_7",
    "InstanceType": "DoubleNode",
    "NodeInfo": [
        {
            "ZoneId": "cn-guangzhou-a",
            "NodeSpec": "rds.mysql.d1.n.1c1g",
            "NodeType": "Primary"
        },
        {
            "ZoneId": "cn-guangzhou-b",
            "NodeSpec": "rds.mysql.d1.n.1c1g",
            "NodeType": "Secondary"
        },
        {
            "ZoneId": "cn-guangzhou-a",
            "NodeSpec": "rds.mysql.d1.n.1c1g",
            "NodeType": "ReadOnly"
        }
    ],
    "StorageType": "LocalSSD",
    "StorageSpace": 20,
    "InstanceName": "测试实例-green",
    "ChargeInfo": {
        "ChargeType": "PostPaid"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250724164709DE5361052ED14F0ABE61-64f8a2",
        "Action": "CreateDBBlueGreenInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "InstanceId": "mysql-1252c254****",
        "OrderId": "Order2180000035163379202"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

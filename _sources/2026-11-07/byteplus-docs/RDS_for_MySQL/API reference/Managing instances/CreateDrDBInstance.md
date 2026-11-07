---
title: "CreateDrDBInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdrdbinstance"
---

Call the CreateDrDBInstance API to create a disaster recovery instance for the specified instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The request must be sent to the region where the disaster recovery instance is located.

* MySQL 8.4 instances do not support creating a disaster recovery instance.

* Instances with TDE encryption enabled do not support creating disaster recovery instances.

* Single\-node instances do not support creating disaster recovery instances.

* Creating a disaster recovery instance for a green instance in a blue\-green deployment is not supported.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDrDBInstance&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|MasterInstanceId |String |Yes |mysql\-cb50000b\*\*\*\* |The ID of the primary instance. |
|MasterRegion |String |Yes |cn\-shanghai |The region where the primary instance is located. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/54499#nodeinfoobject) |Yes |See the request example. |Specification of the disaster recovery instance. |
|StorageSpace |Integer |Yes |20 |The storage space of the disaster recovery instance. For more information on the value range of storage space corresponding to each specification, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). The unit is GiB, and the step size is 10 GiB. |
|VpcId |String |Yes |vpc\-3revrf005h5a85zsk2hlu\*\*\*\* |Virtual private cloud (VPC) ID. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Shared VPCs are not supported.</div><br> |
|SubnetId |String |Yes |subnet\-2bzpnnjy4b1ts2dx0efn9\*\*\*\* |Subnet ID. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) and specify the VpcId and ZoneId (the Availability zone of the primary node or secondary node) to query for available subnets. |
|InstanceName |String |No |Test instance |Instance name. The naming rules for the instance name are as follows:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* Length must be between 1 and 128.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If not specified, the instance ID is used as the instance name.</div><br> |
|DeletionProtection |String |No |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yYes.<br><br>* `Disabled`: o. Default value. |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/54499#proxynodecustom) |No |See the request example. |The database proxy configuration of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This field is required when the primary instance is a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Database proxy configuration is not supported when the primary instance is a double\-node instance.</div><br> |
|StorageType |String |No |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
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


<span id="proxynodecustom"></span>
### ProxyNodeCustom


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Values are as follows:<br><br><br>* Value range: Upper limit 1024.<br><br>* For a multiple\-node instance,<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For a double\-node instance,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-9522449c\*\*\*\* |The ID of the created disaster recovery instance. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDrDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "MasterInstanceId": "mysql-cb50000b****",
    "MasterRegion": "cn-shanghai",
    "NodeInfo": [
        {
            "ZoneId": "cn-beijing-a",
            "NodeType": "Primary",
            "NodeSpec": "rds.mysql.d1.n.1c1g"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeType": "Secondary",
            "NodeSpec": "rds.mysql.d1.n.1c1g"
        }
    ],
    "StorageSpace": 20,
    "VpcId": "vpc-3revrf005h5a85zsk2hlu****",
    "SubnetId": "subnet-2bzpnnjy4b1ts2dx0efn9****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241205224453AFE647500FC978A40031-70c7af",
        "Action": "CreateDrDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guilin-boe"
    },
    "Result": {
        "InstanceId": "mysql-9522449c****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

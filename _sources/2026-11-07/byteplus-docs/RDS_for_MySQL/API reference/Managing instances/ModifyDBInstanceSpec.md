---
title: "ModifyDBInstanceSpec"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbinstancespec1"
---

Call the ModifyDBInstanceSpec API to modify instance configurations.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API is deprecated. Use the following APIs to modify the instance configuration:


* Call the [CreateDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbnodes) API to add nodes to an instance.

* Call the [ModifyDBNodeSpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodespec) API to modify the node specification and storage space of an instance.

* Call the [DeleteDBNodes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes) API to delete nodes from an instance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceSpec&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-e26822cf\*\*\*\* |Instance ID. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/15524#nodeinfoobject) |No |[<br><br>{<br><br>"NodeId": "mysql\-7d1efb9f\*\*\*\*\-0","NodeType": "Primary",<br><br>"NodeSpec": "rds.mysql.1c2g",<br><br>"NodeOperateType": "Modify"<br><br>},<br><br>{<br><br>"NodeId": "mysql\-7d1efb9f\*\*\*\*\-1",<br><br>"NodeType": "Secondary",<br><br>"NodeSpec": "rds.mysql.1c2g",<br><br>"NodeOperateType": "Modify"<br><br>},<br><br>{<br><br>"NodeId": "mysql\-7d1efb9f\*\*\*\*\-r\*\*\*\*",<br><br>"NodeType": "ReadOnly",<br><br>"NodeSpec": "rds.mysql.1c2g",<br><br>"NodeOperateType": "Delete"<br><br>},<br><br>{<br><br>"NodeType": "ReadOnly",<br><br>"NodeSpec": "rds.mysql.1c2g",<br><br>"NodeOperateType": "Create"<br><br>},<br><br>{<br><br>"NodeId": "mysql\-7d1efb9f\*\*\*\*\-r\*\*\*\*",<br><br>"NodeType": "ReadOnly",<br><br>"NodeSpec": "rds.mysql.1c2g",<br><br>"NodeOperateType": "Modify"<br><br>}<br><br>] |The specifications of the instance. There is exactly 1 primary node, exactly 1 standby node, and 0 to 10 optional read\-only nodes. Ignore ZoneId except when adding a read\-only node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">One of the parameters Storage space or this parameter must be selected, and both parameters can be modified simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">RDS for MySQL supports creating primary and secondary nodes in different availability zones, but read\-only nodes must be added in the availability zone of the primary or secondary node.</div><br> |
|ModifyType |String |No |Usually |The modification type for the instance specification. The value is `Usually`, which indicates a regular modification of specification. |
|StorageType |String |Yes |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0 or CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|StorageSpace |Integer |No |100 |The storage space for the instance. Value range: [20, 3000]. Unit in GB, and step size of 10GB. The default value is the same as the current value.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">One of this parameter and NodeInfo is required, and both can be modified simultaneously.</div><br> |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the <code>SpecifiedSwitchStartTime</code> and <code>SpecifiedSwitchEndTime</code> parameters.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time for execution in a Specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The start time of the task cannot be later than seven days after the current date.</div><br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period for execution. Format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of SwitchType is <code>SpecifiedTime</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is one hour and fifty\-nine minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.</div><br> |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node. |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of the secondary node must be the same as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If StorageType is set to <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>, only the general type can be passed for NodeSpec.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nodes of an instance can be distributed across a maximum of three availability zones.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During a single configuration change, you can add or delete nodes in up to three availability zones.</div><br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: add.<br><br>* `Modify`: modify.<br><br>* `Delete`: delete. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-7d1efb9f\*\*\*\* |Instance ID. |
|OrderId |String |Order71220115095297\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f4cba23f****",
    "NodeInfo": [
        {
            "NodeId": "mysql-f4cba23f****-0",
            "NodeType": "Primary",
            "NodeSpec": "rds.mysql.2c4g",
            "NodeOperateType": "Modify"
        },
        {
            "NodeId": "mysql-f4cba23f****-1",
            "NodeType": "Secondary",
            "NodeSpec": "rds.mysql.2c4g",
            "NodeOperateType": "Modify"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeType": "ReadOnly",
            "NodeSpec": "rds.mysql.2c4g",
            "NodeOperateType": "Create"
        }
    ],
    "StorageType": "LocalSSD",
    "StorageSpace": 200
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220719173634010212035227001977AC",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-f4cba23f****",
        "OrderId": "Order71220115095297****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

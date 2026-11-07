---
title: "ModifyDBInstanceSpec"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec"
---

Call the ModifyDBInstanceSpec API to modify instance configurations.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |Instance ID. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/61/15771#nodeinfoobject) |No |Refer to the request example. |Instance specification configuration. There is exactly one primary node and one secondary node, with 0 to 10 optional read\-only nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">One of the parameters <code>Storage space</code> or this parameter must be selected, and both parameters can be modified simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only the nodes involved in the specification modification need to be passed in this parameter.</div><br> |
|ModifyType |String |No |Temporary |Modification method. Values are:<br><br><br>* `Usually`: regular modification of specification, which takes effect immediately. Default value.<br><br>* `Temporary`: elastic upgrade, that is, temporary upgrade.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only instances with the billing method of subscription support the parameter value <code>Temporary</code>. You can query the instance's billing method by calling the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail">DescribeDBInstanceDetail</a> API.</div><br> |
|RollbackTime |String |No |2023\-12\-16T03:59:10.000Z |Restoration time. The time format is `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when ModifyType is <code>Temporary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is effective only when ModifyType is <code>Temporary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The set restoration time should not differ from the API call time by more than 2 minutes. The actual restoration time is based on the API call time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Temporary upgrades can be initiated multiple times to extend the temporary upgrade period, but the total duration cannot exceed 30 days (based on the time of the first temporary upgrade initiation).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple temporary upgrades can be initiated, but their duration cannot be shortened. If the instance is already in the temporary upgrade period:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">The new restoration date cannot be earlier than the effective restoration date.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the subscription instance is within five days of expiration, initiating another temporary upgrade is not allowed.</div><br> |
|StorageType |String |No |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">One of this parameter and <code>NodeInfo</code> is required, and both can be modified simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When ModifyType is set to <code>Temporary</code>, setting this parameter is not supported.</div><br> |
|StorageSpace |Integer |No |100 |Instance storage space. Unit is GB, with a step size of 10 GB.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications?lang=zh">Product specifications</a>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">One of this parameter and <code>NodeInfo</code> is required, and both can be modified simultaneously.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When ModifyType is set to <code>Temporary</code>, setting this parameter is not supported.</div><br> |
|SwitchType |String |No |Immediate |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default)<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the SpecifiedSwitchStartTime and SpecifiedSwitchEndTime parameters.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time for execution within a specific time period. Format is `yyyy-MM-ddTHH:mm:ssZ`. |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time for execution within the specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum time period is one hour and fifty\-nine minutes.</div><br> |
|EstimateOnly |Boolean |No |true |Specifies whether to initiate a specification change assessment. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this parameter is specified, the system evaluates the specification change based on the parameters set for other fields without performing the actual change. After you initiate a configuration change assessment, the EstimationResult parameter is returned to describe the impact of the change.</div><br> |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |postgres\-ca7b7019\*\*\*\* |Node ID. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) API to query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when modifying node specification and deleting nodes (ModifyDBInstancesSpec).</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required when creating an instance (CreateDBInstance), restoring to a new instance (RestoreToNewInstance), and adding or modifying nodes (ModifyDBInstancesSpec).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeSpec |String |Yes |rds.postgres.1c2g |Node specification. Query specifications available for sale via [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) API. |
|NodeOperateType |String |No |Create |Operation type. Range:<br><br><br>* `Create`: add.<br><br>* `Delete`: delete.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">In the CreateDBInstance and RestoreToNewInstance APIs, this field can only be set to <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When modifying instance configuration, the specified NodeOperateType must be passed in for the involved nodes.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|OrderId |String |Order725743560891294\*\*\*\* |Order ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When EstimateOnly is <code>true</code>, this field returns empty.</div><br> |
|EstimationResult |Object of [ModifyDBInstanceSpecEstimationResult](https://docs.byteplus.com/en/docs/61/15771#modifydbinstancespecestimationresult) |Refer to the sample response. |The estimated impact on the instance after the change based on the current configuration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is not returned if the EstimateOnly parameter is set to <code>false</code> or is not specified.</div><br> |


<span id="modifydbinstancespecestimationresult"></span>
### ModifyDBInstanceSpecEstimationResult


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Plans |Array of String |["AddNode", "RebuildPrimary"] |The estimated impact on the read/write connection of the instance after the configuration change. Values:<br><br><br>* `AddNode`: there are nodes to be added.<br><br>* `DeleteNode`: there are nodes to be deleted.<br><br>* `RebuildPrimary`: the primary database may be migrated.<br><br>* `RebuildReadOnly`: the read\-only node may be migrated.<br><br>* `RebuildSecondary`: the secondary database may be migrated. |
|Effects |Array of String |["ReadWriteConnectionTransientError",<br><br>"ReadOnlyConnectionTransientError"<br><br>] |The estimated impact on the read/write connection of the instance after the configuration change. Values:<br><br><br>* `ReadOnlyConnectionTransientError`: read\-only connection transient disconnection.<br><br>* `ReadWriteConnectionTransientError`: read\-write connection transient disconnection. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LLTE="></span>
### Request example 1 Regular modification of specification

```json
POST /?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "StorageType": "LocalSSD",
    "StorageSpace": 60,
    "NodeInfo": [
        {
            "NodeId": "postgres-ca7b7019****",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Primary"
        },
        {
            "NodeId": "postgres-ca7b7019****-wmjy",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Secondary"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "ReadOnly",
            "NodeOperateType": "Create"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LLTE="></span>
### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202308011557433BA18653C86F63A04B1B",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-21a3333b****",
        "OrderId": "Order725743560891294****"
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2 Temporary upgrade example (upgrade primary and secondary node specification)

```json
POST /?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "NodeInfo": [
        {
            "NodeId": "postgres-ca7b7019****",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.2c4g",
            "NodeType": "Primary",
            "NodeOperateType": "Modify"
        },
        {
            "NodeId": "postgres-ca7b7019****-wmjy",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.2c4g",
            "NodeType": "Secondary",
            "NodeOperateType": "Modify"
        }
    ],
    "ModifyType": "Temporary",
    "RollbackTime": "2023-12-16T03:59:10.000Z"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202308011557433BA18653C86F63A04B1B",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-21a3333b****",
        "OrderId": "Order725743560891294****"
    }
}
```


<span id=".6K-35rGC56S65L6LLTM="></span>
### Request example 3 Modification impact estimation

```json
POST /?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "StorageType": "LocalSSD",
    "StorageSpace": 60,
    "NodeInfo": [
        {
            "NodeId": "postgres-ca7b7019****",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Primary"
        },
        {
            "NodeId": "postgres-ca7b7019****-wmjy",
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Secondary"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "ReadOnly",
            "NodeOperateType": "Create"
        }
    ],
    "EstimateOnly": true
}
```


<span id=".6L-U5Zue56S65L6LLTM="></span>
### Sample response 3

```json
{
    "ResponseMetadata": {
        "RequestId": "202510101646419FA4685B4AC9EDAF4B05-85d668",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "EstimationResult": {
            "Effects": [
                "ReadWriteConnectionTransientError"
            ],
            "Plans": [
                "AddNode"
            ]
        },
        "InstanceId": "postgres-36cd1f06e9f3",
        "OrderId": ""
    }
}
```

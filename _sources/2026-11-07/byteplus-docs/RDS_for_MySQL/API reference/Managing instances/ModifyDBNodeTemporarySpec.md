---
title: "ModifyDBNodeTemporarySpec"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbnodetemporaryspec"
---

Call the ModifyDBNodeTemporarySpec API to temporarily upgrade the configuration of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The temporary upgrade is currently an allowlisted feature. While there are a few minor areas for experience optimization, they do not affect the normal operation of the instance. If your business has specific needs for this feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to apply for allowlist access.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBNodeTemporarySpec&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/54495#nodeinfoobject) |Yes |See the request example. |The node configuration change information of the instance. |
|RollbackTime |String |Yes |2024\-10\-16T03:59:10.000Z |Restoration time of temporary upgrade. The restoration time can be set to any time between 5 and 30 days after the current time. Time format is `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the SpecifiedSwitchStartTime and SpecifiedSwitchEndTime parameters.</div><br> |
|RequestSource |String |No |EventType_Web |The source of the request. Values:<br><br><br>* `EventType_Web`: from the Web.<br><br>* `EventType_OpenAPI`: From Open API. |
|EstimateOnly |Boolean |No |true |Specifies whether to initiate an assessment for the specification change. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is specified, the system evaluates the specification change based on the parameters set for other fields without performing the actual change. After you initiate the evaluation, the system returns the EstimationResult parameter, which describes the impact of the specification change.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time of the specific time period for execution(UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The start time of the task cannot be later than seven days after the current date.</div><br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period for execution (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of SwitchType is <code>SpecifiedTime</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is one hour and fifty\-nine minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.</div><br> |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is optional for the DescribeDBInstancePriceDetail API.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add a node by calling the CreateDBNodes API, you can set this parameter only to <code>ReadOnly</code> for a double\-node instance or <code>Secondary</code> for a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A double\-node instance consists of one primary node, one secondary node, and 0 to 10 optional read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A multiple\-node instance consists of one primary node, and at least one and up to eight secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.</div><br> |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of the secondary node must be the same as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If StorageType is set to <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>, only the general type can be passed for NodeSpec.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nodes of an instance can be distributed across a maximum of three availability zones.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During a single configuration change, you can add or delete nodes in up to three availability zones.</div><br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: add.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding a node (CreateDBNodes), this field can only be <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the configuration, this parameter can only be set to <code>Modify</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This value has no actual meaning when set to <code>Delete</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-db6d920e\*\*\*\* |Instance ID. |
|OrderId |String |Order71220115095297\*\*\*\* |Order ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When EstimateOnly is <code>true</code>, this field is empty.</div><br> |
|EstimationResult |Object of [ModifyDBInstanceSpecEstimationResult](https://docs.byteplus.com/en/docs/40/54495#modifydbinstancespecestimationresult) |Refer to the Sample response. |Estimated impact on the instance after changing the current configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned if the EstimateOnly parameter is set to <code>false</code> or is not specified.</div><br> |


<span id="modifydbinstancespecestimationresult"></span>
### ModifyDBInstanceSpecEstimationResult


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Plans |Array of String |[<br><br>"AddNode"<br><br>] |Estimated impact on the instance after changing the current configuration. Values:<br><br><br>* `AddNode`: new node(s) will be added.<br><br>* `DeleteNode`: there are nodes to be deleted.<br><br>* `RebuildPrimary`: the primary database may be migrated.<br><br>* `RebuildReadOnly`: the read\-only node may be migrated.<br><br>* `RebuildSecondary`: the secondary database may be migrated. |
|Effects |Array of String |[<br><br>"ReadWriteConnectionTransientError",<br><br>"ReadOnlyConnectionTransientError"<br><br>] |The estimated impact on the read/write connection of the instance after the configuration change. Values:<br><br><br>* `ReadOnlyConnectionTransientError`: read\-only connection transient disconnection.<br><br>* `ReadWriteConnectionTransientError`: read\-write connection transient disconnection. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBNodeTemporarySpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-66347599****",
    "NodeInfo": [
        {
            "NodeId": "mysql-66347599****-rd49e",
            "ZoneId": "cn-beijing-a",
            "NodeType": "ReadOnly",
            "NodeSpec": "rds.mysql.d1.n.2c8g",
            "NodeOperateType": "Modify"
        }
    ],
    "RollbackTime": "2024-11-28T10:59:10.000Z"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024112020583642C7DB9CF0747D184FAA-f990a2",
        "Action": "ModifyDBNodeTemporarySpec",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-c9b0dce8****",
        "OrderId": "Order2180008796437128674"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

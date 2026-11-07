---
title: "DeleteDBNodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbnodes"
---

Call the DeleteDBNodes API to remove nodes from an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

You cannot delete nodes from a single\-node instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDBNodes&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|DBNodeIds |Array of String |Yes |["mysql\-c9b0dce8\*\*\*\*\-r2b33","mysql\-c9b0dce8\*\*\*\*\-r3e7f"] |The list of Node IDs to delete.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The Node specified in DBNodeIds must belong to the instance specified in InstanceId.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a double\-node instance, the primary and secondary nodes cannot be deleted. You can have 0 to 10 read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a multiple\-node instance, the primary node cannot be deleted. You must have at least 1 and at most 8 secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.</div><br> |
|SwitchType |String |No |MaintainTime |Execution time. The valid values are:<br><br><br>* `Immediate`: switch now (default).<br><br>* `MaintainTime`: switch during the maintenance window.<br><br>* `SpecifiedTime`: switch during the specified time period.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail">DescribeDBInstanceDetail</a> API to query the instance's maintenance window.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the value is <code>SpecifiedTime</code>, you must set the start and end time of the time period in the SpecifiedSwitchStartTime and SpecifiedSwitchEndTime parameters.</div><br> |
|RequestSource |String |No |EventType_Web |Request source. Values:<br><br><br>* `EventType_Web`: from the Web.<br><br>* `EventType_OpenAPI`: From Open API. |
|EstimateOnly |Boolean |No |true |Specifies whether to initiate an assessment for the specification change. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is specified, the system evaluates the specification change based on the parameters set for other fields without performing the actual change. After you initiate the evaluation, the system returns the EstimationResult parameter, which describes the impact of the specification change.</div><br> |
|SpecifiedSwitchStartTime |String |No |2024\-12\-25T14:00:00Z |The start time of the specific time period for execution(UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When SwitchType is set to <code>SpecifiedTime</code>, this parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The start time of the task cannot be later than seven days after the current date.</div><br> |
|SpecifiedSwitchEndTime |String |No |2024\-12\-25T15:59:00Z |The end time of the specific time period for execution (UTC time). The format is `yyyy-MM-ddTHH:mm:ssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required when the value of SwitchType is <code>SpecifiedTime</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The minimum time period is one hour and fifty\-nine minutes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days. The task's start and end times must be within a 24\-hour window.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceId |String |mysql\-db6d920e\*\*\*\* |Instance ID. |
|OrderId |String |Order71220115095297\*\*\*\* |Order ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is empty when EstimateOnly is <code>true</code>.</div><br> |
|EstimationResult |Object of [ModifyDBInstanceSpecEstimationResult](https://docs.byteplus.com/en/docs/40/54486#modifydbinstancespecestimationresult) |Refer to the Sample response. |The estimated impact on the instance after the change based on the current configuration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned if the EstimateOnly parameter is set to <code>false</code> or is not specified.</div><br> |


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
POST /?Action=DeleteDBNodes&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-cf4f3ddc****",
    "DBNodeIds": [
        "mysql-cf4f3ddc****-r290e",
        "mysql-cf4f3ddc****-r3104",
        "mysql-cf4f3ddc****-r615f"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024112020341683DE8B8D60C055DE3413-6e37f0",
        "Action": "DeleteDBNodes",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mysql-cf4f3ddc****",
        "OrderId": "Order2180000010993392034"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

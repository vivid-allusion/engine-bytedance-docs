---
title: "DescribeDBInstanceHAConfig"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBInstanceHAConfig"
---

Call the DescribeDBInstanceHAConfig API to query the high availability configuration of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceHAConfig&serviceCode=rds_mysql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Nodes |Array of [NodeDetailInfoObject](https://docs.byteplus.com/en/docs/40/61048#nodedetailinfoobject) |Refer to the Sample response. |Instance node information. |
|DataSyncMode |String |Async |Data synchronization method:<br><br><br>* `SemiSync`: semisynchronous.<br><br>* `Async`: asynchronous. |
|AutoStorageScalingConfig |Object of [AutoStorageScalingConfig](https://docs.byteplus.com/en/docs/40/61048#autostoragescalingconfig) |Refer to the Sample response. |Auto scaling rules for storage space. |
|AutoSpecScalingConfig |Object of [AutoSpecScalingConfig](https://docs.byteplus.com/en/docs/40/61048#autospecscalingconfig) |Refer to the sample response. |The scaling rule of the node specification. |


<span id="nodedetailinfoobject"></span>
### NodeDetailInfoObject


|Parameter |Type |Example |Description |
|---|---|---|---|
|CreateTime |String |2024\-10\-29T08:45:28.000Z |The creation time of the node (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|DelayReplicationTime |Long |1000 |The replication delay for a read\-only node ranges from 0 to 604,800, and the unit is seconds. |
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|Memory |Integer |2 |Memory size. Unit is GiB. |
|NodeId |String |mysql\-h441603c\*\*\*\*\-01 |Node ID. |
|NodeSpec |String |rds.mysql.d1.n.2c4g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|NodeStatus |String |Running |Node status, with values:<br><br><br>* `Running`: running.<br><br>* `Creating`: creating.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Restoring`: recovering.<br><br>* `Updating`: modifying.<br><br>* `Upgrading`: upgrading.<br><br>* `Error`: error. |
|NodeType |String |Primary |Node type. Values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node. |
|RegionId |String |cn\-beijing |Region ID, use [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions) to query the available region list. Use this parameter to specify the region for creating the instance. |
|SyncDelay |Long |28 |The delay between the node and the primary node. The unit is milliseconds (ms). |
|UpdateTime |String |2024\-10\-31T08:45:28.000Z |The local update time of the node (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|VCPU |Integer |1 |CPU cores of the node. |
|ZoneId |String |cn\-beijing\-a |Availability zone ID. |


<span id="autostoragescalingconfig"></span>
### AutoStorageScalingConfig


|Parameter |Type |Example |Description |
|---|---|---|---|
|EnableStorageAutoScale |Boolean |true |Indicates whether to enable automatic expansion of storage space. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When StorageConfig is used as a request parameter, if EnableStorageAutoScale is set to <code>false</code>, the StorageThreshold and StorageUpperBound parameters are optional.</div><br> |
|StorageThreshold |Integer |20 |The percentage of available storage space that triggers automatic scale\-out. The value range is 10 to 50, with a default value of 10. The unit is %. |
|StorageUpperBound |Integer |3000 |The upper limit of storage space for automatic scale\-out. The lower limit of this field is the `instance storage space + 20 GiB`, and the upper limit is the upper limit of the storage space value range corresponding to the instance primary node specifications, in GiB. For more information about the range of storage space values that can be selected for different specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ScalingDetectNode |String |MasterNode |The range of nodes to check for automatic expansion. Values:<br><br><br>* `MasterNode`: primary node.<br><br>* `MasterSlaveNodes`: primary and secondary nodes.<br><br>* `AllNodes`: all nodes.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>MasterNode</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a multiple\-node instance, setting this parameter to <code>MasterSlaveNodes</code> or <code>AllNodes</code> has the same effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single\-node instance, setting this parameter to <code>MasterNode</code>, <code>MasterSlaveNodes</code>, or <code>AllNodes</code> has the same effect.</div><br> |


<span id="autospecscalingconfig"></span>
### AutoSpecScalingConfig


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|LatestExpandTime |String |2026\-07\-25T06:25:22Z |The latest scaling trigger time of the instance. Format: yyyy\-MM\-dd HH:mm:ss (UTC time).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter will not be returned if no scaling has been triggered for the instance.</div><br> |
|CronAutoScalingSpecRules |Array of [CronAutoScalingSpecRule](https://docs.byteplus.com/en/docs/40/61048#cronautoscalingspecrule) |Refer to response results |Scheduled scaling rules. |
|SupportCloudDiskAutoScaling |Boolean |true |Whether cloud disk instances support automatic scaling. Values:<br><br><br>* `true`: supported.<br><br>* `false`: not supported. |
|ExpandObservableAutoScalingSpecRules |Array of [ExpandObservableAutoScalingSpecRule](https://docs.byteplus.com/en/docs/40/61048#expandobservableautoscalingspecrule) |Refer to the sample response. |Automatic expansion rules. |
|ReduceObservableAutoScalingSpecRules |Array of [ReduceObservableAutoScalingSpecRule](https://docs.byteplus.com/en/docs/40/61048#reduceobservableautoscalingspecrule) |Refer to the sample response. |Automatic scale\-down rules. |


<span id="cronautoscalingspecrule"></span>
### CronAutoScalingSpecRule


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RuleId |String |rule\-6311830b433\*\*\*\* |Scheduled scaling rule ID. |
|Enabled |Boolean |true |Whether to enable the rule. Values:<br><br><br>* `true`: Enabled.<br><br>* `false`: disable. |
|ExpandTime |Object of [CycleTimeInfo](https://docs.byteplus.com/en/docs/40/61048#cycletimeinfo) |Refer to the sample response. |The start time of the expansion. |
|ReduceTime |Object of [CycleTimeInfo](https://docs.byteplus.com/en/docs/40/61048#cycletimeinfo) |Refer to the sample response. |The start time of the scale\-down operation. |
|CyclePeriod |String |Once |The cycle for expansion and scale\-down. Values:<br><br><br>* `Once`: Scaling is triggered only once at the specified expansion start time and scale\-down start time.<br><br>* `ByDay`: Scaling will be automatically triggered daily at the specified expansion start time and scale\-down start time.<br><br>* `ByWeek`: Scaling will be automatically triggered weekly at the specified expansion start time and scale\-down start time.<br><br>* `ByMonth`: Scaling will be automatically triggered monthly at the specified expansion start time and scale\-down time. |
|RuleEndTime |String |2026\-07\-31T00:00:00.000Z |Effective end time of scheduled scaling rules, formatted as yyyy\-MM\-dd HH:mm:ss (UTC).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the value of the <code>CyclePeriod</code> parameter is <code>ByDay</code>, <code>ByWeek</code>, or <code>ByMonth</code>.</div><br> |
|NodeIdsToSpec |JSON Map |{<br><br>"mysql\-8b56e2f0\*\*\*\*\-m\*\*\*\*\*\-0": "rds.mysql.c.s.2c4g",<br><br>"mysql\-8b56e2f0\*\*\*\*\-r\*\*\*\*": "rds.mysql.c.s.2c4g"，<br><br>"mysql\-8b56e2f0\*\*\*\*\*\-s\*\*\*\*\*\-0": "rds.mysql.c.s.2c4g"<br><br>} |Node IDs pending expansion and scale\-down and the target specification for expansion are returned in JSON format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the start time of the scale\-down operation arrives, the system will automatically scale the instance back to its original specification.</div><br> |
|RuleBeginTime |String |2026\-07\-23T00:00:00.000Z |Effective start time of scheduled scaling rules, formatted as yyyy\-MM\-dd HH:mm:ss (UTC).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the value of the <code>CyclePeriod</code> parameter is <code>ByDay</code>, <code>ByWeek</code>, or <code>ByMonth</code>.</div><br> |
|NodeIdsToOriginalSpec |JSON Map |{<br><br>"mysql\-8b56e2f0\*\*\*\*\-m\*\*\*\*\-0": "rds.mysql.c.s.1c2g",<br><br>"mysql\-8b56e2f0\*\*\*\*\-r\*\*\*\*": "rds.mysql.c.s.1c2g",<br><br>"mysql\-8b56e2f0\*\*\*\*\-s\*\*\*\*\-0": "rds.mysql.c.s.1c2g"<br><br>} |The Node IDs and original specifications of the nodes in the instance, in JSON format first.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the start time of the scale\-down operation arrives, the system will automatically scale the instance back to its original specification.</div><br> |


<span id="cycletimeinfo"></span>
### CycleTimeInfo


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|OnceTime |String |2026\-07\-23T13:03:00.000Z |Trigger time of the expansion operation, formatted as yyyy\-MM\-dd HH:mm:ss (UTC).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the value of the <code>CyclePeriod</code> parameter is <code>Once</code>.</div><br> |
|DayOfWeek |Integer |1 |Execution cycle of scaling operations; the valid value range for weekdays is `0~6`, where 0 stands for Sunday.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the value of the <code>CyclePeriod</code> parameter is <code>ByWeek</code>.</div><br> |
|TimeOfDay |Integer |3600 |The trigger time of expansion and scale\-down operations. The format is `1-24*3600`, and the unit is second. |
|DayOfMonth |Integer |10 |Execution cycle of scaling operations, which refers to the date of each month, with the value range `1~31`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is returned only when the value of the <code>CyclePeriod</code> parameter is <code>ByMonth</code>.</div><br> |


<span id="expandobservableautoscalingspecrule"></span>
### ExpandObservableAutoScalingSpecRule


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RuleId |String |rule\-b3b22c3c9xxxx |Rule ID for automatic expansion. |
|Enabled |Boolean |true |Indicates whether to enable automatic expansion rules. Values are as follows:<br><br><br>* `true`: Enabled.<br><br>* `false`: disable. |
|RuleType |String |PrimaryAndSecondary |Automatic expansion rule type. Values are as follows:<br><br><br>* `PrimaryAndSecondary`: Configure auto scaling rules only for primary and secondary nodes.<br><br>* `AllReadOnlyNodes`: Configure auto scaling rules for all read\-only nodes. |
|StopToSpec |String |rds.mysql.c.s.1c2g |Target node specification for the expansion. |
|ExcludeNodeIds |Array of String |mysql\-8b56e2fxxxx\-rxxxx |The read\-only node ID that is not checked for and does not trigger automatic expansion. |
|TriggerThreshold |Integer |90 |Average CPU utilization when the expansion operation is triggered. Value range: [50\-90]. |
|ObservationTimeDuration |Integer |300 |Duration for average CPU utilization exceeding the threshold when the expansion operation is triggered. The unit is seconds. Values are as follows:<br><br><br>* `300`<br><br>* `600`<br><br>* `1200`<br><br>* `1800`<br><br>* `2400`<br><br>* `3600` |


<span id="reduceobservableautoscalingspecrule"></span>
### ReduceObservableAutoScalingSpecRule


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|RuleId |String |rule\-b3b22c3c9xxxx |Rule ID for automatic scale\-down. |
|Enabled |Boolean |true |Indicates whether to enable automatic scale\-down rules. Values are as follows:<br><br><br>* `true`: Enabled.<br><br>* `false`: disable. |
|RuleType |String |PrimaryAndSecondary |Automatic scale\-down rule type. Values are as follows:<br><br><br>* `PrimaryAndSecondary`: Configure auto scaling rules only for primary and secondary nodes.<br><br>* `AllReadOnlyNodes`: Configure auto scaling rules for all read\-only nodes. |
|StopToSpec |String |rds.mysql.c.s.1c2g |Target node specification for scale\-down operations. |
|ExcludeNodeIds |Array of String |mysql\-8b56e2fxxxx\-rxxxx |The read\-only node ID that is not checked for and does not trigger automatic scale\-down. |
|TriggerThreshold |Integer |90 |Average CPU utilization when the scale\-down operation is triggered. Value range: [5~30]. |
|ObservationTimeDuration |Integer |300 |Duration for average CPU utilization exceeding the threshold when the scale\-down operation is triggered. The unit is seconds. Values are as follows:<br><br><br>* `300`<br><br>* `600`<br><br>* `1800`<br><br>* `3600`<br><br>* `7200`<br><br>* `10800`<br><br>* `86400`<br><br>* `604800` |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceHAConfig&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f83edc2e****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507241457515F39A06698620102A016-980eb2",
        "Action": "DescribeDBInstanceHAConfig",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AutoStorageScalingConfig": {
            "EnableStorageAutoScale": true,
            "ScalingDetectNode": "MasterNode",
            "StorageThreshold": 10,
            "StorageUpperBound": 3000
        },
        "DataSyncMode": "SemiSync",
        "Nodes": [
            {
                "CreateTime": "2025-07-23T03:40:54.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-f83edc2e****",
                "Memory": 1,
                "NodeId": "mysql-f83edc2e****-me954-0",
                "NodeSpec": "rds.mysql.d1.n.1c1g",
                "NodeStatus": "Running",
                "NodeType": "Primary",
                "RegionId": "cn-guangzhou",
                "ShardId": "",
                "SubInstanceId": "mysql-f83edc2e****-me954",
                "SyncDelay": 0,
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-guangzhou-a"
            },
            {
                "CreateTime": "2025-07-23T03:40:54.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-f83edc2e****",
                "Memory": 1,
                "NodeId": "mysql-f83edc2e****-s8e03-0",
                "NodeSpec": "rds.mysql.d1.n.1c1g",
                "NodeStatus": "Running",
                "NodeType": "Secondary",
                "RegionId": "cn-guangzhou",
                "ShardId": "",
                "SubInstanceId": "mysql-f83edc2e****-s8e03",
                "SyncDelay": 0,
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-guangzhou-a"
            },
            {
                "CreateTime": "2025-07-23T06:17:13.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-f83edc2e****",
                "Memory": 2,
                "NodeId": "mysql-f83edc2e****-r8386",
                "NodeSpec": "rds.mysql.d1.n.1c2g",
                "NodeStatus": "Running",
                "NodeType": "ReadOnly",
                "RegionId": "cn-guangzhou",
                "ShardId": "",
                "SubInstanceId": "mysql-f83edc2e****-r8386",
                "SyncDelay": 0,
                "UpdateTime": "",
                "VCPU": 1,
                "ZoneId": "cn-guangzhou-a"
            },
            {
                "CreateTime": "2025-07-24T06:06:31.000Z",
                "DelayReplicationTime": 0,
                "InstanceId": "mysql-f83edc2e****",
                "Memory": 4,
                "NodeId": "mysql-f83edc2e****-r9dcf",
                "NodeSpec": "rds.mysql.d1.n.2c4g",
                "NodeStatus": "Running",
                "NodeType": "ReadOnly",
                "RegionId": "cn-guangzhou",
                "ShardId": "",
                "SubInstanceId": "mysql-f83edc2e****-r4974",
                "SyncDelay": 0,
                "UpdateTime": "",
                "VCPU": 2,
                "ZoneId": "cn-guangzhou-a"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

---
title: "DescribePlannedEvents"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeplannedevents"
---

Call the DescribePlannedEvents API to query operation and maintenance events.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |No |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|BeginTime |String |No |2023\-08\-03T06:25:22Z |The start time of the event occurrence. Format: `yyyy-MM-dd HH:mm:ss`(UTC time). |
|EndTime |String |No |2023\-08\-12T06:25:34Z |The end time of the event occurrence. Format: `yyyy-MM-dd HH:mm:ss`(UTC time). |
|EventId |String |No |df078de739d3412aa430905bcd13\*\*\*\* |Event ID. |
|EventType |String[] |No |["VersionUpgrade"] |Event types. Values:<br><br><br>* `VersionUpgrade`: Version upgrade.<br><br>* `SSLCertificateUpdate`: SSL certificate update.<br><br>* `HostOffline`: Host maintenance.<br><br>* `NodeRebuild`: Node reconstruction.<br><br>* `StoppedDBInstanceRestart`: Recovery of a stopped database instance.<br><br>* `TemporaryScaleRevert`: Reversion of a temporary scale\-up. |
|Status |String[] |No |["Waiting"] |Event status. Valid values (multiple values can be selected):<br><br><br>* `Canceled`: Canceled.<br><br>* `Running_BeforeSwitch`: Running \- Before switchover.<br><br>* `WaitSwitch`: Pending switchover.<br><br>* `Running_Switching`: Running \- Switching.<br><br>* `Running_AfterSwitch`: Running \- After switchover.<br><br>* `Running`: Running.<br><br>* `Success`: Success.<br><br>* `Failed`: Failed.<br><br>* `Timeout`: Timeout.<br><br>* `Rollbacking`: Rolling back.<br><br>* `RollbackFailed`: Rollback failed.<br><br>* `Paused`: Paused.<br><br>* `Stopped`: Stopped.<br><br>* `Stopping`: Stopping.<br><br>* `WaitStart`: Not executed. |

## Response parameters

null

|Name |Type |Example |Description |
|---|---|---|---|
|Total |Integer |3 |Total number of planned events. |
|PlannedEvents |Object[] |Please refer to the response example. |Information about planned events. |
|BusinessImpact |String |Brief connection interruptions (lasting seconds) may occur during the switchover. It is recommended to configure automatic retry and reconnection mechanisms in your application to avoid business impact. |Impact of the event. |
|DBEngine |String |MySQL |Database engine, fixed value `MySQL`. |
|EventAction |String |RestartDBInstance |The specific operation interface name within the corresponding event type. For example, instance management includes creation, deletion, configuration change, restart, etc. |
|EventID |String |d64eda8b7f47414e95a4e4654032\*\*\*\* |Event ID. |
|EventName |String |This is an event name |Event name. |
|EventType |String |VersionUpgrade |Event type. |
|InstanceId |String |mysql\-5564bc65\*\*\*\* |Instance ID. |
|InstanceName |String |Test instance |Instance name. |
|MaxDelayTime |String |2024\-12\-18T15:03:05Z |Latest deferrable time. Format: `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|OriginBeginTime |String |2024\-12\-17T15:03:05Z |Originally scheduled start time. Format: `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|PlannedBeginTime |String |2024\-12\-18T14:48:00Z |Planned start time of execution. Format: `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|PlannedEndTime |String |2024\-12\-19T14:48:00Z |Planned end time of execution. Format: `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|PlannedEventDescription |String |upgrade instance to 2.10.2.28 |Description of the operation and maintenance event. |
|PlannedEventReason |String |Host hardware aging requires maintenance, or host module needs upgrade. |Reason for the event, helping you understand the cause of unexpected events. |
|PlannedSwitchBeginTime |String |2024\-12\-18T15:03:00Z |Planned start time of switchover. Format: `yyyy-MM-ddTHH:mm:ssZ`(UTC time). |
|PlannedSwitchEndTime |String |2024\-12\-19T15:03:00Z |Planned end time of switchover. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|Region |String |cn\-beijing |Region. |
|Status |String |Waiting |Event status.<br><br><br>* `Canceled`: Canceled.<br><br>* `Running_BeforeSwitch`: Running \- Before switchover.<br><br>* `WaitSwitch`: Pending switchover.<br><br>* `Running_Switching`: Running \- Switching.<br><br>* `Running_AfterSwitch`: Running \- After switchover.<br><br>* `Running`: Running.<br><br>* `Success`: Success.<br><br>* `Failed`: Failed.<br><br>* `Timeout`: Timeout.<br><br>* `Rollbacking`: Rolling back.<br><br>* `RollbackFailed`: Rollback failed.<br><br>* `Paused`: Paused.<br><br>* `Stopped`: Terminated.<br><br>* `Stopping`: Terminating.<br><br>* `WaitStart`: Not executed. |

## Sample request

```json
POST /?Action=DescribePlannedEvents&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "StartTime": "2024-01-08T06:00:00Z",
    "EndTime": "2024-01-15T06:00:00Z"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230810145403789088F993D213731417",
        "Action": "DescribePlannedEvents",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PlannedEvents": [
            {
                "BusinessImpact": "火山引擎数据库控制台实例列表页面会有短暂的状态展示延迟，不影响数据库使用",
                "DBEngine": "MySQL",
                "EventAction": "UpgradeResource",
                "EventID": "d64eda8b7f47414e95a4e46540320b70",
                "InstanceId": "mysql-5564bc65****",
                "InstanceName": "测试实例",
                "IsUrgent": true,
                "MaxDelayTime": "2024-02-02T15:10:00Z",
                "OriginBeginTime": "2024-01-02T15:10:00Z",
                "PlannedBeginTime": "2024-01-02T15:10:00Z",
                "PlannedEndTime": "2024-01-02T15:59:00Z",
                "PlannedEventDescription": "upgrade instance to 2.10.2.28",
                "PlannedEventReason": "instance version upgrade",
                "Region": "ap-southeast-1",
                "Status": "Initiated"
            }
        ],
        "Total": 1
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

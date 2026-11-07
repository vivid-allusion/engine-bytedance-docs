---
title: "DescribePlannedEvents"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribePlannedEvents"
---

Call the DescribePlannedEvents API to query the operation and maintenance events in the current region.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceName |String |No |Test instance |Storage type. |
|InstanceId |String |No |postgres\-a2f9831f\*\*\*\* |Instance ID. |
|EventId |String |No |61c7adeb0f49426ab032cb8cf1e2\*\*\*\* |Event ID. |
|EventType |Array of String |No |["VersionUpgrade"] |Event type. Value range (multiple values allowed):<br><br><br>* `VersionUpgrade`: version upgrade<br><br>* h`HostOffline`: Host offline. |
|Status |Array of String |No |["WaitStart"] |State of operation and maintenance events. Value range (multiple values allowed):<br><br><br>* `Canceled`: cancelled.<br><br>* `WaitStart`: waiting for execution.<br><br>* `WaitSwitch`: to be switched.<br><br>* `Running`: running.<br><br>* `Running_BeforeSwitch`: running \- before switching.<br><br>* `Running_Switching`: running \- switching.<br><br>* `Running_AfterSwitch`: running \- after switching.<br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `Timeout`: timeout.<br><br>* `Rollbacking`: rolling back.<br><br>* `RollbackFailed`: failed to rollback. |
|PlannedBeginTimeSearchRangeStart |String |No |2025\-09\-01T02:06:53.000Z |Start time of the time range when querying events by planned execution time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PlannedBeginTimeSearchRangeEnd |String |No |2025\-09\-01T17:40:53.000Z |End time of the time range when querying events by planned execution time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">PlannedBeginTimeSearchRangeEnd should be later than PlannedBeginTimeSearchRangeStart.</div><br><br><br>* <div data-tips="true" data-tips-type="default">PlannedBeginTimeSearchRangeStart and PlannedBeginTimeSearchRangeEnd define a time range. When an event meets the condition that its “planned execution time” falls within this range, the event will be retrieved and returned.</div><br> |
|PlannedSwitchTimeSearchRangeStart |String |No |2025\-09\-01T18:17:28.000Z |Start time of the time range when querying events by scheduled switching time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PlannedSwitchTimeSearchRangeEnd |String |No |2025\-09\-01T18:47:28.000Z |End time of the time range when querying events by scheduled switching time. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). PlannedSwitchTimeSearchRangeStart and PlannedSwitchTimeSearchRangeEnd define a time range. When the scheduled switching time period of an event overlaps with the range of the time period, the event will be returned. |
|PageNumber |Integer |No |2 |The query offset of the current page. The default value is 1. |
|PageSize |Integer |No |20 |The number of records on each page. The value must be greater than 0 and no more than 1,000. The default value is 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |4 |Total number of operation and maintenance events. |
|PlannedEvents |Array of [PlannedEvent](https://docs.byteplus.com/en/docs/61/45566#plannedevent) |Refer to the sample response. |The list of operation and maintenance events in the current region under the current query conditions. |


<span id="plannedevent"></span>
### PlannedEvent


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BusinessImpact |String |The connection may be broken in seconds during the switching process. It is recommended that the program set an automatic retry and reconnect mechanism to avoid the impact of the event. |Impact of operation and maintenance events on business. |
|EventID |String |61c7adeb0f49426ab032cb8cf1e2ca83 |ID of the operation and maintenance events. |
|EventType |String |VersionUpgrade |Operation and maintenance event type. Range:<br><br><br>* `VersionUpgrade`: version upgrade<br><br>* h`HostOffline`: Host offline. |
|InstanceId |String |postgres\-a2f9831f\*\*\*\* |ID of the operation and maintenance event instance. |
|InstanceName |String |Test instance |Name of the operation and maintenance event instance. |
|MaxDelayTime |String |2025\-07\-30T20:00:00.000Z |Latest postponed time of operation and maintenance events. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PlannedBeginTime |String |2025\-09\-01T17:43:09.000Z |Start time of the operation and maintenance event. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PlannedEventReason |String |Instance version routine upgrade and iteration, fixing known issues and releasing new features. |Reason for initiating operation and maintenance events. Values are:<br><br><br>* Instance version routine upgrade and iteration, fixing known issues and releasing new features.<br><br>* Host operation and maintenance is initiated for hardware maintenance on the host machine of the instance due to hardware aging, abnormality, or the need to upgrade the host module. |
|PlannedSwitchBeginTime |String |2025\-09\-01T18:00:23.000Z |Start time of operation and maintenance events plan switching. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|PlannedSwitchEndTime |String |2025\-09\-01T18:30:23.000Z |End time of the scheduled switching for operation and maintenance events. Format: `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time). |
|Region |String |cn\-beijing |Region ID. |
|Status |String |WaitStart |State of operation and maintenance events. Values are as follows:<br><br><br>* `Canceled`: cancelled.<br><br>* `WaitStart`: waiting for execution.<br><br>* `WaitSwitch`: to be switched.<br><br>* `Running`: running.<br><br>* `Running_BeforeSwitch`: running \- before switching.<br><br>* `Running_Switching`: running \- switching.<br><br>* `Running_AfterSwitch`: running \- after switching.<br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `Timeout`: timeout.<br><br>* `Rollbacking`: rolling back.<br><br>* `RollbackFailed`: failed to rollback. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribePlannedEvents&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025031921035852D25471A9CB03E58270-2c52e4",
        "Action": "DescribePlannedEvents",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "PlannedEvents": [
            {
                "BusinessImpact": "切换过程会可能有秒级连接闪断，建议程序设置自动重试重连机制以避免事件影响。",
                "EventID": "01ba7dca897b46b5b352cba1e286b1c8",
                "EventType": "VersionUpgrade",
                "InstanceId": "postgres-fdc70683****",
                "InstanceName": "",
                "MaxDelayTime": "2025-07-30T20:00:00.000Z",
                "PlannedBeginTime": "2025-09-01T18:06:53.000Z",
                "PlannedEventReason": "实例版本例行升级迭代, 修复已知问题和发布新特性。",
                "PlannedSwitchBeginTime": "2025-09-01T18:17:28.000Z",
                "PlannedSwitchEndTime": "2025-09-01T18:47:28.000Z",
                "Region": "cn-beijing",
                "Status": "WaitStart"
            },
            {
                "BusinessImpact": "切换过程会可能有秒级连接闪断，建议程序设置自动重试重连机制以避免事件影响。",
                "EventID": "2420468b1ddd4a1782d2dc3e2945f107",
                "EventType": "VersionUpgrade",
                "InstanceId": "postgres-09631f39****",
                "InstanceName": "",
                "MaxDelayTime": "2025-07-31T20:00:00.000Z",
                "PlannedBeginTime": "2025-09-01T18:04:48.000Z",
                "PlannedEventReason": "实例版本例行升级迭代, 修复已知问题和发布新特性。",
                "PlannedSwitchBeginTime": "2025-09-01T18:13:12.000Z",
                "PlannedSwitchEndTime": "2025-09-01T18:43:12.000Z",
                "Region": "cn-beijing",
                "Status": "WaitStart"
            }
        ],
        "Total": 2
    }
}
```

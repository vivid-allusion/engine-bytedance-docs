---
title: "DescribePlannedEvents"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeplannedevents"
---

Call the DescribePlannedEvents API to query scheduled events of the target Redis instance within a specified time range.

## Request type

Synchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePlannedEvents&serviceCode=Redis&version=2020-12-07&groupName=事件管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |1 |Page number of the planned event list. The value ranges from 1 to the maximum value of the Integer data type. |
|PageSize |Integer |Yes |10 |Number of records per page. An integer with a value between 1 and 1000. |
|InstanceId |String |No |redis\-cn0212gzmh2xsbelz |Instance ID. Fuzzy query.<br><br>> **tip**<br><br><br><br>* > If this parameter is blank, you cannot filter by the instance ID.<br><br><br>* > Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|MinStartTime |String |No |2025\-02\-26T19:00:00Z |The earliest execution time of the scheduled event to be queried. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> If this parameter is left blank, it means that the earliest planned execution time will not be used for filtering.<br> |
|MaxStartTime |String |No |2025\-02\-26T19:01:00Z |The latest execution time for the scheduled event to be queried. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > If this parameter is left empty, the latest scheduled execution time will not be used for filtering.<br><br><br>* > The query end time must be later than the start time.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|PlannedEvents |Array of [PlannedEventInfo](https://docs.byteplus.com/en/docs/55/40223#plannedeventinfo) |Refer to the Sample response. |List of planned event information |
|Total |Integer |1 |Total number of scheduled events. |

### PlannedEventInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Action |String |ModifyDBInstanceAZConfigure |Operation action. |
|ActionName |String |Upgrade kernel version |Event action name. |
|CanCancel |Boolean |false |Whether the current event can be canceled. Valid values:<br><br><br>* `true`: Can be canceled.<br><br>* `false`: Cannot be canceled.<br><br><br>> **tip**<br><br><br>> For more details about canceling scheduled events, see [Canceling planned event](https://docs.byteplus.com/en/docs/redis/cancel-planned-event).<br> |
|CanModifyTime |Boolean |false |Whether the current event allows postponing its execution time. Valid values:<br><br><br>* `true`: Can be postponed.<br><br>* `false`: Cannot be postponed.<br><br><br>> **tip**<br><br><br>> For more details about postponing event execution time, see [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time).<br> |
|EventId |String |event\-cn0212gzmh2xsbelz |Event ID. |
|ExeEndTime |String |2026\-08\-24T18:35:08Z |The actual end time of the event, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> Returns empty if the event is not executed.<br> |
|ExeStartTime |String |2026\-08\-24T18:25:21Z |The actual start time of the event, in the format of `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br>> Returns empty if the event is not executed.<br> |
|ImpactSummary |Object of [ImpactSummary](https://docs.byteplus.com/en/docs/55/40223#impactsummary) |Refer to the Sample response. |The scope(number of nodes) of primary nodes, secondary nodes, and proxy nodes affected by the event. |
|InstanceId |String |redis\-cn0212gzmh2xsbelz |Instance ID of the current event. |
|InstanceName |String |test |Instance name. |
|MaxEndTime |String |null |The latest postponable time for the current event.<br><br>> **tip**<br><br><br>> This parameter is returned only if the event can be postponed (i.e., when `CanModifyTime` is `true`).<br> |
|PlanEndTime |String |2025\-02\-26T19:59:59Z |Latest planned execution time for the event. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|PlanStartTime |String |2025\-02\-26T19:00:00Z |The event's earliest planned execution time. The format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|Status |String |Waiting |Event state. Valid values:<br><br><br>* `Waiting`: Waiting for execution.<br><br>* `Running`: In progress.<br><br>* `Success`: Successful.<br><br>* `Failed`: Failed.<br><br>* `Canceled`: Canceled. |
|Type |String |SystemMaintenance |Event type. Valid values:<br><br><br>* `SystemMaintenance`: System maintenance.<br><br>* `UserOperation`: User operation. |

### ImpactSummary

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NotGenerated |Boolean |false |Whether impact has been generated for the event. Values:<br><br><br>* `true`: Not generated.<br><br>* `false`: Generated.<br><br><br>> **tip**<br><br><br>> Impact is generated only for scheduled events with the event type “System maintenance”.<br> |
|PrimaryCount |Integer |0 |Number of affected primary nodes. |
|ProxyCount |Integer |2 |Number of affected proxy nodes. |
|SecondaryCount |Integer |0 |Number of affected secondary nodes. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribePlannedEvents&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "PageNumber": 1,
    "PageSize": 10,
    "InstanceId": "redis-cn0212gzmh2xsbelz",
    "MinStartTime": "2025-02-26T19:00:00Z",
    "MaxStartTime": "2025-02-26T19:01:00Z"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePlannedEvents",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "PlannedEvents": [
{
                "Action": "ModifyInstanceProxySpec",
                "ActionName": "维护",
                "BusinessImpact": "",
                "CanCancel": true,
                "CanModifyTime": true,
                "Description": "实例系统维护",
                "EventId": "event-cq01ojqnj86l****",
                "ExeEndTime": "2026-09-19T04:21:55Z",
                "ExeStartTime": "2026-09-19T04:19:55Z",
                "ImpactSummary": {
                    "NotGenerated": false,
                    "PrimaryCount": 0,
                    "ProxyCount": 2,
                    "SecondaryCount": 0
                },
                "InstanceId": "redis-cq01zxtvwojju****",
                "InstanceName": "ao023-owned-c",
                "MaxEndTime": "2026-09-21T05:18:59Z",
                "MinStartTime": "2026-09-19T04:01:54Z",
                "PlanEndTime": "2026-09-19T05:18:59Z",
                "PlanStartTime": "2026-09-19T04:19:00Z",
                "Reason": "instance maintenance",
                "Status": "Success",
                "Type": "SystemMaintenance"
            }
        ],
        "Total": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

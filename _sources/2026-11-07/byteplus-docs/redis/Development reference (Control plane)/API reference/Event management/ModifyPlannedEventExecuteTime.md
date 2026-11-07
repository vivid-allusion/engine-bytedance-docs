---
title: "ModifyPlannedEventExecuteTime"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifyplannedeventexecutetime"
---

Call the ModifyPlannedEventExecuteTime API to modify the execution time of planned system maintenance events.

## Request type

Synchronous request.

## Precautions

* The status of a scheduled maintenance event changes to **In progress** once execution starts. Instance node switchover may occur during the maintenance event execution process, which may result in second\-long non\-writability or temporary disconnections. Please ensure that your services operate with an automatic reconnection mechanism. For more information on supported event operations and their impact on your services, see [Event types and operation impacts](https://docs.byteplus.com/en/docs/redis/event-center).

* Before the scheduled maintenance event is executed, its status is shown as **Waiting for execution**. Normal data access to the database will not be affected.

* After the scheduled maintenance event is completed, the instance's address and access method remain the same as the source instance. The instance's network configuration will not change, and migration tasks will not be affected by maintenance events.

* Redis does not limit the number of operations to defer execution time, but each deferred execution time must be later than the end time of the previous scheduled execution and earlier than the latest deferrable time. For more details, refer to [Modifying execution time](https://docs.byteplus.com/en/docs/redis/postpone-execution-time).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyPlannedEventExecuteTime&serviceCode=Redis&version=2020-12-07&groupName=事件管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EventIds |Array of String |Yes |["event\-cn0212gzmh2xs\*\*\*\*"] |The ID of the scheduled event whose execution time needs to be modified. Only scheduled events with `CanModifyTime` set to `true` allow modification of their execution time.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) API to query scheduled event information for the target Redis instance within a specified time range, including whether execution time can be modified and the event ID.<br> |
|TargetStartTime |String |Yes |2025\-05\-13T19:00:00Z |Modified schedule start time, in the format of `yyyy-MM-ddTHH: mm: ssZ` (UTC). |
|TargetEndTime |String |Yes |2025\-05\-23T19:59:59Z |Modified scheduled end time, in `yyyy-MM-ddTHH:mm:ssZ` (UTC) format.<br><br>> **tip**<br><br><br>> The planned end time must be later than the planned start time but earlier than the latest postponable time allowed for the current event. You can call the [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) API to query planned event information for the target Redis instance within a specified time period, including the latest postponable time (the value of `MaxEndTime` in the returned result).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyPlannedEventExecuteTime&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "EventIds": [
        "event-cn0212gzmh2xs****"
    ],
    "TargetStartTime": "2025-05-13T19:00:00Z",
    "TargetEndTime": "2025-05-23T19:59:59Z"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyPlannedEventExecuteTime",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

---
title: "ExecutePlannedEvent"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/executeplannedevent"
---

Call the ExecutePlannedEvent API to immediately execute the scheduled event.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ExecutePlannedEvent&serviceCode=Redis&version=2020-12-07&groupName=事件管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EventId |String |Yes |event\-cn0212gzmh2xs\*\*\*\* |Event ID of the scheduled event to be executed immediately. Only scheduled events with the status 'Waiting for execution' (i.e., `Status` is `Waiting`) can be executed immediately.<br><br>> **tip**<br><br><br>> You can call the [DescribePlannedEvents](https://docs.byteplus.com/en/docs/redis/describeplannedevents) API to query the scheduled event information of the target Redis instance for a specified time period, including event ID and event status.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ExecutePlannedEvent&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "EventId": "event-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ExecutePlannedEvent",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

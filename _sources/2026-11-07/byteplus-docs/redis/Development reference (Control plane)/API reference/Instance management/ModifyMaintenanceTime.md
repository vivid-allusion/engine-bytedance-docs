---
title: "ModifyMaintenanceTime"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifymaintenancetime"
---

Call the ModifyMaintenanceTime API to modify the maintenance period of target Redis instance.

## Request type

Synchronous request.

## Precautions

* If the relevant operations listed in [Application scenarios](https://docs.byteplus.com/en/docs/redis/set-maintenance-period) are performed within the maintenance period, the instance may experience a brief connection interruption. It is recommended to set the maintenance period during the off\-peak hours of the business and ensure that the application has an automatic reconnection mechanism. For more details, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).

* **If you choose to perform some database O&M operations (such as ** **`changing configuration`** **) within the maintenance period, the instance status will immediately change (for example, to Configuration modifying) and this status will persist until the task is complete, but the actual execution time of the operation task will still be within the maintenance period.**

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyMaintenanceTime&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|TimeScope |String |Yes |00:00\-01:59 |Set the instance's maintenance period range, formatted as `HH:mm-HH:mm` (UTC+8).<br><br>> **tip**<br><br><br><br>* > Within the provided maintenance period range, the `mm` for the start time must be `00`, and the `mm` for the end time must be `59`. e.g., you can set the maintenance period to `00:00-01:59.`<br><br><br>* > To ensure tasks proceed normally within the maintenance period, the duration of the maintenance period must be between 2 and 24 hours.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyMaintenanceTime&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "TimeScope": "00:00-01:59"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyMaintenanceTime",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

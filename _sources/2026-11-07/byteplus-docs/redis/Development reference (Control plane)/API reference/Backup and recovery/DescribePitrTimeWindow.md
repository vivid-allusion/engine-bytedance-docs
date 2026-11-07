---
title: "DescribePitrTimeWindow"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describepitrtimewindow"
---

Call the DescribePitrTimeWindow API to query the recoverable time range supported by the target Redis instance for point\-in\-time recovery.

## Request type

Synchronous request.

## Prerequisites

The target instance has enabled the Data flashback feature. You can call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to enable the data flashback function.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery\-related actions and do not support calling this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePitrTimeWindow&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|StartTime |String |2022\-11\-24T08:07:01 |The supported recoverable start time (UTC) when restoring data to a specific point in time. |
|EndTime |String |2022\-11\-24T08:07:29Z |The supported recoverable end time (UTC) when restoring data by point\-in\-time. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribePitrTimeWindow&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022112411414201022514515203F7xxxx",
        "Action": "DescribePitrTimeWindow",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "EndTime": "2022-11-24T03:41:42Z",
        "StartTime": "2022-11-24T03:39:02Z"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

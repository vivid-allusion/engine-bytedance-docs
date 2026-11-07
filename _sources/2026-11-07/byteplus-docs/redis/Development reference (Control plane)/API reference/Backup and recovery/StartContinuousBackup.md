---
title: "StartContinuousBackup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/startcontinuousbackup"
---

Call the StartContinuousBackup API to enable data flashback for target Redis instance.

## Request type

Synchronous request.

## Precautions

* Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery\-related actions and do not support calling this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* After enabling the flashback feature, the system requires some time to perform a full backup. The duration of the backup depends on the data volume. After enabling the data flashback feature, it is recommended to wait for a while until the full backup is completed before using the point\-in\-time recovery feature.

* The recoverable time range is between the time when the data flashback feature is enabled and the current time, with the earliest recovery point being 7 days before the current time.

   Examples are as follows:

   * If the current time is `2024-01-18 06:00:00` and Data flashback was enabled at `2024-01-10 10:00:00`, then the recoverable time range is `2024-01-11 06:00:00 ~ 2024-01-18 06:00:00`.

   * If the current time is `2024-01-18 06:00:00` and the data flashback feature was enabled at `2024-01-12 10:00:00`, then the recoverable time range is `2024-01-12 10:00:00 ~ 2024-01-18 06:00:00`.

* After enabling data flashback, certain operations may affect the data flashback feature, including:

   * Performing operations such as [Modifying instance configuration](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification), [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az), or system maintenance (for example, upgrading kernel version, hardware/software, network, etc.) will cause the data flashback feature to **automatically disable**. After the data flashback feature is disabled, previous flashback points will no longer be retained.

      > Description

> Cache for Redis provides events feature that supports system maintenance operations such as hardware, software, or network upgrades on machines hosting specified instances through planned events, ensuring the stability and sustainability of the cloud database service. For more details, refer to [Events](https://docs.byteplus.com/en/docs/redis/event-center).

   * Performing [Restore to original instance by backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set) or [Restore to original instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point) operations will cause the Data flashback feature to **first automatically disable and then re\-enable**. After the Data flashback feature is reopened, the recoverable time point will start from the time point when the restore to original instance operation is completed.

* Cache for Redis supports configuring the Append only file persistence feature through the `appendonly-switch` parameter, but there is a constraint relationship between the AOF feature and the [Data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback) feature, where:

   * When the `appendonly-switch` parameter is set to `off`, the data flashback feature cannot be enabled.

   * When the data flashback feature is enabled, the `appendonly-switch` parameter cannot be adjusted to `off`.

      For more details about the `appendonly-switch` parameter, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=StartContinuousBackup&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xsh2xs |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=StartContinuousBackup&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn0212gzmh2xsh2xs"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022112411414201022514515203F703F7",
        "Action": "StartContinuousBackup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

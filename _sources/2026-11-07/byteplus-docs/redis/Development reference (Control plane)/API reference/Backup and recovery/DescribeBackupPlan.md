---
title: "DescribeBackupPlan"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describebackupplan"
---

Call the DescribeBackupPlan API to query the automatic backup policy of the target Redis instance, including the backup type, backup cycle, and expected time of the next backup.

## Request type

Synchronous request.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackupPlan&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Active |Boolean |true |Whether to enable automatic backup. Valid values:.<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |
|BackupHour |Integer |5 |The time period for starting backup (UTC+8). The value can be any integer from 0 to 23. `0` indicates that the system will perform the backup between `00:00~00:59`, `1` indicates it will perform the backup between `01:00~01:59`, and so on. |
|BackupType |String |Full |Restore method. Valid values:<br><br><br>* `Full`: full recovery, that is, restore by backup set.<br><br>* `Inc`: incremental recovery, i. e., recovery based on a specific point in time. |
|ExpectNextBackupTime |String |2024\-07\-10T20:20:20Z |Expected time for next backup, the format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|LastUpdateTime |String |2024\-07\-10T00:00:00Z |Time of last backup policy modification, the format is `yyyy-MM-ddTHH:mm:ssZ` (UTC). |
|Period |Array of Integer |[1,2,3,4,5,6,7] |Backup cycle. Value range: any integer between 1 and 7. Where, `1` indicates a backup on Monday, `2` indicates a backup on Tuesday, and so on. |
|TTL |Integer |7 |Backup retention period, in days. Default value: 7 days. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeBackupPlan&Version=2020-12-07 HTTP/1.1
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
        "RequestId": "202204151618440102121681030A63xxxx",
        "Action": "DescribeBackupPlan",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "Active": true,
        "BackupHour": 5,
        "BackupType": "Full",
        "ExpectNextBackupTime": "2024-07-10T20:20:20Z",
        "InstanceId": "redis-cn0212gzmh2xs****",
        "LastUpdateTime": "2024-07-10T00:00:00Z",
        "Period": [
        		1, 
            2, 
            3, 
            4, 
            5, 
            6, 
            7
        ],
        "TTL": 7
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

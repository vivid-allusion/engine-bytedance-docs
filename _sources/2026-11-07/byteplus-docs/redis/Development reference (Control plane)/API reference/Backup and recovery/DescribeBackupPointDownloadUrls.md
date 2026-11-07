---
title: "DescribeBackupPointDownloadUrls"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describebackuppointdownloadurls"
---

Call the DescribeBackupPointDownloadUrls API to query the download address of the specified backup file in the target Redis instance.

## Request type

Synchronous request.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBackupPointDownloadUrls&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|BackupPointId |String |Yes |b\-cn02wp9k2wlw9z9gzl76n2vd\*\*\*\* |Backup ID of the target backup file.<br><br>> **tip**<br><br><br>> You can call the [DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) API to view the list of backup set information for a specified instance, including the backup ID information for each backup file.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID. |
|ShardNumber |Integer |1 |Total number of shards in the instance. |
|BackupPointDownloadUrls |Array of [BackupPointDownloadUrl](https://docs.byteplus.com/en/docs/55/12501#backuppointdownloadurl) | |Download address information for the backup file at the current backup point. |

### BackupPointDownloadUrl

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ShardId |String |server\-redis\-cn0212gzmh2xs\*\*\*\*\-0 |Shard ID of the RDB file. |
|RdbFileSize |Long |8359 |Redis Database file size, unit: Byte. |
|PublicDownloadUrl |String |http://redis\-dts\-beijing.volces.com/bytedance.redis.redis\-cn0212gzmh2xs\*\*\*\*/20221226182521/0/20221226182521/0.rdb?\*\*\*\* |Public network download URL of the RDB file. |
|PrivateDownloadUrl |String |http://redis\-dts\-beijing.ivolces.com/bytedance.redis.redis\-cn0212gzmh2xs\*\*\*\*/20221226182521/0/20221226182521/0.rdb?\*\*\*\* |The private network download address for the RDB file. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeBackupPointDownloadUrls&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn0212gzmh2xs****",
    "BackupPointId":"b-cn02xmmrp751i9cdzcphjmk4****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221226190044FC2ED3F63B861BF6xxxx",
        "Action": "DescribeBackupPointDownloadUrls",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupPointDownloadUrls": [
            {
                "PrivateDownloadUrl": "http://redis-dts-beijing.ivolces.com/bytedance.redis.redis-cn0212gzmh2xs****/20221226182521/0/20221226182521/0.rdb?****",
                "PublicDownloadUrl": "https://redis-dts-beijing.volces.com/bytedance.redis.redis-cn0212gzmh2xs****/20221226182521/0/20221226182521/0.rdb?****",
                "RdbFileSize": 8359,
                "ShardID": "server-redis-cn0212gzmh2xs****-0"
            }
        ],
        "InstanceId": "redis-cn0212gzmh2xs****",
        "ShardNumber": 1
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

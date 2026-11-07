---
title: "CreateBackup"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createbackup"
---

Call the CreateBackup API to create backup manually for a specified Redis instance.

## Request type

Asynchronous request.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateBackup&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn02aqusft7ws\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|BackupPointName |String |No |testbackup |Set a backup name for manually created backups. To set a backup name, it must meet all of the following conditions:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br>> If no backup name is set, the backup ID generated when the backup task was created will be used by default.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |redis\-cn02aqusft7ws\*\*\*\* |Instance ID. |
|BackupPointId |String |b\-cn02xmmrp751i9cdzcphjmk4\*\*\*\* |The backup ID generated when creating a backup task. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateBackup&Version=2020-12-07 HTTP/1.1
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
        "RequestId": "202207271102110102252431250149xxxx",
        "Action": "CreateBackup",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "BackupPointId": "b-cn02xmmrp751i9cdzcphjmk4****",
        "InstanceId": "redis-cn02aqusft7ws****"
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

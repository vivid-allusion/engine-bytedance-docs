---
title: "ModifyBackupPlan"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifybackupplan"
---

Call the ModifyBackupPlan API to modify the automatic backup settings of specified Redis instance, including backup cycle, automatic backup enable or disable, and other settings.

## Request type

Synchronous request.

## Precautions

Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBackupPlan&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|Active |Boolean |No |true |Whether to enable automatic backup. Valid values:<br><br><br>* `false` (Default): Do not enable.<br><br>* `true`: Enable. |
|Period |Array of Integer |No |[1, 2, 3, 4, 5, 6, 7] |Backup cycle. Value range: any integer between 1 and 7. Where, 1 indicates a backup on Monday, 2 indicates a backup on Tuesday, and so on.<br><br>> **tip**<br><br><br>> When automatic backup is enabled (`Active` is `true`), this parameter is required.<br> |
|BackupHour |Integer |No |7 |Set the start time for backup execution (UTC+8). Value range: Any integer between 0 and 23. Where, `0` indicates the system will perform a backup within the `00:00~00:59` period, `1` indicates it will perform a backup within the `01:00~01:59` period, and so on.<br><br>> **tip**<br><br><br>> When automatic backup is enabled (`Active` is `true`), this parameter is required.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyBackupPlan&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"Period": [1, 2, 3, 4, 5, 6, 7],
	"BackupHour": 7,
	"Active": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022041516250701020405722002631111",
        "Action": "ModifyBackupPlan",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

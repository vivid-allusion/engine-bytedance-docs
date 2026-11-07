---
title: "RestoreDBInstance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/restoredbinstance"
---

Call the RestoreDBInstance API to restore the data in a backup set to the original Redis instance.

## Request type

Asynchronous request.

## Precautions

* Only primary\-secondary instances (i.e., where `InstanceClass` is `PrimarySecondary`) support calling this API. Single node instances (i.e., where `InstanceClass` is `Standalone`) do not support backup and recovery operations and cannot call this API. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* After enabling data flashback, restoring to the original instance results in **automatic shut\-off and restart of data flashback**. After enabling data flashback again, recoverable point in times start from the time when the original instance is restored. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestoreDBInstance&serviceCode=Redis&version=2020-12-07&groupName=备份恢复)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|BackupType |String |No |Full |Restore method. Valid values:<br><br><br>* `Full` (default): Select a backup file with backup type `Full` (i.e., full backup) for recovery, restoring from the backup set.<br><br>* `Inc`: Select a backup file with backup type `Inc` (i.e., incremental backup) for recovery, meaning point\-in\-time recovery.<br><br><br>> **tip**<br><br><br><br>* > If you need to restore by point in time (i.e., `BackupType` is `Inc`), you must first turn on the Data flashback feature. For more details, see [Restore to original instance by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point#.5oGi5aSN5Yiw5Y6f5a6e5L6L).<br><br><br>* > You can call the [StartContinuousBackup](https://docs.byteplus.com/en/docs/redis/startcontinuousbackup) API to turn on the Data flashback feature for the specified instance.<br> |
|TimePoint |String |No |2021\-11\-09T06:07:26Z |Used to specify the point in time for point\-in\-time recovery, in the format `yyyy-MM-ddTHH:mm:ssZ` (UTC).<br><br>> **tip**<br><br><br><br>* > This parameter is required when selecting to restore by point\-in\-time (i.e., when `BackupType` is `Inc`).<br><br><br>* > You can call the [DescribePitrTimeWindow](https://docs.byteplus.com/en/docs/redis/describepitrtimewindow) API to query the supported recoverable time range for a specified instance.<br> |
|BackupPointId |String |No |b\-cnlfs97a4tuhjxguaffl7qu81111 |Backup ID, used to specify the backup when restoring by backup set.<br><br>> **tip**<br><br><br><br>* > This parameter is required when selecting to restore by backup set (i.e., when `BackupType` is `Full`).<br><br><br>* > You can call the [DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) API to query all backup information for the specified instance, including the backup ID (i.e., the value of `BackupPointId` in the returned parameters).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=RestoreDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"TimePoint": "2021-11-09T14:07:26Z"
        "BackupType": "Inc"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022041517560801021204519716631111",
        "Action": "RestoreDBInstance",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=RestoreDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"BackupType": "Full",
	 "BackupPointId": "b-cnlfs97a4tuhjxguaffl7qu81111"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022041517560801021204519716631111",
        "Action": "RestoreDBInstance",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

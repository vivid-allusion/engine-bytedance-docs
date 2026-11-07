---
title: "DeleteBlueGreenDeployment"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deletebluegreendeployment"
---

Call the DeleteBlueGreenDeployment API to cancel the blue\-green deployment task for the target Redis instance.

## Request type

Asynchronous request.

## Precautions

* You can cancel the blue\-green deployment task only when the blue\-green deployment enters the states of **Data synchronizing**, **Switchable**, **Waiting for switch**, or **Switch failed** (that is, the `Status` is `DATA_SYNCHRONIZING`, `SWITCHOVER_AVAILABLE`, `SWITCHOVER_PENDING`, or `SWITCHOVER_FAILED`). For more information about the blue\-green deployment status, refer to [Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA).

* After you call the DeleteBlueGreenDeployment API to cancel the upgrade, the blue instance and green instance in the blue\-green deployment no longer have a synchronization or association relationship, and are converted into regular instances while retaining their existing configurations. We recommend that you promptly delete the green instance to avoid resource waste. For specific procedures, refer to [Deleting pay-as-you-go instance](https://docs.byteplus.com/en/docs/redis/delete-instance).

* After issue is resolved, you can re\-initiate a major version upgrade task for instance. For more details, refer to [Upgrading major versions using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment?lang=en&type=preview).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteBlueGreenDeployment&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|SourceInstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the source instance (i.e., the blue instance).<br><br>> **tip**<br><br><br>> Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CreateTime |String |2026\-01\-15 12:57:12 |Blue\-green deployment creation time, in the format `yyyy-MM-dd HH:mm:ss`. |
|DataSyncProgress |Double |99 |Data synchronization progress, in percentage (%), with a range of 0\-100. |
|EndTime |String |2026\-01\-15 14:37:00 |Blue\-green deployment end time. The format is `yyyy-MM-dd HH:mm:ss`.<br><br>> **tip**<br><br><br>> This field is returned only when the blue\-green deployment status is `DELETE_COMPLETED` or `SWITCHOVER_COMPLETED`.<br> |
|Name |String |upgradeversion |Blue\-green deployment name. |
|SourceEngineVersion |String |5.0 |Database version number for the blue instance. |
|SourceInstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the blue instance. |
|SourceInstanceName |String |upgradeversion |Instance name of the blue instance. |
|Status |String |SWITCHOVER_AVAILABLE |Blue\-green deployment status. For more information on blue\-green deployment status, refer to <br><br>[Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA). |
|TargetEngineVersion |String |7.0 |Database version for green instances. |
|TargetInstanceId |String |redis\-cn01y2c6v6y6m\*\*\*\* |Instance ID of the green instance. |
|TargetInstanceName |String |redistest\-green |Instance name of the green instance. |

## Example

### Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteBlueGreenDeployment&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "SourceInstanceId": "redis-cn0212gzmh2xs****"
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "DeleteBlueGreenDeployment",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
            "Name": "upgradeversion",
            "Status": "SWITCHOVER_AVAILABLE",
            "EndTime": "2026-01-15 14:37:00",
            "CreateTime": "2026-01-15 12:57:12",
            "DataSyncProgress": 99,
            "SourceInstanceId": "redis-cn0212gzmh2xs****",
            "TargetInstanceId": "redis-cn01y2c6v6y6m****",
            "SourceInstanceName": "upgradeversion",
            "TargetInstanceName": "redistest-green",
            "SourceEngineVersion": "5.0",
            "TargetEngineVersion": "7.0"
    }
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).

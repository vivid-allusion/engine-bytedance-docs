---
title: "DescribeBlueGreenDeployments"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describebluegreendeployments"
---

Call the DescribeBlueGreenDeployments API to query blue\-green deployment task details for target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBlueGreenDeployments&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |The instance ID of the blue or green instance for which a blue\-green deployment task has been created.<br><br>> **tip**<br><br><br>> Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|ExcludeCompleted |Boolean |No |false |Whether to query blue\-green deployment tasks that are already in a completed status (including switchover completed `SWITCHOVER_COMPLETED` and deletion completed `DELETE_COMPLETED`). Valid values:<br><br><br>* `false` (default): Do not query.<br><br>* `true`: Query. |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|BlueGreenDeployments |Array of [BlueGreenDeployment](https://docs.byteplus.com/en/docs/55/84491#bluegreendeployment) |Refer to the Sample response. |Blue\-green deployment information list. |

### BlueGreenDeployment

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |upgradeversion |Blue\-green deployment name. |
|Status |String |SWITCHOVER_AVAILABLE |Blue\-green deployment status. For more information about the blue\-green deployment status, refer to [Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA). |
|CreateTime |String |2026\-01\-15 12:57:12 |Blue\-green deployment creation time, in the format of `yyyy-MM-dd HH:mm:ss`. |
|EndTime |String |2026\-01\-15 14:37:00 |Blue\-green deployment end time. The format is `yyyy-MM-dd HH:mm:ss`.<br><br>> **tip**<br><br><br>> This field is returned only when the blue\-green deployment status is `DELETE_COMPLETED` or `SWITCHOVER_COMPLETED`.<br> |
|DataSyncProgress |Double |99 |Data synchronization progress. |
|SourceInstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the blue instance. |
|TargetInstanceId |String |redis\-cn01y2c6v6y6m\*\*\*\* |The instance ID of the green instance. |
|SourceInstanceName |String |upgradeversion |Instance name of the blue instance. |
|TargetInstanceName |String |redistest\-green |Instance name of the green instance. |
|SourceEngineVersion |String |5.0 |Database version number for the blue instance. |
|TargetEngineVersion |String |7.0 |Database version for green instances. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeBlueGreenDeployments&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****",
    "ExcludeCompleted": false
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "DescribeBlueGreenDeployments",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "BlueGreenDeployments": [
            {
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
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

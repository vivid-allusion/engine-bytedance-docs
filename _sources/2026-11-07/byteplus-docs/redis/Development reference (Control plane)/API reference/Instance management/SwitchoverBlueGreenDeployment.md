---
title: "SwitchoverBlueGreenDeployment"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/switchoverbluegreendeployment"
---

Call the SwitchoverBlueGreenDeployment API to perform blue\-green deployment switch for target Redis instance.

## Request type

Asynchronous request.

## Precautions

* You can only perform the blue\-green switchover operation when the blue\-green deployment status of the source instance is **Switchable** (that is, `Status` is `SWITCHOVER_AVAILABLE`). For more information about the blue\-green deployment status, refer to [Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA).

* The duration of blue\-green switch operations is affected by factors such as data write load and data synchronization links. If the switch operation takes too long to complete, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for assistance in troubleshooting.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=SwitchoverBlueGreenDeployment&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|SourceInstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the source instance (i.e., the blue instance).<br><br>> **tip**<br><br><br>> Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|ApplyImmediately |Boolean |Yes |true |Perform blue\-green switchover immediately. Valid values:<br><br><br>* `true`: Switch immediately.<br><br>* `false`: The switchover is performed during the maintenance period.<br><br><br>> **tip**<br><br><br>> If you choose to execute during the maintenance period, the blue\-green deployment will enter the **Waiting for switch** status, which will persist until the task is complete. For more information on blue\-green deployment statuses, refer to [Blue\-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA). For the method to set the maintenance period, refer to [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CreateTime |String |2026\-01\-15 12:57:12 |Blue\-green deployment creation time, in the format `yyyy-MM-dd HH:mm:ss`. |
|DataSyncProgress |Double |99 |Data synchronization progress. |
|EndTime |String |2026\-01\-15 14:37:00 |Blue\-green deployment end time. The format is `yyyy-MM-dd HH:mm:ss`.<br><br>> **tip**<br><br><br>> This field is returned only when the blue\-green deployment status is `DELETE_COMPLETED` or `SWITCHOVER_COMPLETED`.<br> |
|Name |String |upgradeversion |Blue\-green deployment name. |
|SourceEngineVersion |String |5.0 |Instance name of the green instance. |
|SourceInstanceName |String |upgradeversion |Instance name of the blue instance. |
|SourceInstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the blue instance. |
|Status |String |SWITCHOVER_AVAILABLE |Blue\-green deployment status. For more information on blue\-green deployment status, refer to <br><br>[Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA). |
|TargetEngineVersion |String |7.0 |Database version for green instances. |
|TargetInstanceName |String |redistest\-green |Instance name of the green instance. |
|TargetInstanceId |String |redis\-cn01y2c6v6y6m\*\*\*\* |Instance ID of the green instance. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=SwitchoverBlueGreenDeployment&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "SourceInstanceId": "redis-cn0212gzmh2xs****",
    "ApplyImmediately": true
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "SwitchoverBlueGreenDeployment",
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

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

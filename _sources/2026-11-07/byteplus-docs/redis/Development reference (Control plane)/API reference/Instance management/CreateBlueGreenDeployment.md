---
title: "CreateBlueGreenDeployment"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createbluegreendeployment"
---

Call the CreateBlueGreenDeployment API to create blue\-green deployment task for target Redis instance.

## Request type

Asynchronous request.

## Precautions

* A single instance can have at most one ongoing blue\-green deployment process each time. For more details, refer to [Upgrading major versions using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment).

* Instances needed to upgrade major versions using blue\-green deployment must meet the following requirements:

   * The instance's database version is not Redis 7.0.

   * The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

   * The instance does not use additional bandwidth. If additional bandwidth is in use, cancel it first. For specific procedures, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).

   * The instance with sharding cluster enabled has not applied for direct connection address. If a direct connection address has been applied for, release it first. For specific procedures, refer to [Releasing direct connection addresses](https://docs.byteplus.com/en/docs/redis/release-direct-connection-address).

* Currently, only support creating **Pay\-as\-you\-go** green instances. Therefore, before creating green instance, ensure that the total value of your account balance (that is, cash balance) and vouchers must be at least USD 100. For more information, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateBlueGreenDeployment&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|SourceInstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the source instance (i.e., the blue instance).<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|Name |String |No |upgradeversion |Description of the blue\-green deployment task. The description must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1 to 128 characters.<br><br><br>> **tip**<br><br><br>> If this parameter is left empty, no description will be added for this task.<br> |
|TargetInstanceName |String |No |redistest\-green |Set the name of the target instance (i.e., green instance). The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters.<br><br><br>> **tip**<br><br><br><br>* > If the name of the green instance is not set, `<blue instance name>-green-<six-digit random code>` will be used as its default instance name.<br><br><br>   > For example, if the blue instance name is `redistest`, the default name of the green instance created for it might be `redistest-green-b4bf10`.<br>   <br><br>* > The instance name for Cache for Redis cannot exceed 128 characters, and `-green-<six-digit random code>` occupies a fixed 13 characters. Therefore, the `<Blue instance name>` part of the green instance name will retain at most the first 115 characters of the blue name to accommodate the total length limit.<br> |
|TargetEngineVersion |String |No |7.0 |Set the database version for the green instance.<br><br>> **tip**<br><br><br>> The database version of the green instance must be greater than that of the blue instance. For example, if the database version of the blue instance is 5.0, then the database version of the green instance can be 6.0 or 7.0.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CreateTime |String |2026\-01\-15 12:57:12 |Blue/Green deployment creation time, in the format of<br><br>`yyyy-MM-dd HH:mm:ss`。 |
|DataSyncProgress |Double |99 |Data synchronization progress. |
|EndTime |String |2026\-01\-15 14:37:00 |Blue\-green deployment end time. The format is `yyyy-MM-dd HH:mm:ss`.<br><br>> **tip**<br><br><br>> This field is returned only when the blue\-green deployment status is `DELETE_COMPLETED` or `SWITCHOVER_COMPLETED`.<br> |
|Name |String |upgradeversion |Blue\-green deployment name. |
|SourceInstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID of the blue instance. |
|SourceInstanceName |String |upgradeversion |Instance name of the blue instance. |
|SourceEngineVersion |String |5.0 |Database version number for the blue instance. |
|Status |String |SWITCHOVER_AVAILABLE |Blue\-green deployment status. For more information on blue\-green deployment status, refer to <br><br>[Blue-green deployment status](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment#NFCgYsLA). |
|TargetInstanceId |String |redis\-cn01y2c6v6y6m\*\*\*\* |Instance ID of the green instance. |
|TargetInstanceName |String |redistest\-green |Instance name of the green instance. |
|TargetEngineVersion |String |7.0 |Database version for green instances. |

## Example

### Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateBlueGreenDeployment&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "SourceInstanceId": "redis-cn0212gzmh2xs****",
    "Name": "upgradeversion",
    "TargetInstanceName": "redistest-green",
    "TargetEngineVersion": "7.0"
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "CreateBlueGreenDeployment",
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

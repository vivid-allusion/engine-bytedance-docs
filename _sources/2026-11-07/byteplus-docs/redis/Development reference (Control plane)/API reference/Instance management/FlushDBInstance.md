---
title: "FlushDBInstance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/flushdbinstance"
---

Call the FlushDBInstance API to clear all business data in the target Redis instance.

## Request type

Synchronous request.

## Precautions

* After clearing data, existing business data in the instance will be erased and cannot be recovered. Proceed with caution.

* We recommend manually backing up Redis instance data before clearing it. For manual backup method, refer to [Manual backup](https://docs.byteplus.com/en/docs/redis/manual-backup) and [CreateBackup](https://docs.byteplus.com/en/docs/redis/createbackup).

* Single node instances (i.e., where `InstanceClass` is set to `Standalone`) do not support persistence and backup features; therefore, data cannot be recovered after being cleared. Proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* Disabling the `flushall` command in **parameter configuration** (that is, adding the `flushall` command to the `disabled-commands` parameter) does not affect the normal execution of the data clearing function on the Redis console and the normal invocation of the FlushDBInstance API. For parameter settings, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

* After successfully calling the FlushDBInstance interface, Redis will immediately start executing the `flushall async` operation, and the execution time of the operation will be affected by the size of the data to be cleared.

* The data clearing operation does not affect newly written data. This means data written after calling the FlushDBInstance API will not be cleared.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=FlushDBInstance&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=FlushDBInstance&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230915202143DA8DBA604CA9E91C****",
        "Action": "FlushDBInstance",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

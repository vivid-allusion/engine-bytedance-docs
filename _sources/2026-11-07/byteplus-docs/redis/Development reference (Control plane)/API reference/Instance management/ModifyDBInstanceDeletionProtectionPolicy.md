---
title: "ModifyDBInstanceDeletionProtectionPolicy"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancedeletionprotectionpolicy"
---

Call the ModifyDBInstanceDeletionProtectionPolicy API to enable or disable the instance deletion protection.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceDeletionProtectionPolicy&serviceCode=Redis&version=2020-12-07&groupName=实例管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|DeletionProtection |String |Yes |enabled |Enable or disable instance deletion protection. Valid values:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable.<br><br><br>> **tip**<br><br><br>> For more information on deletion protection, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceDeletionProtectionPolicy&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"DeletionProtection": "enabled"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022072317504601017424420201BD1111",
        "Action": "ModifyDBInstanceDeletionProtectionPolicy",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

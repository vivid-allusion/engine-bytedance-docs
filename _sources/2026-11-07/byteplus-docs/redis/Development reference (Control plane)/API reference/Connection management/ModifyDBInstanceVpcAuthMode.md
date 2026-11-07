---
title: "ModifyDBInstanceVpcAuthMode"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode"
---

Call the ModifyDBInstanceVpcAuthMode API to enable or disable password\-free access.

## Request type

Synchronous request.

## Precautions

* After a Redis instance is successfully created, password\-free access is disabled by default. For more details, refer to [Password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).

* After enabling password\-free access, if no account is entered, the default account is used, allowing access to the Redis instance without a password.

* After enabling password\-free access, it also remains compatible with connecting to Redis instances using account and password authentication. You can still connect to the Redis instance with an account and password.

* To ensure database security, account and password information must be verified when connecting to the Redis instance via public network address with any account, regardless of whether the password\-free feature is enabled.

* For data security reasons, it is not allowed to add the address `0.0.0.0/0` to the allowlist of the instance while enabling the password\-free access function. To enable password\-free access, first delete the `0.0.0.0/0` address from the instance allowlist. For more information on how to modify allowlist, refer to [ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceVpcAuthMode&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|VpcAuthMode |String |Yes |open |Enable or disable password\-free access. Valid values:<br><br><br>* `open`: enable password\-free access.<br><br>* `close`: disable password\-free access.<br><br><br>> **tip**<br><br><br><br>* > Parameter values are case\-insensitive.<br><br><br>* > For more information on password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceVpcAuthMode&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"VpcAuthMode": "open"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151850520102121450480E601111",
          "Action": "ModifyDBInstanceVpcAuthMode",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

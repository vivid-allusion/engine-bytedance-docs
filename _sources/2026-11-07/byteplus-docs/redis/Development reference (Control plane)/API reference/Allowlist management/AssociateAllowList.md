---
title: "AssociateAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/associateallowlist"
---

Call the AssociateAllowList API to associate the target instance to the specified IP address allowlist.

## Request type

Asynchronous request.

## Precautions

* When using the allowlist in Cache for Redis, there are some constraints and limitations. For the details, please refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist#.5rOo5oSP5LqL6aG5).

* For data security reasons, adding address `0.0.0.0/0` to the instance's allowlist is not allowed while enabling passwordless access. If you need to set address `0.0.0.0/0` in the allowlist, disable the instance's password\-free access feature first. For more information on password\-free access, refer to [ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateAllowList&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["redis\-cn0212gzmh2xs\*\*\*\*"] |ID of the instance to associate with an allowlist.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > You cannot pass multiple instance IDs and multiple allowlists at the same time. You can only associate multiple instances with one allowlist, or one instance with multiple allowlists.<br> |
|AllowListIds |Array of String |Yes |["acl\-cn02f66vyjw7aj9\*\*\*\*","acl\-cn02iaiectnt2ls\*\*\*\*"] |The ID of the allowlist to associate with the instance.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query information about all allowlists in a specified region, including their allowlist IDs.<br><br><br>* > You can pass multiple allowlist IDs, separated by commas (,).<br><br><br>* > You cannot pass multiple instance IDs and multiple allowlists at the same time. You can only associate multiple instances with one allowlist, or one instance with multiple allowlists.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=AssociateAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceIds": [
        "redis-cn0212gzmh2xs****"
    ],
    "AllowListIds": [
        "acl-cn02f66vyjw7aj9****",
        "acl-cn02iaiectnt2ls****"
    ]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "AssociateAllowList",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

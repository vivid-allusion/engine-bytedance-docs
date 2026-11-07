---
title: "DescribeDBInstanceAclCategories"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories"
---

Call the DescribeDBInstanceAclCategories API to query the command categories supported by target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceAclCategories&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfqfxzk8zxt9ghz |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Categories |Array of String |["keyspace","read","write","set","sortedset","list","hash","string","bitmap","hyperloglog","geo","stream","pubsub","admin","fast","slow","blocking","dangerous","connection","transaction","scripting"] |Command categories supported by the current instance.<br><br>> **tip**<br><br><br>> Cache for Redis provides five roles by default: `Administrator`, `NotDangerous`, `ReadWrite`, `ReadOnly`, and `NotWrite`. Each role has different ACL rules, as well as different supported command categories and corresponding commands. For more details, refer to [ACL Syntax](https://docs.byteplus.com/en/docs/redis/create-role#G8lTkW04).<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceAclCategories&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json
X-Date: 20240926T113612Z
Authorization: HMAC-SHA256 Credential=AKLTO*****U2NGM/20240926/cn-beijing/Redis/request, SignedHeaders=x-content-sha256;x-date, Signature=e769f*****bf440
{
  "InstanceId": "redis-cnlfqfxzk8zxt9ghz"
}
```

## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20240926193612F1B41A449DB5EFC04A19-13880a",
    "Action": "DescribeDBInstanceAclCategories",
    "Version": "2020-12-07",
    "Service": "Redis",
    "Region": "cn-beijing"
  },
  "Result": {
    "Categories": [
      "keyspace",
      "read",
      "write",
      "set",
      "sortedset",
      "list",
      "hash",
      "string",
      "bitmap",
      "hyperloglog",
      "geo",
      "stream",
      "pubsub",
      "admin",
      "fast",
      "slow",
      "blocking",
      "dangerous",
      "connection",
      "transaction",
      "scripting"
    ]
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

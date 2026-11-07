---
title: "DescribeDBInstanceAclCommands"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands"
---

Call the DescribeDBInstanceAclCommands API to query the list of commands supported by the specified command category in target Redis instance.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceAclCommands&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfqfxzk8zxt9ghz |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|Category |String |Yes |admin |Specify the command category to query.<br><br>> **tip**<br><br><br><br>* > Only one command category's command support list can be queried at a time.<br><br><br>* > You can call the [DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) API to query the details of command categories supported by the target Redis instance.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Commands |Array of String |["client","cluster","config","monitor"] |List of commands supported under the current command category.<br><br>> **tip**<br><br><br>> Cache for Redis provides five default roles: `Administrator`, `NotDangerous`, `ReadWrite`, `ReadOnly`, and `NotWrite`. Each role has different ACL rules, supported command categories, and corresponding commands. For more details, refer to [ACL Syntax](https://docs.byteplus.com/en/docs/redis/create-role#G8lTkW04).<br> |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeDBInstanceAclCommands&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json
X-Date: 20240926T114317Z
Authorization: HMAC-SHA256 Credential=AKLTO*****U2NGM/20240926/cn-beijing/Redis/request, SignedHeaders=x-content-sha256;x-date, Signature=c220b*****e0941
{
  "InstanceId": "redis-cnlfqfxzk8zxt9ghz",
  "Category": "admin"
}
```

## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20240926194317097E9108DCFD7EC29192-882b05",
    "Action": "DescribeDBInstanceAclCommands",
    "Version": "2020-12-07",
    "Service": "Redis",
    "Region": "cn-beijing"
  },
  "Result": {
    "Commands": [
      "client",
      "cluster",
      "config",
      "monitor"
    ]
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

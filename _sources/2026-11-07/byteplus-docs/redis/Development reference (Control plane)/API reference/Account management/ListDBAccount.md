---
title: "ListDBAccount"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/listdbaccount"
---

Call the ListDBAccount API to query the information of specified accounts or all accounts for a Redis instance, including the account name and account role.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListDBAccount&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AccountName |String |No |test1 |Account name.<br><br>> **tip**<br><br><br>> If this parameter is left empty, account names are not used as a filter condition.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Accounts |Array of [AccountInfo](https://docs.byteplus.com/en/docs/55/12476#accountinfo) |Refer to the Sample response. |Account information list. |

### AccountInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AccountName |String |test1 |Account name. |
|RoleName |String |ReadWrite |Account role. The following default roles are supported:<br><br><br>* `Administrator`: allows using all commands supported by Redis instances for all keys.<br><br>* `ReadWrite`: allows using all commands for all keys except those in the `admin` category.<br><br>* `ReadOnly`: allows using all commands in the `read` category for all keys.<br><br>* `NotDangerous`: allows using all commands for all keys except those in the `dangerous` category. |
|InstanceId |String |redis\-cn0212gzmh2xs\*\*\*\* |The instance ID of the account. |
|Description |String |test account |Account description. |
|AccountStatus |String |Available |Account status. Valid values:<br><br><br>* `Available`: available.<br><br>* `Unavailable`: unavailable. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ListDBAccount&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId":"redis-cn0212gzmh2xs****"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041520051001021204519717631763",
          "Action": "ListDBAccount",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "Accounts":[
              {
                  "AccountName": "test1",
                  "AccountStatus": "Available",
                  "Description": "test account",
                  "InstanceId": "redis-cn0212gzmh2xs****",
                  "RoleName": "Administrator"
              }
          ]
     }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

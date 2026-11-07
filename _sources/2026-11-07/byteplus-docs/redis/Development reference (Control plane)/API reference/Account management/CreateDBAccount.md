---
title: "CreateDBAccount"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createdbaccount"
---

Call the CreateDBAccount API to create an account for target Redis instance.

## Request type

Asynchronous request.

## Precautions

Each Redis instance can have up to 100 accounts by default. If you need to create more accounts, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to modify relevant parameters.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBAccount&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AccountName |String |Yes |test1 |Account name. The name must meet the following requirements:<br><br><br>* It starts with a lowercase letter and ends with a lowercase letter or number.<br><br>* The length should be 2 to 16 characters.<br><br>* It consists of only lowercase letters, digits, and underscores (_). |
|RoleName |String |Yes |ReadWrite |Account role. The following default roles are supported:<br><br><br>* `Administrator`: allows using all commands supported by Redis instances for all keys.<br><br>* `ReadWrite`: allows using all commands for all keys except those in the `admin` category.<br><br>* `ReadOnly`: allows using all commands in the `read` category for all keys.<br><br>* `NotDangerous`: allows using all commands for all keys except those in the `dangerous` category.<br><br>* `NotWrite`: Permission to use all commands other than `write` commands on all keys.<br><br><br>> **tip**<br><br><br><br>* > For details on the specific commands supported by ACL rules corresponding to each role, see [ACL Syntax](https://docs.byteplus.com/en/docs/redis/create-role#G8lTkW04).<br><br><br>* > You can call the [DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) API to query the command categories supported by the target Redis instance, and call the [DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) API to query the details of commands supported for a specified command category.<br> |
|Password |String |Yes |Pwd@121111 |Account password. The password must meet the following requirements:<br><br><br>* The length is 8~64 characters.<br><br>* It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* It supports the following special characters:<br><br>   ```Plain```<br>```   ()`~!@#$%^&*-+=_\|{}[];<>,.?```<br>```   ```<br>    |
|Description |String |No |The_test_account |Account description, with a maximum length of 256 characters.<br><br>> **tip**<br><br><br>> If this parameter is empty, it means no account description is set.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateDBAccount&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"AccountName": "test1",
	"RoleName": "ReadWrite",
	"Password": "Pwd@121111",
	"Description": "The_test_account"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204152003120102121940390A641111",
          "Action": "CreateDBAccount",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

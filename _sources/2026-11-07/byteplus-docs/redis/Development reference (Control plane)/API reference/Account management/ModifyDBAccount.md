---
title: "ModifyDBAccount"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbaccount"
---

Call the ModifyDBAccount API to modify the information of a specified account, including the account role, password, and description.

## Request type

Asynchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBAccount&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AccountName |String |Yes |test1 |Account name.<br><br>> **tip**<br><br><br>> You can call the [ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) API to query the information of all accounts in a target Redis instance.<br> |
|RoleName |String |No |ReadWrite |Account role. The following default roles are supported:<br><br><br>* `Administrator`: allows using all commands supported by Redis instances for all keys.<br><br>* `ReadWrite`: allows using all commands for all keys except those in the `admin` category.<br><br>* `ReadOnly`: allows using all commands in the `read` category for all keys.<br><br>* `NotDangerous`: allows using all commands for all keys except those in the `dangerous` category.<br><br>* `NotWrite`: Permission to use all commands other than `write` commands on all keys.<br><br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the account's role will not be modified.<br><br><br>* > The role of the default account is fixed as `Administrator` and cannot be modified.<br><br><br>* > For details on the specific commands supported by ACL rules corresponding to each role, see [ACL Syntax](https://docs.byteplus.com/en/docs/redis/create-role#G8lTkW04).<br> |
|Password |String |No |Pwd@123456 |The modified account password. The modified password must also meet the following requirements:<br><br><br>* The length is 8~64 characters.<br><br>* It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* It supports the following special characters:<br><br>   ```Plain```<br>```   ()`~!@#$%^&*-+=_\|{}[];<>,.?```<br>```   ```<br>   <br><br><br>> **tip**<br><br><br>> If this parameter is empty, it means that the account password will not be modified.<br> |
|Description |String |No |The_test_account |The modified account description, with a maximum length of 256 characters.<br><br>> **tip**<br><br><br>> If this parameter is blank, the account description is not modified.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBAccount&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"AccountName": "test1",
	"RoleName": "ReadWrite",
	"Description": "The_test_account"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041520143801021203723005621111",
          "Action": "ModifyDBAccount",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

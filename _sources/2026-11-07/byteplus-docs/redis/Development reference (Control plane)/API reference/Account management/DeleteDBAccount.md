---
title: "DeleteDBAccount"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deletedbaccount"
---

Call the DeleteDBAccount API to delete the specified account from the target Redis instance.

## Request type

Asynchronous request.

## Precautions

You cannot delete a default account.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDBAccount&serviceCode=Redis&version=2020-12-07&groupName=账号管理)

## Request parameters

|**Parameter** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AccountName |String |Yes |test1 |Account name to delete.<br><br>> **tip**<br><br><br><br>* > You cannot delete a default account.<br><br><br>* > You can call the [ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) API to query the information of all accounts in a target Redis instance.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteDBAccount&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111",
	"AccountName": "test1"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041520162801021203522722651111",
          "Action": "DeleteDBAccount",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

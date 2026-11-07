---
title: "DeleteDBEndpointPublicAddress"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deletedbendpointpublicaddress"
---

Call the DeleteDBEndpointPublicAddress API to release the public connection address of the target Redis instance, that is, to disable public access.

## Request type

Asynchronous request.

## Precautions

* For instances created before May 17, 2022, directly calling this API to release the public connection address may result in an error. If the call fails, please [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) to contact technical support.

* After disabling internet access, clients cannot access Redis instances through their original public domain names and ports. Confirm your services are not using the public address to avoid unnecessary losses.

* After the public address is released, the EIP is automatically disassociated. However, the EIP will not be released and will still be retained and continue to be billed. If an EIP is no longer in use, you can release it by calling [ReleaseEipAddress](https://docs.byteplus.com/en/docs/eip/ReleaseEipAddress).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDBEndpointPublicAddress&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

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
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteDBEndpointPublicAddress&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceId": "redis-cn0212gzmh2xs1111"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022042511064401022524311809C8****",
          "Action": "DeleteDBEndpointPublicAddress",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

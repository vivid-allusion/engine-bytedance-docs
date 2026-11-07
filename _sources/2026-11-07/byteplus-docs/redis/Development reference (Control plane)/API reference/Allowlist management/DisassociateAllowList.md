---
title: "DisassociateAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/disassociateallowlist"
---

Call the DisassociateAllowList API to disassociate the target Redis instance from the specified IP allowlist.

## Request type

Asynchronous request.

## Precautions

After instances and allowlists are disassociated, all IP addresses in the original allowlist cannot access the instances. Ensure that the IP addresses of devices that still require access to the current instance are added to other allowlists first. For more details, see [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/redis/disassociate-allowlist).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateAllowList&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["redis\-cn02he8bhzsji\*\*\*\*"] |ID of the instance to disassociate with an allowlist.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > You cannot pass multiple instance IDs and multiple allowlists simultaneously. You can only disassociate multiple instances from one allowlist, or disassociate one instance from multiple allowlists.<br> |
|AllowListIds |Array of String |Yes |["acl\-cn0212fjx4815ke\*\*\*\*"] |The ID of the allowlist to be disassociated from the instance.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query information about all allowlists in a specified region, including allowlist IDs.<br><br><br>* > You cannot pass multiple instance IDs and multiple allowlists simultaneously. You can only disassociate multiple instances from one allowlist, or disassociate one instance from multiple allowlists.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DisassociateAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"InstanceIds": ["redis-cn02he8bhzsji****"],
	"AllowListIds": ["acl-cn0212fjx4815ke****"]
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "DisassociateAllowList",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

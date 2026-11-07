---
title: "DeleteAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/deleteallowlist"
---

Call the DeleteAllowList API to delete the target IP allowlist.

## Request type

Synchronous request.

## Precautions

An allowlist can be deleted only after all instances are disassociated from it. Call the [DisassociateAllowList](https://docs.byteplus.com/en/docs/redis/disassociateallowlist) API to disassociate instances and allowlists.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAllowList&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-cn022p4qmcz2p26\*\*\*\* |Allowlist ID<br><br>> **tip**<br><br><br>> You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query all allowlist information, including allowlist IDs, for the specified region.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DeleteAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "AllowListId":"acl-cn022p4qmcz2p26****"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "DeleteAllowList",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

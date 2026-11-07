---
title: "CreateDBEndpointDirectLinkAddress"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createdbendpointdirectlinkaddress"
---

Call the CreateDBEndpointDirectLinkAddress API to apply for a direct connection address for target Redis instance.

## Request type

Asynchronous request.

## Precautions

* When a client first uses a direct connection address to access instance, the direct connection address will be resolved to the fixed Virtual IP (VIP) address allocated by Redis to all shards, and then routed to each data shard via the Redis cluster protocol. Therefore, your client needs to support the Redis cluster protocol.

* If you release the direct connection address and then apply for a new one, the IP address corresponding to the newly applied direct connection address may be different from the previous one. It is recommended to use the direct connection address domain name instead of IP address to access the Redis instance, to avoid connection issues caused by IP address changes.

* Access through direct addresses to save time in processing requests through proxies. In theory, this can shorten the response time of the server to the client, but automatic load balancing, automatic read/write splitting, and other advanced features are lost. We recommend that you exercise due caution when selecting the address type according to your actual needs. For more details, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBEndpointDirectLinkAddress&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|Port |Integer |No |6379 |Set the port number for the direct connection address. The value range is 1024\-4000 and 5100\-64512.<br><br>> **tip**<br><br><br><br>* > If this parameter is not specified, the direct connection address defaults to using port 6379.<br><br><br>* > After the application is completed, you can also call the [ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) API to modify the domain name and port number of the direct connection address.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhTOYhT |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateDBEndpointDirectLinkAddress&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs1111",
    "Port": 6379
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDBEndpointDirectLinkAddress",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

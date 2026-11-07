---
title: "CreateDBEndpointPublicAddress"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress"
---

Call the CreateDBEndpointPublicAddress API to create the public address for a specified Redis instance (enable Internet access for an instance).

## Request type

Asynchronous request.

## Precautions

* Since May 17, 2022, customers who newly activate Redis and customers with existing instances must complete cross\-service access authorization. Complete the authorization as soon as possible; otherwise, an error will occur when calling APIs such as [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance), [ModifyDBInstanceSubnet](https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet), and [CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress).

   For information on cross\-service access authorization, see [Cross-Service Access Authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization).

* Compared with private network access, internet access has a higher latency and involves certain security risks. We recommend that you only use it in testing environments, while private network access is recommended for production environments. When devices outside the VPC no longer need to access Redis instances, promptly disable public network access. You can call the [DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointpublicaddress) to disable the public network access function.

## Billing Details

Public network addresses will be associated with your Elastic IP (EIP), and fees are charged by EIP. For more details, refer to [EIP billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBEndpointPublicAddress&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|EipId |String |Yes |eip\-2fef2qcfbfw8w5oxruw3w\*\*\*\* |The EIP ID to bind to the instance.<br><br>> **tip**<br><br><br>> You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) API to query the details of created EIPs, including EIP IDs.<br> |
|Port |Integer |No |6379 |Set the port number for the public IP address. The value range is 1024 to 65535.<br><br>> **tip**<br><br><br><br>* > If this parameter is not specified, the public network address defaults to port 6379.<br><br><br>* > After the application is complete, you can also call the [ModifyDBInstanceVisitAddress](https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress) interface to modify the domain name and port number of the public IP address.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateDBEndpointPublicAddress&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs****",
        "EipId": "eip-2fef2qcfbfw8w5oxruw3w****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDBEndpointPublicAddress",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
"Result":null
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).

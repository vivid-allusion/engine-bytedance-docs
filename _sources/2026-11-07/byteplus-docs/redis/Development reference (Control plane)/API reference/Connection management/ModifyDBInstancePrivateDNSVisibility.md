---
title: "ModifyDBInstancePrivateDNSVisibility"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstanceprivatednsvisibility"
---

Call the ModifyDBEndpointPrivateDNSVisibility API to enable or disable the public network resolution function for the target Redis instance.

## Request type

Asynchronous request.

## Precautions

* Due to the complex public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed, so this function is limited to non\-production environments. For production environments, it is strongly recommended to use a DNS Forward solution by configuring your local DNS server to forward to BytePlus DNS, where 100.96.0.2 and 100.96.0.3 are the DNS servers used by BytePlus, to achieve domain name resolution in a private network environment. For detailed instructions, please refer to [Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/redis/set-public-network-resolution).

* If the error `The prefix of address already existed` occurs when enabling public network resolution, you need to modify the private address for the current instance before enabling public network resolution. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstancePrivateDNSVisibility&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cnlfkmh6uiii8\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|PrivateDNSVisibility |String |Yes |Public |Enable or disable public network resolution for the instance. Valid values:<br><br><br>* `Public`: Enable public network resolution.<br><br>* `Private`: Disable public network resolution. |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstancePrivateDNSVisibility&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cnlfkmh6uiii8****",
    "PrivateDNSVisibility": "Public"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyDBInstancePrivateDNSVisibility",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

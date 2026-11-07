---
title: "ModifyDBInstanceVisitAddress"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancevisitaddress"
---

Call the ModifyDBInstanceVisitAddress API to modify the address or port number of the target connection address of the specified instance.

## Request type

Asynchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceVisitAddress&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br> |
|AddrType |String |Yes |Private |Connection address type requiring an address prefix. Valid values:<br><br><br>* `Public`: Public network address.<br><br>* `Private`: Private network address.<br><br>* `DirectLink`: Direct connection address.<br><br><br>> **tip**<br><br><br><br>* > To modify the connection address of direct connection addresses or public network addresses, you must first apply for the corresponding connection address. For specific procedures, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address) and [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br><br><br>* > For more information on Redis connection addresses, refer to [Connection address types](https://docs.byteplus.com/en/docs/redis/view-address#.6L-e5o6l5Zyw5Z2A57G75Z6L).<br> |
|NewAddressPrefix |String |No |testaddrpre |Modified connection address prefix. The connection address prefix must meet the following requirements:<br><br><br>* It consists of lowercase letters, numbers, or hyphens (\-).<br><br>* Start with a letter and end with a letter or number.<br><br>* The length is 8 to 53 characters.<br><br>* The modified connection address needs to be globally unique and cannot have the same name as any connection address in any region of BytePlus.<br><br><br>> **warning**<br><br><br><br>* > If this parameter is left blank, the connection address prefix will not be modified.<br><br><br>* > When you need to upgrade the domain suffix (that is, `UpgradeRegionDomain` to `true`), you must also pass in the connection address prefix information (that is, the `NewAddressPrefix` parameter is not allowed to be empty.)<br><br><br>* > When you do not need to upgrade the domain suffix (i.e. `UpgradeRegionDomain` is `false`), you need to select at least one of the `NewAddressPrefix` or `NewPort` parameters to modify.<br><br><br>* > After modifying the connection address, existing connections will be disconnected. Promptly modify the connection information of the client and use the new connection address to connect to the instance. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).<br><br><br>* > Currently, you can only modify the prefix of the connection address, specifically the part before `redis.ivolces.com` or `redis.volces.com`. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address).<br> |
|NewPort |Integer |No |6379 |Modified connection address port number. Different connection address types support different port number ranges:<br><br><br>* Both private and public network addresses support port numbers ranging from 1024 to 65535.<br><br>* Direct connection addresses support port numbers ranging from 1024 to 4000 and from 5100 to 64512.<br><br><br>> **warning**<br><br><br><br>* > If this parameter is left blank, the port number of the connection address will not be modified.<br><br><br>* > When you do not need to upgrade the domain suffix (i.e. `UpgradeRegionDomain` is `false`), you need to select at least one of the `NewAddressPrefix` or `NewPort` parameters to modify.<br><br><br>* > After modifying the connection address or port number, existing connections will be disconnected. Promptly modify the client's connection information and use the new port number to connect to the instance. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).<br><br><br>* > Modifying the port will temporarily affect access to some services. Operate with caution. For specific procedures, refer to [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).<br> |
|UpgradeRegionDomain |Boolean |No |false |Whether to upgrade the domain suffix of the connection address. Valid values:<br><br><br>* `true`: Upgrade.<br><br>* `false` (default): Do not upgrade.<br><br><br>> **warning**<br><br><br><br>* > When you need to upgrade the domain suffix (that is, `UpgradeRegionDomain` to `true`), you must also pass in the connection address prefix information (that is, the `NewAddressPrefix` parameter is not allowed to be empty.)<br><br><br>* > After upgrading the domain suffix, existing connections will be disconnected. Update the client's connection information promptly and use the new connection address to connect to the instance. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).<br><br><br>* > After the connection address domain suffix is upgraded, downgrading back to the original suffix is not supported. Proceed with caution.<br><br><br>* > After upgrading, the domain name suffix of the connection address will automatically contain the region information to which the instance belongs. That is, the domain name suffix will change from `redis.ivolces.com` (or `redis.volces.com`) to `redis.{Region ID}.ivolces.com` (or `redis.{Region ID}.volces.com`). The old connection address will be retained for 12 hours and will be automatically released after the expiration of the 12\-hour retention period. For more details, refer to [Upgrading domain name suffix](https://docs.byteplus.com/en/docs/redis/upgrade-domain-suffix).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.volcengineapi.com/?Action=ModifyDBInstanceVisitAddress&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "redis-cn0212gzmh2xs1111",
    "AddrType": "Private",
    "NewAddressPrefix": "testaddrpre",
    "NewPort": 6379
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202306041104205y43100232280022D312D31",
        "Action": "ModifyDBInstanceVisitAddress",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

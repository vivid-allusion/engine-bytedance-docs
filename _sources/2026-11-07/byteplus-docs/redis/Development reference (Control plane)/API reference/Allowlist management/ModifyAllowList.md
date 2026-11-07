---
title: "ModifyAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifyallowlist"
---

Call the ModifyAllowList API to modify the setting of a target allowlist (allowlist name, allowlist IP address, etc.).

## Request type

Asynchronous request.

## Precautions

* When using the allowlist in Cache for Redis, there are some constraints and limitations. For the details, please refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist#.5rOo5oSP5LqL6aG5).

* For data security reasons, adding address `0.0.0.0/0` to the instance's allowlist is not allowed while enabling passwordless access. If you need to set address `0.0.0.0/0` in the allowlist, disable the instance's password\-free access feature first. For more information on password\-free access, refer to [ModifyDBInstanceVpcAuthMode](https://docs.byteplus.com/en/docs/redis/modifydbinstancevpcauthmode).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyAllowList&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-cnlf3xgczbjldzy\*\*\*\* |Allowlist ID<br><br>> **tip**<br><br><br>> You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query all allowlist information, including allowlist IDs, for the specified region.<br> |
|AllowListName |String |No |test |Allowlist name.<br><br>> **tip**<br><br><br><br>* > If this parameter is not set, the allowlist's original name is used by default.<br><br><br>* > To modify the allowlist name, enter a new allowlist name. The name must meet the following requirements:<br><br><br>   * > It cannot start with a number or hyphen (\-).<br><br><br>   * > It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>   * > The length should be 1 to 128 characters.<br> |
|ModifyMode |String |No |Cover |The modification method. The value range is as follows:<br><br><br>* `Cover` (Default value): Overwrites the original allowlist with the value of the `AllowList` parameter.<br><br>* `Append`: Adds the IP addresses entered in the `AllowList` parameter to the original allowlist.<br><br>* `Delete`: Deletes the IP addresses entered in the `AllowList` parameter from the original allowlist. At least one IP address must be retained. |
|AllowListDesc |String |No |test allowlist |The description of the allowlist cannot exceed 200 characters.<br><br>> **tip**<br><br><br><br>* > If this parameter is not set, the allowlist description will not be updated.<br><br><br>* > If an empty string is passed (i.e., `"AllowListDesc":""`), the allowlist description will be cleared.<br> |
|AllowList |String |No |192.168.0.1 |Enter an IP address or an address range in CIDR format.<br><br>> **tip**<br><br><br><br>* > This parameter is required only when changing IP addresses in the allowlist.<br><br><br>* > Duplicate addresses are not allowed. Separate multiple addresses with commas (,).<br><br><br>* > Setting `0.0.0.0/0` allows access from all addresses; setting `127.0.0.1` denies access from all addresses; setting both `0.0.0.0/0` and `127.0.0.1` allows access from all addresses.<br><br><br>* > Setting CIDR `192.168.1.0/24` indicates that IP addresses within this network segment are allowed to access. If set `192.168.1.1`, only this IP address is allowed to access.<br> |
|ApplyInstanceNum |Integer |No |1 |The number of instances associated with the current allowlist.<br><br>> **tip**<br><br><br><br>* > This parameter is required when modifying the allowlist IP (i.e., `AllowList`) or associated security group (i.e., `SecurityGroupBindInfos`) information.<br><br><br>* > The value passed for this parameter must match the number of instances associated with the current allowlist; otherwise, calling this API will result in an error.<br><br><br>* > You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query all allowlist information for the current account within the specified region, including the total number of associated instances (i.e., the value of the `AssociatedInstanceNum` parameter in the returned parameters).<br> |
|AllowListCategory |String |No |Default |Allowlist type. Valid values:<br><br><br>* `Ordinary` (default value): Ordinary allowlist.<br><br>* `Default`: Default allowlist.<br><br><br>> **tip**<br><br><br>> Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/55/12493#securitygroupbindinfo) |No |Refer to the Sample response. |List of ECS security group information to associate.<br><br>> **tip**<br><br><br><br>* > If this parameter is not set, the security group will not be modified.<br><br><br>* > If an empty array (i.e., `"SecurityGroupBindInfos":[]`) is passed in, the security group will be cleared.<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### SecurityGroupBindInfo

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|BindMode |String |Yes |AssociateEcsIp |Security group association mode. Valid values:<br><br><br>* `IngressDirectionIp`: Inbound IP, which allows IP addresses involved in TCP and ALL protocols in the inbound source addresses of the security groups to access the database. If the source address is configured as a security group, it will be ignored.<br><br>* `AssociateEcsIp`: Associate ECS IP. This allows Elastic Compute Service instances within the security groups to access the database. Currently, only IP information from the primary network interface is supported for import.<br><br><br>> **tip**<br><br><br>> For more details on the security group association mode, see [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).<br> |
|SecurityGroupId |String |Yes |sg\-rrzrivu0yc5cv0x588n\*\*\*\* |The security group ID to associate.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group information, including the security group ID.<br><br><br>* > Up to 10 security groups can be added to a single allowlist at a time.<br><br><br>* > An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"AllowListId": "acl-cnlf3xgczbjldzy****",
	"AllowListName": "test",
	"AllowList": "192.168.0.1",
	"ApplyInstanceNum": 1
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "202204151541400102120740810061****",
          "Action": "ModifyAllowList",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

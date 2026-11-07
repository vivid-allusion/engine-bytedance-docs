---
title: "CreateAllowList"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/createallowlist"
---

Call the CreateAllowList API to create a new IP address allowlist.

## Request type

Synchronous request.

## Precautions

When using the allowlist in Cache for Redis, there are some constraints and limitations. For the details, please refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist#.5rOo5oSP5LqL6aG5).

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAllowList&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListName |String |Yes |test |The allowlist name. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters. |
|AllowList |String |No |10.1.1.1,10.2.3.0/24 |Enter an IP address or a CIDR\-formatted address range.<br><br>> **tip**<br><br><br><br>* > The parameters `AllowList` and `SecurityGroupBindInfos` cannot be empty at the same time.<br><br><br>* > Duplicate addresses are not allowed. Separate multiple addresses with commas (,).<br><br><br>* > Setting `0.0.0.0/0` allows access from all addresses; setting `127.0.0.1` denies access from all addresses; setting both `0.0.0.0/0` and `127.0.0.1` allows access from all addresses.<br><br><br>* > Setting CIDR `192.168.1.0/24` indicates that IP addresses within this network segment are allowed to access. If set `192.168.1.1`, only this IP address is allowed to access.<br> |
|AllowListDesc |String |No |test |The description of the allowlist cannot exceed 200 characters.<br><br>> **tip**<br><br><br>> If this parameter is not set, the description for the new allowlist is empty by default.<br> |
|AllowListCategory |String |No |Default |Allowlist type. Valid values:<br><br><br>* `Ordinary` (default value): Ordinary allowlist.<br><br>* `Default`: Default allowlist.<br><br><br>> **tip**<br><br><br>> Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/55/12488#securitygroupbindinfo) |No |Refer to the sample request. |List of ECS Security Group information to associate.<br><br>> **tip**<br><br><br>> The parameters `AllowList` and `SecurityGroupBindInfos` cannot be empty at the same time.<br> |
|ProjectName |String |No |default |Set the project that the allowlist belongs to.<br><br>> **tip**<br><br><br>> If this parameter is left blank, the new allowlist will be added to the default (i. e. `default` ) project.<br> |
|AllowListType |String |No |DualStack |This field is deprecated and no longer used. Disregard it. |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

### SecurityGroupBindInfo

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|BindMode |String |Yes |AssociateEcsIp |Security group association mode. Valid values:<br><br><br>* `IngressDirectionIp`: Inbound IP, which allows IP addresses involved in TCP and ALL protocols in the inbound source addresses of the security groups to access the database. If the source address is configured as a security group, it will be ignored.<br><br>* `AssociateEcsIp`: Associate ECS IP. This allows Elastic Compute Service instances within the security groups to access the database. Currently, only IP information from the primary network interface is supported for import.<br><br><br>> **tip**<br><br><br>> For more details on the security group association mode, see [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).<br> |
|SecurityGroupId |String |Yes |sg\-rrzrivu0yc5cv0x588n\*\*\*\* |The security group ID to associate.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group information, including the security group ID.<br><br><br>* > Up to 10 security groups can be added to a single allowlist at a time.<br><br><br>* > An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-cnlf3xgczbjldzy\*\*\*\* |Allowlist ID |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=CreateAllowList&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"AllowListName": "test",
	"AllowList": "10.1.1.1,10.2.3.0/24"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022041515414001021207408100610061",
          "Action": "CreateAllowList",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
          "AllowListId": "acl-cnlf3xgczbjldzy****"
     }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

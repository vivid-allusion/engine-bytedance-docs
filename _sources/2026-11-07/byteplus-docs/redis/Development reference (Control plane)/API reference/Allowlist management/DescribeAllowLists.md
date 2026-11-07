---
title: "DescribeAllowLists"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeallowlists"
---

Call the DescribeAllowLists API to query the IP allowlists in the specified region under the current account.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllowLists&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br>> **tip**<br><br><br>> You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query all region information supported by a Redis instance, including the region IDs.<br> |
|InstanceId |String |No |redis\-cn0212gzmh2xs\*\*\*\* |Instance ID.<br><br>> **tip**<br><br><br><br>* > You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query the basic information of all Redis instances in the target region, including the instance ID.<br><br><br>* > If this parameter is blank, you cannot filter by the instance ID.<br> |
|QueryDefault |Boolean |No |false |Filter by allowlist type to determine whether to query only default allowlists. Valid values:<br><br><br>* `true`: Yes, query default allowlists only.<br><br>* `false`: No, query regular allowlists only.<br><br><br>> **tip**<br><br><br>> If this parameter is left empty, it means that the allowlist type condition is not used for filtering, that is, all types of allowlist information will be returned.<br> |
|IPAddress |String |No |100.64. ** *.* ** ,192.168. ** *.* **  |Filter out the allowlist that meets the conditions based on the IP address. When querying with `IPAddress`, it precisely matches this IP address and the IP address block containing this IP address for filtering.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, the query results are not filtered by IP address.<br><br><br>* > Supports passing in multiple IP addresses simultaneously, up to 50 IP addresses. Separate multiple IP addresses with English commas (,).<br> |
|IPSegment |String |No |100.64. ** *.* ** /10,192.168. ** *.* ** /32 |Filter allowlists that meet the conditions by IP address ranges. When querying with `IPSegment`, filtering precisely matches this IP address range.<br><br>> **tip**<br><br><br><br>* > If this parameter is left blank, IP address ranges will not be used to filter the query results.<br><br><br>* > You can pass multiple IP address ranges simultaneously, up to a maximum of 50. Separate multiple IP address ranges with English commas (,).<br> |
|ProjectName |String |No |default |The name of the project to which the allowlist belongs.<br><br>> **tip**<br><br><br>> If this parameter is left blank, it means that the project name condition of the allowlist is not used for screening.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowLists |Array of [AllowListObject](https://docs.byteplus.com/en/docs/55/12494#allowlistobject) |Refer to the Sample response. |A list of allowlist information. |

### AllowListObject

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-cn02zv7944lzokt\*\*\*\* |Allowlist ID |
|AllowListDesc |String |test allowlist |Description of the allowlist. |
|AllowListName |String |api_test |Allowlist name. |
|AllowListType |String |DualStack |This field is deprecated and no longer used. Disregard it. |
|AllowListIPNum |Integer |1 |Total number of IP addresses or address ranges in the allowlist. |
|AssociatedInstanceNum |Integer |1 |Number of instances associated with the current allowlist. |
|ProjectName |String |default |The name of the project to which the allowlist belongs. |
|AllowListCategory |String |Default |Allowlist type. Valid values:<br><br><br>* `Ordinary`: General allowlist.<br><br>* `Default`: Default allowlist. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/55/12494#securitygroupbindinfo) |Refer to the Sample response. |List of security group information associated with the current allowlist.<br><br>> **tip**<br><br><br>> This parameter will only be returned when there is an associated security group in the allowlist.<br> |

### SecurityGroupBindInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IpList |Array of String |["100.64. ** *.* ** /10"] |IP list in associated security groups. |
|BindMode |String |AssociateEcsIp |Security group association mode. Valid values:<br><br><br>* `IngressDirectionIp`: Inbound IP, which allows IP addresses involved in TCP and ALL protocols in the inbound source addresses of the security groups to access the database. If the source address is configured as a security group, it will be ignored.<br><br>* `AssociateEcsIp`: Associate ECS IP. This allows Elastic Compute Service instances within the security groups to access the database. Currently, only IP information from the primary network interface is supported for import.<br><br><br>> **tip**<br><br><br>> For more details on the security group association mode, see [Creating an allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).<br> |
|SecurityGroupId |String |sg\-rrzrivu0yc5cv0x588n\*\*\*\* |Associated security group ID. |
|SecurityGroupName |String |test\-sg |Associated security group name. |

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeAllowLists&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
	"RegionId": "cn-beijing",
	"InstanceId": "redis-cn0232ip1hewz****"
}
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2022041515414001021207408100610061",
        "Action": "DescribeAllowLists",
        "Version": "2020-12-07",
        "Service": "Redis",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListCategory": "Default",
                "AllowListDesc": "test allowlist",
                "AllowListIPNum": 1,
                "AllowListId": "acl-cnlf3xgczbjldzy****",
                "AllowListName": "api_test",
                "AllowListType": "DualStack",
                "AssociatedInstanceNum": 1,
                "ProjectName": "default",
                "SecurityGroupBindInfos": [
                    {
                        "BindMode": "AssociateEcsIp",
                        "IpList": [
                            "100.64.***.***/10"
                        ],
                        "SecurityGroupId": "sg-rrzrivu0yc5cv0x588n****",
                        "SecurityGroupName": "test-sg"
                    }
                ]
            }
        ]
    }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

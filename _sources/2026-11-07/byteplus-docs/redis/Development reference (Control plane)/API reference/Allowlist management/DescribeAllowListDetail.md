---
title: "DescribeAllowListDetail"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/describeallowlistdetail"
---

Call the DescribeAllowListDetail API to query details about the target allowlist, including IP addresses and details about bound instances.

## Request type

Synchronous request.

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAllowListDetail&serviceCode=Redis&version=2020-12-07&groupName=白名单管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-cn022p4qmcz2p26\*\*\*\* |Allowlist ID<br><br>> **tip**<br><br><br>> You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) API to query all allowlist information for the current account within a specified region, including the allowlist ID.<br> |

## Response parameters

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-cn022p4qmcz2p26\*\*\*\* |Allowlist ID |
|AllowListCategory |String |Default |Allowlist type. Valid values:<br><br><br>* `Ordinary`: General allowlist.<br><br>* `Default`: Default allowlist. |
|AllowListName |String |api_test |Allowlist name. |
|AllowListDesc |String |test allowlist |Description of the allowlist. |
|AllowListType |String |DualStack |This field is deprecated and no longer used. Disregard it. |
|AllowList |String |10.1. ** *.* **  |The list of IP addresses in the allowlist. |
|AssociatedInstances |Array of [AssociatedInstanceInfo](https://docs.byteplus.com/en/docs/55/12492#associatedinstanceinfo) |Refer to the Sample response. |Instances associated with the current allowlist. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/55/12492#securitygroupbindinfo) |Refer to the Sample response. |Information about the security group associated with the allowlist.<br><br>> **tip**<br><br><br>> This parameter will only be returned when there is an associated security group in the allowlist.<br> |
|ProjectName |String |default |The name of the project to which the allowlist belongs. |
|AssociatedInstanceNum |Integer |1 |The total number of instances associated with the allowlist. |

### AssociatedInstanceInfo

|**Parameters** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |redis\-cn02j292it8lc\*\*\*\* |ID of the instance associated with the current allowlist. |
|InstanceName |String |test |The name of the instance associated with the current allowlist. |
|VPC |String |vpc\-1g0moeeypecjk8ibuxwu8\*\*\*\* |The ID of the instance's virtual private cloud. |
|ProjectName |String |default |The name of the project to which the instance belongs. |

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
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=DescribeAllowListDetail&Version=2020-12-07 HTTP/1.1
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
          "RequestId": "2022041515414001021207408100610061",
          "Action": "DescribeAllowListDetail",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": {
         "AllowList": "10.0.***.***",
         "AllowListCategory": "Default",
         "AllowListDesc": "test allowlist",
         "AllowListId": "acl-cn022p4qmcz2p26****",
         "AllowListName": "api_test",
         "AllowListType": "DualStack",
         "ProjectName": "default",
         "AssociatedInstances": [
             {
                 "InstanceId": "redis-cn02j292it8lc****",
                 "InstanceName": "test",
                 "VPC": "vpc-1g0moeeypecjk8ibuxwu8****",
                 "ProjectName": "default"
             }
         ],
        "SecurityGroupBindInfos": [
        {
            "BindMode": "AssociateEcsIp",
            "IpList": [
            "100.64.***.***/10"
            ],
            "SecurityGroupId": "sg-rrzrivu0yc5cv0x588n****",
            "SecurityGroupName": "test-sg"
        }
        ],
        "AssociatedInstanceNum": 1
  }
}
```

## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/redis/error-code).

---
title: "DescribeAllowListDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlistdetail1"
---

Call the DescribeAllowListDetail API to view the details of an allowlist.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-b2a5bf3e471c433096232082c199\*\*\*\* |The allowlist ID.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in a specified region, including the allowlist ID. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account with permissions limited to a specific project, this parameter must be specified. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|AllowList |String |10.1. ** *.* ** ,10.2. ** *.* ** /24 |The list of IP addresses in the allowlist. |
|AllowListCategory |String |Default |Classification of the whitelist. Values:<br><br><br>* `Ordinary`: Ordinary whitelist.<br><br>* `Default`: Default whitelist.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Ordinary`. |
|AllowListDesc |String |test |The remarks for the allowlist. |
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\* |The allowlist ID. |
|AllowListName |String |test |The name of the allowlist. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Currently, only IPv4 addresses are supported. |
|AssociatedInstances |Object[] |[{ "InstanceId": "mysql\-e26822cf\*\*\*\*", "InstanceName": "test", "VPC": "vpc\-3tgjebmlgq4e8i4m\*\*\*" }] |Information about the instances bound to the current allowlist. |
|InstanceId |String |mysql\-h441603c\*\*\*\* |The ID of the instance bound to the current whitelist. |
|InstanceName |String |test |The name of the instance bound to the current whitelist. |
|InstanceStatus |String |Running |Instance status. |
|IsLatest |Boolean |true |Whether the latest whitelist has been synchronized. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No.<br><br><br>tip<br><br>When modifying the whitelist, if the instance status is not **Running**, the allowlist modification will not be immediately synchronized to the instance. |
|VPC |String |vpc\-2743n1ihbxla87fap8tap\*\*\*\* |The ID of the private network to which the instance belongs. |
|SecurityGroupBindInfos |Object[] |Refer to the response example. |Information about the security groups associated with the allowlist.<br><br>tip<br><br>If the allowlist is not bound to a security group, this parameter will not be returned. |
|BindMode |String |AssociateEcsIp |The mode of associating the security group. Values:<br><br><br>* `IngressDirectionIp`: Inbound IP.<br><br>* `AssociateEcsIp`: Associate ECS IP.<br><br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|SecurityGroupId |String |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID.<br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|IpList |String[] |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |The IP of the security group. |
|UserAllowList |String |10. ** *.* ** .1 |The IP addresses manually entered in this allowlist. The IPs in the `AllowList` field are the union of the IPs in `UserAllowList` and `SecurityGroupBindInfos`. |
|ProjectName |String |default |The project to which the allowlist belongs.<br><br>tip<br><br>If the allowlist is a legacy allowlist and has not been assigned to a specific project, an empty value will be returned. |

## Sample request

```json
POST /?Action=DescribeAllowListDetail&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031919065456B2AA76C3D558CD4485",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowList": "1.1.1.1,2.2.2.2",
        "AllowListCategory": "Ordinary",
        "AllowListDesc": "",
        "AllowListId": "acl-04908986ad034ac0ba1fb1e3a754****",
        "AllowListName": "测试白名单",
        "AllowListType": "IPv4",
        "AssociatedInstances": [
            {
                "InstanceId": "mysql-b11255cc****",
                "InstanceName": "测试实例1",
                "InstanceStatus": "Restarting",
                "IsLatest": false,
                "VPC": "vpc-b81xq5qk9wjk28j06k3l****"
            },
            {
                "InstanceId": "mysql-d7127b90****",
                "InstanceName": "测试实例2",
                "InstanceStatus": "Running",
                "IsLatest": true,
                "VPC": "vpc-b8pzuqn05yio28j06j1v****"
            }
        ],
        "SecurityGroupBindInfos": [
            {
                "BindMode": "IngressDirectionIp",
                "IpList": [
                    "1.1.1.1",
                    "2.2.2.2"
                ],
                "SecurityGroupId": "sg-24mm6n4***1hc4acvz5is****",
                "SecurityGroupName": "测试安全组"
            }
        ],
        "UserAllowList": "1.***.***.0,2.***.***.0"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

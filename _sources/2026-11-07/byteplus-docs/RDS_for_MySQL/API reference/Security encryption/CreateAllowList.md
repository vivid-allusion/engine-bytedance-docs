---
title: "CreateAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/createallowlist1"
---

Call the CreateAllowList API to create an allowlist.

## Request type

Synchronous request.

## Precautions

This API supports creating an allowlist by binding security groups or entering IP addresses. At least one method must be chosen, or both can be used simultaneously. When binding security groups, either the `SecurityGroupIds` or `SecurityGroupBindInfos` field can be used, but not both. When entering IP addresses, either the `AllowList` or `UserAllowList`field can be used, but not both.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListName |String |Yes |test |The name of the allowlist, which must meet the following requirements:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |
|AllowListDesc |String |No |test |The remark information of the allowlist, with a maximum length of 200 characters. |
|AllowListType |String |No |IPv4 |The type of IP addresses in the allowlist. Currently, only IPv4 addresses are supported. |
|AllowList |String |No |10. ** *.* ** .1,10. ** *.* ** .0/24 |Enter IP addresses or CIDR\-formatted IP address ranges.<br><br>tip<br><br><br>* Each allowlist group supports a maximum of 300 IP addresses or CIDR\-formatted IP address ranges.<br><br>* Duplicate addresses are not allowed; multiple addresses should be separated by commas (,).<br><br>* Setting `0.0.0.0/0` allows all addresses to access.<br><br>* Setting `127.0.0.1` denies all addresses access.<br><br>* Setting both `0.0.0.0/0` and `127.0.0.1` allows all addresses access.<br><br>* Setting CIDR `192.168.1.0/24` allows IP addresses within this subnet to access.<br><br>* Setting `192.168.1.1` allows only this IP address to access.<br><br>* This field cannot be used simultaneously with the `UserAllowList` field. |
|SecurityGroupIds |String[] |No |["sg\-13fuw9bo2hlhc3n6nu4g\*\*\*\*"] |A list of security group IDs to be associated.<br><br>tip<br><br><br>* You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group information, including security group IDs. A single allowlist can add up to 10 security groups at a time.<br><br>* This field cannot be used simultaneously with `SecurityGroupBindInfos`. |
|SecurityGroupBindInfos |Object[] |No |Refer to the request example. |Information about the security groups associated with the allowlist.<br><br>tip<br><br>This field cannot be used simultaneously with `SecurityGroupIds`. |
|BindMode |String |Yes |AssociateEcsIp |The mode of associating the security group. Values:<br><br><br>* `IngressDirectionIp`: Inbound IP.<br><br>* `AssociateEcsIp`: Associate ECS IP.<br><br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|SecurityGroupId |String |Yes |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID.<br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|IpList |String[] |No |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |The IP of the security group. |
|SecurityGroupName |String |No |Test security group |Security group name.<br><br>tip<br><br>In the DescribeAllowLists interface, this field is not returned when SecurityGroupBindInfoObject is used as a return parameter. |
|AllowListCategory |String |No |Default |Classification of the whitelist. Values:<br><br><br>* `Ordinary`: Ordinary whitelist.<br><br>* `Default`: Default whitelist.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Ordinary`. |
|UserAllowList |String |No |11. ** *.* ** .1,10. ** *.* ** .0/24 |IP addresses outside the security group that need to be added to the allowlist. You can enter IP addresses or CIDR\-formatted IP address ranges.<br><br>tip<br><br>This field cannot be used simultaneously with the `AllowList` field. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account with permissions limited to a specific project, this parameter must be provided. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |The ID of the allowlist. |

## Sample request

```json
POST /?Action=CreateAllowList&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListName": "test1234",
    "AllowList": "10.1.1.1,10.2.3.0/24",
    "SecurityGroupIds": [
        "sg-13fuw9bo2hlhc3n6nu4g****"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20220916143231010225099008069A****",
        "Action": "CreateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****"
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

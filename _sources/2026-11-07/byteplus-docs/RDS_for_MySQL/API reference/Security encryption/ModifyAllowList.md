---
title: "ModifyAllowList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyallowlist1"
---

Call the ModifyAllowList API to modify an allowlist.

## Request type

Asynchronous request.

## Precautions

* This API supports modifying the allowlist by binding security groups or entering IP addresses, and both methods can be used simultaneously. When binding security groups, you can use either the SecurityGroupIds or SecurityGroupBindInfos field, but these two fields cannot be used together. When entering IP addresses, you can use either the AllowList or UserAllowList field, but these two fields cannot be used together.

* If you use this API to modify the security groups bound to the allowlist, only the overwrite modification method is supported, meaning the request parameter ModifyMode must be set to `Cover`. If you need to modify both the security groups and IP addresses of the allowlist, be aware of the impact of the overwrite modification method on the IP addresses.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-04908986ad034ac0ba1fb1e3a754\*\*\*\* |The ID of the allowlist.<br><br>tip<br><br>You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in the specified region, including the allowlist ID. |
|AllowListName |String |Yes |test |The name of the allowlist.<br><br>tip<br><br><br>* To modify the IP addresses of an existing allowlist, simply enter the name of the original allowlist. You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in the specified region, including the allowlist name.<br><br>* To modify the allowlist name, simply enter the new allowlist name. The name must meet the following requirements:<br><br>   * Cannot start with a number or hyphen (\-).<br><br>   * Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>   * Must be 1~32 characters in length. |
|ModifyMode |String |No |Cover |The modification methods and value ranges are as follows:<br><br><br>* `Cover` (default value): Use the values in the `AllowList` parameter to overwrite the original whitelist.<br><br>* `Append`: Add the IP addresses entered in the `AllowList` parameter to the original whitelist.<br><br>* `Delete`: Delete the IP addresses entered in the `AllowList`parameter from the original whitelist. At least one IP address must be retained. |
|AllowListDesc |String |No |test |The remarks of the allowlist, which cannot exceed 200 characters in length. |
|AllowList |String |No |192. ** *.* ** .1 |IP addresses outside the security group that need to be added to the allowlist. You can enter IP addresses or CIDR\-formatted IP address ranges.<br><br>tip<br><br><br>* Each allowlist supports a maximum of 300 IP addresses or CIDR\-formatted IP address ranges.<br><br>* Duplicate addresses are not allowed. Multiple addresses should be separated by commas (,).<br><br>* Setting `0.0.0.0/0` allows all addresses to access.<br><br>* Setting `127.0.0.1` denies all addresses from accessing.<br><br>* Setting both `0.0.0.0/0` and `127.0.0.1` allows all addresses to access.<br><br>* Setting the CIDR `192.168.1.0/24` allows IP addresses within this subnet to access.<br><br>* Setting `192.168.1.1` allows only this IP address to access.<br><br>* This field cannot be used simultaneously with UserAllowList. |
|ApplyInstanceNum |Integer |No |1 |The number of instances bound to the current allowlist.<br><br>tip<br><br><br>* This parameter is required when modifying the AllowList or UserAllowList parameters.<br><br>* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to query all allowlist information in the specified region, including the total number of instances bound to the allowlist. |
|SecurityGroupIds |String[] |No |["sg\-13fuw9bo2hlhc3n6nu4g\*\*\*\*"] |The list of security group IDs to be modified.<br><br>tip<br><br><br>* You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group information, including security group IDs.<br><br>* A single allowlist can add up to 10 security groups at a time.<br><br>* This field cannot be used simultaneously with SecurityGroupBindInfos. |
|SecurityGroupBindInfos |Object[] |No |Please refer to the request example. |Information about the security groups associated with the allowlist.<br><br>tip<br><br>This field cannot be used simultaneously with SecurityGroupIds. |
|BindMode |String |Yes |AssociateEcsIp |The mode of associating the security group. Values:<br><br><br>* `IngressDirectionIp`: Inbound IP.<br><br>* `AssociateEcsIp`: Associate ECS IP.<br><br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|SecurityGroupId |String |Yes |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID.<br><br>tip<br><br>In the CreateAllowList interface, the BindMode and SecurityGroupId fields of the SecurityGroupBindInfoObject are required. |
|IpList |String[] |No |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |The IP of the security group. |
|SecurityGroupName |String |No |Test security group |Security group name.<br><br>tip<br><br>In the DescribeAllowLists interface, this field is not returned when SecurityGroupBindInfoObject is used as a return parameter. |
|AllowListCategory |String |No |Default |Classification of the whitelist. Values:<br><br><br>* `Ordinary`: Ordinary whitelist.<br><br>* `Default`: Default whitelist.<br><br><br>tip<br><br>When this parameter is used as a request parameter, the default value is `Ordinary`. |
|UserAllowList |String |No |10. ** *.* ** .1,10. ** *.* ** .0/24 |IP addresses outside the security group that need to be added to the allowlist. You can enter IP addresses or CIDR\-formatted IP address ranges.<br><br>tip<br><br>This field cannot be used simultaneously with AllowList. |
|UpdateSecurityGroup |Boolean |No |true |Whether to update the security groups bound to the allowlist.<br><br><br>* `true`: Update.<br><br>* `false`: Do not update. Default value.<br><br><br>tip<br><br>This field only takes effect when the allowlist has already bound security groups. You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) API to check whether the allowlist has bound security groups. |
|IgnoreInstanceStatus |Boolean |No |true |Whether to ignore instance status verification. Valid values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. Default value. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account with permissions only for a specific project, this request parameter must be provided. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyAllowList&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-63f61303c8ca430ebffb4eccd12d****",
    "AllowListName": "test1234",
    "AllowList": "10.1.1.1,10.2.3.0/24",
    "ModifyMode": "Append",
    "ApplyInstanceNum": 0,
    "SecurityGroupIds": [
        "sg-mjhwycciqgow5smt1bp6****",
        "sg-rr01k8rpkh6ov0x57uk****"
    ]
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022031913012601022509900809B3****",
        "Action": "ModifyAllowList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

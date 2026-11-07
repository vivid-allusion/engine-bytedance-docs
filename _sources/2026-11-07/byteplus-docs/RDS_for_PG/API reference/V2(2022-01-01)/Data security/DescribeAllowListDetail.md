---
title: "DescribeAllowListDetail"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlistdetail"
---

Call the DescribeAllowListDetail API to query the allowlist details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-fe1339b0024e42ca9872e8f4af12\*\*\*\* |Allowlist ID |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-fe1339b0024e42ca9872e8f4af12\*\*\*\* |Allowlist ID |
|AllowListName |String |Test allowlists |Name of the allowlists. |
|AllowListDesc |String |This is a description of an allowlist. |Description of the allowlist. |
|AllowListType |String |IPv4 |Network protocol type used by the allowlist. Value is `IPv4`. |
|AllowList |String |10.1.1.1,10.2.2.0/24 |List of IP addresses or CIDR blocks in the allowlists. |
|AllowListCategory |String |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter has no default value when used as a request parameter. If not provided, it queries allowlists of all categories.</div><br> |
|AssociatedInstanceNum |Long |8 |Number of instances bound to the allowlist. |
|AssociatedInstances |Array of [AssociatedInstanceObject](https://docs.byteplus.com/en/docs/61/20786#associatedinstanceobject) |Refer to the sample response. |The allowlists\-associated instances list includes instance ID and instance name information. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/61/20786#securitygroupbindinfo) |Refer to the sample response. |List of security groups bound to this allowlist. |
|UserAllowList |String |10.1.1.1,10.2.3.0/24 |IP address added to the allowlists outside the security group. |


<span id="associatedinstanceobject"></span>
### AssociatedInstanceObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-e49268e4\*\*\*\* |Instance ID. |
|InstanceName |String |This is an instance name |Name of the instance. |
|VPC |String |vpc\-b81xq5qk9wjk28j06k3l\*\*\*\* |The ID of the instance's virtual private cloud. |


<span id="securitygroupbindinfo"></span>
### SecurityGroupBindInfo


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|IpList |Array of String |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |IP address in the security group. |
|BindMode |String |IngressDirectionIp |The mode for associating a security group. Values:<br><br><br>* `IngressDirectionIp`: ingress direction IP.<br><br>* `AssociateEcsIp`: associated ECS IP. |
|SecurityGroupId |String |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID. |
|SecurityGroupName |String |Test security group |Security group name. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeAllowListDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-fe1339b0024e42ca9872e8f4af12****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507171609269A59EE64CB5BAB44E8A6-33e3b7",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowList": "1.***.***.1,192.***.***.40,192.***.***.108,192.16***8.***.3",
        "AllowListCategory": "Ordinary",
        "AllowListDesc": "",
        "AllowListId": "acl-9a5faa2306a945b69fea4a65f31f****",
        "AllowListName": "test_allowlist",
        "AllowListType": "IPv4",
        "AssociatedInstanceNum": 8,
        "AssociatedInstances": [
            {
                "InstanceId": "postgres-f006d308****",
                "InstanceName": "测试实例",
                "VPC": "vpc-2gdku6nvnp1xc50ztz0py****"
            }
        ],
        "SecurityGroupBindInfos": [
            {
                "BindMode": "AssociateEcsIp",
                "SecurityGroupId": "sg-2gdgzrxi8uigw50ztz0e9****"
            },
            {
                "BindMode": "AssociateEcsIp",
                "IpList": [
                    "192.***.***.40",
                    "192.***.***.108",
                    "192.***.***.3"
                ],
                "SecurityGroupId": "sg-2gdku6tsr17uo50ztyz9h****"
            },
            {
                "BindMode": "AssociateEcsIp",
                "SecurityGroupId": "sg-30ud5qcwpx6v47r2qr1kl****"
            }
        ],
        "UserAllowList": "1.***.***.1"
    }
}
```

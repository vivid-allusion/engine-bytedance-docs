---
title: "DescribeAllowLists"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists"
---

Call the DescribeAllowLists API to query the allowlists list in a specific region.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|RegionId |String |Yes |cn\-beijing |Region ID. Call the [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_PG/describeregions) API to query available regions. |
|InstanceId |String |No |postgres\-sdasd\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this parameter is not set, return all allowlists under the current region. If this parameter is set, return all allowlists of the instance.</div><br> |
|AllowListCategory |String |No |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter has no default value when used as a request parameter. If not provided, it queries allowlists of all categories.</div><br> |
|AllowListDesc |String |No |This is a description of an allowlist. |Description of the allowlist. Fuzzy search by description information is supported. |
|AllowListId |String |No |acl\-fe1339b0024e42ca9872e8f4af12\*\*\*\* |Allowlist ID. |
|AllowListName |String |No |Test_Allowlist |Name of the allowlists. |
|IPAddress |String |No |"2.2.2.2,1.1.1.1" |Search allowlists by IP address. Multiple IP addresses are supported. Separate multiple IP addresses with commas (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If an allowlist contains any subset of the specified IP addresses, the allowlist is returned.</div><br> |
|PageNumber |Long |No |2 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Long |No |20 |Number of records per page. The minimum value is 1, and the maximum value does not exceed the Integer's maximum value. Default value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowLists |Array of [AllowListObject](https://docs.byteplus.com/en/docs/61/20785#allowlistobject) |Refer to the sample response. |Allowlist information. |
|Total |Long |20 |Total number of allowlists. |


<span id="allowlistobject"></span>
### AllowListObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListDesc |String |This is a description of an allowlist. |Description of the allowlist. |
|AllowListIPNum |Integer |2 |Quantity of IP addresses or IP address ranges in the allowlist. |
|AllowListId |String |acl\-fe1339b0024e42ca9872e8f4af12\*\*\*\* |Allowlist ID |
|AllowListName |String |This is an allowlist name |Name of the allowlists. |
|AllowListType |String |IPv4 |Network protocol type used by the allowlist. Value is `IPv4`. |
|AssociatedInstanceNum |Integer |3 |Number of instances bound to the allowlist. |
|AllowListCategory |String |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter has no default value when used as a request parameter. If not provided, it queries allowlists of all categories.</div><br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/61/20785#securitygroupbindinfo) |Refer to the sample response. |Information about the security group associated with the allowlist. If the allowlist is not associated with a security group, then return`null`。 |


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
POST /?Action=DescribeAllowLists&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "RegionId": "cn-guangzhou",
    "InstanceId": "postgres-4b38053d****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423185439A247C098FE59A9DE6193-3ecfa4",
        "Action": "DescribeAllowLists",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListCategory": "Ordinary",
                "AllowListDesc": "",
                "AllowListIPNum": 4,
                "AllowListId": "acl-9a5faa2306a945b69fea4a65f31f****",
                "AllowListName": "test-allowlist",
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 0,
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
                ]
            }
        ]
    }
}
```

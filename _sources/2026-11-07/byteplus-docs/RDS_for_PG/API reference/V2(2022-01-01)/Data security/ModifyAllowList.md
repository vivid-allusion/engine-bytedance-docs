---
title: "ModifyAllowList"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifyallowlist"
---

Call the ModifyAllowList API to modify the allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-2b7d64502b0a4210a24c58e739de\*\*\*\* |Allowlist ID Refer to the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists) API for the query |
|AllowListName |String |Yes |New allowlist name |Can be the same as the original allowlist name or different. If different, the allowlist will be renamed using the value in the AllowListName field. The naming rules for allowlists are as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1\-128 characters. |
|AllowListDesc |String |No |This is a new allowlist description. |Description of the allowlist. Length is within 200 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If this parameter is not set, the original description information is not modified.</div><br> |
|AllowList |String |No |10.1.1.1,10.2.3.0/24 |IP address included in the allowlist. Multiple IP addresses are separated by commas (,). IP address cannot be duplicated. The following two formats are supported:<br><br><br>* IP address format. For example: `10.23.12.24`.<br><br>* IP address range in CIDR format. For example: `10.23.12.0/24` (classless inter\-domain routing, 24 indicates the prefix length in the address, ranging from 1 to 32).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each allowlist can contain up to 300 IPs or CIDR blocks. When there are many IPs, it is recommended to merge them into CIDR blocks, such as 10.23.12.0/24.</div><br><br><br>* <div data-tips="true" data-tips-type="default">It is forbidden to add IP addresses, in the form of <code>x.x.x.x/0</code> other than <code>0.0.0.0/0</code>, to the allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Default value. If this parameter is not set, the original IPs in the allowlist are not modified.</div><br> |
|ModifyMode |String |No |Cover |Modify an allowlist method. Values:<br><br><br>* `Cover`: overwrite, which means overwriting the original allowlist with the value of the AllowList field. Default value.<br><br>* `Append`: append, which means adding the IP addresses contained in the AllowList field to the original allowlists.<br><br>* `Delete`: delete, which means deleting the IP addresses contained in the AllowList field from the original allowlists. At least one IP address must be retained.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the allowlist to be modified is bound to a security group, or if the allowlist needs to be bound to a security group when modifying it, ModifyMode can only be set to <code>Cover</code>.</div><br> |
|ApplyInstanceNum |Integer |No |1 |The quantity of instances bound to this allowlist, used to confirm the impact scope of this modification and prevent incorrect operations.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Default value. If no value is passed, it means no confirmation is required for the number of instances affected by modifying the allowlist.</div><br> |
|AllowListCategory |String |No |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter has no default value when used as a request parameter. If not provided, it queries allowlists of all categories.</div><br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/61/20788#securitygroupbindinfo) |No |Refer to the request example. |Information about the security group associated with the allowlist. |
|UpdateSecurityGroup |Boolean |No |true |Whether to update the security group bound to the allowlist. Values:<br><br><br>* `true`: update.<br><br>* `false`: do not update. Default value. |
|UserAllowList |String |No |10.1.1.1,10.2.3.0/24 |The IP address outside the security group that needs to be added to the allowlists. You can enter an IP address or an IP address range in CIDR format. |


<span id="securitygroupbindinfo"></span>
### SecurityGroupBindInfo


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|IpList |Array of String |No |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |IP address in the security group. |
|BindMode |String |Yes |IngressDirectionIp |The mode for associating a security group. Values:<br><br><br>* `IngressDirectionIp`: ingress direction IP.<br><br>* `AssociateEcsIp`: associated ECS IP. |
|SecurityGroupId |String |Yes |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID. |
|SecurityGroupName |String |No |Test security group |Security group name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListId": "acl-2b7d64502b0a4210a24c58e739de****",
    "AllowList": "10.1.1.1,10.2.3.0/23",
    "AllowListDesc": "这是一段新的白名单描述信息。",
    "AllowListName": "新的白名单名称",
    "AllowListType": "IPv4",
    "ModifyMode": "Cover"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423192049E80D10ED81E54EDC1083-5373b8",
        "Action": "ModifyAllowList",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": null
}
```

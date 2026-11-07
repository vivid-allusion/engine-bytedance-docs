---
title: "CreateAllowList"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/createallowlist"
---

Call the CreateAllowList API to create an allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAllowList&serviceCode=rds_postgresql&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|AllowListName |String |Yes |Test allowlists |The naming rules for allowlists are as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1\-128 characters. |
|AllowListDesc |String |No |This is a test allowlist |Description of the allowlist. Length is within 200 characters. The default value is an empty string. |
|AllowListType |String |No |IPv4 |Network protocol type used by the allowlist. Value is `IPv4` (default value). |
|AllowList |String |No |10.1.1.1,10.2.3.0/24 |IP address included in the allowlist. Multiple IP addresses are separated by commas (,). IP address cannot be duplicated. The following two formats are supported:<br><br><br>* IP address format. For example: `10.23.12.24`.<br><br>* IP address range in CIDR format. For example: `10.23.12.0/24` (classless inter\-domain routing, where 24 indicates the prefix length in the address, ranging from 1 to 32).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Each allowlist can contain up to 300 IPs or CIDR blocks. When there are many IPs, it is recommended to merge them into CIDR blocks, such as 10.23.12.0/24.</div><br><br><br>* <div data-tips="true" data-tips-type="default">IP addresses ending with <code>x.x.x.x/0</code> except <code>0.0.0.0/0</code> are prohibited from being added to the allowlists.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If passed together with UserAllowList, the value of UserAllowList takes precedence.</div><br> |
|AllowListCategory |String |No |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter has no default value when used as a request parameter. If not provided, it queries allowlists of all categories.</div><br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/61/20787#securitygroupbindinfo) |No |Refer to the request example. |Information on security groups that need to be associated with the allowlists. |
|UserAllowList |String |No |10.1.1.1,10.2.3.0/24 |The IP address outside the security group that needs to be added to the allowlists. You can enter an IP address or an IP address range in CIDR format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this field is passed together with AllowList, the value of this field takes precedence.</div><br> |


<span id="securitygroupbindinfo"></span>
### SecurityGroupBindInfo


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|IpList |Array of String |No |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |IP address in the security group. |
|BindMode |String |Yes |IngressDirectionIp |The mode for associating a security group. Values:<br><br><br>* `IngressDirectionIp`: ingress direction IP.<br><br>* `AssociateEcsIp`: associated ECS IP. |
|SecurityGroupId |String |Yes |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID. |
|SecurityGroupName |String |No |Test security group |Security group name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|AllowListId |String |acl\-2b7d64502b0a4210a24c58e739de\*\*\*\* |Allowlist ID |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "AllowListDesc": "这是一个测试白名单",
    "AllowListName": "测试白名单",
    "AllowList": "10.1.1.1,10.2.3.0/24",
    "SecurityGroupIds": [
        "sg-13fuw9bo2hlhc3n6nu4g****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024042319123272910D61D1EA53CF50B2-0a580d",
        "Action": "CreateAllowList",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AllowListId": "acl-2b7d64502b0a4210a24c58e739de****"
    }
}
```

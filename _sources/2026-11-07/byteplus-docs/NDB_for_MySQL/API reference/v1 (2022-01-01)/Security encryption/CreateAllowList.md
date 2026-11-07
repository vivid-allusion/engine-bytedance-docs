---
title: "CreateAllowList"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateAllowList"
---

Call the CreateAllowList to create a new allowlist.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAllowList&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|AllowListName |String |Yes |test |Allowlist name. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |
|AllowList |String |No |127.0.0.1 |Enter an IP address or an IP address segment in CIDR format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If passed with <code>UserAllowList</code>, the value of <code>UserAllowList</code> takes precedence.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Each allowlist group can contain up to 300 IP addresses or IP address segments in CIDR format. Duplicate addresses are not allowed. Separate multiple addresses with commas (,). The following are special examples:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Setting <code>0.0.0.0/0</code> allows access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Setting <code>127.0.0.1</code> blocks access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Setting both <code>0.0.0.0/0</code> and <code>127.0.0.1</code> allows access from all addresses.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Setting <code>192.168.1.1</code> allows access from this IP address only.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Setting CIDR <code>192.168.1.0/24</code> allows access from IP addresses within that network segment.</div><br> |
|AllowListDesc |String |No |test |The description of the allowlist cannot exceed 200 characters. |
|AllowListType |String |No |IPv4 |The type of IP addresses in the allowlist. Only `IPv4` is currently supported, representing an IPv4 address. |
|ProjectName |String |No |default |The name of the project to which the allowlist belongs. If this parameter is left empty, the new allowlist is added to the `default` project. |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/265/57377#securitygroupbindinfo) |No |See the request example |The security group information associated with the allowlist. |
|UserAllowList |String |No |192.168.\*\*\*.7 |The Internet protocol address outside the security group that needs to be added to the allowlists. Enter an IP address or a CIDR block. Separate multiple addresses with a comma (,).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this field and <code>AllowList</code> are both passed, the Value of this field takes precedence.</div><br> |


<span id="securitygroupbindinfo"></span>
### SecurityGroupBindInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|IpList |Array of String |No |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |The list of IP addresses in the security group. |
|BindMode |String |No |IngressDirectionIp |The mode for associating a security group. Value:<br><br><br>* `IngressDirectionIp`: Ingress direction IP.<br><br>* `AssociateEcsIp`: Associated ECS IP. |
|SecurityGroupId |String |No |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID. |
|SecurityGroupName |String |No |Test security group |Security group name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlist ID |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=CreateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "AllowListName": "test",
    "AllowList": "127.0.0.1",
    "AllowListDesc": "test",
    "AllowListType": "IPv4"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20220316143231010225099008069A****",
        "Action": "CreateAllowList",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowListId": "acl-d1fd76693bd54e658912e7337d5b****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).

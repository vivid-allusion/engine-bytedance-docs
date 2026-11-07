---
title: "ModifyAllowList - Modify an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/ModifyAllowList"
---

Call the ModifyAllowList API to modify the allowlist of an instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|OsrB6A">必选</span> `Example value: ModifyAllowList`

The operation to perform. The value is `ModifyAllowList`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|wqs2Zc">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example value: test`

Project name.



**AllowListId ** <span data-label="purple">string </span><span data-api-tag="require|XCAY6a">必选</span> `Example value: acl-04908986ad034ac0ba1fb1e3a754****`

The allowlist IDs.



**AllowListName ** <span data-label="purple">string </span><span data-api-tag="require|XjhhW6">必选</span> `Example value: test`

Allowlist name.



**AllowListDesc ** <span data-label="purple">string </span>`Optional` `Example value: Description`

The allowlist description.



**AllowList ** <span data-label="purple">string </span>`Optional` `Example value: 10.1.****.****`

An IP address or an IP address range in CIDR format.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The AllowList and SecurityGroupBindInfos parameters cannot both be empty.</div>


* <div data-tips="true" data-tips-type="tip">Do not set duplicate addresses. Separate multiple addresses with a comma (,).</div>


* <div data-tips="true" data-tips-type="tip">If you set <code>0.0.0.0/0</code>, it allows access from all addresses, and the <code>0.0.0.0/0</code> entry has a higher priority than other network ranges.</div>


* <div data-tips="true" data-tips-type="tip">Setting the CIDR to <code>192.168.1.0/24</code> allows access from IP addresses within that network range; setting <code>192.168.1.1</code> allows access from only that IP address.</div>




**UserAllowList ** <span data-label="purple">string </span>`Optional` `Example: 0.0.****.****/0,192.168.****.****/24`

The IP addresses outside the security group that need to be added to the allowlist. You can enter an IP address or an IP address range in CIDR format.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this field is used with the AllowList field, UserAllowList takes precedence.</div>




**ModifyMode ** <span data-label="purple">string </span>`Optional` `Example value: Cover`

The modification mode. Valid values:

`Cover`: Overwrites the original allowlist with the value of the AllowList parameter.



**ApplyInstanceNum ** <span data-label="purple">integer </span>`Optional` `Example value: 2`

The number of instances associated with the current allowlist.


* This parameter is required when modifying the IP addresses in the allowlist (the `AllowList` parameter) or its associated security groups (the `SecurityGroupBindInfos` parameter).

* The value for this parameter must match the number of instances currently associated with the allowlist; otherwise, the API call will return an error.

* You can call the [DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowLists) API to query information about all allowlists in a specified region under the current account, including the total number of associated instances (the value of the `AssociatedInstanceNum` parameter in the response).



**AllowListCategory ** <span data-label="purple">string </span>`Optional` `Example value: Ordinary`

The allowlist category. Possible values:


* `Ordinary`: An ordinary allowlist. Default value.

* `Default`: A default allowlist.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=ModifyAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "AllowListId": "acl-ba7e0e2ab5f04a9f94dc397a9a******",
    "AllowListName": "test",
    "AllowListDesc": "test",
    "AllowList": "0.0.****.****/0,192.168.****.****/24",
    "ApplyInstanceNum": 0,
    "SecurityGroupBindInfos": [
        {
            "BindMode": "AssociateEcsIp",
            "IpList": [
                "172.31.0.4"
            ],
            "SecurityGroupId": "sg-3ez4xt2d8vf2872200s******",
            "SecurityGroupName": "Default"
        },
        {
            "BindMode": "IngressDirectionIp",
            "IpList": [
                "192.168.0.0/16"
            ],
            "SecurityGroupId": "sg-3f01ez24xury872200******",
            "SecurityGroupName": "sg-for-vpc-b8pzuqn05yio28j0******"
        }
    ],
    "AllowListCategory": "Default",
    "UserAllowList": "0.0.****.****/0,192.168.****.****/24"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20251117170520211075046087E62647",
    "Action": "ModifyAllowList",
    "Version": "2022-01-01",
    "Service": "rds_mssql",
    "Region": "cn-beijing"
  },
  "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |

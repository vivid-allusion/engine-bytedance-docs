---
title: "CreateAllowList - Create an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createAllowList"
---

Call the CreateAllowList API to create an allowlist.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Synchronous request

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



Action string Example value: CreateAllowList

The operation to perform. The value is `CreateAllowList`.



Version string Example value: 2022\-01\-01

The API version is `2022-01-01`.



AllowListName stringExample value: Allowlist

Allowlist name.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example: Default`

Project name.



**AllowListDesc ** <span data-label="purple">string </span>`Optional` `Example value: Allowlist`

The allowlist description.



**AllowListType ** <span data-label="purple">string </span>`Optional` `Example value: IPv4`

The type of IP address in the allowlist. Only the IPv4 address type is supported.



**AllowListCategory ** <span data-label="purple">string </span>`Optional` `Example value: Ordinary`

Allowlist category. Possible values:


* `Ordinary`: Ordinary allowlist (Default value).

* `Default`: Default allowlist.



**UserAllowList ** <span data-label="purple">string </span>`Optional` `Example value: 11.****.****.1,10.****.****.0/24`

The IP addresses outside the security group that need to be added to the allowlist. Enter an IP address or an IP address range in CIDR format.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this field and AllowList are both specified, UserAllowList takes precedence.</div>




**SecurityGroupBindInfos ** <span data-label="purple">object[] </span>`Optional` `Example value: [ { "BindMode": "IngressDirectionIp", "IpList": [ "10.1.1.2/32", "10.1.1.1/32" ], "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******", "SecurityGroupName": "Default" } ]`

Information about the security groups associated with the allowlist.



**AllowList ** <span data-label="purple">string </span>`Optional` `Example value: 10.1.****.****`

An IP allowlist. Separate multiple IP addresses with commas (,). Duplicates are not allowed. The following two formats are supported:


* IP address format, e.g., 10.23.12.24.

* CIDR format, e.g., 10.23.12.0/24 (Classless Inter\-Domain Routing, where 24 represents the prefix length in the address, with a range from `1 to 32`).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The AllowList and SecurityGroupBindInfos parameters cannot both be empty.</div>


* <div data-tips="true" data-tips-type="tip">Setting <code>0.0.0.0/0</code> allows access from all addresses, and the <code>0.0.0.0/0</code> entry takes priority over other network segments.</div>


* <div data-tips="true" data-tips-type="tip">Setting the CIDR to <code>192.168.1.0/24</code> allows access from IP addresses within that network segment; setting <code>192.168.1.1</code> allows access from only that IP address.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AllowListId ** <span data-label="purple">string </span>`Example value: acl-ba7e0e2ab5f04a9f94dc397a9****`

The allowlist IDs.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=CreateAllowList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "AllowListType": "IPv4",
    "AllowList": "0.0.0.0/0",
    "AllowListName": "test",
    "AllowListDesc": "test",
    "SecurityGroupBindInfos": [
        {
            "BindMode": "AssociateEcsIp",
            "IpList": [
                "172.31.0.4"
            ],
            "SecurityGroupId": "sg-3ez4xt2d8vf2872200*******",
            "SecurityGroupName": "Default"
        },
        {
            "BindMode": "IngressDirectionIp",
            "IpList": [
                "192.168.0.0/16"
            ],
            "SecurityGroupId": "sg-3f01ez24xury872200s*******",
            "SecurityGroupName": "sg-for-vpc-b8pzuqn05yio28j06*******"
        }
    ],
    "AllowListCategory": "Default",
    "UserAllowList": "0.0.0.0/0"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202511171643460822430692037E28AA",
    "Action": "CreateAllowList",
    "Version": "2022-01-01",
    "Service": "rds_mssql",
    "Region": "cn-beijing"
  },
  "Result": {
    "AllowListId": "acl-b5a1d7f114714315b69***********"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|404 |InvalidProject.NotFound |The specified project does not exist. |The project does not exist. |

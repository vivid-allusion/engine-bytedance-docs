---
title: "DescribeInstanceAllowLists - Query the allowlists associated with an instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeInstanceAllowLists"
---

Call the DescribeInstanceAllowLists API to query the allowlists associated with an instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Q0LSQJ">必选</span> `Example: DescribeInstanceAllowLists`

The operation to perform. The value is `DescribeInstanceAllowLists`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|1jd17G">必选</span>`Example value: 2022-01-01`

The API version is `2022-01-01`.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Example value: mssql-04a9110****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> API to query the basic information of all SQL Server instances in the target region, including their instance IDs.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AuthorizedAllowLists ** <span data-label="purple">object[] </span>`Example: [ { "AllowListCategory": "Ordinary", "AllowListDesc": "", "AllowListIPNum": 2, "AllowListId": "acl-9501e882510249348c1990a30******", "AllowListName": "dyh-test-sg", "AllowListType": "IPv4", "AssociatedInstanceNum": 0, "ProjectName": "", "SecurityGroupBindInfos": [ { "BindMode": "IngressDirectionIp", "IpList": [ "10.1.1.2/32", "10.1.1.1/32" ], "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******" } ] } ]`

A list of allowlists associated with the instance.


**AllowListId ** <span data-label="purple">string </span>`Example: acl-9501e882510249348c1990a30******`

The allowlist IDs.



**AllowListName ** <span data-label="purple">string </span>`Example value: test`

Allowlist name.



**AllowListDesc ** <span data-label="purple">string </span>`Example value: Description`

Allowlist description.



**AllowListType ** <span data-label="purple">string </span>`Example value: IPv4`

The type of IP addresses in the allowlist. Only the IPv4 address type is supported.



**AllowListIPNum ** <span data-label="purple">long </span>`Example value: 2`

The number of IP addresses in the allowlist.



**AssociatedInstanceNum ** <span data-label="purple">long </span>`Example value: 0`

The number of instances associated with the allowlist.



**AssociatedLBNum ** <span data-label="purple">long </span>`Example value: 2`

The number of LBs associated with the allowlist.



**ProjectName ** <span data-label="purple">string </span>`Example: Default`

The name of the project to which the allowlist belongs.



**SecurityGroupBindInfos ** <span data-label="purple">object[] </span>`Example value: [ { "BindMode": "IngressDirectionIp", "IpList": [ "10.1.1.2/32", "10.1.1.1/32" ], "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******" } ]`

Security groups to associate with the allowlist.



**AllowListCategory ** <span data-label="purple">string </span>`Example value: Ordinary`

The allowlist category. Possible values:


* `Ordinary`: Ordinary allowlist.

* `Default`: Default allowlist.




**UnauthorizedAllowListNum ** <span data-label="purple">long </span>`Example value: 2`

The total number of unauthorized allowlists.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeInstanceAllowLists&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251117T070858Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251117/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "RegionId": "cn-beijing",
  "InstanceId": "mssql-dab1be87****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025051317510473B1EF8F50DAB40480A4-cb45fa",
        "Action": "DescribeInstanceAllowLists",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "AuthorizedAllowLists": [
            {
                "AllowListCategory": "Ordinary",
                "AllowListDesc": "",
                "AllowListIPNum": 2,
                "AllowListId": "acl-9501e882510249348c1990a30******",
                "AllowListName": "dyh-test-sg",
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 0,
                "ProjectName": "",
                "SecurityGroupBindInfos": [
                    {
                        "BindMode": "IngressDirectionIp",
                        "IpList": [
                            "10.1.1.2/32",
                            "10.1.1.1/32"
                        ],
                        "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******"
                    }
                ]
            }
        ],
        "UnauthorizedAllowListNum": 0
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |

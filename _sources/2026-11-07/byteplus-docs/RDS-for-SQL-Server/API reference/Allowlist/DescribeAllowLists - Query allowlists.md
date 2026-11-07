---
title: "DescribeAllowLists - Query allowlists"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowLists"
---

Call the DescribeAllowLists API to query allowlists.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Opkst4">必选</span> `Example value: DescribeAllowLists`

The operation to perform. The value must be `DescribeAllowLists`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|vTvCsf">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example: Default`

The project to which the allowlist belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is left empty, the allowlist name will not be used as a filter.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AllowLists ** <span data-label="purple">object[] </span>`Example value: [ { "AllowListId": "acl-cdcbb69328cd40b7a9fa5d4c2cf8****", "AllowListDesc": "test", "AllowListName": "test_allowlist", "AllowListType": "IPv4", "AllowListIPNum": 395, "AssociatedInstanceNum": 181, "ProjectName": "test_project", "AllowListCategory": "Default", "SecurityGroupBindInfos": [ { "BindMode": "IngressDirectionIp", "IpList": [ "10.1.1.2/32", "10.1.1.1/32" ], "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******" } ] } ]`

Allowlists.


**AllowListId ** <span data-label="purple">string </span>`Example: acl-cdcbb69328cd40b7a9fa5d4c2cf8****`

The allowlist IDs.



**AllowListDesc ** <span data-label="purple">string </span>`Example value: test`

Allowlist description.



**AllowListName ** <span data-label="purple">string </span>`Example value: Allowlist`

Allowlist name.



**AllowListType ** <span data-label="purple">string </span>`Example value: IPv4`

The type of IP addresses in the allowlist. Currently, only IPv4 addresses are supported.



**AllowListIPNum ** <span data-label="purple">long </span>`Example: 5`

The total number of IP addresses (or address ranges) in the allowlist.



**AssociatedInstanceNum ** <span data-label="purple">long </span>`Example value: 5`

The total number of instances associated with the allowlist.



**ProjectName ** <span data-label="purple">string </span>`Example value: Default`

The project to which the allowlist belongs.



**AllowListCategory ** <span data-label="purple">string </span>`Example: Default`

The allowlist type. The valid values are:


* `Ordinary`: An ordinary allowlist.

* `Default`: A default allowlist.



**SecurityGroupBindInfos ** <span data-label="purple">object[] </span>`Example: [ { \"BindMode\": \"AssociateEcsIp\", \"SecurityGroupId\": \"sg-b8pzuwk3i4g028j06k*****\", \"SecurityGroupName\": \"Default\" }, { \"BindMode\": \"IngressDirectionIp\", \"IpList\": [ \"0.0.0.0/0\" ], \"SecurityGroupId\": \"sg-b8pzuwk3i4g028j06k*****\", \"SecurityGroupName\": \"Default\" } ]`

The security group binding information.




**Total ** <span data-label="purple">long </span>`Example: 5`

The total number of allowlists.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeAllowLists&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****

{
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2025111717534101113502116763DB68",
    "Action": "DescribeAllowLists",
    "Version": "2022-01-01",
    "Service": "rds_mssql",
    "Region": "cn-beijing"
  },
  "Result": {
    "AllowLists": [
      {
        "AllowListId": "acl-cdcbb69328cd40b7a9fa5d4c2cf8****",
        "AllowListDesc": "test",
        "AllowListName": "test_allowlist",
        "AllowListType": "IPv4",
        "AllowListIPNum": 395,
        "AssociatedInstanceNum": 181,
        "ProjectName": "test_project",
        "AllowListCategory": "Default",
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
    "Total": 51
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |Instance does not exist. |
|500 |InternalError |The request failed with internal server error. |Internal error. |

---
title: "DescribeAllowListDetail - Queries the details of an allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/DescribeAllowListDetail"
---

Call DescribeAllowListDetail API to query the details of an allowlist.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Synchronous request

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|NJEdZ9">必选</span> `Example value: DescribeAllowListDetail`

The operation to perform. Value: `DescribeAllowListDetail`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|VhxkJQ">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**AllowListId ** <span data-label="purple">string </span><span data-api-tag="require|r5hu4Y">必选</span> `Example value: acl-f0b3a98402144871ae22d3ef******`

The allowlist IDs.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AllowListId ** <span data-label="purple">string </span>`Example: acl-9e73f3425e57405fbe7145cdac******`

The allowlist IDs.



**AllowListName ** <span data-label="purple">string </span>`Example value: test`

Allowlist name.



**AllowListDesc ** <span data-label="purple">string </span>`Example value: Allowlist`

Allowlist description.



**AllowListType ** <span data-label="purple">string </span>`Example value: IPv4`

The IP address type in the allowlist. Only the IPv4 address type is supported.



**AllowList ** <span data-label="purple">string </span>`Example value: 10.1.***.***`

The list of IP addresses in the allowlist.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP addresses in the AllowList field are the union of the IP addresses included in UserAllowList and SecurityGroupBindInfos.</div>




**AssociatedInstances ** <span data-label="purple">object[] </span>`Example value: [ { "InstanceId": "mssql-04a9110*****", "InstanceName": "mssql-04a9110*****", "VPC": "vpc-b8pzuqn05yio28j06j*****" } ]`

The list of associated instances.


**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-04a9110*****`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example value: mssql-04a9110*****`

The instance name.



**VPC ** <span data-label="purple">string </span>`Example value: vpc-b8pzuqn05yio28j06j*****`

The ID of the VPC to which the instance belongs.



**IsLatest ** <span data-label="purple">boolean </span>`Example value: true`

Indicates whether to sync the latest allowlist IPs. Possible values:


* `true`: Yes.

* `false`: No.



**InstanceStatus ** <span data-label="purple">string</span> `Example value: Deleting`

The status of the instance. The status of the instance. The valid values are:


* `Running`: Running.

* `Creating`: Creating.

* `Deleting`: Deleting.

* `Restarting`: Restarting.

* `Updating`: Changing.

* `MasterChanging`: Primary node switching.

* `Error`: Error.



**ProjectName ** <span data-label="purple">string </span>`Example: Default`

The name of the project to which the instance belongs.




**SecurityGroupBindInfos ** <span data-label="purple">object[] </span>`Example: [ { "BindMode": "IngressDirectionIp", "IpList": [ "10.1.1.2/32", "10.1.1.1/32" ], "SecurityGroupId": "sg-30up5lo07p7nk7r2qr******", "SecurityGroupName": "Default" } ]`

A list of security groups associated with the allowlist.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when the allowlist contains associated security groups.</div>




**UserAllowList ** <span data-label="purple">string </span>`Example value: 100.64.****.****/10`

The IP address you entered in this list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP addresses in the AllowList field are the union of the IP addresses included in <code>UserAllowList</code> and <code>SecurityGroupBindInfos</code>.</div>




**ProjectName ** <span data-label="purple">string </span>`Example: Default`

The name of the project.



**AssociatedInstanceNum ** <span data-label="purple">long </span>`Example value: 2`

The number of associated instances.



**AllowListCategory ** <span data-label="purple">string </span>`Example value: Default`

The allowlist category. Possible values:


* `Ordinary`: Ordinary allowlist (default value).

* `Default`: The default allowlist.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeAllowListDetail&Version=2022-01-01 HTTP/1.1
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251117T092153Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251117/cn-beijing/rds_mssql/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "AllowListId": "acl-b5a1d7f114714315b6987*********"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025051411220873B50BBA7E25A766B623-ca80a3",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowList": "0.0.****.****/0,100.64.****.****/10",
        "AllowListCategory": "Ordinary",
        "AllowListDesc": "",
        "AllowListId": "acl-9e73f3425e57405fbe7145cdac*****",
        "AllowListName": "DBW_Sole_Group_Name_For_mssql",
        "AllowListType": "IPv4",
        "AssociatedInstances": [
            {
                "InstanceId": "mssql-04a9110*****",
                "InstanceName": "mssql-04a9110*****",
                "VPC": "vpc-b8pzuqn05yio28j06j*****"
            }
        ],
        "SecurityGroupBindInfos": [
            {
                "BindMode": "AssociateEcsIp",
                "SecurityGroupId": "sg-b8pzuwk3i4g028j06k*****",
                "SecurityGroupName": "Default"
            },
            {
                "BindMode": "IngressDirectionIp",
                "IpList": [
                    "0.0.0.0/0"
                ],
                "SecurityGroupId": "sg-b8pzuwk3i4g028j06k*****",
                "SecurityGroupName": "Default"
            }
        ],
        "UserAllowList": "100.64.****.****/10",
        "ProjectName": "default",
        "AssociatedInstanceNum": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |

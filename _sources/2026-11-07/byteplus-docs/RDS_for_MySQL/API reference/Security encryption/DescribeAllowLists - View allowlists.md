---
title: "DescribeAllowLists - View allowlists"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1"
---

Call the DescribeAllowLists API to view the allow list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|RegionId |String |No |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you specify a region for this parameter, a list of allowlists that meet other query conditions in the specified region is returned. If this parameter is not specified, the returned list is empty. Call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions">DescribeRegions</a> operation to query information about the regions, including region IDs, where you can create MySQL instances.</div><br> |
|InstanceId |String |No |mysql\-h441603c\*\*\*\* |Instance ID. When you specify `InstanceId`, the `DescribeAllowLists` operation returns the allowlists associated with the specified instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the basic information about all MySQL instances in the target region, including their instance IDs.</div><br> |
|QueryDefault |Boolean |No |false |Whether to query only the default allowlist. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|IPAddress |String |No |"2.2.2.2,1.1.1.1" |Search allowlists by Internet protocol address. Multiple IP addresses are supported. Separate multiple IP addresses with commas (,).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If an allowlist contains any subset of the specified Internet protocol addresses, the allowlist is returned.</div><br> |
|ProjectName |String |No |default |The project to which it belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the AK/SK used for the API call belongs to an IAM account that only has permissions for a specific project.</div><br> |
|WithIpList |Boolean |No |true |Specifies whether to return a list of IP addresses or CIDR blocks in the allowlists. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. Default value. |
|QueryInstance |Boolean |No | |Query the allowlists associated with the instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AllowLists |Array of [AllowListObject](https://docs.byteplus.com/en/docs/40/15494#allowlistobject) |Refer to the Sample response. |The list of allowlist information. |


<span id="allowlistobject"></span>
### AllowListObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AllowListCategory |String |Default |Allowlist category. Values:<br><br><br>* `Ordinary`: ordinary allowlist.<br><br>* `Default`: default allowlist.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When this parameter is used as a request parameter, the default value is <code>Ordinary</code>.</div><br> |
|AllowListDesc |String |test |The description of the allowlist. |
|AllowListId |String |acl\-d1fd76693bd54e658912e7337d5b\*\*\*\* |Allowlists ID. |
|AllowListName |String |test |Allowlist name. |
|AllowListIPNum |Integer |2 |Total number of IP addresses or address ranges in the allowlist. |
|AllowListType |String |IPv4 |The type of IP addresses in the allowlist. Only IPv4 addresses are supported. |
|AssociatedInstanceNum |Integer |1 |The total number of instances associated with the allowlist. |
|IpList |Array of String |[ "172. ** *.* ** .0/18","192. ** *.* ** .6","10. ** *.* ** .1/32","10. ** *.* ** .2/32"<br><br>] |A list of IP addresses and CIDR blocks in the allowlist. Returned when the request parameter WithIpList is set to `true`, and when the value is `false` or no value is passed, it is returned as`null`. |
|ProjectName |String |default |The project to which the allowlist belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the allowlist is an existing one and has not been assigned to a specific project, this parameter is empty.</div><br> |
|SecurityGroupBindInfos |Array of [SecurityGroupBindInfo](https://docs.byteplus.com/en/docs/40/15494#securitygroupbindinfo) |None. |Information about the security group associated with the allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not returned if the allowlist is not associated with a security group.</div><br> |


<span id="securitygroupbindinfo"></span>
### SecurityGroupBindInfo


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BindMode |String |AssociateEcsIp |The mode for associating a security group. Values:<br><br><br>* `IngressDirectionIp`: Ingress direction IP.<br><br>* `AssociateEcsIp`: Associated ECS IP.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the CreateAllowList API, the BindMode and SecurityGroupId fields in SecurityGroupBindInfoObject are required.</div><br> |
|SecurityGroupId |String |sg\-b8pzuwk3i4g028j06k8f\*\*\*\* |Security group ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the CreateAllowList API, the BindMode and SecurityGroupId fields in SecurityGroupBindInfoObject are required.</div><br> |
|IpList |Array of String |["10. ** *.* ** .1/32","10. ** *.* ** .2/32"] |IP of the security group. |
|SecurityGroupName |String |Test security group |Security group name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned when SecurityGroupBindInfoObject is a response parameter in the DescribeAllowLists API.</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeAllowLists&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-h441603c****",
    "RegionId": "cn-beijing",
    "WithIpList": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031919043065E0B28E05E6A2AF458A",
        "Action": "DescribeAllowLists",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListCategory": "Default",
                "AllowListDesc": "",
                "AllowListIPNum": 4,
                "AllowListId": "acl-f90a90d96ee7401e912649bee4e2****",
                "AllowListName": "AllowlistName",
                "AllowListType": "IPv4",
                "AssociatedInstanceNum": 8,
                "IpList": [
                    "172.***.***.0/18",
                    "192.***.***.6",
                    "10.***.***.1/32",
                    "10.***.***.2/32"
                ],
                "ProjectName": "default",
                "SecurityGroupBindInfos": [
                    {
                        "BindMode": "IngressDirectionIp",
                        "IpList": [
                            "10.***.***.251/32",
                            "192.***.***.1/32",
                            "192.***.***.0/32",
                            "10..***.***.252/32"
                        ],
                        "SecurityGroupId": "sg-1mwy7b2bd0074j63v426****"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).

---
title: "DescribeSubnetAttributes - Querying the subnet details"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeSubnetAttributes"
---

Call the DescribeSubnetAttributes API to view details of the specified subnet.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSubnetAttributes&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|8X78Yv">必选</span> `Example: DescribeSubnetAttributes`

The interface name. The current API is `DescribeSubnetAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|4AogRh">必选</span>`Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**SubnetId ** <span data-label="purple"> String  </span><span data-api-tag="require|oDMknz">必选</span> `Example: subnet-23dscddcffvf3****`

ID of the subnet.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple"> String  </span>`Example: 210000****`

ID of the current account.



**RequestId ** <span data-label="purple"> String  </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



**SubnetId ** <span data-label="purple"> String  </span>`Example: subnet-25bcdxs7pv1****`

ID of the subnet.



**VpcId ** <span data-label="purple"> String  </span>`Example value: vpc-257gcdcdq64****`

ID of the VPC to which the subnet belongs.



**Status ** <span data-label="purple"> String  </span>`Example value: Available`

The current state of the subnet.


* Pending: Configuring.

* Available



**CidrBlock ** <span data-label="purple"> String  </span>`Example: 172.XX.XX.0/24`

IPv4 CIDR block of the subnet.



**Ipv6CidrBlock ** <span data-label="purple"> String  </span>`Example value: 2408:XXXX:0:a600::/64`

IPv6 CIDR block of subnet.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.</div>




**ZoneId ** <span data-label="purple"> String  </span>`Example value: cn-beijing-a`

The availability zone of the subnet.



**AvailableIpAddressCount ** <span data-label="purple"> Integer  </span>`Example: 1`

Count of available IP addresses within the subnet.



**Description ** <span data-label="purple"> String  </span>`Example: Description`

Description of the subnet.



**SubnetName ** <span data-label="purple"> String </span>`Example value: subnet-1`

The name of the subnet.



**CreationTime ** <span data-label="purple"> String </span>`Example value: 2018-01-18T12:43:57+08:00`

Creation time of the subnet



**RouteTable ** <span data-label="purple"> Object </span>`Example value: -`

Route table information.


**RouteTableId ** <span data-label="purple"> String  </span>`Example value: vrt-bp145q7glnuzdv****`

ID of the route table associated with the subnet.



**RouteTableType ** <span data-label="purple"> String </span>`Example value: System`

Type of the route table associated with the subnet.


* System: System route table.

* Custom: Custom route table.




**UpdateTime ** <span data-label="purple"> String  </span>`Example value: 2021-01-11T10:23:57+08:00`

The update time of the subnet.



**TotalIpv4Count ** <span data-label="purple"> Integer  </span>`Example: 253`

Total number of available IPs in the subnet.



**NetworkAclId ** <span data-label="purple"> String  </span>`Example: acl-bp1fg655nh68xyz9****`

ID of the network ACL associated with the subnet.



**ProjectName ** <span data-label="purple"> String </span>`Example value: default`

Name of the project to which the current subnet belongs.



**Tags ** <span data-label="purple"> Object[]  </span>`Example: -`

Tag information of the subnet.


**Key ** <span data-label="purple"> String </span>`Example value: k1`

The tag key of the tag.



**Value ** <span data-label="purple"> String  </span>`Example value: v1`

The tag value.




**IsDefault ** <span data-label="purple"> Boolean  </span>`Example: false`

Whether the subnet is a default subnet.


* true: Default subnet, indicating the subnet was automatically created by the system when an ECS instance was launched.

* false: Non\-default subnet, indicating the subnet was manually created by the user.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeSubnetAttributes&Version=2020-04-01&SubnetId=subnet-23dscddcffvf3**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSubnetAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "210000****",
        "AvailableIpAddressCount": 1,
        "CidrBlock": "172.XX.XX.0/24",
        "CreationTime": "2018-01-18T12:43:57+08:00",
        "Description": "Description",
        "Ipv6CidrBlock": "2408:XXXX:0:a600::/64",
        "IsDefault": false,
        "NetworkAclId": "acl-bp1fg655nh68xyz9****",
        "ProjectName": "default",
        "RequestId": "2021062415303301022514515207C4****",
        "RouteTable": {
            "RouteTableId": "vrt-bp145q7glnuzdv****",
            "RouteTableType": "System"
        },
        "Status": "Available",
        "SubnetId": "subnet-25bcdxs7pv1****",
        "SubnetName": "subnet-1",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "TotalIpv4Count": 253,
        "UpdateTime": "2021-01-11T10:23:57+08:00",
        "VpcId": "vpc-257gcdcdq64****",
        "ZoneId": "cn-beijing-a"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |

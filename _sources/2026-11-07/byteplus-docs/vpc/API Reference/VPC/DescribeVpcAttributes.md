---
title: "DescribeVpcAttributes"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes"
---

Call the DescribeVpcAttributes interface to view the details of the specified VPC.

<div data-tips="true" data-tips-type="default">tip</div>


<div data-tips="true" data-tips-type="default">IPv6 is currently in Beta. If you need a trial, please contact your account manager.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter  |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes   |DescribeVpcAttributes |actions to be executed. The value is DescribeVpcAttributes. |
|Version |String |Yes   |2020\-04\-01 |API version information, value is: 2020\-04\-01. |
|VpcId |String |Yes   |vpc\-bp1b1llp3ve5yze\*\*\*\* |The ID of the VPC to view.<br><br>You may call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) interface to query the ID of VPC. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |
|VpcId |String |vpc\-bp1b1llp3ve5yze\*\*\*\* |The ID of the Virtual Private Cloud (VPC). |
|Status |String |Available |Status of the VPC.<br><br><br>* Creating: being created<br><br>* Pending: The Internet Tunnel virtual interface is being configured.<br><br>* Available: The BGP peer is available. |
|VpcName |String |vpc\-1 |Name of the VPC. |
|CreationTime |String |2021\-07\-27T14:44:00+08:00 |Time to create VPC. |
|UpdateTime |String |2021\-08\-27T15:33:44+08:00 |Update time of the VPC. |
|CidrBlock |String |10.XX.XX.0/24 |VPC's IPv4 CIDR block. |
|Ipv6CidrBlock |String |2408:XXXX:0:a600::/56 |VPC IPv6 CIDR block. |
|Ipv6CidrBlocks |Array of Struct |\- |VPC IPv6 CIDR block information. |
|Description |String |This is my VPC. |The description information of the VPC. |
|SubnetIds |Array |["subnet\-bp1nhbnpv2blyz8dl\*\*\*\*","subnet\-kjrivdfkjgfw8sfvb\*\*\*\*"] |List of subnets within the VPC. |
|NatGatewayIds |Array |["ngw\-3tjx9odz8q3vj0x1\*\*\*\*","ngw\-3tjtu8hzu23vj0x1\*\*\*\*"] |ID of the NAT gateway created in the VPC. |
|AssociateCens |Array of Struct |\- |CEN information attached to the VPC. Specifically, please refer to the table “ **AssociateCens structure** ”. |
|RouteTableIds |Array |["vtb\-bp1krxxzp0c29fmon\*\*\*\*","vtb\-alferonxxcnzdfe3jd\*\*\*\*"] |ID of the route table created under the VPC. |
|SecurityGroupIds |Array |["securitygroup178ftwt45bg\*\*\*\*","securitygroup4838fsjfhsjf\*\*\*\*"] |VPC's security group list. |
|DnsServers |Array |["100.96.0.2","100.96.0.3"] |VPC's DNS server address. |
|AccountId |String |21000\*\*\*\* |ID of the VPC's Account. |
|SecondaryCidrBlocks |Array |["10.XX.XX.0/16", "10.XX.XX.1/16"] |Secondary CIDR block of the VPC. |
|UserCidrBlocks |Array |["72.XX.XX.0/24", "96.XX.XX.0/24"] |User CIDR block of the VPC.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The VPC's user CIDR block is currently in Beta. If you need to trial, please contact your account manager.</div><br> |
|NetworkAclNum |Integer |5 |The number of Network Access Control Lists in the VPC. |
|ProjectName |String |default |The name of the project to which the VPC belongs. |
|Tags |Array of Struct |\- |VPC tag information. Please refer to the table below "**Tag Structure**". |
|IsDefault |Boolean |false |Whether this VPC is the Default VPC.<br><br><br>* true: Default VPC, indicates that this VPC is automatically created by the system when creating an ECS instance.<br><br>* false: Non\-default VPC, indicates that this VPC is manually created by the user. |


**AssociateCens structure**


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|CenId |String |cen\-23887d\*\*\*\* |ID of the Cloud Enterprise Network. |
|CenOwnerId |String |12223\*\*\*\* |ID of the user who owns the Cloud Enterprise Network. |
|CenStatus |String |Attached |VPC status in CEN.<br><br>Attaching<br><br>Attached: loaded |


**Tag structure**


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|Key |String |k1 |The key of the VPC tag. |
|Value |String |v1 |The value of the VPC tag. |


**IPv6CidrBlock structure**


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|Ipv6CidrBlock |String |2408:XXXX:0:a600::/56 |The IPv6 CIDR block of VPC. |
|Ipv6Isp |String |ChinaMobile |The line type.<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* ChinaMobile: China Mobile static single line.<br><br>* ChinaTelecom: China Telecom static single\-line.<br><br>* ChinaUnicom: Static single ISP for China Unicom<br><br>* ChinaMobile_Value: China Mobile Offer static single\-line.<br><br>* China Unicom Offer static single line.<br><br>* China Telecom Offer static single line.<br><br><br><div data-tips="true" data-tips-type="tip">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Except for BGP (Multi\-ISP), all other ISPs only support China (Shanghai) Region.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=DescribeVpcAttributes&Version=2020-04-01&VpcId=vpc-bp1b1llp3ve5yze**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeVpcAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210830115555****2524310006EC08C8",
        "VpcId": "vpc-bp15zkdt37pq72zv****",
        "VpcName": "test",
        "Description": "",
        "CreationTime": "2021-07-27T14:44:00+08:00",
        "UpdateTime": "2021-08-27T15:33:44+08:00",
        "CidrBlock": "10.XX.XX.0/24",
        "Ipv6CidrBlock": "2408:XXXX:0:a600::/56",
        "Status": "Available",
        "IsDefault": false,
        "SubnetIds": [
            "subnet-2fenv7f****hs5oxruuvxz107",
            "subnet-2fenv7l****f45oxruv8j3agc"
        ],
        "NatGatewayIds": [
            "ngw-3tjtu8hzu23vj0x1****"
        ],
        "AssociateCens":  [
             {
                "CenId": "cen-23af29****",
                "CenOwnerId": "12230****",
                "CenStatus": "Attached"
             }
        ],
        "RouteTableIds": [
            "vtb-2fenv5ztv****5oxruv1kuqfq",
            "vtb-2feoladfk****5oxruvb6l5t1"
        ],
        "SecurityGroupIds": [
            "sg-2fenv63****345oxruwfsklo8"
        ],
        "DnsServers":  [
            "172.XX.XX.1",
            "172.XX.XX.2"
.       ],
        "AccountId": "210000****",
        "NetworkAclNum": "5",
        "SecondaryCidrBlocks": [
             "172.XX.XX.0/12",
             "192.XX.XX.0/16"
        ],
        "UserCidrBlocks": [],
        "ProjectName": "default",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            },
            {
                "Key": "k2",
                "Value": "v2"
            }
        ],
        "Ipv6CidrBlock": [
             {
                 "Ipv6CidrBlock":"2408:XXXX:0:a600::/56",
                 "Ipv6Isp":"BGP"
             }
         ]    
    }    
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

The current API has no error codes. For more error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/vpc/Public-error-codes).

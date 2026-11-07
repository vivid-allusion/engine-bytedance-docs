---
title: "AssociateVpcCidrBlock - Adding a secondary CIDR block"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock"
---

Call the AssociateVpcCidrBlock API to add a secondary CIDR block to the specified VPC.

> **tip**

> IPv6 is currently in the invite\-only Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

## Instructions

* A VPC can have a maximum of 1 secondary IPv4 CIDR block.

* The secondary IPv4 CIDR block must belong to the same larger IP block as the VPC's primary CIDR block.

   For example, if the primary CIDR of the target VPC belongs to the 192.168.0.0/16~24 block, any secondary CIDR must also fall within this same block range. It cannot use segments from 10.0.0.0/8~24 or 172.16.0.0/12~24.

* If the primary CIDR block of a VPC is already the largest possible block (e.g., 192.168.0.0/16), no secondary CIDR blocks can be added.

* The secondary CIDR block must not overlap with any other existing CIDR blocks in the target VPC.

* Once added, a secondary CIDR block cannot be modified.

* AssociateVpcCidrBlock is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) API to check the VPC status; `Pending` means configuring, and `Available` means configuration is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateVpcCidrBlock&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: AssociateVpcCidrBlock`

The interface name. The current API name is `AssociateVpcCidrBlock`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**VpcId ** String必选 `Example: vpc-257gqcdfvx6n****`

The VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**SecondaryCidrBlock ** String`optional` `Example: 172.16.XX.0/24`

The secondary IPv4 CIDR block of the VPC to be added. You can use a non\-overlapping subset from the following ranges as the VPC's secondary CIDR block:

* 192.168.0.0/16~28

* 10.0.0.0/8~28

* 172.16.0.0/12~28

> **tip**

> The secondary CIDR block must be within the same supernet as the primary CIDR block.

**Ipv6Isp ** String`optional` `Example: ChinaMobile`

ISP. Valid values:

* BGP: BGP (Multi\-ISP).

* ChinaMobile: Static single\-ISP provided by China Mobile.

* ChinaTelecom: Static single\-ISP provided by China Telecom.

* ChinaUnicom: Static single\-ISP provided by China Unicom.

* ChinaMobile_Value: The static preferential single ISP provided by China Mobile.

* ChinaUnicom_Value: The static preferential single ISP provided by China Unicom.

* ChinaTelecom_Value: The static preferential single ISP provided by China Telecom.

**Ipv6MaskLen ** Integer`optional` `Example: 62`

Mask length.

* When Ipv6Isp is set to BGP, only a prefix length of /56 is supported. Otherwise, this parameter supports /62 to /64.

* After the parameter `Ipv6CidrBlock` is provided, this parameter does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

**Ipv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/56`

The secondary IPv6 CIDR block of the VPC to be added.

* When this parameter is provided, the parameter `Ipv6MaskLen` does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

**Ipv4IpamPoolId ** String`optional` `Example: ipam-bp15zkdt37pq72zv****`

The ID of the IPAM pool.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**VpcId ** String`Example: vpc-257gqcdfvx6n****`

The VPC ID.

**SecondaryCidrBlocks ** String[]`Example: 172.16.1.0/24`

Secondary IPv4 CIDR block of the VPC.

**Ipv6CidrBlocks ** Object[]`Example: -`

The IPv6 CIDR block information of the VPC.

**Ipv6CidrBlock ** String`Example: 2408:XXXX:0:a600::/56`

IPv6 CIDR block of the VPC.

**Ipv6Isp ** String`Example: ChinaMobile`

ISP.

* BGP: BGP (Multi\-ISP).

* ChinaMobile: Static single\-ISP provided by China Mobile.

* ChinaTelecom: Static single\-ISP provided by China Telecom.

* ChinaUnicom: Static single\-ISP provided by China Unicom.

* ChinaMobile_Value: The static preferential single ISP provided by China Mobile.

* ChinaUnicom_Value: The static preferential single ISP provided by China Unicom.

* ChinaTelecom_Value: The static preferential single ISP provided by China Telecom.

> **tip**

> Except for BGP (Multi\-ISP), all other line types are only supported in the China (Shanghai) region.

## Request example

```json
GET /?Action=AssociateVpcCidrBlock&Version=2020-04-01&VpcId=vpc-257gqcdfvx6n****&SecondaryCidrBlock=172.16.XX.0/24  HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AssociateVpcCidrBlock",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv6CidrBlocks": [
            {
                "Ipv6Isp": "ChinaMobile",
                "Ipv6CidrBlock": "2408:XXXX:0:a600::/56"
            }
        ],
        "RequestId": "2021062415303301022514515207C4****",
        "SecondaryCidrBlocks": [
            ""
        ],
        "VpcId": "vpc-257gqcdfvx6n****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InsufficientIpv6Blocks |The specified pool does not contain enough free IPv6 blocks to fulfill your request. |The IPv6 pool has insufficient IPv6 address range resources. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The specified CIDR block format is invalid. |
|400 |InvalidIpamPoolCidrAllocation.Malformed |The specified CIDR in the IPAM pool is unavailable. |The specified IPAM pool cannot allocate CIDR blocks. |
|400 |InvalidIpv6CidrBlock.NotReserved |The specified IPv6 CIDR block is not reserved. |The specified IPv6 address range is not reserved. |
|400 |InvalidParameter.EnableIpv6 |The EnableIpv6 parameter is currently not supported. |The EnableIpv6 request parameter is not currently supported. |
|400 |InvalidParameter.MaskLength |The IPv6 mask length in this request is invalid. |The IPv6 mask length in this request is invalid. |
|400 |InvalidParameter.SecondaryCidrAndIpv6Cidr |The param of request are mutually exclusive. |The request contains mutually exclusive parameters. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.VpcIpv6Cidr |You've reached the limit on the number of IPv6 CIDR blocks per VPC that you can create. |The maximum number of IPv6 CIDR blocks allowed for the specified VPC has been reached. |
|400 |QuotaExceeded.VpcSecondaryCidr |You've reached the limit on the number of secondary cidr blocks per VPC. |The maximum number of secondary CIDR blocks allowed for the VPC has been reached. |
|403 |Forbidden.IpamPoolAllocationResourceDiscovery |The IPAM pool owner cannot discover resources from the specified account. |The IPAM pool owner cannot discover resources of the specified account. |
|403 |Forbidden.Ipv6IspType |You are not authorized to create this type IPv6 CIDR. |You do not have permission to create an IPv6 CIDR block for the specified ISP type. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|409 |InvalidSecondaryCidrBlock.Conflict |The specified secondary CIDR block conflicts with that of another block in your VPC. |The specified Secondary CIDR block conflicts with another CIDR block in the associated VPC. |

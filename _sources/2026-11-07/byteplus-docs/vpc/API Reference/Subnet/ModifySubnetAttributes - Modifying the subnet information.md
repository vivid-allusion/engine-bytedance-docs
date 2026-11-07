---
title: "ModifySubnetAttributes - Modifying the subnet information"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes"
---

Call the ModifySubnetAttributes API to modify the specified subnet information.

## Instructions

* If the following optional parameters are not configured, the existing configurations will be preserved.

* ModifySubnetAttributes is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeSubnetAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSubnetAttributes) to check the subnet status. `Pending` means configuring, and `Available` means configuration is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySubnetAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifySubnetAttributes`

The interface name. The current API name is `ModifySubnetAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**SubnetId ** String必选 `Example: subnet-bp1qtch57ywecf****`

The ID of the subnet for which to modify information.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**SubnetName ** String`optional` `Example: test`

Name of the subnet.

* Length limit: 1 to 128 characters.

* The name must start with a letter, Chinese character, or number. It may contain periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: This is my subnet.`

Description of the subnet.

* Length limit: 0 to 255 characters.

* It must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**EnableIpv6 ** Boolean`optional` `Example: false`

Enable or disable IPv6. This parameter can be configured only when the VPC to which the subnet belongs has IPv6 enabled.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Enable.

* false: Disable. This value can be configured only when no cloud resources within the subnet have been assigned IPv6 addresses.

> **tip**

> IPv6 is currently in the invite\-only Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

**Ipv6CidrBlock ** Integer`optional` `Example: 99`

The last 8 bits of an IPv6 subnet CIDR (the subnet has a fixed mask of /64).

* Value range: 0 to 255. The mask is fixed at /64.

* This parameter can only be configured when EnableIpv6 is set to true.

> **tip**

> After the parameter VpcIpv6CidrBlock is provided, this parameter does not take effect.

**VpcIpv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/64`

IPv6 CIDR block of subnet. The mask is fixed at /64.

> **tip**

> When this parameter is provided, the parameter Ipv6CidrBlock does not take effect.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=ModifySubnetAttributes&Version=2020-04-01&SubnetId=subnet-bp15qtc7ywecf****&Description=This is my subnet&SubnetName=subnet-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifySubnetAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and try again. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.EnableIpv6 |Operation failed because IPv6 for the subnet is enabled already. |The subnet already has IPv6 enabled. |
|400 |InvalidParameter.EnableIpv6 |Operation failed because IPv6 for the vpc of this subnet is not enabled. |The VPC to which the subnet belongs does not have IPv6 enabled. |
|400 |InvalidParameter.EnableIpv6 |Operation failed because IPv6 is not enabled for the subnet. |The subnet does not have IPv6 enabled. |
|400 |InvalidParameter.Ipv6CidrBlock |Specified subnet IPv6CidrBlock is invalid. |The subnet IPv6 CIDR is invalid. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the IPv6 does not match with the zone if subnet. |The availability zone of the subnet does not match the specified egress for public IPv6. |
|400 |InvalidSubnet.EnableIPv6 |Operation failed because disabling IPv6 is not allowed for the IPv6 only subnet. |The IPv6 function cannot be disabled for an IPv6\-only subnet. |
|400 |InvalidSubnet.InUse |The specified subnet has dependent resource of an elastic network interface. |The specified subnet contains ENIs and cannot be deleted. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidSubnetCidr.Malformed |The specified subnet cidr is malformed. If you are specifying a subnet cidr, ensure the CIDR of the subnet must fall into the range of the CIDR of the VPC to which the subnet belongs to. |The specified subnet CIDR block is invalid. Ensure the subnet CIDR block falls within the CIDR range of its VPC. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot process this request. |
|400 |InvalidVpcIPv6Cidr.Malformed |The specified vpc IPv6 cidr is malformed. If you are specifying a vpc IPv6 cidr, ensure the CIDR must fall into the range of the CIDR of the VPC to which the subnet belongs to. |The specified VPC IPv6 CIDR block is invalid. Ensure the subnet CIDR block falls within the CIDR range of its VPC. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the same route table. |
|409 |InvalidSubnetCidr.Conflict |The specified CIDR block conflicts with that of another subnet in your VPC. |The specified CIDR block conflicts with another subnet CIDR block in the associated VPC. |
|409 |InvalidSubnetCidr.IPv6Conflict |The specified IPv6 CIDR block conflicts with that of another subnet in your VPC. |The specified IPv6 CIDR block conflicts with another subnet IPv6 CIDR block in the associated VPC. |

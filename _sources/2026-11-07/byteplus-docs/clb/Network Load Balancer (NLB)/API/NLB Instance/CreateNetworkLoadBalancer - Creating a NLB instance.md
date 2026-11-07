---
title: "CreateNetworkLoadBalancer - Creating a NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateNetworkLoadBalancer"
---

Call the CreateNetworkLoadBalancer API to create a Network Load Balancer (NLB) instance.

## Instructions

The status changes for NLB instances created through the console are as follows: Creating \> Active. The status changes for NLB instances created through the API are as follows: Provisioning \> Creating \> Active.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNetworkLoadBalancer&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

In the table below, the "N" in ZoneMappings.N.a type parameter represents the serial number of the Availability Zone and its corresponding subnet, IP address, or Elastic IP (EIP). The value range is 1 to n, where n depends on the number of Availability Zones in the Region. For details, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/clb/NLB-Regions-and-availability-zones). Separate resources with ampersands (&).

**Action ** String必选 `Example: CreateNetworkLoadBalancer`

Action to execute. Set the value to CreateNetworkLoadBalancer.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**RegionId ** String必选 `Example: cn-beijing`

Request region.

**NetworkType ** String`optional` `Example: intranet`

The IPv4 network type of the NLB instance. Valid values:

* internet: Public network.

* intranet: Private network.

**LoadBalancerName ** String`optional` `Example: nlb-test`

Name of the NLB instance.

* Must start with a letter, number, or Chinese character, and may include the following special characters: dot (.), underscore (_), and hyphen (\-).

* Length limit: 1 to 128 characters.

* If this parameter is not passed in, the default is the instance ID.

**Description ** String`optional` `Example: This is an NLB.`

Description of the NLB instance.

* Must start with a letter, number, or Chinese character and may contain the following special characters: half\-width commas ( , ), half\-width periods ( . ), underscores ( _ ), spaces ( ), equal signs ( = ), hyphens ( \- ), full\-width comma ( ， ), and full\-width period ( 。 ).

* Length limit: 0 to 255 characters.

* If the parameter is not passed in, it defaults to an empty string.

**IpAddressVersion ** String`optional` `Example: ipv4`

The IP address type of the NLB instance. Valid values:

* ipv4 (default): Indicates that the NLB instance is of IPv4 type and only supports forwarding IPv4 requests.

* dualstack: Indicates that the NLB instance is of dual\-stack type and supports forwarding both IPv4 and IPv6 requests.

> **tip**

> NLB IPv6 feature is currently in the invite\-only Beta stage. For trial requests, please contact the account manager.

**Ipv4BandwidthPackageId ** String`optional` `Example: bwp-wedfvcrt56hnm****`

ID of the IPv4 Bandwidth Package.

> **tip**

> When the `NetworkType` parameter is set to intranet, this parameter cannot be passed.

**VpcId ** String必选 `Example: vpc-bp1aevy8sofi8mh1****`

The ID of the VPC to which the NLB instance belongs. You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC ID.

**CrossZoneEnabled ** Boolean`optional` `Example: true`

Enable cross\-az forwarding for the NLB instance.

Please input the enumerated values strictly in the case form as follows, and do not pass in other values.

* true (default): Enable.

* false: Disable.

**ZoneMappings.N.ZoneId ** String必选 `Example: cn-beijing-a`

The ID within the Availability Zone supported by the NLB instance. You can call the [DescribeNLBZones](https://docs.byteplus.com/en/docs/clb/DescribeNLBZones) API to get the availability zone IDs.

Specify at least 2 availability zones.

**ZoneMappings.N.SubnetId ** String必选 `Example: subnet-bp12mw1f8k3jgy****`

Subnet ID within the Availability Zone supported by the NLB instance. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to obtain subnet IDs.

Specify one subnet per availability zone.

**ZoneMappings.N.Ipv4Address ** String`optional` `Example: 192.XX.XX.6`

The private IPv4 VIP address of the NLB instance.

If this parameter is not passed in, the system will automatically assign an available IPv4 address from the subnet.

**ZoneMappings.N.EipId ** String`optional` `Example: eip-3ciyamhu46c6rrswwusg****`

The ID of the EIP attached to the Internet NLB instance.

* When `NetworkType` is set to "internet":

   * Specify an existing EIP.

   * Not passing in indicates purchasing a new EIP.

* When `NetworkType` is set to "intranet", passing this parameter is not allowed.

**SecurityGroupIds.N ** String必选 `Example: sg-bp67acfmxazb4p****`

Security group ID associated with the NLB instance.

* N: Indicates the serial number of the security group, the value range is 1 to 4.

* Separate security group IDs with ampersands (&).

**ModificationProtectionStatus ** String`optional` `Example: ConsoleProtection`

Whether the NLB instance has modification protection enabled on the console. Valid values:

* NonProtection (default): Disable, allowing modification or deletion of the instance through the console.

* ConsoleProtection: Enable, prohibiting modifications or deletions of the instance via the console.

**ProjectName ** String`optional` `Example: default`

Name of the project to which the NLB instance belongs.

If this parameter is not provided, it defaults to "default".

**Tags.N.Key ** String`optional` `Example: k1`

The tag key of the custom tag.

N specifies the serial number of the tag information. It must be filled in numerical order starting from 1, with a value range of 1 to 20. Separate multiple tag keys with ampersands ( & ).

* Must be 1 to 128 characters in length.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Cannot start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> **tip**

> Tag keys of the same resource must be unique.

**Tags.N.Value ** String`optional` `Example: v1`

The tag value of the custom tag.

N specifies the serial number of the tag information. It must be filled in numerical order starting from 1, with a value range of 1 to 20. Separate multiple tag values with ampersands (&). Each tag key corresponds to one tag value.

* Length limit: 0 to 255 characters.

* It is case\-sensitive. It cannot start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* This parameter value is auto\-generated by the client to ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* The value can only contain ASCII characters and cannot exceed 64 characters in length.

* If this parameter is not specified, idempotence validation will not be performed.

**DNSAffinity ** Boolean`optional` `Example: true`

Whether to enable DNS Availability Zone (AZ) affinity.

* true: Private network clients preferentially resolve to the IPs of NLB nodes in the same AZ, so traffic does not cross AZs. If a node in the same AZ fails, the IPs of all non\-faulty AZs are automatically returned.

* false (default): DNS returns the IPs of nodes in all AZs of the instance, and clients select randomly or by round\-robin, which may result in cross\-AZ access.

> **tip**

> This applies only to private network resolution; public DNS is not affected.

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

**LoadBalancerId ** String`Example: nlb-bp1o94dp5i6ea****`

The ID of the NLB instance.

## Request example

```json
GET /?Action=CreateNetworkLoadBalancer&Version=2020-04-01&RegionId=cn-beijing&VpcId=vpc-bp1aevy8sofi8mh1****&ZoneMappings.1.ZoneId=cn-beijing-a&ZoneMappings.1.SubnetId=subnet-bp12mw1f8k3jgy****&SecurityGroupIds.1=sg-bp67acfmxazb4p**** HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateNetworkLoadBalancer",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LoadBalancerId": "nlb-bp1o94dp5i6ea****",
        "RequestId": "2024092952539010225146063030****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |InvalidBandwidthPackage.InvalidBusinessStatus |The specified bandwidth package is not in the correct business status for the request. |The specified Shared Bandwidth Package's billing state is incompatible with this request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|400 |InvalidCrossZoneEnabled.Malformed |The specified CrossZoneEnabled is malformed. |The specified CrossZoneEnabled parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEip.InvalidBusinessStatus |The specified Eip is not in the correct business status for the request. |The specified EIP is in a billing state that cannot respond to this request. |
|400 |InvalidEip.InvalidStatus |The specified Eip is not in the correct status for the request. |The specified EIP is in a state that cannot respond to this request. |
|400 |InvalidEipBillingType.NotSupport |The specified billing type of Eip dose not support this action. |The specified EIP billing methods do not support the current action. |
|400 |InvalidEipISP.NotSupport |The specified isp of Eip dose not support this action. |The specified EIP ISP does not support the current action. |
|400 |InvalidEipSecurityProtectionTypes.NotSupport |The specified security types protection of Eip dose not support this action. |The specified EIP security protection type does not support the current action. |
|400 |InvalidEipSpecificEgress.NotSupport |The specified specific egress of Eip dose not support this action. |The specified EIP Internet egress does not support the current action. |
|400 |InvalidISP.Mismatch |The isp of the bandwidth package does not match with the Eip. |The ISP of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidIpAddressVersion.Malformed |The specified IpAddressVersion is malformed. |The specified IpAddressVersion format is invalid. |
|400 |InvalidIpv4BandwidthPackageId.Malformed |The specified Ipv4BandwidthPackageId is malformed. |The format of the specified Ipv4BandwidthPackageId is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName parameter format is invalid. |
|400 |InvalidModificationProtectionStatus.Malformed |The specified ModificationProtectionStatus is malformed. |The specified ModificationProtectionStatus format is invalid. |
|400 |InvalidNetworkType.Malformed |The specified NetworkType is malformed. |The specified NetworkType format is invalid. |
|400 |InvalidNetworkType.UnSupportAction |The specified NetworkType does not support this action in this region. |The specified network type does not support the current actions in this region. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the Eip. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidRegionId.Malformed |The specified RegionId is malformed. |The specified RegionId format is invalid. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified SecurityGroup is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidSecurityProtectionTypes.Mismatch |The specified security protection types of the bandwidth package does not match with the Eip. |The protection type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the Eip. |The specified egress of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSubnetIPv4Cidr.NotSupport |The specified subnet does not support ipv4 cidr. |The specified subnet does not support IPv4 CIDR blocks. |
|400 |InvalidSubnetIPv6Cidr.NotSupport |The specified subnet does not support ipv6 cidr. |The specified subnet does not support IPv6 CIDR block. |
|400 |InvalidSubnetIPv6CidrISP.Mismatch |The ipv6 cidr isp of the subnets is not same. |The ISP of multiple subnet IPv6 CIDR blocks are inconsistent. |
|400 |InvalidSubnetIPv6CidrSpecificEgress.Mismatch |The ipv6 cidr specific egress of the subnets is not same. |The EIP egress of multiple subnet IPv6 CIDR blocks are inconsistent. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is malformed. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidZoneMapping.SubnetAndZoneMismatch |The specified subnet and zone is mismatched. |The specified subnet does not match the availability zone. |
|400 |InvalidZoneMappingCount |The specified number of zone mappings is less than the minimum number of zones. |The specified number of available zones is less than the minimum number of availability zones. |
|400 |InvalidZoneMappings.EipId.Malformed |The specified ZoneMappings.EipId is malformed. |The specified ZoneMappings.EipId format is invalid. |
|400 |InvalidZoneMappings.EipIsp.Malformed |The specified ZoneMappings.EipIsp is malformed. |The specified ZoneMappings.EipIsp parameter format is invalid. |
|400 |InvalidZoneMappings.EipSpecificEgress.Malformed |The specified ZoneMappings.EipSpecificEgress is malformed. |The specified ZoneMappings.EipSpecificEgress format is invalid. |
|400 |InvalidZoneMappings.Ipv4Address.Malformed |The specified ZoneMappings.Ipv4Address is malformed. |The specified ZoneMappings.Ipv4Address format is invalid. |
|400 |InvalidZoneMappings.SubnetId.Malformed |The specified ZoneMappings.SubnetId is malformed. |The specified ZoneMappings.SubnetId format is invalid. |
|400 |InvalidZoneMappings.UnSupportAction |The specified ZoneMappings does not support this action, due to local zone only support single zone. |The specified availability zone mapping is invalid. LocalZone supports only a single availability zone. |
|400 |InvalidZoneMappings.ZoneId.Malformed |The specified ZoneMappings.ZoneId is malformed. |The specified ZoneMappings.ZoneId format is invalid. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'VpcId'. |This request does not contain the required parameter. Confirm that this request contains all required parameters (such as VpcId). |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |QuotaExceed.Eni |You've reached the limit on the number of ENI that you can create. |You have reached the quota limit for the number of ENIs that can be created. |
|400 |QuotaExceed.InstanceNumber |You've reached the limit on the number of instances that you can create. |Quota limit for the number of Load Balancer instances has been reached. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of EIPs that you can add to a Bandwidth Package. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of network interfaces (ENI) that can be associated with the security group has been reached. |
|400 |QuotaExceeded.SecurityGroup |You've reached the limit on the number of security groups that you can create. |You have reached the maximum of security groups that can be created. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The request on the specified instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.BalanceNotEnough |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The request to operate on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform this operation on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the specified Region. |No permission to manage in the specified region. |
|403 |Forbidden |You are not authorized to perform operations on the specified Zone. |No permission to perform actions on the specified availability zone. |
|403 |InvalidSecurityGroup.ServiceManaged |The specified SecurityGroup is managed by a service. |The specified security group is managed to a service. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified Eip does not exist. |The specified EIP does not exist. |
|404 |InvalidSecurityGroup.NotFound |The specified SecurityGroup does not exist. |The specified security group does not exist. |
|404 |InvalidSharedVPC.UnSupportAction |The specified shared VPC does not support this action. |The specified shared VPC does not support the current action. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidZone.NotFound |The specified Zone mapping does not exist. |The specified availability zone does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The CLB service\-attached role does not exist. |
|409 |InvalidEip.Conflict |The specified Eip conflicts with that of another Eip in your bandwidth package. |The specified EIP is already associated with a bandwidth package. |
|409 |InvalidEipServiceManage.Conflict |The specified Eip already another service manage. |The specified EIP is already service\-managed. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|409 |InvalidSecurityGroup.Conflict |The specified SecurityGroup already exists. |The specified security group already exists. |
|409 |InvalidZone.Conflict |The specified zone already exists. |The specified availability zone already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |

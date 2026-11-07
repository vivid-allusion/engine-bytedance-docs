---
title: "ModifyNetworkLoadBalancerZones - Adding or deleting a availability zone for an NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerZones"
---

Call the ModifyNetworkLoadBalancerZones API to add or delete an availability zone for a Network Load Balancer (NLB) instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkLoadBalancerZones&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

In the table below:

* In parameters of the format ZoneMappings.N.a, the "N" represents the sequence number of the availability zone and its corresponding subnet, IP address, or elastic IP address (EIP). The value range is 1 to n, where n depends on the number of availability zones in the region. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/clb/NLB-Regions-and-availability-zones). Separate resources with ampersands (&).

* If an optional parameter is not provided, it indicates that the value of this parameter will retain its original configuration.

**Action ** String必选`Example: ModifyNetworkLoadBalancerZones`

Action to execute. Set the value to ModifyNetworkLoadBalancerZones.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**LoadBalancerId ** String必选 `Example: nlb-bp1b6c719dfa08ex****`

The ID of the NLB instance.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.

**AddZoneMappings.N.ZoneId ** String`optional` `Example: cn-beijing-a`

The ID of the availability zone to be added.

**AddZoneMappings.N.SubnetId ** String`optional` `Example: subnet-bp12mw1f8k3jgy****`

The ID of the subnet to which the NLB instance belongs in the corresponding availability zone.

You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to obtain the subnet ID.

> **tip**

> When `AddZoneMappings.N.ZoneId` is provided, this parameter is required.

**AddZoneMappings.N.Ipv4Address ** String`optional` `Example: 192.XX.XX.2`

The NLB instance's IPv4 private VIP address in the corresponding availability zone.

**AddZoneMappings.N.EipId ** String`optional` `Example: eip-2ziwb7ujxscd****`

The ID of the EIP attached to the Internet NLB instance in the corresponding availability zone.

**DeleteZoneMappings.N ** String`optional` `Example: cn-beijing-a`

The ID of the availability zone to be deleted.

## Response parameters

**RequestId ** String`Example: 202409291106382514606306AF947C****`

Request ID.

## Request examples

```json
GET /?Action=ModifyNetworkLoadBalancerZones&Version=2020-04-01&LoadBalancerId=nlb-bp1b6c719dfa08ex**** HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNetworkLoadBalancerZones",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202409291106382514606306AF947C****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InvalidBandwidthPackage.InvalidBusinessStatus |The specified bandwidth package is not in the correct business status for the request. |The specified Bandwidth Package cannot respond to this request due to its status. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidEip.InvalidBusinessStatus |The specified Eip is not in the correct business status for the request. |The specified elastic IP address (EIP) cannot respond to this request due to its billing status. |
|400 |InvalidEip.InvalidStatus |The specified Eip is not in the correct status for the request. |The specified EIP cannot respond to this request due to its status. |
|400 |InvalidEipBillingType.NotSupport |The specified billing type of Eip dose not support this action. |The specified EIP billing method do not support the current action. |
|400 |InvalidEipISP.NotSupport |The specified isp of Eip dose not support this action. |The specified EIP ISP does not support the current action. |
|400 |InvalidEipSecurityProtectionTypes.NotSupport |The specified security types protection of Eip dose not support this action. |The specified EIP security protection type does not support the current action. |
|400 |InvalidEipSpecificEgress.NotSupport |The specified specific egress of Eip dose not support this action. |The specified EIP egress does not support the current action. |
|400 |InvalidISP.Mismatch |The isp of the bandwidth package does not match with the Eip. |The ISP of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidListener.InvalidStatus |The specified Listener is not in the correct status for the request. |The specified listener cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified load balancer cannot respond to this request due to its billing status. |
|400 |InvalidOperation.Malformed |The specified Operation is malformed. |The specified Operation format is invalid. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the Eip. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSecurityProtectionTypes.Mismatch |The specified security protection types of the bandwidth package does not match with the Eip. |The protection type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the Eip. |The specified egress of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSubnetIPv4Cidr.NotSupport |The specified subnet does not support ipv4 cidr. |The specified subnet does not support IPv4 CIDR blocks. |
|400 |InvalidSubnetIPv6Cidr.NotSupport |The specified subnet does not support ipv6 cidr. |The specified subnet does not support IPv6 CIDR blocks. |
|400 |InvalidSubnetIPv6CidrISP.Mismatch |The ipv6 cidr isp of the subnets is not same. |The ISP of multiple subnet IPv6 CIDR blocks are inconsistent. |
|400 |InvalidZoneMapping.SubnetAndZoneMismatch |The specified subnet and zone is mismatched. |The specified subnet does not match the availability zone. |
|400 |InvalidZoneMappings.EipId.Malformed |The specified ZoneMappings.EipId is malformed. |The specified ZoneMappings.EipId format is invalid. |
|400 |InvalidZoneMappings.Ipv4Address.Malformed |The specified ZoneMappings.Ipv4Address is malformed. |The specified ZoneMappings.Ipv4Address format is invalid. |
|400 |InvalidZoneMappings.SubnetId.Malformed |The specified ZoneMappings.SubnetId is malformed. |The specified ZoneMappings.SubnetId format is invalid. |
|400 |InvalidZoneMappings.ZoneId.Malformed |The specified ZoneMappings.ZoneId is malformed. |The specified ZoneMappings.ZoneId format is invalid. |
|400 |QuotaExceed.Eni |You've reached the limit on the number of ENI that you can create. |You have reached the quota limit for the number of elastic network interfaces (ENIs) that can be created. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of elastic IP addresses (EIPs) that you can add to a Bandwidth Package. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to lack of Eip allocated. |The action request for this instance was rejected because allocated EIPs are insufficient. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to Eip service manage. |The action request for this instance was rejected due to EIP service hosting failure. |
|400 |UnsupportedOperation |The specified instance is denied due to the number of zones are less than the minimum number of zones. |The action request for this instance was rejected because the number of availability zones under the instance is less than the minimum required. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the specified Zone. |No permission to perform actions on the specified availability zone. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified Eip does not exist. |The specified EIP does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidSharedVPC.UnSupportAction |The specified shared VPC does not support this action. |The specified shared VPC does not support the current action. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidZone.NotFound |The specified Zone mapping does not exist. |The specified availability zone does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidEip.Conflict |The specified Eip conflicts with that of another Eip in your bandwidth package. |The specified EIP is already added to a Bandwidth Package. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|409 |InvalidZone.Conflict |The specified zone already exists. |The specified availability zone already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |

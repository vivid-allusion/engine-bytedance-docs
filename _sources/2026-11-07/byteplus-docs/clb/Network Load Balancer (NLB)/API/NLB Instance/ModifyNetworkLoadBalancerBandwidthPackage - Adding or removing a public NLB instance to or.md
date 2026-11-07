---
title: "ModifyNetworkLoadBalancerBandwidthPackage - Adding or removing a public NLB instance to or from a Bandwidth Package"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerBandwidthPackage"
---

Call the ModifyNetworkLoadBalancerBandwidthPackage API to add or remove an Internet Network Load Balancer (NLB) instance to/from a Bandwidth Package.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkLoadBalancerBandwidthPackage&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ObHB6f">必选</span> `Example: ModifyNetworkLoadBalancerBandwidthPackage`

Action to execute. Set the value to ModifyNetworkLoadBalancerBandwidthPackage.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|yAa3Xh">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|NZDZsg">必选</span> `Example: nlb-bp1b6c719dfa08ex****`

The ID of the NLB instance.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.



**Operation ** <span data-label="purple">String </span><span data-api-tag="require|TjHh1u">必选</span> `Example: add`

Add or remove the NLB instance to/from a Bandwidth Package.


* add: Add to a Bandwidth Package.

* remove: Remove from the Bandwidth Package.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>Protocol</code> is "ipv4", it means that the elastic IP address (EIP) attached to the NLB instance is added to or removed from a Bandwidth Package.</div>


* <div data-tips="true" data-tips-type="tip">When <code>Protocol</code> is "ipv6", it means that the IPv6 Internet bandwidth attached to the NLB instance is added to or removed from a Bandwidth Package.</div>




**Protocol ** <span data-label="purple">String </span><span data-api-tag="require|PXNB5v">必选</span> `Example: ipv4`

The protocol type of the NLB network address.


* ipv4

* ipv6



**BandwidthPackageId ** <span data-label="purple">String </span><span data-api-tag="require|jZeoFW">必选</span> `Example: bwp-2zeo05qre24nhrqpy****`

ID of the Bandwidth Package.


* You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to get the ID of the Bandwidth Package that the NLB instance can be added to.

* You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the ID of the Bandwidth Package that the NLB instance is already added to.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409291106382514606306AF947C****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNetworkLoadBalancerBandwidthPackage&Version=2020-04-01&LoadBalancerId=nlb-bp1b6c719dfa08ex****&Operation=add&Protocol=ipv4&BandwidthPackageId=bwp-2zeo05qre24nhrqpy**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNetworkLoadBalancerBandwidthPackage",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202409291106382514606306AF947C****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidBandwidthPackage.InvalidBusinessStatus |The specified bandwidth package is not in the correct business status for the request. |The specified Bandwidth Package cannot respond to this request due to its status. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidEip.InvalidBusinessStatus |The specified Eip is not in the correct business status for the request. |The specified elastic IP address (EIP) cannot respond to this request due to its billing status. |
|400 |InvalidEip.Malformed |The specified Eip is malformed.The specified Eip not exist in the bandwidth package. |The specified EIP is not associated with the specified Bandwidth Package. |
|400 |InvalidISP.Mismatch |The isp of the bandwidth package does not match with the Eip. |The ISP of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidLoadBalancer.InvalidNetworkType |The specified LoadBalancer is not in the correct network type for the request. |The specified load balancer cannot respond to this request due to its network type. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified load balancer cannot respond to this request due to its billing status. |
|400 |InvalidOperation.Malformed |The specified Operation is malformed. |The specified Operation format is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol format is invalid. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the Eip. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSecurityProtectionTypes.Mismatch |The specified security protection types of the bandwidth package does not match with the Eip. |The protection type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the Eip. |The specified egress of the Bandwidth Package does not match that of the EIP. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of elastic IP addresses (EIPs) that you can add to a Bandwidth Package. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified Eip does not exist. |The specified EIP does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidEip.Conflict |The specified Eip conflicts with that of another Eip in your bandwidth package. |The specified EIP is already added to a Bandwidth Package. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |

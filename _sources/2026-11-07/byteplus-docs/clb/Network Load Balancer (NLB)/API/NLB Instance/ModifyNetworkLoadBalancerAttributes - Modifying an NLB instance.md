---
title: "ModifyNetworkLoadBalancerAttributes - Modifying an NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes"
---

Call the ModifyNetworkLoadBalancerAttributes API to modify the name, description, cross\-AZ forwarding, IP version, and other information of an NLB instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkLoadBalancerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

If an optional parameter in the table below is not provided, it indicates that the value of this parameter will retain its original configuration.



**Action ** <span data-label="purple">String </span><span data-api-tag="require|xBjU05">必选</span> `Example: ModifyNetworkLoadBalancerAttributes`

Action to execute. Set the value to ModifyNetworkLoadBalancerAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ypb9C1">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|2L78VH">必选</span> `Example: nlb-bp1b6c719dfa08ex****`

NLB instance ID.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.



**LoadBalancerName ** <span data-label="purple">String </span>`optional` `Example: nlb-test1`

Name of the NLB instance.


* Must start with a letter, number, or Chinese character. May include the following symbols: periods (.), underscore (_), and hyphen (\-).

* Length limit: 1 to 128 characters.



**Description ** <span data-label="purple">String </span>`optional` `Example: test`

Description of the NLB instance.


* Must start with a letter, number, or Chinese character. It may contain the following special characters: comma ( , ), period ( . ), underscore ( _ ), space ( ), equal sign ( = ), hyphen ( \- ), full\-width comma (， ), and full\-width period ( 。 )

* Length limit: 0 to 255 characters.



**CrossZoneEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

NLB instance enables cross\-AZ forwarding.

Please input the enumerated values strictly in case as follows, and do not pass in other values.


* true: Enable.

* false: Disable.



**IpAddressVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

IP address version.


* ipv4: IPv4 only.

* dualstack: Dual\-stack, supports both IPv4 and IPv6.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an IPv4 NLB instance has a TLS listener, modifying it to dual\-stack is not supported.</div>




**ModificationProtectionStatus ** <span data-label="purple">String </span>`optional` `Example: NonProtection`

Modify the protection status of an NLB instance in the console.


* NonProtection: Disable, allowing modification or deletion of instances by the console.

* ConsoleProtection: Enable, prohibiting modifications or deletions of the instance via the console.



**DNSAffinity ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Whether to enable DNS Availability Zone (AZ) affinity.


* true: Private network clients preferentially resolve to the IPs of NLB nodes in the same AZ, so traffic does not cross AZs. If a node in the same AZ fails, the IPs of all non\-faulty AZs are automatically returned.

* false: DNS returns the IPs of nodes in all AZs of the instance, and clients select randomly or by round\-robin, which may result in cross\-AZ access.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This applies only to private network resolution; public DNS is not affected.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409291106382514606306AF947C****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyNetworkLoadBalancerAttributes&Version=2020-04-01&LoadBalancerId=nlb-bp1b6c719dfa08ex****&LoadBalancerName=nlb-test1&Description=test&CrossZoneEnabled=true&IpAddressVersion=ipv4&ModificationProtectionStatus=NonProtection HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNetworkLoadBalancerAttributes",
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


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|400 |InvalidCrossZoneEnabled.Malformed |The specified CrossZoneEnabled is malformed. |The specified CrossZoneEnabled parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidIpAddressVersion.Malformed |The specified IpAddressVersion is malformed. |The specified IpAddressVersion format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified CLB's state is incompatible with this request. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified CLB's billing state is incompatible with this request. |
|400 |InvalidLoadBalancerIPAddressVersion.UnSupportAction |The specified IPAddressVersion of LoadBalancer does not support this action. |The specified instance does not support the current operation due to its IP address type constraint. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidModificationProtectionStatus.Malformed |The specified ModificationProtectionStatus is malformed. |The specified ModificationProtectionStatus format is invalid. |
|400 |InvalidSubnetIPv6Cidr.NotSupport |The specified subnet does not support ipv6 cidr. |The specified subnet does not support IPv6 CIDR blocks. |
|400 |InvalidSubnetIPv6CidrISP.Mismatch |The ipv6 cidr isp of the subnets is not same. |The ISP types of multiple subnet IPv6 CIDR blocks are inconsistent. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|404 |InvalidSharedVPC.UnSupportAction |The specified shared VPC does not support this action. |The specified shared VPC does not support the current action. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The CLB service\-attached role does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |

---
title: "ModifyNetworkLoadBalancerNetworkType - Modifying the network type of an NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerNetworkType"
---

Call the ModifyNetworkLoadBalancerNetworkType API to modify the network type of an Network Load Balancer (NLB) instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkLoadBalancerNetworkType&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

If an optional parameter in the table below is not provided, it indicates that the value of this parameter will retain its original configuration.



**Action ** <span data-label="purple">String </span><span data-api-tag="require|XDOoLY">必选</span> `Example: ModifyNetworkLoadBalancerNetworkType`

Action to execute. Set the value to ModifyNetworkLoadBalancerNetworkType.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|5QGYe5">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|IO7DGq">必选</span> `Example: nlb-bp1b6c719dfa08ex****`

The ID of the NLB instance.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.



**Protocol ** <span data-label="purple">String </span><span data-api-tag="require|HHLT70">必选</span> `Example: ipv4`

The protocol type of the NLB instance IP address.


* ipv4

* ipv6



**Network type ** <span data-label="purple">String </span><span data-api-tag="require|J2Omvu">必选</span> `Example: internet`

The network type of the NLB instance after modification.


* internet: Public network.

* intranet: Private network.



**ZoneMappings.N.ZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-beijing-a`

The ID of the availability zone to which the EIP to be attached belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>NetworkType</code> is set to "intranet", this parameter must be omitted.</div>


* <div data-tips="true" data-tips-type="tip">The parameters <code>ZoneMappings.N.ZoneId</code> and <code>ZoneMappings.N.EipId</code> must be either both provided or both omitted.</div>




**ZoneMappings.N.EipId ** <span data-label="purple">String </span>`optional` `Example: eip-bp12mw1f8k3jgy****`

The ID of the EIP to be attached. Each availability zone is associated with an EIP.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>NetworkType</code> is set to "intranet", this parameter must be omitted.</div>


* <div data-tips="true" data-tips-type="tip">The parameters <code>ZoneMappings.N.ZoneId</code> and <code>ZoneMappings.N.EipId</code> must be either both provided or both omitted.</div>


* <div data-tips="true" data-tips-type="tip">When the parameter <code>NetworkType</code> is set to "internet",</div>


   * <div data-tips="true" data-tips-type="tip">Specify an existing EIP.</div>


   * <div data-tips="true" data-tips-type="tip">Omit to purchase a new EIP.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409291106382514606306AF947C****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyNetworkLoadBalancerNetworkType&Version=2020-04-01&LoadBalancerId=nlb-bp1b6c719dfa08ex****&Protocol=ipv4&NetworkType=internet&ZoneMappings.1.ZoneId=cn-beijing-a&ZoneMappings.1.EipId=eip-bp12mw1f8k3jgy**** HTTP/1.1
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
        "Action": "ModifyNetworkLoadBalancerNetworkType",
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
|400 |InvalidEip.InvalidStatus |The specified Eip is not in the correct status for the request. |The specified EIP cannot respond to this request due to its status. |
|400 |InvalidEipBillingType.NotSupport |The specified billing type of Eip dose not support this action. |The specified EIP billing method do not support the current action. |
|400 |InvalidEipISP.NotSupport |The specified isp of Eip dose not support this action. |The specified EIP ISP does not support the current action. |
|400 |InvalidEipSecurityProtectionTypes.NotSupport |The specified security types protection of Eip dose not support this action. |The specified EIP security protection type does not support the current action. |
|400 |InvalidEipSpecificEgress.NotSupport |The specified specific egress of Eip dose not support this action. |The specified EIP egress does not support the current action. |
|400 |InvalidISP.Mismatch |The isp of the bandwidth package does not match with the Eip. |The ISP of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified load balancer cannot respond to this request due to its billing status. |
|400 |InvalidNetworkType.Malformed |The specified NetworkType is malformed. |The specified NetworkType format is invalid. |
|400 |InvalidNetworkType.UnSupportAction |The specified NetworkType does not support this action in this region. |The specified network type does not support the current actions in this region. |
|400 |InvalidOperation.Malformed |The specified Operation is malformed. |The specified Operation format is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol format is invalid. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the Eip. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSecurityProtectionTypes.Mismatch |The specified security protection types of the bandwidth package does not match with the Eip. |The protection type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the Eip. |The specified egress of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidZoneMappings.EipId.Malformed |The specified ZoneMappings.EipId is malformed. |The specified ZoneMappings.EipId format is invalid. |
|400 |InvalidZoneMappings.EipIsp.Malformed |The specified ZoneMappings.EipIsp is malformed. |The specified ZoneMappings.EipIsp format is invalid. |
|400 |InvalidZoneMappings.EipSpecificEgress.Malformed |The specified ZoneMappings.EipSpecificEgress is malformed. |The specified ZoneMappings.EipSpecificEgress format is invalid. |
|400 |InvalidZoneMappings.Malformed |The specified ZoneMappings is malformed. |The specified ZoneMappings format is invalid. |
|400 |InvalidZoneMappings.ZoneId.Malformed |The specified ZoneMappings.ZoneId is malformed. |The specified ZoneMappings.ZoneId parameter format is invalid. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to lack of Eip allocated. |The action request for this instance was rejected because allocated EIPs are insufficient. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified Eip does not exist. |The specified EIP does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidEip.Conflict |The specified Eip conflicts with that of another Eip in your bandwidth package. |The specified EIP is already added to a Bandwidth Package. |
|409 |InvalidEipServiceManage.Conflict |The specified Eip already another service manage. |The specified EIP is already service\-managed. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |

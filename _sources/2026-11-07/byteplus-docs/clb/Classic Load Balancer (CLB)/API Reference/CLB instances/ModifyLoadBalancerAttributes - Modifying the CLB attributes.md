---
title: "ModifyLoadBalancerAttributes - Modifying the CLB attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes"
---

Call the ModifyLoadBalancerAttributes API to modify the specified CLB instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

When calling this API, if an optional parameter is not configured, its existing configuration remains unchanged.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyLoadBalancerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|W119ST">必选</span> `Example: ModifyLoadBalancerAttributes`

Action to execute. Set the value to **ModifyLoadBalancerAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|NAYrMb">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|zjL7AF">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**LoadBalancerName ** <span data-label="purple">String </span>`optional` `Example: clb-1`

Name of the CLB instance.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.



**Description ** <span data-label="purple">String </span>`optional` `Example: test`

Description of the CLB instance.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.



**LoadBalancerSpec ** <span data-label="purple">String </span>`optional` `Example: small_1`

CLB instances come in different specifications, each offering different forwarding performance. For more information, see [Product types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). Values:


* small_1: Small I

* small_2: Small II

* medium_1: Medium I

* medium_2: Medium II

* large_1: Large I

* large_2: Large II


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The modified instance specification bandwidth must be greater than or equal to the total bandwidth of the configured listeners; otherwise, the specification cannot be modified.</div>




**Type ** <span data-label="purple">String </span>`optional` `Example: private`

Type of the CLB instance. Values:

private: Indicates converting a public CLB instance to a private instance. After conversion, the lifecycle of the CLB instance and the associated EIP becomes independent; you can unbind the EIP as needed.



**AddressIpVersion ** <span data-label="purple">String </span>`optional` `Example: DualStack`

IP version of the CLB instance. Supports mutual conversion between IPv4 and dual\-stack for private CLB instances. If a public CLB instance needs to be converted, please first see [Converting a public instance to a private instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-04) to convert it to a private instance.


* ipv4: IPv4 only.

* DualStack: Dual stack.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in beta stage. For trial requests, please contact your account manager.</div>




**Ipv6Address ** <span data-label="purple">String </span>`optional` `Example: 2408:4005:XX:XX:200`

IPv6 address of the CLB instance.

This parameter is valid only when `AddressIpVersion` is changed from ipv4 to DualStack.


* Specify an available private IPv6 address from the subnet.

* If left blank, an available private IPv6 address will be automatically allocated from the subnet.



**ModificationProtectionStatus ** <span data-label="purple">String </span>`optional` `Example: ConsoleProtection`

Enable console modification protection for the CLB instance. After enabling, modifying or deleting the instance via the console is prohibited. Values:


* NonProtection or Empty: Disabled

* ConsoleProtection: Enable.



**ModificationProtectionReason ** <span data-label="purple">String </span>`optional` `Example: managed instance`

The reason for setting console modification protection.

This parameter is valid only when the parameter `ModificationProtectionStatus` is set to ConsoleProtection.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: half\-width periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 80 characters.



**BypassSecurityGroupEnabled ** <span data-label="purple">String </span>`optional` `Example: off`

CLB instance enables the "Allow Backend Security Group Traffic" feature.


* on: Enable. After enabling, the security group of the ECSs in the backend server group (server type only) no longer checks CLB traffic; it is allowed by default.

* off: Disable.



**TimestampRemoveEnabled ** <span data-label="purple">String </span>`optional` `Example: off`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202108161106382514606306AF947C****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyLoadBalancerAttributes&Version=2020-04-01&Description=test&LoadBalancerId=clb-bp1b6c719dfa08ex****&LoadBalancerName=clb-test1&LoadBalancerSpec=small_1&ModificationProtectionReason=实例托管&ModificationProtectionStatus=ConsoleProtection HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202108161106382514606306AF947C****",
        "Action": "ModifyLoadBalancerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106382514606306AF947C****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAddressIpVersion.Malformed |The specified AddressIpVersion is malformed. |The specified AddressIpVersion parameter format is invalid. |
|400 |InvalidAddressIpVersionConvert.UnSupport |The specified LoadBalancer not support convert address Ip version. |The specified CLB does not support IP type conversion. |
|400 |InvalidAllowedPorts.Conflict |The specified AllowedPorts has conflict. |The specified allowed port ranges overlap. |
|400 |InvalidAllowedPorts.InUse |The specified AllowedPorts is in use. |The specified allowed port range is currently in use by a listener. |
|400 |InvalidAllowedPorts.Malformed |The specified AllowedPorts is malformed. |The specified AllowedPorts parameter format is invalid. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format specified for Bandwidth is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.Malformed |The specified BypassSecurityGroupEnabled is malformed. |The specified BypassSecurityGroupEnabled parameter format is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.NotSupport |The specified LoadBalancer does not support BypassSecurityGroupEnabled. |The specified CLB does not support the Bypass security group feature. |
|400 |InvalidEniIpv6Address.Malformed |The specified EniIpv6Address is malformed. |The specified EniIpv6Address parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerDescription.Malformed |The specified LoadBalancerDescription is malformed. |The specified LoadBalancerDescription parameter format is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidLoadBalancerSpec.ListenerBandwidthMismatch |The total bandwidth of all listeners exceeds the upper limit of the specified spec. |The total bandwidth specified for the listeners within the instance exceeds the limit of the designated CLB specification. |
|400 |InvalidLoadBalancerSpec.Malformed |The specified LoadBalancerSpec is malformed. |The specified LoadBalancerSpec parameter format is invalid. |
|400 |InvalidModificationProtectionReason.Malformed |The specified ModificationProtectionReason is malformed. |The specified ModificationProtectionReason parameter format is invalid. |
|400 |InvalidModificationProtectionStatus.Malformed |The specified ModificationProtectionStatus is malformed. |The specified ModificationProtectionStatus format is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidSubnetIPv6Cidr.NotSupport |The specified subnet does not support ipv6 cidr. |The specified subnet does not support IPv6 CIDR blocks. |
|400 |InvalidTimestampRemoveEnabled.Malformed |The specified TimestampRemoveEnabled is malformed. |The specified TimestampRemoveEnabled parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |QuotaExceed.AllowedPortNumberEachInstance |You've reached the limit on the number of AllowedPort that you can operate. |The maximum number of configurable allowed port ranges has been reached. |
|400 |QuotaExceed.XLargeOneInstanceNumber |You've reached the limit on the number of xlarge_1 instance that you can create. |The quota limit for the number of ultra\-large I CLB instances that can be created has been reached. |
|400 |QuotaExceed.XLargeTwoInstanceNumber |You've reached the limit on the number of xlarge_2 instance that you can create. |The quota limit for the number of ultra\-large II CLB instances that can be created has been reached. |
|400 |UnSupportedOperation.SpecUnchanged |The request on the specified LoadBalancer is denied due to the LoadBalancerSpec has not changed. |The CLB specification has not changed. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation.MainAccountNotSupportPaypal |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The post‑paid items in this order do not support PayPal. Please contact the root user to add an alternative payment method. |
|400 |UnsupportedOperation.NotSupportPaypal |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |The post‑paid items in this order do not support PayPal. Please add an alternative payment method. |
|403 |Forbidden |The specified LoadBalancer not support convert address IP version, because owner of the Eni is not in sharing. |The specified CLB does not support IP type conversion because the owner of the ENI is not in the sharing relationship. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'AllowedPorts'. |No permission to operate on the specified service, such as AllowedPorts. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'TimestampRemoveEnabled'. |No permission to operate on the specified service, such as TimestampRemoveEnabled. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidLoadBalancerSpec.NotFound |The specified LoadBalancerSpec does not exist. |The specified CLB specification does not exist. |
|409 |InvalidAllowedPort.Conflict |The specified AllowedPort already exists. |The specified allowed port range already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|412 |InvalidLoadBalancer.InvalidBillingType |The specified LoadBalancer is not in the correct BillingType for the request. |The specified CLB's billing method is incompatible with this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |

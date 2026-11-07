---
title: "ConvertLoadBalancerBillingType - Converting the CLB billing methods"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ConvertLoadBalancerBillingType"
---

Call the ConvertLoadBalancerBillingType API to change the metering method of the CLB instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API supports the following billing conversions:


* Conversion between Pay\-by\-Specification and Subscription.

* Conversion between Pay\-by\-Specification and Pay\-by\-CU.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Direct conversion from Subscription to Pay\-by\-CU is not supported. To convert, you must first change to Pay\-by\-Specification, and then to Pay\-by\-CU.</div>


<div data-tips="true" data-tips-type="tip">For public CLB instances whose associated EIP is of the enhanced protection type or is part of a Shared Bandwidth Package, conversion to the Subscription billing is not supported.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ConvertLoadBalancerBillingType&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|5ssX1A">必选</span> `Example: ConvertLoadBalancerBillingType`

Action to execute. Set the value to **ConvertLoadBalancerBillingType**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|vt3wyN">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|1lNeLt">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**LoadBalancerBillingType ** <span data-label="purple">Integer </span><span data-api-tag="require|5xM41W">必选</span> `Example: 1`

Metering methods of the CLB instance. Valid values:


* 1: Subscription

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pay\-by\-CU is in the beta stage. To request a trial, please contact your account manager.</div>




**LoadBalancerSpec ** <span data-label="purple">String </span>`optional` `Example: small_1`

CLB instances come in different specifications, each offering different forwarding performance. For more information, see [Product type and specification](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). Valid values:


* small_1: Small I

* small_2: Small II

* medium_1: Medium I

* medium_2: Medium II

* large_1: Large I

* large_2: Large II


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is mandatory when the <code>LoadBalancerBillingType</code> parameter is set to 2, and the CLB instance's original billing method is Pay\-by\-CU.</div>




**PeriodUnit ** <span data-label="purple">String </span>`optional` `Example: Month`

Billing duration unit for subscription billing. Valid values:


* Month (default): Monthly billing

* Year: Yearly billing



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Billing duration for Subscription billing.


* When `PeriodUnit` is set to Month, valid values include 1 to 9, 12, 24, and 36.

* When `PeriodUnit` is set to Year, valid values range from 1 to 3.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is omitted or left unset, the default value is 1.</div>




**AutoRenewal ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable automatic renewal.


* true: Yes. Default auto\-renewal period: 1 month.

* false (default): No.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**OrderId ** <span data-label="purple">String </span>`Example: Order705261343570982****`

The order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ConvertLoadBalancerBillingType&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex****&LoadBalancerBillingType=1&LoadBalancerSpec=small_1&PeriodUnit=Month&Period=1&AutoRenewal=true
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ConvertLoadBalancerBillingType",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order705261343570982****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAutoRenewal.Malformed |The specified AutoRenewal is malformed. |The specified AutoRenewal parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidLoadBalancerBillingType.Malformed |The specified LoadBalancerBillingType is malformed. |The specified LoadBalancerBillingType parameter format is invalid. |
|400 |InvalidLoadBalancerSpec.ListenerBandwidthMismatch |The total bandwidth of all listeners exceeds the upper limit of the specified spec. |The total bandwidth specified for the listeners within the instance exceeds the limit of the designated CLB specification. |
|400 |InvalidLoadBalancerSpec.Malformed |The specified LoadBalancerSpec is malformed. |The specified LoadBalancerSpec parameter format is invalid. |
|400 |InvalidPeriod.Malformed |The specified Period is malformed. |The specified Period format is invalid. |
|400 |InvalidPeriodUnit.Malformed |The specified PeriodUnit is malformed. |The specified PeriodUnit parameter format is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerSpec'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerSpec. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerBillingType'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerBillingType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |UnSupportedOperation.SpecUnchanged |The request on the specified LoadBalancer is denied due to the LoadBalancerSpec has not changed. |The CLB specification has not changed. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|412 |InvalidLoadBalancer.InvalidBillingType |The specified LoadBalancer is not in the correct BillingType for the request. |The specified CLB's billing method is incompatible with this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |

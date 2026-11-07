---
title: "RenewLoadBalancer - Renewing a CLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/RenewLoadBalancer"
---

Call the RenewLoadBalancer API to renew a subscription Classic Load Balancer (CLB) instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RenewLoadBalancer&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ELRaKa">必选</span> `Example: RenewLoadBalancer`

Action to execute. Set the value to **RenewLoadBalancer**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|gxtl1x">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|0OcTOy">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**PeriodUnit ** <span data-label="purple">String </span>`optional` `Example: Month`

Billing duration unit for subscription billing. Valid values:


* Month (default): Monthly billing

* Year: Yearly billing



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Billing Duration for Subscription Billing Default: 1.


* When `PeriodUnit` is set to Month, valid values include: 1\-9, 12, 24, and 36.

* When `PeriodUnit` is set to Year, valid values range from 1 to 3.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=RenewLoadBalancer&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex****&PeriodUnit=Month&Period=1
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
        "Action": "RenewLoadBalancer",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidPeriod.Malformed |The specified Period is malformed. |The specified Period format is invalid. |
|400 |InvalidPeriodUnit.Malformed |The specified PeriodUnit is malformed. |The specified PeriodUnit parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|404 |InvalidLoadBalancerSpec.NotFound |The specified LoadBalancerSpec does not exist. |The specified CLB specification does not exist. |
|412 |InvalidLoadBalancer.InvalidBillingType |The specified LoadBalancer is not in the correct BillingType for the request. |The specified CLB's billing method is incompatible with this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |

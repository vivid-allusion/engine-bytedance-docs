---
title: "SetLoadBalancerRenewal - Setting the CLB renewal type"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/SetLoadBalancerRenewal"
---

Call the SetLoadBalancerRenewal API to set the renewal type for subscription CLB instances.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SetLoadBalancerRenewal&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|029OXE">必选</span> `Example: SetLoadBalancerRenewal`

Action to execute. Set the value to **SetLoadBalancerRenewal**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ziMEhF">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|uy6UHx">必选</span> `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.



**RenewType ** <span data-label="purple">Integer </span><span data-api-tag="require|ZQ5suP">必选</span> `Example: 2`

Renewal type of the CLB instance. Valid values:


* 1: Manual renewal

* 2: Automatic renewal.



**RenewPeriodTimes ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The period for a single automatic renewal, in month.

This parameter is valid when the parameter `RenewType` is set to 2.

Valid values: 1–3, 6, and 12. Default: 1.



**RemainRenewTimes ** <span data-label="purple">Integer </span>`optional` `Example: -1`

The number of automatic renewals available.

This parameter is valid when the parameter `RenewType` is set to 2.

Values include \-1 and 1 to 100. The default is \-1, meaning unlimited automatic renewals.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=SetLoadBalancerRenewal&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex****&RenewType=2&RenewPeriodTimes=1&RemainRenewTimes=-1
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
        "Action": "SetLoadBalancerRenewal",
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
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancer.UnSupportAction |The specified LoadBalancer does not support this action. |The specified CLB does not support this action. |
|400 |InvalidRemainRenewTimes.Malformed |The specified RemainRenewTimes is malformed. |The specified RemainRenewTimes parameter format is invalid. |
|400 |InvalidRenewPeriodTimes.Malformed |The specified RenewPeriodTimes is malformed. |The specified RenewPeriodTimes parameter format is invalid. |
|400 |InvalidRenewType.Malformed |The specified RenewType is malformed. |The specified RenewType parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'RenewType'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as RenewType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|412 |InvalidLoadBalancer.InvalidBillingType |The specified LoadBalancer is not in the correct BillingType for the request. |The specified CLB's billing method is incompatible with this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |

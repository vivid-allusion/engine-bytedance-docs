---
title: "DeleteLoadBalancer - Deleting a CLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer"
---

Call the DeleteLoadBalancer API to delete a CLB instance.

## Instructions

* Subscription CLB instances cannot be deleted using this API before they expire and are deactivated.

* For actions and prerequisites, see [Deleting a CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-09).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteLoadBalancer&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DeleteLoadBalancer`

Action to execute. Set the value to **DeleteLoadBalancer**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**LoadBalancerId ** String必选 `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.

## Response parameters

**RequestId ** String`Example: 2021081115332201042142000A01EA****`

Request ID.

## Request examples

```json
GET /?Action=DeleteLoadBalancer&Version=2020-04-01&LoadBalancerId=clb-bp1b6c719dfa08ex**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteLoadBalancer",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081115332201042142000A01EA****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidListener.InUse |The specified Listener is in use. |The specified CLB has listeners in use. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidServerGroup.InUse |The specified ServerGroup is in use. |The specified CLB has backend server groups in use. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |UnSupportedOperation.AssociatedByPrivateLink |The specified LoadBalancer associated by PrivateLink. |The specified CLB is bound by a private connection. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|412 |InvalidLoadBalancer.InvalidBillingType |The specified LoadBalancer is not in the correct BillingType for the request. |The specified CLB's billing method is incompatible with this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |

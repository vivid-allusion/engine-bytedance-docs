---
title: "DeleteLoadBalancer - Deleting an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DeleteLoadBalancer"
---

Call the DeleteLoadBalancer API to delete the ALB instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Submit up to 5 API requests per second.

* If the ALB instance has listeners configured, you must [Delete listener](https://docs.byteplus.com/en/docs/clb/Managing-listeners) before deleting the ALB instance.

* If the instance has WAF protection, deletion protection, or global acceleration enabled, you must disable the corresponding features before deleting the instance.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After the instance is deleted, it can no longer provide load balancer services and cannot be restored. Proceed with caution.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteLoadBalancer&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|JgbPf4">必选</span> `Example: DeleteLoadBalancer`

Action to execute. Set the value to DeleteLoadBalancer.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OC21Ip">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">string </span><span data-api-tag="require|zkqD3b">必选</span> `Example: alb-bp1b6c719dfa08ex****`

ALB instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId** <span data-label="purple">string</span> `Example: CEF72CEB-54B6-4AE8-B225-F876FF7BA****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteLoadBalancer&Version=2020-04-01&LoadBalancerId=alb-bp1b6c719dfa08ex**** HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DeleteLoadBalancer",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811153322010****42142000A01EA"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidLoadBalancer.InUse |The specified LoadBalancer is being used by listeners. |The specified ALB instance is currently used by a listener. |
|400 |OperationDenied.DeletionProtectionEnabled |The request on the specified LoadBalancer is denied due to deletion protection is enabled. |Because deletion protection is enabled, the operation request for this ALB instance is rejected. |
|400 |OperationFailed.QueryTrade |The request on the specified resource failed due to the query on Trade failed. |The request to operate on this resource failed because the billing platform request failed. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |OperationFailed.CreatePreOrderFailed |The request on the specified LoadBalancer failed due to creating a pre order failed. |Because the configuration order failed to be placed, the operation request for this ALB instance fails. |
|400 |OperationFailed.CreateOrderFailed |The request on the specified LoadBalancer failed due to creating an order failed. |Because the order payment failed, the operation request for this ALB instance fails. |
|400 |OperationFailed.EipUsedByBandwidthPackage |The request on the specified LoadBalancer failed due to eip being used by bandwidth package. |Because the EIP instance is still being used by a bandwidth package, the operation request for this ALB instance fails. Please remove the EIP instance from the bandwidth package before performing the operation. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
